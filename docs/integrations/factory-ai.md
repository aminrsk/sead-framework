# Factory.ai Integration Guide

This guide covers how to use SEAD Framework specifically with Factory.ai.

## Overview

Factory.ai provides a suite of AI "Droids" that map well to SEAD phases:

| Droid | SEAD Phase | Purpose |
|-------|------------|---------|
| **Product Droid** | Phase 1 | PRD generation, spec writing |
| **Knowledge Droid** | Phase 1-2 | ADRs, documentation |
| **Code Droid** | Phase 3 | Feature implementation, TDD |
| **PR Review Droid** | Phase 3 | Automated code review |
| **Reliability Droid** | Phase 4 | Incident response, monitoring |

## Setup

### 1. Connect Factory.ai to Linear

Factory.ai works best with Linear for issue tracking:
- Connect your Linear workspace to Factory.ai
- Enable the `@Factory` mention trigger
- Configure project defaults

### 2. Create AGENTS.md

Factory.ai reads `AGENTS.md` from your repository root. Use the Phase 1 template and ensure it includes:

```markdown
# Project Context
[One paragraph describing the project]

# Tech Stack
- Framework: [e.g., Next.js 14]
- Database: [e.g., PostgreSQL via Neon]
- Auth: [e.g., Clerk]
- Hosting: [e.g., Vercel]

# Coding Standards
- TypeScript strict mode
- ESLint + Prettier
- Component naming: PascalCase
- File naming: kebab-case

# Testing Requirements
- Jest for unit tests
- Playwright for E2E
- Minimum 80% coverage for new code
- Tests BEFORE implementation (TDD)

# Security Rules (DO NOT)
- Never commit secrets
- Never access production DB directly
- Never skip input validation
- Never bypass authentication checks
- Never modify auth logic without human review

# AI Boundaries
- AI suggests, human confirms for: schema changes, new integrations
- AI implements autonomously for: UI, business logic, tests
```

## Phase 1: Using Product Droid

### Generating PRD

In Linear, create an issue and mention @Factory:

```
@Factory Generate a PRD for this feature:

[Paste meeting transcript or requirements]

Use SEAD Framework PRD structure:
- Problem statement
- Success metrics
- Feature requirements with acceptance criteria
- AI feature specifications (if applicable)
- Compliance requirements
- Out of scope
```

### Generating Feature-Test Matrix

```
@Factory Based on the PRD in [link to PRD], create a Feature-Test Matrix:

For each feature include:
- Feature ID and name
- Acceptance criteria (Given/When/Then)
- Test scenarios
- Priority (P0/P1/P2)
- Risk classification
- Size estimate (S/M/L)
```

## Phase 2: Using Knowledge Droid

### Generating ADR

```
@Factory Create an ADR for [decision topic]:

Context: [situation]
Options:
A) [Option A]
B) [Option B]

Include pros/cons, risk assessment, and recommendation.
```

### Generating AGENTS.md

```
@Factory Create an AGENTS.md file based on:
- PRD: [link]
- ADR: [link]
- Tech stack: [list]

Include project context, standards, security rules, and AI boundaries.
```

## Phase 3: Code Droid Workflow

### The Factory.ai Development Flow

1. **Create Linear issue** with clear acceptance criteria
2. **Assign to @Factory** — Code Droid picks up the task
3. **Code Droid writes tests first** (respects TDD in AGENTS.md)
4. **Code Droid implements** and opens PR
5. **PR Review Droid triggers automatically**
6. **Human reviews** (Critical/High risk only)
7. **Merge and deploy**

### Triggering Code Droid

In Linear, assign the issue to @Factory:

```
Title: [F001] User authentication flow

Description:
Implement user authentication using Clerk.

Acceptance Criteria:
- Users can sign up with email
- Users can sign in with email/password
- Users can sign out
- Protected routes redirect to sign-in

Reference: Feature-Test Matrix F001

Labels: Critical, Phase-3, M
```

