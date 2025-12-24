# Example: Sample Project Structure

This example shows how a project using SEAD Framework should be organized.

## Project Structure

```
sample-project/
├── AGENTS.md                    # AI coding assistant configuration
├── README.md                    # Project readme
├── docs/
│   ├── PRD.md                   # Product Requirements Document
│   ├── FEATURE-TEST-MATRIX.md   # Feature to test mapping
│   ├── PROGRESS.md              # Development progress tracking
│   ├── adr/
│   │   ├── ADR-001-frontend.md  # Architecture decisions
│   │   ├── ADR-002-database.md
│   │   └── ADR-003-auth.md
│   ├── AGENT-HARNESS-DESIGN.md  # AI session configuration
│   ├── HUMAN-CHECKPOINT-MAP.md  # Review requirements
│   ├── CONTEXT-MANAGEMENT.md    # Context strategies
│   └── QUALITY-GATES.md         # CI/CD configuration
├── src/                         # Source code
├── tests/                       # Test files
├── .github/
│   └── workflows/               # CI/CD pipelines
└── package.json
```

## Phase 1 Outputs

After completing Phase 1: SPECIFY, you should have:

- `AGENTS.md` - In project root
- `docs/PRD.md` - Complete product requirements
- `docs/FEATURE-TEST-MATRIX.md` - All features with test cases
- `docs/adr/*.md` - Architecture decision records

## Phase 2 Outputs

After completing Phase 2: ARCHITECT, add:

- `docs/AGENT-HARNESS-DESIGN.md`
- `docs/HUMAN-CHECKPOINT-MAP.md`
- `docs/CONTEXT-MANAGEMENT.md`
- `docs/QUALITY-GATES.md`
- `docs/PROGRESS.md` (initialized)

## Phase 3 Ongoing

During Phase 3: DEVELOP:

- Update `docs/PROGRESS.md` daily
- Issues in project management tool
- Code in `src/` following TDD
- Tests in `tests/`

## Phase 4 Additions

During Phase 4: DELIVER, add:

- User documentation
- Runbook
- Deployment guide
- Handoff materials

## Using This Example

1. Copy this structure to your new project
2. Replace placeholder content in each file
3. Follow the SEAD workflow guides for each phase

---

*Example Version: 1.0 | SEAD Framework*
