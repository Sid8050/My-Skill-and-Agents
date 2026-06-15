# OpenCode — Elite Agent Team + Skills

A production-ready OpenCode configuration with three interconnected AI agents and 20 battle-tested skills. Drop this into `~/.config/opencode/` and get a complete, professional development workflow.

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

## What's Inside

### Three Interconnected A-Team Agents

| Agent | Mode | Model | Role |
|-------|------|-------|------|
| **Architect** | Primary + Subagent | deepseek-v4-pro | Requirements → Architecture blueprints |
| **Fullstack Dev** | Primary | deepseek-v4-pro | Reads architect/ → Implements flawlessly |
| **QA Tester** | Subagent | kimi-k2.6 | Reads architect/ → Tests rigorously |

### Shared Workspace Protocol

All three agents collaborate through a shared `architect/` folder at project root. The Architect creates numbered blueprint documents. The Developer and QA tester read them before doing anything.

```
User → Architect → Creates architect/ blueprints
         ↓
     Fullstack Dev → Reads architect/ → Implements → Self-reviews → Invokes QA
         ↓
     QA Tester → Reads architect/ → Tests → Reports bugs → Dev fixes → Re-test
```

### 20 Agent Skills (from [@mattpocock/skills](https://github.com/mattpocock/skills))

Skills are reusable instruction sets that agents load on-demand via the `skill` tool.

| Skill | Category | Best For |
|-------|----------|----------|
| `caveman` | Productivity | Ultra-compressed communication, ~75% token savings |
| `diagnose` | Engineering | Structured debugging loop (reproduce → minimise → hypothesise → fix) |
| `tdd` | Engineering | Test-driven development with red-green-refactor |
| `prototype` | Engineering | Rapid throwaway proof-of-concepts before committing to architecture |
| `zoom-out` | Engineering | High-level codebase map when entering unfamiliar code |
| `improve-codebase-architecture` | Engineering | Systematic architecture refactoring |
| `triage` | Engineering | Prioritize issues and requirements |
| `to-issues` | Engineering | Convert specs/bugs into actionable GitHub issues |
| `to-prd` | Engineering | Convert requirements into Product Requirements Documents |
| `grill-with-docs` | Engineering | Verify designs against existing documentation |
| `grill-me` | Productivity | Relentless interview about a plan until shared understanding |
| `review` | In-Progress | Structured code review against architecture specs |
| `handoff` | Productivity | Compact conversation summary for agent-to-agent handoff |
| `teach` | Productivity | Explain concepts, patterns, and decisions |
| `write-a-skill` | Productivity | Encode repeatable patterns as new skills |
| `git-guardrails-claude-code` | Misc | Safe git operations and conventions |
| `setup-pre-commit` | Misc | Bootstrap pre-commit hooks, linting, formatting |
| `writing-beats` | In-Progress | Structured beat-by-beat writing format |
| `writing-fragments` | In-Progress | Composable writing fragments |
| `writing-shape` | In-Progress | Shape-first writing approach |

### Skill-to-Agent Mapping

Each agent has permission-scoped access to relevant skills:

| Skill | Architect | Fullstack Dev | QA Tester |
|-------|:---------:|:-------------:|:---------:|
| zoom-out | ✓ | ✓ | ✓ |
| diagnose | ✓ | ✓ | ✓ |
| handoff | ✓ | ✓ | ✓ |
| teach | ✓ | ✓ | |
| tdd | | ✓ | ✓ |
| to-issues | | ✓ | ✓ |
| caveman | | ✓ | ✓ |
| improve-codebase-architecture | ✓ | | |
| to-prd | ✓ | | |
| grill-with-docs | ✓ | | |
| triage | ✓ | | |
| write-a-skill | ✓ | | |
| prototype | | ✓ | |
| grill-me | | ✓ | |
| git-guardrails-claude-code | | ✓ | |
| setup-pre-commit | | ✓ | |
| review | | | ✓ |

### Context Compaction

DeepSeek V4 Pro is capped at **300k tokens** (down from 1M) for cost efficiency. Auto-compaction is enabled with pruning of old tool outputs. The compaction reserves a 10k token buffer.

