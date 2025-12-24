# Phase 3: DEVELOP - Workflow Guide

This guide walks you through executing Phase 3 development.

---

## Overview

**Goal:** Implement features using TDD, session discipline, and multi-layer review.

**Duration:** Ongoing (based on feature count and sizing)

**Inputs:** Phase 2 outputs (sized features, checkpoints, quality gates, issues)

**Outputs:**
- Working, tested code
- Passing quality gates
- Completed issues

---

## Daily Development Flow

```
┌──────────────────────────────────────────────────────────────┐
│                     DAILY FLOW                                │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  MORNING PLANNING (10 min)                                    │
│  ├── Review PROGRESS.md                                       │
│  ├── Check issue board                                        │
│  ├── Identify today's goals                                   │
│  └── Prepare first session                                    │
│                                                               │
│  DEVELOPMENT SESSIONS (4-6 sessions)                          │
│  ├── Session 1 (25-60 min)                                    │
│  ├── Break (5-10 min)                                         │
│  ├── Session 2 (25-60 min)                                    │
│  ├── Break                                                    │
│  └── ... repeat ...                                           │
│                                                               │
│  END OF DAY (10 min)                                          │
│  ├── Update PROGRESS.md                                       │
│  ├── Push all changes                                         │
│  ├── Update issue statuses                                    │
│  └── Plan tomorrow                                            │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## Step 1: Session Preparation

### 1.1 Select Feature

From your issue board, pick a feature that is:
- "Ready" status (all dependencies met)
- Highest priority available
- Sized S or M

### 1.2 Review Feature Details

Open the issue and review:
- Acceptance criteria
- Test scenarios from Feature-Test Matrix
- Risk classification
- Any notes or context

### 1.3 Prepare Context

Gather:
```
- AGENTS.md (always)
- Feature-Test Matrix entry for this feature
- Related code files (if any)
- Test file location
```

---

## Step 2: Execute TDD Session

### 2.1 Start Session

```
1. Set timer (25-45 min for S, 45-60 min for M)
2. Move issue to "In Progress"
3. Load context into AI coding assistant
4. State the goal clearly
```

### 2.2 TDD Cycle

For each acceptance criterion:

```
┌────────────────────────────────────────────┐
│                TDD CYCLE                    │
├────────────────────────────────────────────┤
│                                            │
│  1. Write test (should fail)               │
│         ↓                                  │
│  2. Run test → Verify FAIL                 │
│         ↓                                  │
│  3. Write minimal implementation           │
│         ↓                                  │
│  4. Run test → Verify PASS                 │
│         ↓                                  │
│  5. Refactor if needed                     │
│         ↓                                  │
│  6. Commit                                 │
│         ↓                                  │
│  7. Next criterion                         │
│                                            │
└────────────────────────────────────────────┘
```

### 2.3 Track Attempts

If struggling with a problem:
- Attempt 1: Initial approach
- Attempt 2: Adjust based on failure
- Attempt 3: Try different angle
- Attempt 4: **STOP** - 4-Attempt Rule triggered

### 2.4 End Session

When timer ends OR goal complete:

```
1. Run all tests: npm test
2. Commit changes: git commit -m "[F001] feat: description"
3. Update PROGRESS.md
4. Update issue status
5. Take break before next session
```

---

## Step 3: Create Pull Request

When feature is complete:

### 3.1 Prepare PR

```bash
# Ensure all tests pass
npm test

# Ensure coverage meets threshold
npm run test:coverage

# Ensure build works
npm run build

# Push branch
git push origin feature/F001-feature-name
```

### 3.2 Create PR

Title: `[F001] Feature Name`

Description:
```markdown
## Summary
Brief description of what this PR does.

## Acceptance Criteria
- [x] Criterion 1
- [x] Criterion 2
- [x] Criterion 3

## Test Coverage
- X new tests added
- Coverage: XX%

## Risk Level
[Critical/High/Medium/Low]

