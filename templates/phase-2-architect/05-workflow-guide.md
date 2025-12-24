# Phase 2: ARCHITECT - Workflow Guide

This guide walks you through completing Phase 2 step-by-step.

---

## Overview

**Goal:** Design the development structure before any code is written.

**Duration:** 1-8 hours depending on complexity

**Inputs:** Phase 1 outputs (PRD, Feature-Test Matrix, ADRs, AGENTS.md)

**Outputs:**
1. Agent Harness Design
2. Human Checkpoint Map
3. Context Management Plan
4. Quality Gate Definitions
5. Issues for all features

---

## Step 1: Feature Sizing (30-60 min)

### 1.1 Review Feature-Test Matrix

Open your Feature-Test Matrix and for each feature:

1. Count the test scenarios
2. Identify dependencies
3. Estimate complexity

### 1.2 Apply Sizing Guidelines

| Size | Indicators | Sessions |
|------|------------|----------|
| **S** | Single file, < 5 scenarios, no deps | 1 |
| **M** | 2-3 files, 5-10 scenarios, clear scope | 2-3 |
| **L** | Cross-cutting, 10+ scenarios, integrations | **Decompose** |
| **Epic** | Architectural change, major feature | **Decompose** |

### 1.3 Decompose L and Epic Features

For each L or Epic:

```
[Original Feature]
├── Setup subtask (S)
├── Core logic subtask (M)
├── Integration subtask (M)
├── Testing subtask (S)
└── [More subtasks as needed]
```

**Prompt for AI assistance:**

```
I need to decompose this feature for AI development:

Feature: [Name]
Description: [Description]
Test Scenarios: [List]

Break this into subtasks where each is either:
- S (small): 1 session, single file
- M (medium): 2-3 sessions, clear boundaries

Ensure clear dependencies between subtasks.
```

### 1.4 Update Feature-Test Matrix

Add size to each feature. Verify no L or Epic remains without decomposition.

---

## Step 2: Risk Classification (20-30 min)

### 2.1 Classify Each Feature

For each feature, assess:

| Factor | Risk Increase |
|--------|---------------|
| Handles PII/sensitive data | +1 |
| Touches auth/authorization | +2 |
| Involves payments/money | +2 |
| Uses AI for decisions | +1 |
| Integrates external service | +1 |
| Can delete/modify data | +1 |

**Score:**
- 4+ = Critical
- 2-3 = High
- 1 = Medium
- 0 = Low

### 2.2 Document in Feature-Test Matrix

Add risk classification column if not present.

---

## Step 3: Create Agent Harness Design (30-45 min)

### 3.1 Identify Session Types Needed

Review your features and identify which session types apply:

- [ ] Initialization (project setup)
- [ ] Feature Development (standard features)
- [ ] Integration (external services)
- [ ] AI Feature (AI-powered features)
- [ ] Review/Fix (addressing issues)
- [ ] Refactor (code improvements)

### 3.2 Customize Session Configurations

For each session type you'll use, define:
- Duration limits
- Context to load
- Success criteria
- Recovery procedures

### 3.3 Document the Harness

Fill out the Agent Harness Design template with your project-specific configurations.

---

## Step 4: Map Human Checkpoints (30-45 min)

### 4.1 Identify Checkpoint Triggers

Based on risk classifications:

| Risk Level | Required Checkpoints |
|------------|---------------------|
| Critical | Security, Architecture |
| High | Appropriate type + spot-check |
| Medium | AI review only |
| Low | Automated only |

### 4.2 Assign Reviewers

For each checkpoint, assign:
- Primary reviewer
- Backup reviewer
- Review SLA

### 4.3 Document Checkpoint Map

Complete the Human Checkpoint Map template with your features and reviewers.

---

## Step 5: Plan Context Management (20-30 min)

### 5.1 Establish PROGRESS.md

Create `/docs/PROGRESS.md` with:
- Current sprint section
- Session log format
- Initial feature status

### 5.2 Define Session Protocols

Customize for your team:
- Session duration limits
- Context loading rules
- Handoff artifact format

### 5.3 Document the Plan

Complete Context Management Plan template.

---

## Step 6: Configure Quality Gates (45-60 min)

### 6.1 Level 1: Pre-commit

Set up:
- Husky or pre-commit
- Lint-staged configuration
- ESLint rules
- Prettier configuration
- TypeScript config

### 6.2 Level 2: Pull Request

Configure CI/CD:
- Test runner
- Coverage threshold
- Build verification
- Security scanning

### 6.3 Level 3: Staging

Set up:
- Staging environment
- E2E test suite
- Performance baseline

### 6.4 Level 4: Production

Configure:
- Smoke tests
- Monitoring integration
- Rollback mechanism

### 6.5 Document Gate Definitions

Complete Quality Gate Definitions template.

---

## Step 7: Create Issues (30-60 min)

### 7.1 Issue Structure

For each feature, create an issue with:

```
Title: [Feature ID] Feature Name

Description:
Brief description

Acceptance Criteria:
[Paste from Feature-Test Matrix]

Labels:
- Size: S/M
- Risk: Critical/High/Medium/Low
- Phase: 1/2/3
- Type: feature/integration/ai

Definition of Done:
- [ ] Tests written (TDD)
- [ ] Implementation complete
- [ ] AI review done
- [ ] Human review done (if Critical/High)
- [ ] Quality gates passing
```

### 7.2 Set Dependencies

Link related issues:
- Blocks / Blocked by
- Parent / Child
- Related

### 7.3 Create Board

Set up project board with columns:
- Backlog
- Ready
- In Progress
- In Review
- Done

---

## Phase 2 Completion

### Final Checklist

- [ ] All features sized (S/M only, L/Epic decomposed)
- [ ] Risk classifications assigned
- [ ] Agent Harness Design complete
- [ ] Human Checkpoint Map complete
- [ ] Context Management Plan complete
- [ ] Quality Gate Definitions complete
- [ ] All features have issues
- [ ] Issues labeled correctly
- [ ] Dependencies mapped
- [ ] Board configured

### Output Files

```
/docs/
  AGENT-HARNESS-DESIGN.md
  HUMAN-CHECKPOINT-MAP.md
  CONTEXT-MANAGEMENT-PLAN.md
  QUALITY-GATE-DEFINITIONS.md
  PROGRESS.md (initialized)
```

### Time Summary

| Step | Simple | Standard | Enterprise |
|------|--------|----------|------------|
| Feature Sizing | 20 min | 30 min | 60 min |
| Risk Classification | 15 min | 20 min | 30 min |
| Agent Harness | 20 min | 30 min | 45 min |
| Checkpoint Map | 20 min | 30 min | 45 min |
| Context Management | 15 min | 20 min | 30 min |
| Quality Gates | 30 min | 45 min | 90 min |
| Create Issues | 20 min | 45 min | 90 min |
| **Total** | **~2 hrs** | **~4 hrs** | **~7 hrs** |

---

## Next Steps

With Phase 2 complete, proceed to **Phase 3: DEVELOP** to:
- Execute TDD workflow
- Maintain session discipline
- Apply multi-layer review process

---

*Workflow Guide Version: 1.0 | SEAD Framework*