```json
"compaction": {
  "auto": true,
  "prune": true,
  "reserved": 10000
}
```

## File Structure

```
~/.config/opencode/
├── opencode.jsonc          # Main config: providers, agents, compaction, permissions
├── agents/
│   ├── architect.md        # System architect — designs before code
│   ├── fullstack-dev.md    # Elite fullstack developer — implements flawlessly
│   └── qa-tester.md        # Relentless QA — tests everything
└── skills/
    ├── caveman/SKILL.md
    ├── diagnose/SKILL.md
    ├── tdd/SKILL.md
    ├── ... (20 total)
    └── zoom-out/SKILL.md
```

## Agent Deep Dive

### Architect (`architect`)

**Purpose:** Convert requirements into crystal-clear architecture blueprints.

**Produces in `architect/` folder:**
```
architect/
├── README.md              # Index + navigation
├── 01-requirements.md      # Distilled functional/non-functional requirements
├── 02-architecture.md      # High-level patterns, layers, deployment
├── 03-tech-stack.md        # Technology choices with justifications
├── 04-data-model.md        # DB schema, entities, relationships, migrations
├── 05-api-design.md        # REST/GraphQL endpoints, request/response shapes
├── 06-component-tree.md    # Frontend hierarchy, state, routing
├── 07-file-structure.md    # Exact project folder structure
├── 08-data-flow.md         # Mermaid diagrams for key flows
├── 09-security.md          # Auth model, threat analysis
├── 10-test-strategy.md     # Testing pyramid, edge cases
└── decisions/              # Architecture Decision Records (ADRs)
```

**Key permissions:** Can write `architect/**` freely, bash denied, edit elsewhere requires approval.

### Fullstack Developer (`fullstack-dev`)

**Purpose:** Implement architecture specs with production-grade code.

**Workflow:**
1. Reads `architect/README.md` — never skips this step
2. Plans implementation order
3. Implements methodically, one module at a time
4. Self-reviews after each module (checklist below)
5. Invokes `@qa-tester` after logical units
6. Fixes QA findings and re-tests before continuing

**Coding standards enforced:**
- Strict TypeScript, no `any`, explicit return types
- Functional React components, proper state management
- RESTful APIs with input validation at every boundary
- Database migrations only, parameterized queries, no N+1
- 80%+ test coverage on new code
- Conventional commits, one logical change per commit
- Handles loading, empty, error, and success states for every component

**Pre-commit self-review checklist:**
- Lint + typecheck pass
- Tests pass
- No console.log / dead code / TODOs
- Error boundaries on every async operation
- Input validation at every entry point
- No secrets in code
- Accessibility + responsive design verified

### QA Tester (`qa-tester`)

**Purpose:** Find every bug before it reaches production.

**Reports in structured format:**
```
## QA Report — [Module Name]
### Summary
- Tests: X passed, Y failed, Z new
- Bugs: P0=X (critical), P1=Y (high), P2=Z (medium), P3=W (low)
### Test Results (table with coverage)
### Bugs Found (severity + file + expected/actual + reproduction + fix)
### Compliance Against Architect/ Specs (requirement-by-requirement)
```

**Bug severity classification:**
- **P0 Critical:** Data loss, security breach, crash, wrong results
- **P1 High:** Broken feature, missing validation, spec violation
- **P2 Medium:** Performance, missing error state, accessibility
- **P3 Low:** Code style, minor UX

**Sandboxed permissions:** Can only write test files, can only run test/lint commands. Cannot touch source code.

## Configuring Your Provider

The default `opencode.jsonc` routes all requests through a local proxy at `localhost:8320`. To use a different provider, update the `provider` section:

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

Then update agent models to match your provider's model IDs.

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

## Credits

- **Skills:** [@mattpocock/skills](https://github.com/mattpocock/skills) — MIT licensed
- **OpenCode:** [opencode.ai](https://opencode.ai) — The AI-powered coding CLI
- **Agent designs:** Custom-built for this configuration

## License

MIT — Use, modify, and share freely.
