# Phase 2: ARCHITECT - Checklist

Use this checklist to verify Phase 2 is complete before moving to Phase 3.

---

## Feature Sizing

- [ ] All features from Phase 1 reviewed
- [ ] Size assigned to each feature (S/M/L/Epic)
- [ ] L features decomposed into S/M subtasks
- [ ] Epic features decomposed into smaller features
- [ ] No L or Epic features remain without decomposition plan
- [ ] Dependencies identified between features
- [ ] Feature-Test Matrix updated with sizes

---

## Risk Classification

- [ ] Each feature assessed for risk factors
- [ ] Risk level assigned (Critical/High/Medium/Low)
- [ ] Critical features identified
- [ ] High-risk features identified
- [ ] Feature-Test Matrix updated with risk levels

---

## Agent Harness Design

- [ ] Session types identified for this project
- [ ] Duration limits defined per session type
- [ ] Context loading rules defined
- [ ] Success criteria defined per session type
- [ ] Recovery procedures documented
- [ ] 4-Attempt Rule documented
- [ ] Feature-to-session-type mapping complete
- [ ] Document saved: `AGENT-HARNESS-DESIGN.md`

---

## Human Checkpoint Map

- [ ] Checkpoint types identified
  - [ ] Architecture checkpoints
  - [ ] Security checkpoints
  - [ ] AI feature checkpoints
  - [ ] Integration checkpoints
  - [ ] Data checkpoints
- [ ] Features mapped to checkpoint types
- [ ] Reviewers assigned (primary and backup)
- [ ] Review SLAs defined
- [ ] Checklists created for each checkpoint type
- [ ] Escalation path documented
- [ ] Document saved: `HUMAN-CHECKPOINT-MAP.md`

---

## Context Management Plan

- [ ] PROGRESS.md template created
- [ ] Session start protocol defined
- [ ] Session end protocol defined
- [ ] Context loading rules documented
- [ ] Handoff artifact format defined
- [ ] Context refresh triggers identified
- [ ] Document saved: `CONTEXT-MANAGEMENT-PLAN.md`

---

## Quality Gate Definitions

- [ ] Level 1 (Pre-commit) configured
  - [ ] Linting
  - [ ] Formatting
  - [ ] Type checking
  - [ ] Secrets scanning
- [ ] Level 2 (Pull Request) configured
  - [ ] All tests
  - [ ] Coverage threshold
  - [ ] Build verification
  - [ ] Security scanning
  - [ ] AI review
- [ ] Level 3 (Staging) configured
  - [ ] E2E tests
  - [ ] Integration tests
  - [ ] Performance tests
- [ ] Level 4 (Production) configured
  - [ ] Smoke tests
  - [ ] Monitoring
  - [ ] Rollback procedure
- [ ] Bypass policies documented
- [ ] Document saved: `QUALITY-GATE-DEFINITIONS.md`

---

## Issue Management

- [ ] Issues created for all features
- [ ] Issues labeled with size
- [ ] Issues labeled with risk
- [ ] Issues labeled with phase
- [ ] Acceptance criteria in each issue
- [ ] Definition of done in each issue
- [ ] Dependencies linked
- [ ] Project board configured
  - [ ] Backlog column
  - [ ] Ready column
  - [ ] In Progress column
  - [ ] In Review column
  - [ ] Done column

---

## Files Created

- [ ] `/docs/AGENT-HARNESS-DESIGN.md`
- [ ] `/docs/HUMAN-CHECKPOINT-MAP.md`
- [ ] `/docs/CONTEXT-MANAGEMENT-PLAN.md`
- [ ] `/docs/QUALITY-GATE-DEFINITIONS.md`
- [ ] `/docs/PROGRESS.md` (initialized)

---

## Final Verification

| Criterion | Status |
|-----------|--------|
| All features sized S/M | ⬜ |
| Risk classifications complete | ⬜ |
| Agent Harness documented | ⬜ |
| Checkpoints mapped | ⬜ |
| Context management planned | ⬜ |
| Quality gates configured | ⬜ |
| Issues created | ⬜ |

**All criteria met:** ⬜ Ready for Phase 3

---

## Notes

[Any notes or items to carry forward to Phase 3]

---

*Checklist Version: 1.0 | SEAD Framework*
