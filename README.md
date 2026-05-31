# Skills

Curated [Agent Skills](https://agentskills.io) for AI coding agents. Each skill is a folder with a `SKILL.md` file — the same format works across Claude Code, Cursor, Codex, Gemini CLI, and Windsurf.

```
.agents/skills/
  git-commit/
    SKILL.md
  grill-me/
    SKILL.md
  ...
```

## Install

Clone this repo into your project (or add it as a submodule). Agents discover skills at `.agents/skills/<skill-name>/SKILL.md` automatically — no per-skill setup.

To use skills globally, copy a skill folder into your agent's global skills directory (see table below).

### Where each agent looks


| Agent        | Global                        | Project             |
| ------------ | ----------------------------- | ------------------- |
| Claude Code  | `~/.claude/skills/`           | `.claude/skills/`   |
| Cursor       | `~/.cursor/skills/`           | `.cursor/skills/`   |
| OpenAI Codex | `~/.agents/skills/`           | `.agents/skills/`   |
| Gemini CLI   | `~/.gemini/skills/`           | `.gemini/skills/`   |
| Windsurf     | `~/.codeium/windsurf/skills/` | `.windsurf/skills/` |


Codex, Gemini, and Windsurf also discover `.agents/skills/` as a cross-agent alias.

---

## Skills

### Git & commits

| Skill | What it does | Triggers |
| --- | --- | --- |
| git-commit | Groups a messy working tree into logical, dependency-ordered commits with tag-grouped messages and approval at each step. | "commit", "save my changes" |
| git-guardrails-claude-code | Sets up Claude Code hooks that block dangerous git commands (`push`, `reset --hard`, `clean`, `branch -D`) before they run. | "block dangerous git", "add git safety hooks" |

### Planning, specs & issues

| Skill | What it does | Triggers |
| --- | --- | --- |
| grill-me | Stress-tests a plan through relentless Q&A, resolving each branch of the decision tree. | "grill me", stress-test a plan |
| grill-with-docs | Grills a plan against the project's domain model, sharpening terms and updating CONTEXT.md / ADRs inline. | stress-test against docs |
| to-prd | Turns the current conversation into a PRD and publishes it to the issue tracker. | "create a PRD" |
| to-issues | Breaks a plan or PRD into independently-grabbable issues using tracer-bullet vertical slices. | "break this into issues" |
| request-refactor-plan | Builds a refactor plan of tiny commits via interview, then files it as a GitHub issue. | "plan a refactor", "refactoring RFC" |
| triage | Triages issues through a role-driven state machine, prepping them for an AFK agent. | "triage issues", "create an issue" |
| qa | Conversational QA session — you report bugs, it explores the code and files GitHub issues. | "QA session", "report bugs" |

### Code quality & dev workflow

| Skill | What it does | Triggers |
| --- | --- | --- |
| tdd | Test-driven development with a strict red-green-refactor loop. | "TDD", "red-green-refactor", "test-first" |
| diagnose | Disciplined debugging loop: reproduce → minimise → hypothesise → instrument → fix → regression-test. | "diagnose this", "it's broken/failing" |
| review | Reviews changes since a ref along two axes — Standards and Spec — in parallel sub-agents. | "review this branch/PR" |
| improve-codebase-architecture | Finds deepening opportunities to make a codebase more testable and AI-navigable. | "improve architecture", "find refactors" |
| setup-pre-commit | Sets up Husky pre-commit hooks with lint-staged, type checking, and tests. | "add pre-commit hooks", "set up Husky" |
| prototype | Builds a throwaway prototype — runnable terminal app or toggleable UI variations — to flesh out a design. | "prototype this", "let me play with it" |
| design-an-interface | Generates radically different interface designs for a module via parallel sub-agents. | "design an API", "design it twice" |
| frontend-design | Produces distinctive, production-grade frontend UI that avoids generic AI aesthetics. | "build a component/page/app" |

### Docs & context

| Skill | What it does | Triggers |
| --- | --- | --- |
| claude-md | Creates, updates, or audits `CLAUDE.md` — the onboarding doc Claude Code loads every session. | create/update CLAUDE.md |
| convert-to-md | Decomposes any file into a dense, Claude-optimized Markdown document. | `convert-to-md <file>`, "break this down" |
| ubiquitous-language | Extracts a DDD glossary from the conversation into `UBIQUITOUS_LANGUAGE.md`. | "build a glossary", "domain model", "DDD" |
| handoff | Compacts the current conversation into a handoff document for the next agent. | "hand off", "compact this session" |
| zoom-out | Steps back to give higher-level context on how code fits the bigger picture. | "zoom out" |
| teach | Teaches a new skill or concept within the current workspace. | "teach me about…" |

### Writing

| Skill | What it does | Triggers |
| --- | --- | --- |
| writing-fragments | Mines you for fragments — claims, vignettes, half-thoughts — as raw material for a future article. | "fragments", "ideate", "raw material" |
| writing-shape | Shapes a pile of raw notes into a publishable article, paragraph by paragraph. | "shape this", "turn notes into an article" |

### Claude Code authoring (plugins, skills, hooks, MCP)

| Skill | What it does | Triggers |
| --- | --- | --- |
| write-a-skill | Creates new agent skills with proper structure, progressive disclosure, and bundled resources. | "create a skill" |
| skill-development | Reference guidance on skill structure and best practices. | "improve skill description", "skill structure" |
| plugin-structure | Scaffolds and organizes Claude Code plugins (`plugin.json`, components, auto-discovery). | "create a plugin", "plugin structure" |
| plugin-settings | Documents the `.claude/plugin-name.local.md` pattern for per-project plugin config. | "plugin settings", "store plugin config" |
| hook-development | Guidance for creating Claude Code hooks (PreToolUse, Stop, SessionStart, …). | "create a hook", "validate tool use" |
| writing-hookify-rules | Helps write hookify rules and understand their syntax. | "create a hookify rule" |
| mcp-integration | Integrates MCP servers (SSE, stdio, HTTP, WebSocket) into a plugin via `.mcp.json`. | "add MCP server", "set up MCP" |

### Integrations & meta

| Skill | What it does | Triggers |
| --- | --- | --- |
| obsidian-vault | Searches, creates, and manages Obsidian notes with wikilinks and index notes. | "find/create/organize notes" |
| caveman-stats | Shows real token usage and estimated savings for the session, read from the session log. | `/caveman-stats` |


---

## Adding a skill

1. Create `.agents/skills/<skill-name>/SKILL.md` with YAML frontmatter:
  ```yaml
   ---
   name: my-skill
   description: What it does and when to use it. Include trigger phrases.
   ---
  ```
2. Add a row to the table above

See [Claude Code skills docs](https://code.claude.com/docs/en/skills) for authoring guidance.