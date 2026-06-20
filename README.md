# OpenCode — The Olympus Team

A production-ready OpenCode configuration with three legendary AI agents, 27 battle-tested skills, and a complete design-quality pipeline.

## Quick Start

```powershell
git clone https://github.com/Sid8050/My-Skill-and-Agents.git $env:USERPROFILE\.config\opencode
```

**Prerequisites:** [OpenCode CLI](https://opencode.ai) v1.17+, Node.js

---

## The Olympus Team

Three legendary agents, each named after history's greatest in their domain. They collaborate through two shared folders — `architect/` for greenfield designs and `plans/` for brownfield audits — a protocol as old as civilization itself.

| Agent | Name | Inspiration | Model | Mode | Role |
|-------|------|-------------|-------|------|------|
| **Vitruvius** | The Architect | Marcus Vitruvius Pollio — Roman architect whose *De Architectura* defined architecture for 2000 years | deepseek-v4-pro | all | Requirements → Blueprints |
| **Da Vinci** | The Maker | Leonardo da Vinci — history's greatest polymath, master of art, science, and engineering | deepseek-v4-pro | primary | Reads `architect/` → Implements |
| **Argus** | The Watcher | Argus Panoptes — the hundred-eyed giant of Greek myth whose gaze never slept | kimi-k2.6 | subagent | Reads `architect/` → Tests |

### The Olympus Protocol

```
# Greenfield Workflow (new projects)
User → Vitruvius → Creates architect/NNN-task/ blueprints (firmitas, utilitas, venustas)
         ↓
     Da Vinci → Reads architect/ → Implements → Self-reviews → Invokes Argus
         ↓
     Argus → Reads architect/ → Hundred-eyed scrutiny → Reports → Da Vinci fixes → Re-test
         ↓
     ✅ Fit for Olympus

# Brownfield Workflow (existing codebases)
User → Vitruvius → Audits codebase via improve skill → Writes plans/NNN-plan/ improvement plan
         ↓
     Da Vinci → Reads plans/ → Executes improvements → Self-reviews → Invokes Argus
         ↓
     Argus → Reads plans/ → Audits against 11-category checklist → Reports → Da Vinci fixes → Re-test
         ↓
     ✅ Fit for Olympus
```

---

## Shared Folder Convention

Both `architect/` and `plans/` use numbered subfolders. The root contains **only** a `README.md` index. Never flat files.

```
architect/                              plans/
├── README.md                           ├── README.md
├── 001-user-auth/                      ├── 001-fix-n-plus-one/
│   ├── README.md                       │   ├── plan.md
│   ├── 01-requirements.md              │   └── findings.md
│   ├── 02-architecture.md              ├── 002-migrate-dependencies/
│   ├── 03-tech-stack.md                │   ├── plan.md
│   ├── 04-data-model.md                │   └── findings.md
│   ├── 05-api-design.md                └── 003-add-rate-limiting/
│   ├── 06-component-tree.md                ├── plan.md
│   ├── 07-file-structure.md                └── findings.md
│   ├── 08-data-flow.md
│   ├── 09-security.md
│   ├── 10-test-strategy.md
│   └── decisions/
├── 002-payment-system/
│   └── ...
└── 003-dashboard/
    └── ...
```

**❌ FORBIDDEN — NEVER DO THIS:**
```
plans/
├── fix-categories.md        ← FLAT FILE IN ROOT — VIOLATION
├── qc-route-card.md         ← FLAT FILE IN ROOT — VIOLATION
├── deployment-plan.md       ← FLAT FILE IN ROOT — VIOLATION
```

**Rules:**
1. Every task/plan gets `NNN-slug/` — three-digit padded number, hyphenated slug
2. Root contains only `README.md` — no `.md` files, no folders besides `NNN-slug/`
3. Architect tasks: numbered docs (`01-requirements.md`, etc.). Plan tasks: `plan.md` + `findings.md`
4. Numbers are monotonic and never reused
5. Cross-item dependencies documented in the master index

---

## Agent Deep Dives

### Vitruvius — The Architect

**Two workflows:**

| Mode | Trigger | Output |
|------|---------|--------|
| **Greenfield** | "Build me X" / "Design X" | `architect/NNN-task/` — numbered architecture documents |
| **Brownfield** | "Audit this codebase" / "Find improvements" | Load `improve` skill → `plans/NNN-plan/plan.md` + `findings.md` |

**What he produces (numbered document set):**
1. `01-requirements.md` — Functional + non-functional requirements
2. `02-architecture.md` — System design, Mermaid diagrams, cross-cutting concerns
3. `03-tech-stack.md` — Language, framework, database, justification for each
4. `04-data-model.md` — SQL/Prisma/Drizzle schemas, TypeScript interfaces
5. `05-api-design.md` — REST endpoints, request/response types, error format
6. `06-component-tree.md` — React component hierarchy, props, state
7. `07-file-structure.md` — Directory layout, barrel exports, naming conventions
8. `08-data-flow.md` — Mermaid sequence diagrams for every critical path
9. `09-security.md` — Auth model, threat surface, input validation strategy
10. `10-test-strategy.md` — Unit/integration/E2E boundaries, coverage targets

**Key skills:** `zoom-out`, `improve`, `torpathy`, `design-craft`, `laws-of-ux`, `to-prd`, `triage`, `grill-with-docs`, `write-a-skill`, `teach`, `handoff`, `diagnose`, `improve-codebase-architecture`, `react-doctor`, `loop-library`

**The Architect's Oath:**
> You do not write code. Ever. Under any circumstances. Not a single line. Not a snippet. Not "just this quick example." Da Vinci codes. You design. Period.

**Every response ends with a handoff:**
```
---
Ready for implementation? Switch to Da Vinci (Tab → Da Vinci) with:
Da Vinci, implement architect/NNN-task/ — start with [suggested first module].
```

---

### Da Vinci — The Maker

**The Da Vinci Code (non-negotiable standards):**
- Strict TypeScript, no `any`, explicit return types
- Functional React components, proper state management (useState/context/zustand/react-query)
- RESTful APIs with input validation at every boundary
- Database migrations only, parameterized queries, no N+1
- 80%+ test coverage on new code
- Handling loading, empty, error, and success states for every component
- Accessibility: semantic HTML, ARIA labels, keyboard navigation
- Responsive: mobile-first, tested at 320px/768px/1024px/1440px

**UI Design Stack — Four Layers:**

| Layer | Skill | Responsibility |
|-------|-------|----------------|
| 1. Component Library | coss.com/ui | 49+ Base UI primitives (Button, Dialog, Table, etc.) |
| 2. Design Craft | `design-craft` | Anti-slop, OKLCH color, typography scale, 4px grid, animation, interactions |
| 3. UX Psychology | `laws-of-ux` | 30 UX laws, navigation design, form flows, CTA hierarchy |
| 4. Design QA | `design-qa` | 11-gate pre-ship scanner (anti-slop, a11y, spacing, interaction, perf) |

**Pre-commit checklist:**
1. Run linter + typecheck — zero errors
2. Run tests — all pass
3. Run `npx react-doctor@latest --score --scope changed` — score stable, no regressions
4. Load `design-qa` — all 11 gates pass, 0 critical failures

**Key skills:** `caveman`, `tdd`, `diagnose`, `react-doctor`, `design-craft`, `design-qa`, `laws-of-ux`, `loop-library`, `improve`, `prototype`, `handoff`, `teach`, `zoom-out`, `to-issues`, `grill-me`, `git-guardrails-claude-code`, `setup-pre-commit`

---

### Argus — The Watcher

**The Hundred-Eyed Method:**
1. Read `architect/README.md` / `plans/README.md`
2. Read relevant architecture docs or improvement plans
3. Read the implementation code
4. Identify test gaps (unit, integration, component, E2E)
5. Write missing tests
6. Run all tests — investigate failures
7. Perform manual code review against 11 audit categories
8. Deliver structured report to Da Vinci

**11-Category Audit Checklist:**
1. **Correctness** — Does it match the spec? Error handling, async hazards, null flows, boundary conditions
2. **Security** — Credential hygiene, injection vectors, access control, input validation, dependency audit
3. **Performance** — N+1 queries, algorithmic complexity, payload size, render waterfalls
4. **Test Coverage** — Critical paths covered, missing test layers, assertion quality
5. **Tech Debt** — Duplication, layering violations, dead code
6. **Dependencies** — Version lag, deprecated APIs, duplicate deps
7. **DX & Tooling** — Build/lint/typecheck passing, .env.example fresh, README correct
8. **Documentation** — Public API documented, stale docs flagged
9. **Spec Compliance** — Field names, types, endpoints match Vitruvius's specs exactly
10. **React Health** — `npx react-doctor@latest --verbose`, no score regression, no anti-patterns
11. **UI Design Quality** — `design-qa` gates: anti-slop, color tokens, spacing, interaction, a11y, edge cases, responsive

**Bug Severity — The Scale of Olympus:**

| Level | Name | Criteria | Action |
|-------|------|----------|--------|
| **P0** | Titan | Data loss, security breach, app crash, wrong results | Fix immediately |
| **P1** | Olympian | Broken feature, missing validation, spec violation | Fix before merge |
| **P2** | Mortal | Performance issue, missing error state, a11y gap | Fix next iteration |
| **P3** | Nymph | Code style, missing comment, minor UX nit | Optional |

**Output format:**
```markdown
## Argus Report — [Module Name]
### Verdict: APPROVED / CHANGES REQUIRED / REJECTED
### Summary (tests run/passed/failed, bugs by severity)
### Test Results (table with coverage)
### Bugs Found (severity + file + expected/actual + reproduction + fix)
### Compliance Against Vitruvius's Specs (requirement-by-requirement)
```

**Key skills:** `diagnose`, `tdd`, `design-qa`, `react-doctor`, `loop-library`, `review`, `to-issues`, `caveman`, `handoff`, `zoom-out`, `improve`, `design-craft`

---

## Skills (27 Total)

### Design (3)

| Skill | Description |
|-------|-------------|
| `design-craft` | Anti-slop rules, OKLCH color system, typography scale, 4px grid, animation gating, interaction states, component patterns. Eliminates AI-generated UI slop |
| `design-qa` | 11-gate pre-ship scanner — anti-slop, typography, color, spacing, reuse, interaction, a11y, edge cases, perf, responsive, error resilience. Binary pass/fail |
| `laws-of-ux` | 30 UX psychology laws + decision matrix. Navigation, forms, flows, CTAs, feedback. The "why" behind design-craft's "how" |

### Engineering (6)

| Skill | Description |
|-------|-------------|
| `react-doctor` | React health scoring (0–100), pre-commit regression check, anti-pattern detection, bundle analysis, accessibility audit |
| `loop-library` | 31 repeatable agent workflows with triggers, verification, stopping conditions, and guardrails. Architecture, engineering, and evaluation loops |
| `improve` | Brownfield codebase auditor — 9-category audit (bugs, security, perf, tests, tech debt, deps, DX, docs, direction) producing executable improvement plans |
| `diagnose` | Structured debugging loop: reproduce → minimise → hypothesise → instrument → fix → regression-test |
| `tdd` | Test-driven development with red-green-refactor loop. Vertical slices, behavior-testing tests |
| `prototype` | Rapid throwaway proof-of-concepts. Routes between terminal apps for logic questions and UI variations for design exploration |

### Architecture (3)

| Skill | Description |
|-------|-------------|
| `torpathy` | Karpathy + Torvalds decision framework. Two-lens analysis: why the system behaves this way (Karpathy) + where the fix/design belongs (Torvalds). Architecture trade-off resolution |
| `zoom-out` | High-level codebase map — dependency graph, module ownership, entry points. For entering unfamiliar codebases |
| `improve-codebase-architecture` | Systematic architecture refactoring. Finds deepening opportunities, tight coupling, testability gaps. Domain-language informed |

### Productivity (9)

| Skill | Description |
|-------|-------------|
| `caveman` | Ultra-compressed communication mode. ~75% token savings, full technical accuracy |
| `handoff` | Compact conversation-to-handoff document for agent-to-agent context transfer |
| `teach` | Teach a concept, pattern, or decision within the workspace |
| `to-prd` | Convert conversation context into a Product Requirements Document |
| `triage` | Issue triage state machine. Prioritize, categorize, route bugs and features |
| `grill-me` | Relentless interview about a plan or design until reaching shared understanding |
| `grill-with-docs` | Challenge a plan against existing domain model and docs, sharpen terminology, update documentation inline |
| `to-issues` | Break a plan/spec/PRD into independently-grabbable issues using tracer-bullet vertical slices |
| `write-a-skill` | Create new agent skills with proper structure, progressive disclosure, and bundled resources |

### Tooling (3)

| Skill | Description |
|-------|-------------|
| `git-guardrails-claude-code` | Block dangerous git commands (push, reset --hard, clean, branch -D) before they execute |
| `setup-pre-commit` | Bootstrap Husky pre-commit hooks with lint-staged, Prettier, type checking, and tests |
| `review` | Review changes along two axes — Standards (coding conventions) and Spec (match to requirements) — in parallel sub-agents |

### Writing (3)

| Skill | Description |
|-------|-------------|
| `writing-beats` | Shape an article as a journey of beats, choose-your-own-adventure style, beat by beat |
| `writing-fragments` | Mining session for raw material — claims, vignettes, sharp sentences — appended to a single document |
| `writing-shape` | Take raw markdown and shape it into a publishable article through conversational editing |

---

## Skill-to-Agent Mapping

| Skill | Vitruvius | Da Vinci | Argus |
|-------|:---------:|:--------:|:-----:|
| `caveman` | | ✓ | ✓ |
| `design-craft` | ✓ | ✓ | ✓ |
| `design-qa` | | ✓ | ✓ |
| `diagnose` | ✓ | ✓ | ✓ |
| `git-guardrails-claude-code` | | ✓ | |
| `grill-me` | | ✓ | |
| `grill-with-docs` | ✓ | | |
| `handoff` | ✓ | ✓ | ✓ |
| `improve` | ✓ | ✓ | ✓ |
| `improve-codebase-architecture` | ✓ | | |
| `laws-of-ux` | ✓ | ✓ | |
| `loop-library` | ✓ | ✓ | ✓ |
| `prototype` | | ✓ | |
| `react-doctor` | ✓ | ✓ | ✓ |
| `review` | | | ✓ |
| `setup-pre-commit` | | ✓ | |
| `tdd` | | ✓ | ✓ |
| `teach` | ✓ | ✓ | |
| `to-issues` | | ✓ | ✓ |
| `to-prd` | ✓ | | |
| `torpathy` | ✓ | | |
| `triage` | ✓ | | |
| `write-a-skill` | ✓ | | |
| `writing-beats` | — | — | — |
| `writing-fragments` | — | — | — |
| `writing-shape` | — | — | — |
| `zoom-out` | ✓ | ✓ | ✓ |

---

## Context Compaction

DeepSeek V4 Pro is capped at **300k tokens** (down from 1M) for cost efficiency. Auto-compaction is enabled with pruning of old tool outputs. A 10k token buffer is reserved.

```jsonc
"compaction": {
  "auto": true,
  "prune": true,
  "reserved": 10000
}
```

---

## File Structure

```
~/.config/opencode/
├── opencode.jsonc              # Main config: providers, agents, compaction, permissions
├── agents/
│   ├── vitruvius.md            # The Architect — designs before code
│   ├── da-vinci.md             # The Maker — implements flawlessly
│   └── argus.md                # The Watcher — tests everything
└── skills/
    ├── caveman/SKILL.md
    ├── design-craft/SKILL.md
    ├── design-qa/SKILL.md
    ├── diagnose/SKILL.md
    ├── git-guardrails-claude-code/SKILL.md
    ├── grill-me/SKILL.md
    ├── grill-with-docs/SKILL.md
    ├── handoff/SKILL.md
    ├── improve/SKILL.md
    ├── improve-codebase-architecture/SKILL.md
    ├── laws-of-ux/SKILL.md
    ├── loop-library/SKILL.md
    ├── prototype/SKILL.md
    ├── react-doctor/SKILL.md
    ├── review/SKILL.md
    ├── setup-pre-commit/SKILL.md
    ├── tdd/SKILL.md
    ├── teach/SKILL.md
    ├── to-issues/SKILL.md
    ├── to-prd/SKILL.md
    ├── torpathy/SKILL.md
    ├── triage/SKILL.md
    ├── write-a-skill/SKILL.md
    ├── writing-beats/SKILL.md
    ├── writing-fragments/SKILL.md
    ├── writing-shape/SKILL.md
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

Available models in the default config: `deepseek-v4-pro`, `deepseek-v4-flash`, `glm-5.1`, `glm-5`, `kimi-k2.6`, `kimi-k2.5`, `mimo-v2.5`, `mimo-v2.5-pro`, `minimax-m3`, `minimax-m2.7`, `minimax-m2.5`, `qwen3.7-max`, `qwen3.7-plus`, `qwen3.6-plus`.

---

## Credits

- **Skills:** [@mattpocock/skills](https://github.com/mattpocock/skills) (base collection), [@shadcn/improve](https://github.com/shadcn/improve), [@millionco/react-doctor](https://github.com/millionco/react-doctor), [@FasalZein/design-skills](https://github.com/FasalZein/design-skills) (design-craft, design-qa, laws-of-ux), [@Forward-Future/loop-library](https://github.com/Forward-Future/loop-library), [@edxeth/torpathy](https://github.com/edxeth/torpathy)
- **OpenCode:** [opencode.ai](https://opencode.ai) — The AI-powered coding CLI
- **Agent designs:** Custom-built, named after history's greatest

## License

MIT — Use, modify, and share freely. Summon the Olympus Team.
