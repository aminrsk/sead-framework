# Getting Started with SEAD Framework

This guide walks you through implementing SEAD on your first project.

## Prerequisites

Before starting, ensure you have:

- An AI coding assistant (Claude, GPT-4, Cursor, etc.)
- Version control (Git + GitHub/GitLab)
- A project management tool (Linear, Jira, etc.)
- Basic CI/CD capability

## Step 1: Project Setup

### Create Your Project Structure

```bash
mkdir my-project
cd my-project
git init

# Create SEAD directories
mkdir -p docs templates
```

### Copy Phase 1 Templates

```bash
# From this repository
cp templates/phase-1-specify/* docs/
```

## Step 2: Phase 1 - SPECIFY

### 2.1 Gather Requirements

Collect all inputs:
- Meeting recordings/transcripts
- Client documents
- Existing system documentation
- Compliance requirements

### 2.2 Generate PRD

Use your AI thinking partner to generate the PRD:

```
Based on the following requirements, generate a complete PRD 
using the SEAD Framework template.

Include:
1. Problem statement with user pain points
2. Success metrics (quantifiable)
3. Feature requirements with acceptance criteria
4. AI feature specifications (if applicable)
5. Compliance requirements
6. Out of scope items

Requirements:
[Paste your gathered requirements]
```

### 2.3 Create Feature-Test Matrix

```
Based on this PRD, create a Feature-Test Matrix with:
1. Each feature from the PRD
2. Acceptance criteria (Given/When/Then format)
3. Test cases for each criterion
4. Priority (P0/P1/P2)
5. Risk classification (Critical/High/Medium/Low)
6. Size estimate (S/M/L/Epic)

PRD:
[Paste your PRD]
```

### 2.4 Document Architecture Decisions

Create an ADR for each major technical decision:
- Tech stack choices
- Database design
- Authentication approach
- External integrations
- AI feature boundaries

### 2.5 Create AGENTS.md

This file constrains AI behavior during development:

```
Create an AGENTS.md file based on:
- The PRD
- The ADR
- The Feature-Test Matrix

Keep under 150 lines. Include:
- Project context
- Tech stack
- Coding standards
- Security rules (what AI must NOT do)
- Testing requirements
```

### 2.6 Verify Exit Criteria

Use the Phase 1 Checklist:
- [ ] PRD reviewed and approved
- [ ] Feature-Test Matrix complete
- [ ] ADRs documented
- [ ] AGENTS.md ready
- [ ] Compliance requirements identified

## Step 3: Phase 2 - ARCHITECT

### 3.1 Size All Features

| Size | Sessions | Action |
|------|----------|--------|
| S | 1 | Direct implementation |
| M | 2-3 | Plan then implement |
| L | 4-6 | **Break down further** |
| Epic | 7+ | **Decompose into S/M** |

**Rule:** No L or Epic features proceed without decomposition.

### 3.2 Classify Risk

| Category | Examples | Required Review |
|----------|----------|-----------------|
| Critical | Auth, payments, data deletion | Full human review |
| High | AI features, integrations | AI review + human spot-check |
| Medium | Core business logic | AI review + automated tests |
| Low | UI tweaks | Automated tests only |

### 3.3 Map Human Checkpoints

Identify where human decisions are required:
- Database schema changes
- API design decisions
- Security implementations
- Third-party integrations

### 3.4 Configure Quality Gates

Set up 4 levels of automated checks:
1. **Pre-commit:** Lint, format, type-check
2. **PR:** All tests, coverage threshold
3. **Staging:** Integration tests, E2E
4. **Production:** Smoke tests, monitoring

### 3.5 Create Issues

Create issues in your project management tool for all features with:
- Size label (S/M)
- Risk classification
- Phase assignment
- Acceptance criteria reference

## Step 4: Phase 3 - DEVELOP

### 4.1 The Development Loop

```
MORNING (10 min)
├── Pull latest, run tests
└── Review what's next

SESSION (30-60 min)
├── Define ONE clear goal
├── TDD: Write tests → Implement → Pass
└── Commit

BREAK (5-10 min)

REPEAT

END OF DAY (10 min)
├── Run all tests
├── Push changes
└── Update progress
```

### 4.2 TDD Workflow

For each feature:
1. Write failing tests based on Feature-Test Matrix
2. Verify tests fail
3. Implement minimal code to pass
4. Verify tests pass
5. Refactor if needed
6. Commit

### 4.3 Multi-Layer Review

| Layer | Who | What |
|-------|-----|------|
| 1 | AI Coder | Initial implementation |
| 2 | AI Reviewer | Fresh context review |
| 3 | Automation | Linting, tests, scans |
| 4 | Human | Architecture + Critical only |

### 4.4 The 4-Attempt Rule

If a problem isn't solved in 4 AI iterations:
1. STOP coding
2. Reassess the architecture
3. Break down the problem differently
4. Simplify scope

## Step 5: Phase 4 - DELIVER

### 5.1 Staged Rollout

**Never go 0→100.**

| Stage | Audience | Duration |
|-------|----------|----------|
| Internal | Team only | 1-2 days |
| Pilot | 5-10% users | 1-2 weeks |
| Expanded | 25% users | 1-2 weeks |
| GA | 100% users | Ongoing |

### 5.2 Rollback Triggers

Immediately rollback if:
- Error rate > 5%
- Critical security issue
- Data integrity concern
- Performance degradation > 20%

### 5.3 Documentation

Deliver complete package:
- User guides
- API documentation
- Operational runbooks
- Training materials

### 5.4 Handoff

- Knowledge transfer sessions
- Support period defined
- Escalation paths documented
- Client sign-off

## Step 6: Maintenance

After GA:
- Change requests follow SEAD from Phase 1
- Bug fixes use Phase 3 (or Emergency Bypass if critical)
- Monthly/quarterly reviews
- Continuous monitoring

## Time Estimates

| Phase | Simple | Standard | Enterprise |
|-------|--------|----------|------------|
| SPECIFY | 2-3 hrs | 4-6 hrs | 1-2 days |
| ARCHITECT | 1-2 hrs | 2-4 hrs | 4-8 hrs |
| DEVELOP | Ongoing | Ongoing | Ongoing |
| DELIVER | 1-2 wks | 2-3 wks | 3-6 wks |

## Common Mistakes

🚩 Jumping to code without PRD/Feature-Test Matrix
🚩 Not breaking down L/Epic features
🚩 Skipping AI review for "simple" changes
🚩 Deploying without staged rollout
🚩 Making architecture decisions without ADR

## Next Steps

- Review [docs/framework.md](framework.md) for complete reference
- Read [docs/principles.md](principles.md) for principle details
- Check [docs/tool-orchestration.md](tool-orchestration.md) for tool setup
