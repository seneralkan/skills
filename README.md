# Skills

Modular skill definitions for AI coding agents. Each skill encapsulates best practices, review checklists, and output templates for a specific language, domain, or problem type.

## What is a skill?

A skill is a structured instruction file (`SKILL.md`) that teaches an AI assistant (Copilot, Claude, Gemini, OpenAI) **what to check**, **how to analyze**, and **how to format its output** for a given engineering topic.

## Available skills

| Skill | Description |
|---|---|
| [go-best-practices](go-best-practices/SKILL.md) | Production-ready standards for Go backend services — structure, error handling, observability, security, performance, testing |
| [go-concurrency](go-concurrency/SKILL.md) | Concurrency design, patterns, debugging, and optimization for Go backends — goroutines, channels, worker pools, graceful shutdown |
| [go-testing](go-testing/SKILL.md) | Testing strategy and implementation for Go services — unit/integration/contract/e2e, determinism, CI quality gates |
| [go-api-design](go-api-design/SKILL.md) | REST and gRPC API design for Go backends — contracts, pagination, versioning, compatibility, idempotency |
| [go-performance-profiling](go-performance-profiling/SKILL.md) | Evidence-driven Go optimization — pprof, benchmarking, allocation analysis, contention tuning |
| [go-clean-architecture](go-clean-architecture/SKILL.md) | Clean architecture and hexagonal design for Go backends — dependency rule, ports/adapters, incremental refactor |
| [go-microservices](go-microservices/SKILL.md) | Go microservices and event-driven patterns — Kafka/SQS/RabbitMQ producer-consumer reliability and contracts |

## Quick start

### 1. Reference in VS Code Copilot Chat
```
#file:skills/go-best-practices/SKILL.md review this service
```

### 2. Auto-load in any Go project
Copy the skill into your project's instruction directory:
```bash
mkdir -p <project>/.github/instructions
cp skills/go-best-practices/SKILL.md <project>/.github/instructions/go-best-practices.instructions.md
```
Add front-matter to scope it:
```markdown
---
applyTo: "**/*.go"
---
```

### 3. Use from terminal
```bash
cat skills/go-concurrency/SKILL.md | gh copilot suggest "is this worker pool safe?"
```

## Structure

```
skills/
├── README.md
├── AGENTS.md                    # Full spec: formats, conventions, contribution guide
├── go-best-practices/
│   ├── SKILL.md                 # Skill definition
│   └── agents/                  # Per-provider configs
│       ├── openai.yaml
│       ├── copilot.yaml
│       ├── claude.yaml
│       └── gemini.yaml
└── go-concurrency/
    ├── SKILL.md
    └── agents/
        ├── openai.yaml
        ├── copilot.yaml
        ├── claude.yaml
        └── gemini.yaml
├── go-testing/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   └── references/
│       ├── ci-quality-gates.md
│       ├── fixtures-and-fakes.md
│       └── test-matrix.md
├── go-api-design/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   └── references/
│       ├── error-and-versioning.md
│       ├── grpc-conventions.md
│       └── rest-conventions.md
└── go-performance-profiling/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── benchmarking.md
        ├── memory-optimization.md
        └── pprof-playbook.md
├── go-clean-architecture/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   └── references/
│       ├── layers-and-dependency-rule.md
│       ├── ports-and-adapters.md
│       └── refactor-playbook.md
└── go-microservices/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── event-driven-fundamentals.md
        ├── kafka-producer-consumer.md
        ├── rabbitmq-producer-consumer.md
        ├── reliability-patterns.md
        └── sqs-sns-producer-consumer.md
```

## Adding a new skill

1. Create `skills/<skill-name>/SKILL.md` with front-matter, rules, and output template
2. Add agent configs under `skills/<skill-name>/agents/`
3. Test via `#file:` reference in VS Code Chat

See [AGENTS.md](AGENTS.md) for the full specification, YAML format, and naming conventions.

## Roadmap

- [ ] `system-design` — Scalability, availability, consistency trade-offs
- [ ] `leetcode-patterns` — Sliding window, two pointers, BFS/DFS, DP patterns
- [ ] `clean-architecture` — Hexagonal, ports & adapters, dependency rule
- [ ] `api-design` — REST, gRPC, versioning, pagination, error contracts
- [ ] `docker-k8s` — Container best practices, Kubernetes manifests, Helm
- [ ] `cloud-architecture` — AWS/GCP/Azure services, cost optimization, security
- [ ] `js-ts-best-practices` — Node.js best practices
- [ ] `js-ts-react-best-practices` — React best practices
- [ ] `js-ts-backend-best-practices` — Backend best practices in JavaScript/TypeScript

## License

Private repository — personal use.
