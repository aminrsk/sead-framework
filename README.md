# SEAD Framework

**Solo Enterprise AI Development** — The engineered bridge from 70% AI generation to 100% enterprise-grade production.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)](https://github.com/aminrsk/sead-framework/releases)

## The Problem

AI coding assistants get you to ~70% of a solution quickly. But enterprise clients demand 100% reliability. The gap isn't about better prompts—it's about structured processes that constrain AI behavior and validate outputs systematically.

**The reliability compounding problem:** If each AI step is 95% reliable, after just 10 steps you're at only 60% system reliability. After 20 steps? 36%.

## The Solution

SEAD Framework uses two levers:

1. **Requirements & ideation to constrain AI** — Better specs = fewer AI errors
2. **Structured validation to catch what you can't manually review** — Tests + automated checks + AI-reviews-AI

## The Four Phases

| Phase | Purpose | Key Deliverables |
|-------|---------|------------------|
| **1. SPECIFY** | Front-load intelligence into specifications | PRD, Feature-Test Matrix, ADR, AGENTS.md |
| **2. ARCHITECT** | Design development structure before coding | Agent Harness, Checkpoint Map, Quality Gates |
| **3. DEVELOP** | Execute with TDD and session discipline | Tests, Code, Multi-layer Reviews |
| **4. DELIVER** | Stage the rollout, never go 0→100 | Staged Rollout, Documentation, Handoff |

## Five Governing Principles

1. **Specification as Constraint** — Better specs = fewer AI errors
2. **Test as Verification** — Tests prove understanding when you can't read every line
3. **AI Reviews AI** — Never trust single-pass generation
4. **Human at Decisions, AI at Execution** — You own architecture; AI owns implementation
5. **The 4-Attempt Rule** — If AI fails 4 times, the architecture is wrong—not the prompt

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/aminrsk/sead-framework.git
cd sead-framework
```

### 2. Start with Phase 1

Copy templates from `templates/phase-1-specify/` to your project:

```bash
cp -r templates/phase-1-specify/* your-project/docs/
```

### 3. Follow the workflow

Each phase has a workflow guide and checklist. Complete all exit criteria before moving to the next phase.

## Repository Structure

```
sead-framework/
├── docs/
│   ├── framework.md          # Complete framework reference
│   ├── principles.md         # Five governing principles in detail
│   ├── getting-started.md    # Step-by-step guide
│   ├── tool-orchestration.md # Tool-agnostic implementation
│   └── integrations/
│       └── factory-ai.md     # Factory.ai specific guide
├── templates/
│   ├── phase-1-specify/      # 6 templates
│   ├── phase-2-architect/    # 6 templates
│   ├── phase-3-develop/      # 6 templates
│   └── phase-4-deliver/      # 6 templates
├── examples/
│   └── sample-project/       # Example project structure
└── README.md
```

## Templates Overview

### Phase 1: SPECIFY (24 templates total)

| Template | Purpose |
|----------|---------|
| PRD Template | Complete product requirements |
| Feature-Test Matrix | Maps features → acceptance criteria → test cases |
| ADR Template | Architecture Decision Records |
| AGENTS.md Template | AI agent configuration and constraints |
| Workflow Guide | Step-by-step process |
| Checklist | Exit criteria verification |

### Phase 2: ARCHITECT

| Template | Purpose |
|----------|---------|
| Agent Harness Design | AI session structure and boundaries |
| Human Checkpoint Map | Decision points requiring human approval |
| Context Management Plan | Prevent context rot across sessions |
| Quality Gate Definitions | 4-level automated checks |
| Workflow Guide | Step-by-step process |
| Checklist | Exit criteria verification |

### Phase 3: DEVELOP

| Template | Purpose |
|----------|---------|
| TDD Workflow Guide | Test-first development process |
| Session Discipline Protocol | Focused sessions with clear goals |
| Multi-Layer Review Process | AI → AI → Automated → Human |
| Prompt Library | Pre-tested prompts for common tasks |
| Workflow Guide | Step-by-step process |
| Checklist | Exit criteria verification |

### Phase 4: DELIVER

| Template | Purpose |
|----------|---------|
| Staged Rollout Plan | Progressive user exposure |
| Client Communication Templates | Updates, notifications, announcements |
| Delivery Documentation Checklist | Enterprise deliverables |
| Handoff and Support Transition | Knowledge transfer procedures |
| Workflow Guide | Step-by-step process |
| Checklist | Exit criteria verification |

## Who Is This For?

- **Solo developers** building enterprise applications with AI assistance
- **Small teams** wanting structured AI development processes
- **Consultants** delivering client projects with AI coding tools
- **Anyone** bridging the gap between AI-generated code and production requirements

## Tool Agnostic

While examples reference specific tools, SEAD works with any AI coding assistant:

- Claude, GPT-4, Gemini for thinking/planning
- Cursor, GitHub Copilot, Factory.ai, Aider for code generation
- Any CI/CD pipeline for quality gates
- Any project management tool for tracking

See [docs/tool-orchestration.md](docs/tool-orchestration.md) for tool-agnostic implementation.

## Compliance Ready

Built-in support for enterprise compliance:

| Standard | Framework Support |
|----------|-------------------|
| SOC2 | ADR templates, Quality gates |
| GDPR | PRD sections, Feature tests |
| ISO27001 | Quality gates, Monitoring |
| HIPAA | Risk classification, Critical reviews |
| WCAG 2.1 | Feature-Test Matrix criteria |

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License - see [LICENSE](LICENSE) for details.

## Author

Created by [Amin R](https://github.com/aminrsk)

---

**Remember:** AI gets you to 70%. This framework gets you to 100%.
