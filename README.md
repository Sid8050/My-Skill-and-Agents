# OpenCode — The Olympus Team

A production-ready OpenCode configuration with three legendary interconnected AI agents and 23 battle-tested skills. Drop this into `~/.config/opencode/` and summon a complete, professional development workflow powered by history's greatest minds.

## Quick Start

```powershell
# Clone into your OpenCode config directory
git clone https://github.com/Sid8050/My-Skill-and-Agents.git $env:USERPROFILE\.config\opencode

# OR clone elsewhere and symlink / copy what you need
```

**Prerequisites:**
- [OpenCode CLI](https://opencode.ai) v1.17+
- Node.js (for npm-based providers)
- Your provider API keys configured via `/connect` or `opencode.jsonc`

---

## The Olympus Team

Three legendary agents, each named after history's greatest in their domain. They collaborate through two shared folders — `architect/` for greenfield designs and `plans/` for brownfield improvement audits — a protocol as old as civilization itself.

| Agent | Name | Inspiration | Model | Role |
|-------|------|-------------|-------|------|
| **Vitruvius** | The Architect | Marcus Vitruvius Pollio — Roman architect whose *De Architectura* defined architecture for 2000 years | deepseek-v4-pro | Requirements → Architecture blueprints |
| **Da Vinci** | The Maker | Leonardo da Vinci — history's greatest polymath, master of art, science, and engineering | deepseek-v4-pro | Reads `architect/` → Implements flawlessly |
| **Argus** | The Watcher | Argus Panoptes — the hundred-eyed giant of Greek myth whose gaze never slept | kimi-k2.6 | Reads `architect/` → Tests relentlessly |

### The Olympus Protocol

```
# Greenfield Workflow (new projects)
User → Vitruvius → Creates architect/ blueprints (firmitas, utilitas, venustas)
         ↓
     Da Vinci → Reads architect/ → Implements → Self-reviews → Invokes Argus
         ↓
     Argus → Reads architect/ → Hundred-eyed scrutiny → Reports → Da Vinci fixes → Re-test
         ↓
     ✅ Fit for Olympus

# Brownfield Workflow (existing codebases)
User → Vitruvius → Audits codebase via improve skill → Writes plans/ improvement plan
         ↓
     Da Vinci → Reads plans/ → Executes improvements → Self-reviews → Invokes Argus
         ↓
     Argus → Reads plans/ → Audits against 9-category playbook → Reports → Da Vinci fixes → Re-test
         ↓
     ✅ Fit for Olympus
```

---

## Agents

### Vitruvius — The Architect

**Purpose:** Vitruvius operates in two modes. In **greenfield** mode he converts requirements into crystal-clear architecture blueprints embodying *firmitas* (durability), *utilitas* (utility), and *venustas* (beauty). In **brownfield** mode he audits existing codebases via the `improve` skill and writes self-contained improvement plans.

**Produces in `architect/` folder (greenfield — task-based subfolders):**
```
architect/
├── README.md                   # Master index + navigation
├── 001-user-auth/
│   ├── 01-requirements.md
│   ├── 02-architecture.md
│   ├── 03-tech-stack.md
│   ├── 04-data-model.md
│   ├── 05-api-design.md
│   ├── 06-component-tree.md
│   ├── 07-file-structure.md
│   ├── 08-data-flow.md
│   ├── 09-security.md
│   ├── 10-test-strategy.md
│   └── decisions/
├── 002-payment/
│   └── ...
└── 003-dashboard/
    └── ...
```

**Produces in `plans/` folder (brownfield — improvement audits):**
```
plans/
├── README.md                   # Master index of all plans
├── 001-refactor-auth-layer/
│   └── plan.md
├── 002-database-migration/
│   └── plan.md
└── 003-api-performance/
    └── plan.md
```

**Key permissions:** Can write `architect/**` freely, bash denied, edit elsewhere requires approval.

**Key skills:** `zoom-out`, `improve`, `improve-codebase-architecture`, `to-prd`, `grill-with-docs`, `triage`, `teach`, `handoff`, `diagnose`

---

### Da Vinci — The Maker

**Purpose:** Implement Vitruvius's architecture specs with production-grade, beautiful code. Masters the full stack — frontend aesthetics, backend precision, database elegance, infrastructure resilience.

**The Da Vinci Code (non-negotiable standards):**
- Strict TypeScript, no `any`, explicit return types
- Functional React components, proper state management (useState/context/zustand/react-query)
- RESTful APIs with input validation at every boundary
- Database migrations only, parameterized queries, no N+1
- 80%+ test coverage on new code
- Handles loading, empty, error, and success states for every component
- Accessibility: semantic HTML, ARIA labels, keyboard navigation
- Responsive: mobile-first, tested at 320px/768px/1024px/1440px

**Workflow:**
1. Reads `architect/README.md` or `plans/README.md` — never skips
2. Plans implementation order
3. Implements methodically, one module at a time
4. Self-reviews after each module
5. Invokes `@argus` after logical units
6. Fixes Argus's findings and re-tests before continuing

**Pre-commit checklist:** react-doctor health score stable + no regressions, lint + typecheck pass, tests pass, no dead code/TODOs, error boundaries on async ops, input validation at entries, no secrets in code, accessible + responsive.

**Key skills:** `caveman`, `tdd`, `improve`, `diagnose`, `prototype`, `to-issues`, `grill-me`, `handoff`, `teach`, `git-guardrails-claude-code`, `setup-pre-commit`, `zoom-out`, `react-doctor`

---

### Argus — The Watcher

**Purpose:** The final guardian. Nothing ships without his hundred-eyed approval. Finds every bug, every edge case, every silent failure before it reaches production.

**The Hundred-Eyed Method (10-category audit-playbook):**
1. Reads `architect/README.md` or `plans/README.md` — understands Vitruvius's vision
2. Reads relevant architecture docs or improvement plans
3. Reads Da Vinci's implementation
4. Identifies test gaps
5. Writes missing tests (unit, integration, component, E2E)
6. Runs all tests
7. Performs manual code review against 10 audit categories
8. Delivers structured report to Da Vinci

**The 10 Audit Categories:**
1. **Correctness** — Does it match the spec?
2. **Security** — Injection, auth, secrets, data exposure
3. **Performance** — N+1 queries, unnecessary re-renders, memory leaks
4. **Error Handling** — Boundaries, fallbacks, user-facing messages
5. **Testing** — Coverage gaps, flaky tests, missing edge cases
6. **Accessibility** — ARIA, keyboard nav, screen readers, contrast
7. **Responsiveness** — 320px/768px/1024px/1440px breakpoints
8. **Code Quality** — Type safety, dead code, naming, coupling
9. **Documentation** — Inline docs, README coverage, ADR freshness
10. **React Health** — `npx react-doctor@latest` scan, no health score regressions, anti-patterns caught (unstable context, missing keys, useEffect deps), bundle size, accessibility

**Bug Severity — The Scale of Olympus:**

| Level | Name | Meaning |
|-------|------|---------|
| **P0** | Titan | Data loss, security breach, crash — Fix immediately |
| **P1** | Olympian | Broken feature, spec violation — Fix before merge |
| **P2** | Mortal | Performance, missing error state — Fix next iteration |
| **P3** | Nymph | Code style, minor UX — Optional |

**Output format:**
```markdown
## Argus Report — [Module Name]
### Verdict: APPROVED / CHANGES REQUIRED / REJECTED
### Summary (tests run/passed/failed, bugs by severity)
### Test Results (table with coverage)
### Bugs Found (severity + file + expected/actual + reproduction + fix)
### Compliance Against Vitruvius's Specs (requirement-by-requirement)
```

**Sandboxed permissions:** Can only write test files, can only run test/lint commands. Cannot touch source code.

**Key skills:** `diagnose`, `tdd`, `improve`, `review`, `to-issues`, `caveman`, `handoff`, `zoom-out`, `react-doctor`

---

## Skills (23 from [@mattpocock/skills](https://github.com/mattpocock/skills))

Skills are reusable instruction sets that agents load on-demand via the `skill` tool.

| Skill | Category | Best For |
|-------|----------|----------|
| `caveman` | Productivity | Ultra-compressed communication, ~75% token savings |
| `diagnose` | Engineering | Structured debugging loop (reproduce → minimise → hypothesise → fix) |
| `tdd` | Engineering | Test-driven development with red-green-refactor |
| `prototype` | Engineering | Rapid throwaway proof-of-concepts before committing |
| `react-doctor` | Engineering | React health scoring, pre-commit guard, accessibility + performance scan |
| `zoom-out` | Engineering | High-level codebase map when entering unfamiliar code |
| `improve-codebase-architecture` | Engineering | Systematic architecture refactoring |
| `triage` | Engineering | Prioritize issues and requirements |
| `to-issues` | Engineering | Convert specs/bugs into actionable GitHub issues |
| `to-prd` | Engineering | Convert requirements into Product Requirements Documents |
| `torpathy` | Engineering | Strategic decision framework — weigh tradeoffs, decide where a fix belongs |
| `grill-with-docs` | Engineering | Verify designs against existing documentation |
| `grill-me` | Productivity | Relentless interview about a plan |
| `review` | In-Progress | Structured code review against specs |
| `handoff` | Productivity | Compact conversation summary for agent-to-agent handoff |
| `improve` | Engineering | Audits codebases and writes self-contained improvement plans in `plans/` |
| `teach` | Productivity | Explain concepts, patterns, and decisions |
| `write-a-skill` | Productivity | Encode repeatable patterns as new skills |
| `git-guardrails-claude-code` | Misc | Safe git operations and conventions |
| `setup-pre-commit` | Misc | Bootstrap pre-commit hooks, linting, formatting |
| `writing-beats` | In-Progress | Structured beat-by-beat writing format |
| `writing-fragments` | In-Progress | Composable writing fragments |
| `writing-shape` | In-Progress | Shape-first writing approach |

### Skill-to-Agent Mapping

| Skill | Vitruvius | Da Vinci | Argus |
|-------|:---------:|:--------:|:-----:|
| zoom-out | ✓ | ✓ | ✓ |
| diagnose | ✓ | ✓ | ✓ |
| handoff | ✓ | ✓ | ✓ |
| improve | ✓ | ✓ | ✓ |
| react-doctor | ✓ | ✓ | ✓ |
| teach | ✓ | ✓ | |
| tdd | | ✓ | ✓ |
| to-issues | | ✓ | ✓ |
| caveman | | ✓ | ✓ |
| improve-codebase-architecture | ✓ | | |
| to-prd | ✓ | | |
| torpathy | ✓ | | |
| grill-with-docs | ✓ | | |
| triage | ✓ | | |
| write-a-skill | ✓ | | |
| prototype | | ✓ | |
| grill-me | | ✓ | |
| git-guardrails-claude-code | | ✓ | |
| setup-pre-commit | | ✓ | |
| review | | | ✓ |

---

## Context Compaction

DeepSeek V4 Pro is capped at **300k tokens** (down from 1M) for cost efficiency. Auto-compaction is enabled with pruning of old tool outputs. The compaction reserves a 10k token buffer.

---

## File Structure

```
~/.config/opencode/
├── opencode.jsonc          # Main config: providers, agents, compaction, permissions
├── agents/
│   ├── vitruvius.md        # The Architect — designs before code
│   ├── da-vinci.md         # The Maker — implements flawlessly
│   └── argus.md            # The Watcher — tests everything
└── skills/
    ├── caveman/SKILL.md
    ├── diagnose/SKILL.md
    ├── tdd/SKILL.md
    ├── ... (23 total)
    └── zoom-out/SKILL.md
```

---

## Configuring Your Provider

The default `opencode.jsonc` routes through a local proxy at `localhost:8320`. To use a different provider, update the `provider` section:

```jsonc
"provider": {
  "opencode-go-zen": {
    "npm": "@ai-sdk/openai-compatible",
    "name": "Your Provider Name",
    "options": {
      "baseURL": "https://your-api-endpoint.com",
      "apiKey": "{env:YOUR_API_KEY}",
      "timeout": 300000
    },
    "models": {
      "your-model-id": { "id": "your-model-id" }
    }
  }
}
```

Then update the agent models (search for `model: opencode-go-zen/` in agent files).

---

## Customization

### Adding new skills
Place new skills in `skills/<skill-name>/SKILL.md` with YAML frontmatter:
```markdown
---
name: my-skill
description: What this skill does and when to use it
---
## Instructions
...
```

### Adding new agents
Create `agents/<agent-name>.md` with YAML frontmatter:
```markdown
---
description: What this agent does
mode: primary|subagent|all
model: provider/model-id
temperature: 0.1
permission:
  edit: allow|deny|ask
  bash: allow|deny|ask
---
# Agent Name
System prompt content...
```

### Overriding per-project
Place an `opencode.json` in your project root. It merges with and overrides the global config.

---

## Credits

- **Skills:** [@mattpocock/skills](https://github.com/mattpocock/skills) — MIT licensed
- **OpenCode:** [opencode.ai](https://opencode.ai) — The AI-powered coding CLI
- **Agent designs:** Custom-built for this configuration, named after history's greatest

## License

MIT — Use, modify, and share freely. Summon the Olympus Team.
