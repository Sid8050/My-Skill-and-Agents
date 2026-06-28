# OpenCode — The Olympus Team

> Four legendary AI agents, 27+ battle-tested skills, a complete design-quality pipeline, and autonomous iterative loops. Drop this into `~/.config/opencode/` and get a world-class AI development team.

---

## Quick Start

**Prerequisites:** OpenCode CLI v1.17+, Node.js

```powershell
git clone https://github.com/Sid8050/My-Skill-and-Agents.git $env:USERPROFILE\.config\opencode
```

That's it. Open OpenCode and your four-agent team is ready.

---

## The Olympus Team — Four Agents

| Agent | Name | Inspiration | Model | Mode | Role |
|---|---|---|---|---|---|
| **Hermes** | The Dispatcher | Hermes — messenger of the gods | deepseek-v4-pro | primary | Receives any raw request, questions the user, reads the codebase, produces the exact optimized prompt for the right agent |
| **Vitruvius** | The Architect | Marcus Vitruvius Pollio | deepseek-v4-pro | all | Requirements Discovery → `architect/` blueprints + `design.md` + `.ralph/` bundle |
| **Da Vinci** | The Maker | Leonardo da Vinci | deepseek-v4-pro | primary | Reads `architect/` or `plans/` → implements flawlessly → invokes Argus |
| **Argus** | The Watcher | Argus Panoptes | glm-5.2 | subagent | Build gates → import checks → API payload verification → 11-category audit |

---

## How to Use It — Start With Hermes

**Hermes is the front door.** Give him any raw request in plain language. He will:

1. Read the codebase for context (read/glob/grep — never writes)
2. Ask clarifying questions in batches of 3 until he fully understands the task
3. Produce a structured routing output: Classification, Agent (in CAPS), a copy-paste prompt, Watch For notes, and What Comes After

### Example Flows

| Your Message | Hermes Routes To | Why |
|---|---|---|
| "the invoice PDF is generating wrong totals" | **ARGUS** | Existing code, targeted audit + fix |
| "we need a supplier approval workflow" | **VITRUVIUS** | New feature, needs blueprints first |
| "fix the login redirect" | **DA VINCI** | Small, well-scoped change, direct implementation |

### The Messenger's Oath

Hermes never writes code. Hermes never calls subagents. Hermes never delegates tasks himself. His job is exactly three things: **Ask → Route → Stop.**

---

## The Olympus Protocol

```
Any request → Hermes (reads codebase, asks questions) → optimized prompt
                                    ↓
              Vitruvius → architect/NNN-task/ + design.md + .ralph/ bundle
                                    ↓
              Da Vinci → reads architect/ → direct (< 10 items) or ralph loop (10+)
                       → invokes Argus after each module
                                    ↓
              Argus → Gate 0 build → Gate 1 imports → Gate 2 API/payloads
                    → 11-category audit → APPROVED or REJECTED
```

---

## Shared Folder Convention

Both `architect/` and `plans/` use identical `NNN-slug/` subfolder naming.

```
architect/
├── 001-auth-refactor/
│   ├── spec.md
│   ├── design.md
│   └── tasks.md
├── 002-invoice-pdf/
│   ├── spec.md
│   └── tasks.md

plans/
├── 001-auth-refactor/
│   └── ...
```

### ❌ FORBIDDEN — flat files

```
architect/
├── auth-spec.md        ← wrong, no NNN-slug/ folder
├── tasks.md            ← wrong, not namespaced
```

Every task gets its own numbered slug folder. No exceptions.

---

## Agent Deep Dives

### Hermes — The Dispatcher

**Two phases:**

- **Phase 1 — Understand:** Read the codebase silently (read/glob/grep only). Ask questions in batches of max 3. Never asks what a file can answer.
- **Phase 2 — Route:** Once fully understood, produce the routing output and stop.

**Tool permissions:**
- Allowed: `read`, `glob`, `grep`
- Denied: `edit`, `bash`, `task`, `write`

**Output format:**

```
Classification: <bug | feature | refactor | audit | ...>
Agent: <HERMES | VITRUVIUS | DA VINCI | ARGUS>
---
Copy-paste prompt:
<exact prompt the user pastes into the target agent>
---
Watch For: <risks, ambiguities, things the agent should probe>
What Comes After: <next step after the routed agent finishes>
```

