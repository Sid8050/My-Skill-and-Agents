---
name: ralph-loop
description: "Plan and run autonomous iterative coding loops. Each iteration uses a fresh context window reading state from .ralph/ on disk. Use when the user asks to ralph-loop, iterate autonomously, or build something step-by-step with fresh context each time."
---

# Ralph Loop — OpenCode Edition

Adapted from FasalZein/ralph-loop (Claude Code plugin port of pi-ralph-loop by @edxeth).

## The Core Idea

Fresh context per iteration is the single most important thing. Each iteration:
1. Reads the plan + progress from `.ralph/` files on disk
2. Does exactly ONE item of work
3. Verifies it passed
4. Commits the change
5. Updates progress
6. Signals NEXT, COMPLETE, or STOP

The agent is sharp at the start of every context window and dumb by the end. A loop exits before decay dominates. State persists via `.ralph/` files and git — not memory.

## Two Modes

### Mode 1 — Plan first, then loop (recommended)

Describe a task. Decompose into 10-25 small independent items. Show user the plan for approval, then execute iteration by iteration.

**Step 1: Create the .ralph/ bundle**

`.ralph/plan.md`
```markdown
# Ralph Plan: [Task Name]

## Items (priority order — risky/architectural first)
1. [ ] [Specific, verifiable item]
2. [ ] ...

## Verification
[Exact commands: npm test, pnpm typecheck, etc.]

## Quality Bar
No placeholders. Full implementations.
```

`.ralph/items.json`
```json
{
  "version": 1,
  "items": [
    {
      "category": "feature",
      "description": "Specific description matching plan.md",
      "steps": ["concrete step", "verification command"],
      "passes": false,
      "regression_notes": ""
    }
  ],
  "runtime_contract": {
    "verification_gates": [{ "name": "tests", "command": "npm test" }],
    "require_commit": true,
    "require_progress_append": true,
    "require_one_item_per_iteration": true
  }
}
```

`.ralph/progress.md`
```markdown
# Progress
<!-- Each iteration appends here. Keep entries concise. Sacrifice grammar for brevity. -->
```

`.ralph/prompt.md`
```markdown
@.ralph/plan.md @.ralph/progress.md

You are in a Ralph loop. Each iteration is a fresh context window.

1. Read .ralph/plan.md and .ralph/progress.md to orient
2. Run: git log --oneline -10
3. Choose the HIGHEST PRIORITY item whose passes is false
4. Before changing anything: search the codebase — do not assume not implemented
5. Implement exactly ONE item fully — no placeholders, no shortcuts, no stubs
6. Run verification commands. If they fail, fix before continuing.
7. Append to .ralph/progress.md what you did, decisions made, files changed
8. In .ralph/items.json flip ONLY that item's "passes" to true
9. git add changed files, git commit with descriptive message

ONE item per iteration. Do NOT skip ahead.

Emit EXACTLY ONE control tag as the LAST line:
  <promise>NEXT</promise>     — one item completed
  <promise>COMPLETE</promise> — every item passes
  <promise>STOP</promise>     — blocked, cannot proceed
```

**Step 2: Show the plan to the user and get approval.**

**Step 3: Run the loop**

Option A — Using the ralph.sh script (if available):
```bash
bash ~/.config/opencode/skills/ralph-loop/scripts/ralph.sh @.ralph/prompt.md -c COMPLETE -n 20
```

Option B — Manual loop within this session (Da Vinci's default):
Da Vinci reads `.ralph/plan.md` and `.ralph/items.json`, then follows the iteration protocol above — one item at a time, verifying, committing, updating progress — until all items pass or a blocker is hit.

### Mode 2 — Direct loop (quick tasks)

For focused tasks without a plan:
```bash
bash ~/.config/opencode/skills/ralph-loop/scripts/ralph.sh "fix the failing auth test" -c DONE -n 10
```

## Rules for Good Plans

- **One item = one iteration.** If it needs two, split it.
- **Risky first.** Architecture and integration before CRUD and polish.
- **Specific items.** "Add JWT validation to /api routes", not "add auth".
- **Exact verification.** The actual command, not "run tests".
- **10–25 items.** More = over-specifying; fewer = items too big.
- **No placeholders.** Full implementations only. Never stub and move on.
- **Search before creating.** Always ripgrep the codebase before implementing — don't assume something isn't there.

## Control Operations

**Status:**
```bash
cat .ralph/loop.md; tail -25 .ralph/progress.md
```

**Stop:**
```bash
touch .ralph/.stop
```

**Resume:**
```bash
bash ~/.config/opencode/skills/ralph-loop/scripts/ralph.sh @.ralph/prompt.md -c COMPLETE -n 20
```

**Restart (clears progress):**
```bash
printf '# Progress\n\n' > .ralph/progress.md
jq '.items |= map(.passes = false)' .ralph/items.json > /tmp/items.tmp && mv /tmp/items.tmp .ralph/items.json
bash ~/.config/opencode/skills/ralph-loop/scripts/ralph.sh @.ralph/prompt.md -c COMPLETE -n 20
```

## OpenCode vs Claude Code

ralph.sh uses `claude-ralph` (Claude Code's CLI subprocess runner). In OpenCode:
- Da Vinci can follow the ralph-loop protocol **manually within his session** — same discipline, same structure, same `.ralph/` state files
- For autonomous background looping: use `opencode` CLI if it supports headless mode, or run ralph.sh with the `CLAUDE_RALPH_PATH` env pointing to any compatible CLI

See `scripts/ralph.sh` for the full loop harness (idle watchdog, promise gating, retry logic).

## Writing Perfect Loops

See `docs/writing-perfect-loops.md` for the full guide. Key principles:
1. Fresh context per iteration is everything
2. One item per loop — always
3. Deterministically load the same files every iteration (plan → progress → task)
4. Progress file is the bridge between context windows
5. Git commit every iteration
6. Automated verification gates are backpressure — the more you have, the better
7. Risky architectural items first, polish last