Code Droid will:
1. Read AGENTS.md for context
2. Write tests based on acceptance criteria
3. Implement to pass tests
4. Open PR linked to Linear issue

### Session Boundaries

Factory.ai handles context automatically through:
- AGENTS.md (always loaded)
- Dynamic code retrieval (pulls relevant files)
- Persistent memory (user + org level)

You don't need manual context compression like with direct AI chat.

## PR Review Droid

### Automatic Triggering

PR Review Droid runs automatically when Code Droid opens a PR. It:
- Reviews code quality
- Checks for logic errors
- Identifies edge cases
- Suggests improvements

### For Critical Features

Even with automatic PR Review, Critical features need additional review:

1. Open new Claude.ai conversation (fresh context)
2. Paste the code from the PR
3. Use the security review prompt:

```
Review this authentication code for security issues:

[Paste code]

Check for:
1. OWASP Top 10 vulnerabilities
2. Authentication bypasses
3. Authorization failures
4. Session management issues
5. Input validation gaps
```

## Phase 4: Reliability Droid

### Incident Response

Reliability Droid monitors Sentry alerts and can:
- Auto-create Linear issues for bugs
- Perform root cause analysis
- Push fixes through Code Droid pipeline

### Setup

1. Connect Sentry to Factory.ai
2. Configure alert thresholds
3. Enable auto-issue creation

### Triggering Manually

For incident investigation:

```
@Factory Investigate this Sentry issue: [link]

Perform root cause analysis and suggest fix.
```

## Quality Gates with Factory.ai

### Pre-commit (Local)

Use standard Git hooks—Factory.ai doesn't affect this layer.

### PR Checks

Factory.ai adds:
- PR Review Droid comments
- Automatic test runs
- Coverage reports

Your CI/CD adds:
- Linting
- Type checking
- Security scans

### Staging

After merge to staging:
- Factory.ai can run integration tests via Code Droid
- You configure E2E tests in CI/CD

### Production

Reliability Droid provides:
- Sentry integration
- Automated incident detection
- Quick fix capability

## The Complete Flow

```
LINEAR ISSUE CREATED
        ↓
ASSIGNED TO @FACTORY
        ↓
CODE DROID PICKS UP
        ↓
    ┌───┴───┐
    │  TDD  │
    │ CYCLE │
    └───┬───┘
        ↓
PR OPENED
        ↓
PR REVIEW DROID (auto)
        ↓
    ┌───────────────────┐
    │ Risk Level?       │
    │ Critical/High → Human Review
    │ Medium/Low → Auto-merge OK
    └───────────────────┘
        ↓
MERGED
        ↓
DEPLOYED (via Vercel/etc)
        ↓
RELIABILITY DROID MONITORS
```

## Best Practices

### DO

- Keep AGENTS.md under 150 lines
- Use clear acceptance criteria in issues
- Let Code Droid handle full features (not micro-tasks)
- Trust PR Review Droid for Low/Medium risk
- Add human review for Critical/High risk

### DON'T

- Skip AGENTS.md setup
- Assign vague issues to @Factory
- Override PR Review Droid comments without reason
- Let Critical features auto-merge
- Ignore Reliability Droid alerts

## Troubleshooting

### Code Droid Not Picking Up Issue

- Check @Factory is mentioned/assigned
- Verify Linear-Factory.ai connection
- Ensure AGENTS.md exists in repo root

### Poor Code Quality

- Review AGENTS.md coding standards
- Add more specific acceptance criteria
- Check if feature is sized correctly (L/Epic needs decomposition)

### 4-Attempt Rule Triggered

If Code Droid fails 4 times:
1. Reassign to human
2. Review architecture
3. Break down the feature
4. Update ADR if approach changes

## Resources

- [Factory.ai Documentation](https://factory.ai/docs)
- [Linear Integration Guide](https://factory.ai/docs/linear)
- [AGENTS.md Reference](https://factory.ai/docs/agents-md)