**The Messenger's Oath:** Hermes never codes. Hermes never delegates. Hermes never continues after routing. One output, then silence.

---

### Vitruvius — The Architect

**Two workflows:**

- **Greenfield** → creates `architect/NNN-task/` with spec, design, tasks, and `.ralph/` bundle
- **Brownfield** → uses the `improve` skill → creates `plans/NNN-slug/` with improvement plan

**5-Phase Requirements Discovery Protocol:**

1. **Understand** — read the codebase, map existing patterns
2. **Explore** — ask questions in batches of 3, never more
3. **Recommend** — propose approach with tradeoffs (torpathy applies here)
4. **Confirm** — get explicit user sign-off before any file creation
5. **Execute** — write all architect/ docs, then produce Da Vinci handoff prompt

**Design Authority:**
Vitruvius owns the component library, color system (OKLCH), typography scale, and `design.md`. He never accepts framework defaults. Every visual decision is intentional and documented.

**Ralph bundle routing:**
- 1–4 items → tell Da Vinci to go direct
- 5–9 items → Da Vinci decides
- 10+ items → create full `.ralph/` bundle (all 4 files required: `plan.md`, `items.json`, `prompt.md`, `progress.md`)

**The Architect's Oath:** Vitruvius never writes application code. Every response ends with a ready-to-paste Da Vinci handoff prompt.

**Key skills:** `zoom-out`, `improve`, `torpathy`, `design-craft`, `laws-of-ux`, `to-prd`, `ralph-loop`, `loop-library`

---

### Da Vinci — The Maker

**Task routing:**
- `< 10 items` → direct implementation in one context window
- `10+ items` → ralph loop (reads `.ralph/` bundle, one item per iteration)

**Context decay awareness:**
Da Vinci knows his own degradation curve. As context fills, quality drops — this is the "dumb zone." When he detects context rot (repetitive code, missed imports, logic drift), he commits with a `wip:` prefix and exits cleanly for the next iteration to pick up.

**4-layer UI stack:**
1. `coss/ui` components — base primitives
2. `design-craft` skill — visual craft rules
3. `laws-of-ux` skill — user psychology
4. `design-qa` skill — 11-gate pre-ship checklist

**Pre-commit checklist:**
`lint → typecheck → tests → react-doctor → design-qa 11 gates`

All gates must pass before any commit. No exceptions.

**WAIT pattern:**
Da Vinci can invoke Argus mid-loop via a `WAIT` tag in his output. He never invokes Vitruvius mid-loop — if architectural questions arise, he stops and surfaces them.

**Key skills:** `caveman`, `tdd`, `diagnose`, `react-doctor`, `design-craft`, `design-qa`, `laws-of-ux`, `ralph-loop`

---

### Argus — The Watcher

Argus is a sandboxed audit subagent. He sees everything, changes almost nothing.

**Three gates (in order):**

- **Gate 0 — Build:** Run the build. If it fails, stop immediately. Severity: Titan (P0). Da Vinci must fix before anything else proceeds.
- **Gate 1 — Imports:** Run `npx tsc --noEmit`. Every unresolved import is a blocker.
- **Gate 2 — API/Payloads:** Trace every button, form submit, and data fetch. Every HTTP call must handle: 200/success, 401 Unauthorized, 403 Forbidden, 404 Not Found, 500 Server Error, and timeout/network failure.

**11-Category Hundred-Eyed Checklist:**

| # | Category | Focus |
|---|---|---|
| 1 | Bugs | Logic errors, edge cases, null safety |
| 2 | Security | Auth, input validation, secrets exposure |
| 3 | Performance | Render costs, bundle size, query efficiency |
| 4 | Tests | Coverage gaps, flaky tests, missing cases |
| 5 | Tech Debt | Dead code, duplication, complexity |
| 6 | Dependencies | Outdated, vulnerable, or unnecessary packages |
| 7 | DX | Dev ergonomics, error messages, tooling |
| 8 | Docs | Missing JSDoc, stale comments, unclear naming |
| 9 | Direction | Architectural drift, pattern violations |
| 10 | React Health | Hook rules, memo abuse, prop drilling |
| 11 | UI Design Quality | Spacing, color, typography, accessibility |

**Bug severity:**

