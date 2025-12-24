# Tool Orchestration Guide

SEAD Framework is tool-agnostic. This guide shows how to implement it with any toolset.

## Core Tool Categories

| Category | Purpose | Examples |
|----------|---------|----------|
| **AI Thinking Partner** | Document generation, analysis, planning | Claude, GPT-4, Gemini |
| **AI Code Generator** | Code implementation, TDD | Cursor, GitHub Copilot, Aider, Factory.ai |
| **Version Control** | Code management, PR workflow | GitHub, GitLab, Bitbucket |
| **CI/CD** | Automated quality gates | GitHub Actions, GitLab CI, CircleCI |
| **Project Management** | Issue tracking, progress | Linear, Jira, Asana, GitHub Issues |
| **Error Monitoring** | Production observability | Sentry, Datadog, New Relic |

## Tool Assignment by Phase

### Phase 1: SPECIFY

**Primary Tool:** AI Thinking Partner (Claude, GPT-4, etc.)

Use for:
- Generating PRD from transcripts/requirements
- Creating Feature-Test Matrix
- Drafting ADRs
- Writing AGENTS.md

**Why not code generators here?**
Phase 1 is about thinking and documenting, not coding. Thinking-optimized models excel at synthesis and analysis.

### Phase 2: ARCHITECT

**Primary Tools:** AI Thinking Partner + Project Management

Use AI for:
- Feature sizing analysis
- Risk classification
- Checkpoint mapping
- Quality gate planning

Use Project Management for:
- Creating issues for all features
- Labeling (size, risk, phase)
- Setting up workflows

### Phase 3: DEVELOP

**Primary Tools:** AI Code Generator + CI/CD

Use Code Generator for:
- TDD: tests first, then implementation
- Feature implementation
- Bug fixes
- Refactoring

Use CI/CD for:
- Pre-commit hooks
- PR checks
- Staging deployment
- Production gates

**Critical:** Use AI Thinking Partner (fresh context) for code reviews on High/Critical features.

### Phase 4: DELIVER

**Primary Tools:** All

| Task | Tool |
|------|------|
| Staged rollout | Hosting platform (Vercel, etc.) |
| Client communication | AI Thinking Partner for drafts |
| Documentation | AI Thinking Partner |
| Monitoring | Error monitoring tool |

## The Tool Flow

```
┌─────────────────────────────────────────────────────────────┐
│ PHASE 1: SPECIFY                                            │
│ ┌─────────────────────────┐                                 │
│ │ AI THINKING PARTNER     │                                 │
│ │ - Generate PRD          │                                 │
│ │ - Create Feature-Test   │                                 │
│ │ - Draft ADR             │                                 │
│ │ - Write AGENTS.md       │                                 │
│ └───────────┬─────────────┘                                 │
│             ↓                                               │
│       Documents ready                                       │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│ PHASE 2: ARCHITECT                                          │
│ ┌─────────────────────────┐   ┌─────────────────────────┐   │
│ │ AI THINKING PARTNER     │   │ PROJECT MANAGEMENT      │   │
│ │ - Size features         │──▶│ - Create issues         │   │
│ │ - Classify risk         │   │ - Apply labels          │   │
│ │ - Map checkpoints       │   │ - Set up board          │   │
│ └─────────────────────────┘   └─────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│ PHASE 3: DEVELOP                                            │
│                                                             │
│ ┌─────────────────────────┐                                 │
│ │ AI CODE GENERATOR       │                                 │
│ │ - Write tests (TDD)     │                                 │
│ │ - Implement features    │                                 │
│ │ - Create PRs            │                                 │
│ └───────────┬─────────────┘                                 │
│             ↓                                               │
│ ┌─────────────────────────┐   ┌─────────────────────────┐   │
│ │ CI/CD PIPELINE          │   │ AI THINKING PARTNER     │   │
│ │ - Run tests             │   │ (Fresh Context)         │   │
│ │ - Check coverage        │   │ - Review Critical code  │   │
│ │ - Security scans        │   │ - Catch edge cases      │   │
│ └───────────┬─────────────┘   └───────────┬─────────────┘   │
│             └───────────┬───────────────────┘               │
│                         ↓                                   │
│                   Human Review                              │
│              (Critical/High only)                           │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│ PHASE 4: DELIVER                                            │
│                                                             │
│ Hosting ─────▶ Staged Rollout                               │
│ Monitoring ──▶ Error Tracking                               │
│ AI Partner ──▶ Documentation                                │
│ All Tools ───▶ Handoff                                      │
└─────────────────────────────────────────────────────────────┘
```