## Checklist
- [ ] Tests pass
- [ ] Coverage meets threshold
- [ ] Build succeeds
- [ ] Documentation updated (if needed)
```

### 3.3 Link to Issue

Connect PR to the tracking issue.

---

## Step 4: Multi-Layer Review

### Layer 1: Generation (Complete)

You've already generated the code via TDD.

### Layer 2: AI Review

**For Medium/Low risk:**
- Automated AI review if available
- Review comments added to PR

**For High/Critical risk:**
- Open new AI conversation (fresh context!)
- Use appropriate review prompt from Prompt Library
- Document findings in PR comments

### Layer 3: Automated Scans

CI/CD runs automatically:
- Linting
- Type checking
- Tests
- Coverage
- Security scan
- Build

All checks must pass.

### Layer 4: Human Review

**For Low risk:** Auto-merge if all checks pass

**For Medium risk:** Quick spot-check, approve

**For High/Critical risk:**
- Review all AI review comments
- Verify issues addressed
- Check architecture alignment
- Check business logic
- Use Human Review Checklist

---

## Step 5: Merge and Deploy

### 5.1 Merge

After approval:
```bash
# Merge PR
# (via GitHub UI or CLI)

# Delete feature branch
git branch -d feature/F001-feature-name
```

### 5.2 Deploy to Staging

Automatic via CI/CD, or manual trigger.

### 5.3 Verify

- Run E2E tests on staging
- Spot-check feature manually
- Verify no regressions

### 5.4 Update Issue

Move issue to "Done"

---

## Handling Special Cases

### 4-Attempt Rule Triggered

```
1. STOP coding immediately
2. Document what was attempted
3. Create "Architecture Review" issue
4. Reassess:
   - Is feature sized correctly?
   - Is there a missing prerequisite?
   - Is the approach wrong?
5. Decompose or change approach
6. Resume with new plan
```

### Blocked by Dependency

```
1. Document the blocker in issue
2. Add "Blocked" label
3. Switch to different feature
4. Create issue for blocker resolution
5. Return when unblocked
```

### Bug Discovered During Development

```
1. Document the bug
2. Decide: fix now or later?
   - If quick (< 15 min): fix in current session
   - If longer: create bug issue, continue current work
3. Don't let bugs derail feature work
```

### Review Finds Critical Issues

```
1. Don't argue - address the feedback
2. Create new commits for fixes
3. Re-request review
4. Verify all issues resolved
```

---

## Progress Tracking

### Update PROGRESS.md Daily

```markdown
## Current Sprint

### In Progress
- [F001] User Registration - 80%
  - Tests: Done
  - Implementation: In progress
  - Next: Complete validation

### Blocked
- [F010] External API - Waiting for credentials

### Completed This Sprint
- [F000] Project Setup

## Session Log

### 2025-12-15 Session 3
- Goal: F001 registration validation
- Outcome: Complete
- Files: auth/validation.ts, auth/validation.test.ts
- Next: Error handling

### 2025-12-15 Session 2
- Goal: F001 basic registration
- Outcome: Complete
- Next: Validation
```

### Update Issues

- Add comments with progress
- Update status labels
- Link to PRs

---

## Time Estimates by Feature Size

| Size | Sessions | Calendar Time |
|------|----------|---------------|
| S | 1 | 0.5 day |
| M | 2-3 | 1-2 days |

**Per sprint capacity:**
- 6 sessions/day × 5 days = 30 sessions/sprint
- Accounting for reviews/meetings: ~20-25 feature sessions
- Typical sprint: 8-12 S features OR 6-8 M features OR mix

---

## Quality Metrics

Track these during Phase 3:

| Metric | Target | Action if Missed |
|--------|--------|------------------|
| Test coverage | > 80% | Add more tests |
| Session success rate | > 80% | Reduce session scope |
| 4-Attempt triggers | < 1/week | Improve decomposition |
| PR first-time approval | > 70% | Better self-review |
| Bugs found in staging | < 2/sprint | More thorough testing |

---

## Exit Criteria

Phase 3 is complete when:

- [ ] All planned features implemented
- [ ] All tests passing
- [ ] Coverage meets threshold (80%+)
- [ ] All quality gates passing
- [ ] All issues in "Done" status
- [ ] No open blockers
- [ ] Code deployed to staging
- [ ] E2E tests passing on staging

---

## Next Steps

With Phase 3 complete, proceed to **Phase 4: DELIVER** to:
- Execute staged rollout
- Communicate with client
- Complete documentation
- Transition to support

---

*Workflow Guide Version: 1.0 | SEAD Framework*