| Severity | Name | Meaning |
|---|---|---|
| P0 | Titan | Blocks everything. Fix now. |
| P1 | Olympian | High impact. Fix before shipping. |
| P2 | Mortal | Should fix. Won't block. |
| P3 | Nymph | Polish. Nice to have. |

**Sandboxed permissions:**
- Can edit: test files only
- Can run: test, build, and lint commands only
- Cannot edit: source files, configs, or anything outside the test layer

**Verdict:** Every Argus run ends with either `APPROVED` or `REJECTED`. If rejected, a prioritized fix list is provided for Da Vinci.

---

## Ralph Loop

The ralph loop is an autonomous iterative build strategy designed to defeat context rot.

**The core idea:** Instead of one giant context window that degrades, each iteration starts fresh — reading state from disk (`.ralph/`) rather than relying on memory of previous turns.

### The 4 Bundle Files

| File | Purpose |
|---|---|
| `plan.md` | Human-readable description of the full task |
| `items.json` | Ordered array of work items with status fields |
| `prompt.md` | The system prompt Da Vinci reads at the start of every iteration |
| `progress.md` | Running log — what was done, what's next, any blockers |

### Promise Tags

Da Vinci uses these tags to signal state at the end of each iteration:

| Tag | Meaning |
|---|---|
| `NEXT` | Item complete, proceed to next item |
| `COMPLETE` | All items done, loop ends |
| `STOP` | Blocker encountered, human input needed |
| `WAIT` | Invoking Argus before continuing |

### When to Use Ralph Loop

- 10+ work items
- Multi-day builds
- Any task where context rot is a real risk
- Features that span multiple modules or files

When in doubt, go direct. Ralph loop is for the big jobs.

### Correct Order

**Vitruvius creates `architect/` docs FIRST.** Then — and only then — creates the `.ralph/` bundle. Da Vinci executes from the bundle. Never run the loop without the architect docs being complete.

---

## Skills (27+)

### Design

| Skill | What It Does |
|---|---|
| `design-craft` | Universal design principles — typography, color, spacing, animation, layout, interaction |
| `design-qa` | 11-gate UI quality checklist — accessibility, consistency, performance, responsive |
| `laws-of-ux` | User psychology rules — cognitive load, attention, memory, motor cost, mental models |

### Engineering

| Skill | What It Does |
|---|---|
| `react-doctor` | React diagnostics — lint, a11y, bundle size, architecture, regression check |
| `loop-library` | Find, compare, and design repeatable AI-agent loops |
| `improve` | Senior advisor survey — prioritized implementation plans for another agent to execute |
| `diagnose` | Disciplined debug loop — reproduce → minimise → hypothesise → instrument → fix |
| `tdd` | Red-green-refactor TDD loop with integration test support |
| `prototype` | Throwaway prototypes — terminal app or multi-variation UI from one route |

### Architecture

| Skill | What It Does |
|---|---|
| `torpathy` | Strategic decision framework — where a fix belongs, which tradeoff dominates |
| `zoom-out` | Broader context and higher-level perspective on a section of code |
| `improve-codebase-architecture` | Deepening opportunities informed by domain language and ADRs |
| `ralph-loop` | Plan and run autonomous iterative coding loops with fresh context per iteration |

### Productivity

| Skill | What It Does |
|---|---|
| `caveman` | Ultra-compressed communication — ~75% token reduction, full technical accuracy |
| `handoff` | Compact the current conversation into a handoff document for another agent |
| `teach` | Teach the user a new skill or concept within the workspace |
| `to-prd` | Turn current conversation context into a PRD on the issue tracker |
| `triage` | Triage issues through a state machine driven by triage roles |
| `grill-me` | Relentless interview to stress-test a plan or design |
| `grill-with-docs` | Grilling session against the existing domain model, updates CONTEXT.md and ADRs |
| `to-issues` | Break a plan or PRD into independently-grabbable issues |
| `write-a-skill` | Create new agent skills with proper structure and progressive disclosure |

### Tooling

| Skill | What It Does |
|---|---|
| `git-guardrails-claude-code` | Block dangerous git commands before they execute via hooks |
| `setup-pre-commit` | Set up Husky pre-commit hooks with lint-staged, typecheck, and tests |
| `review` | Review changes against coding standards and spec in parallel sub-agents |

### Writing