## Quality Gates Configuration

### Level 1: Pre-commit

**Tool:** Git hooks (Husky, pre-commit, etc.)

```yaml
# Example: .pre-commit-config.yaml
repos:
  - repo: local
    hooks:
      - id: lint
        name: Lint
        entry: npm run lint
        language: system
      - id: typecheck
        name: Type Check
        entry: npm run typecheck
        language: system
      - id: format
        name: Format Check
        entry: npm run format:check
        language: system
```

### Level 2: Pull Request

**Tool:** CI/CD (GitHub Actions, etc.)

```yaml
# Example: .github/workflows/pr.yml
name: PR Checks
on: [pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci
      - run: npm test
      - run: npm run test:coverage
      # Fail if coverage below threshold
      - run: |
          COVERAGE=$(npm run test:coverage -- --json | jq .total.lines.pct)
          if (( $(echo "$COVERAGE < 80" | bc -l) )); then
            exit 1
          fi
```

### Level 3: Staging

**Tool:** CI/CD + Hosting Platform

```yaml
# Deploy to staging, run integration tests
staging:
  runs-on: ubuntu-latest
  steps:
    - run: npm run deploy:staging
    - run: npm run test:e2e
    - run: npm run test:integration
```

### Level 4: Production

**Tool:** Hosting Platform + Monitoring

- Smoke tests post-deploy
- Monitoring alerts configured
- Rollback capability ready

## Session Discipline Protocol

### Starting a Session

```
1. Pick ONE issue from backlog
2. Load relevant context:
   - AGENTS.md
   - Related files only
   - Acceptance criteria
3. Set timer (25-60 min)
4. Start with test writing
```

### Ending a Session

```
1. Tests passing?
2. Commit with clear message
3. Update issue status
4. If blocked → Document what's needed
```

### Between Sessions

```
- Clear AI context (new session)
- Don't carry forward assumptions
- Fresh context = fresh perspective
```

## Multi-Layer Review Setup

### Layer 1: Generation

Your AI Code Generator creates the implementation.

### Layer 2: AI Review

**For Low/Medium risk:** Automated AI review if your tool supports it.

**For High/Critical risk:** Manual review in fresh AI session:

1. Open new conversation with AI Thinking Partner
2. Paste code for review
3. Use review prompts from Prompt Library
4. Log issues found
5. Fix in Code Generator

### Layer 3: Automated Scans

CI/CD runs:
- Linting
- Type checking
- Security scanning
- Test coverage

### Layer 4: Human Decision

For Critical/High risk only:
- Review the PR yourself
- Focus on architecture alignment
- Check business logic correctness
- Approve and merge

## Recommended Tool Stacks

### Minimal Setup

| Category | Tool |
|----------|------|
| AI Partner | Claude.ai (free tier) |
| Code Gen | Cursor (free tier) |
| Version Control | GitHub |
| CI/CD | GitHub Actions |
| PM | GitHub Issues |

### Professional Setup

| Category | Tool |
|----------|------|
| AI Partner | Claude Pro |
| Code Gen | Cursor Pro / GitHub Copilot |
| Version Control | GitHub |
| CI/CD | GitHub Actions |
| PM | Linear |
| Monitoring | Sentry |

### Enterprise Setup

| Category | Tool |
|----------|------|
| AI Partner | Claude Max / GPT-4 Team |
| Code Gen | Factory.ai / Cursor Business |
| Version Control | GitHub Enterprise |
| CI/CD | GitHub Actions + Custom |
| PM | Linear / Jira |
| Monitoring | Sentry + Datadog |
| Hosting | Vercel / AWS |

## Tool-Specific Guides

For detailed configuration of specific tools, see:

- [Factory.ai Integration](integrations/factory-ai.md)
- More integrations coming soon

## Key Rules

1. **Thinking Partner for Phase 1-2** — Don't use code generators for planning
2. **Code Generator for Phase 3** — Don't use thinking partners for implementation
3. **Fresh Context for Reviews** — Never review in the same session that generated code
4. **CI/CD for Quality Gates** — Automate everything automatable
5. **Human for Decisions** — Tools execute, you decide
