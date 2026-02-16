# Skills Repository

Modular skill definitions for AI agents. Each skill provides specialized knowledge and rules for a specific language, domain, or problem type.

## Purpose

This repo hosts **structured instruction files** that AI coding assistants (Copilot, Claude, Gemini, OpenAI) consume as context. Skills teach the agent what to know, how to analyze, and how to format its output.

## Scope

| Area | Examples |
|---|---|
| Software Development | Best practices, code review, refactoring, testing, CI/CD |
| Software Architecture | Design patterns, clean architecture, DDD, microservices |
| Algorithms & DSA | LeetCode patterns, complexity analysis, data structures |
| Concurrency & Systems | Parallelism, synchronization, distributed systems |
| Language-Specific | Go, Java, Python, TypeScript, Rust, etc. |

## Directory structure

```
skills/
├── AGENTS.md                          # This file
├── <skill-name>/
│   ├── SKILL.md                       # Skill definition, rules, checklist
│   └── agents/
│       ├── openai.yaml                # OpenAI agent config
│       ├── copilot.yaml               # GitHub Copilot config
│       ├── claude.yaml                # Claude config
│       └── gemini.yaml                # Gemini config
```

## SKILL.md format

Every skill file follows this structure:

```markdown
---
name: skill-name
description: Single paragraph explaining when the skill should be triggered.
---

# Skill Title

## Quick start
Step-by-step bootstrapping process.

## Rules / Checklist
Numbered sections with checkpoints.

## Output template
Expected output format for the agent.
```

### Front-matter fields

| Field | Required | Description |
|---|---|---|
| `name` | ✅ | Kebab-case skill name, must match folder name |
| `description` | ✅ | Description the agent uses to decide whether to apply this skill |

## Agent YAML format

```yaml
display_name: Human-readable name
short_description: One-line summary
default_prompt: >
  Default instruction given to the agent when the skill is triggered.
```

## Adding a new skill

1. Create folder: `skills/<skill-name>/`
2. Write `SKILL.md`: front-matter + quick start + rules + output template
3. Add YAML configs under `agents/` (openai, copilot, claude, gemini)
4. Test it: reference via `#file:skills/<skill-name>/SKILL.md` in VS Code Chat

## Using skills

### VS Code Copilot Chat
```
#file:skills/go-best-practices/SKILL.md review this service
```

### Project-level auto-loading
```
<project>/.github/instructions/go-best-practices.instructions.md
```
Filter with front-matter:
```markdown
---
applyTo: "**/*.go"
---
```

### Terminal (gh copilot)
```bash
cat skills/go-concurrency/SKILL.md | gh copilot suggest "is this worker pool correct?"
```

## Naming conventions

| Element | Rule | Example |
|---|---|---|
| Skill folder | `<lang>-<domain>` kebab-case | `go-concurrency`, `python-testing` |
| General skill | `<domain>` kebab-case | `system-design`, `leetcode-patterns` |
| SKILL.md | Always uppercase | `SKILL.md` |
| Agent YAML | Provider name lowercase | `openai.yaml`, `claude.yaml` |

## Planned skills 
- [ ] `system-design` — Scalability, availability, consistency trade-offs
- [ ] `leetcode-patterns` — Sliding window, two pointers, BFS/DFS, DP patterns
- [ ] `clean-architecture` — Hexagonal, ports & adapters, dependency rule
- [ ] `api-design` — REST, gRPC, versioning, pagination, error contracts
- [ ] `docker-k8s` — Container best practices, Kubernetes manifests, Helm
- [ ] `cloud-architecture` — AWS/GCP/Azure services, cost optimization, security
- [ ] `js-ts-best-practices` — Node.js best practices
- [ ] `js-ts-react-best-practices` — React best practices
- [ ] `js-ts-backend-best-practices` — Backend best practices in JavaScript/TypeScript