| Skill | What It Does |
|---|---|
| `writing-beats` | Shape an article as a journey of beats, one beat at a time |
| `writing-fragments` | Mine raw fragments — claims, vignettes, sharp sentences — for future articles |
| `writing-shape` | Turn raw notes or a rough draft into something publishable |

---

## Skill-to-Agent Mapping

| Skill | Hermes | Vitruvius | Da Vinci | Argus |
|---|:---:|:---:|:---:|:---:|
| `caveman` | ✓ | — | ✓ | ✓ |
| `triage` | ✓ | ✓ | — | — |
| `zoom-out` | ✓ | ✓ | ✓ | ✓ |
| `improve` | — | ✓ | ✓ | ✓ |
| `torpathy` | — | ✓ | — | — |
| `design-craft` | — | ✓ | ✓ | ✓ |
| `laws-of-ux` | — | ✓ | ✓ | — |
| `to-prd` | — | ✓ | — | — |
| `ralph-loop` | — | ✓ | ✓ | — |
| `loop-library` | — | ✓ | ✓ | ✓ |
| `improve-codebase-architecture` | — | ✓ | — | — |
| `grill-me` | — | — | ✓ | — |
| `grill-with-docs` | — | ✓ | — | — |
| `to-issues` | — | — | ✓ | ✓ |
| `tdd` | — | — | ✓ | ✓ |
| `diagnose` | — | ✓ | ✓ | ✓ |
| `react-doctor` | — | ✓ | ✓ | ✓ |
| `design-qa` | — | — | ✓ | ✓ |
| `prototype` | — | — | ✓ | — |
| `handoff` | — | ✓ | ✓ | ✓ |
| `review` | — | — | — | ✓ |
| `git-guardrails-claude-code` | — | — | ✓ | — |
| `setup-pre-commit` | — | — | ✓ | — |
| `write-a-skill` | — | ✓ | — | — |
| `teach` | — | ✓ | ✓ | — |

---

## Models

| Agent | Model | Context | Output |
|---|---|---|---|
| Hermes | deepseek-v4-pro | 300k | 32k |
| Vitruvius | deepseek-v4-pro | 300k | 32k |
| Da Vinci | deepseek-v4-pro | 300k | 32k |
| Argus | glm-5.2 | 300k | 32k |

All 20 models available via proxy at `localhost:8320`. Auto-compaction triggers at 300k tokens — context is summarized and the window resets cleanly.

---

## Configuring Your Provider

In `opencode.jsonc`, update the provider block to point at your proxy:

```jsonc
{
  "providers": {
    "my-proxy": {
      "baseURL": "http://localhost:8320/v1",
      "apiKey": "your-key-here",
      "models": ["deepseek-v4-pro", "glm-5.2"]
    }
  }
}
```

Replace `baseURL` and `apiKey` with your own values. The proxy handles routing to the underlying model endpoints.

---

## File Structure

```
~/.config/opencode/
├── opencode.jsonc
├── agents/
│   ├── hermes.md
│   ├── vitruvius.md
│   ├── da-vinci.md
│   └── argus.md
└── skills/          (27+ directories)
    ├── caveman/
    ├── design-craft/
    ├── design-qa/
    ├── diagnose/
    ├── git-guardrails-claude-code/
    ├── grill-me/
    ├── grill-with-docs/
    ├── handoff/
    ├── improve/
    ├── improve-codebase-architecture/
    ├── laws-of-ux/
    ├── loop-library/
    ├── prototype/
    ├── ralph-loop/
    ├── react-doctor/
    ├── review/
    ├── setup-pre-commit/
    ├── tdd/
    ├── teach/
    ├── to-issues/
    ├── to-prd/
    ├── torpathy/
    ├── triage/
    ├── write-a-skill/
    ├── writing-beats/
    ├── writing-fragments/
    ├── writing-shape/
    └── zoom-out/
```

---

## Credits

- Skills: [@mattpocock/skills](https://github.com/mattpocock), [@shadcn/improve](https://github.com/shadcn), [@millionco/react-doctor](https://github.com/aidenybai), [@FasalZein/design-skills](https://github.com/FasalZein), [@FasalZein/ralph-loop](https://github.com/FasalZein), [@Forward-Future/loop-library](https://github.com/Forward-Future), [@edxeth/torpathy](https://github.com/edxeth)
- OpenCode: [opencode.ai](https://opencode.ai)
- Agent designs: Custom-built for this configuration

---

## License

MIT
