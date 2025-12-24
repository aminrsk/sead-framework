# Agent Harness Design

**Project:** [Project Name]

**Version:** 1.0

**Last Updated:** [Date]

---

## Overview

This document defines how AI coding sessions are structured, including session types, boundaries, and recovery procedures.

---

## Session Types

### Type 1: Initialization

**Purpose:** Project setup, configuration, boilerplate

**Duration:** 30-45 minutes

**Context to Load:**
- AGENTS.md
- ADR decisions
- Tech stack requirements

**Success Criteria:**
- Project structure created
- Dependencies installed
- Configuration files set up
- Initial commit made

**Recovery if Failed:**
- Clear generated files
- Start fresh session
- Simplify scope if needed

---

### Type 2: Feature Development

**Purpose:** Implement individual features using TDD

**Duration:** 25-45 minutes

**Context to Load:**
- AGENTS.md
- Feature-Test Matrix entry for this feature
- Related existing code (if any)
- Acceptance criteria

**Success Criteria:**
- Tests written and failing
- Implementation passes tests
- Code committed

**Recovery if Failed:**
- Document what's blocking
- Apply 4-Attempt Rule
- Decompose if feature too large

---

### Type 3: Integration

**Purpose:** Connect external services/APIs

**Duration:** 45-60 minutes

**Context to Load:**
- AGENTS.md
- ADR for this integration
- External API documentation
- Existing integration patterns

**Success Criteria:**
- Connection established
- Error handling implemented
- Tests cover success and failure

**Recovery if Failed:**
- Isolate integration code
- Mock external service
- Escalate if API issues

---

### Type 4: AI Feature

**Purpose:** Implement AI-powered functionality

**Duration:** 45-60 minutes

**Context to Load:**
- AGENTS.md
- AI feature specification from PRD
- AI boundary definitions
- Existing AI patterns

**Success Criteria:**
- Prompts tested and working
- Boundaries enforced
- Human confirmation implemented
- Fallbacks in place

**Recovery if Failed:**
- Simplify prompt
- Add more constraints
- Test in isolation

---

### Type 5: Review/Fix

**Purpose:** Address issues from AI review or testing

**Duration:** 25-30 minutes

**Context to Load:**
- AGENTS.md
- Review comments
- Specific code to fix
- Test results

**Success Criteria:**
- All review items addressed
- Tests still passing
- No regressions

**Recovery if Failed:**
- Prioritize critical issues
- Defer low-priority items
- Document for later

---

### Type 6: Refactor

**Purpose:** Improve code quality without changing behavior

**Duration:** 25-45 minutes

**Context to Load:**
- AGENTS.md
- Code to refactor
- All related tests
- Style guidelines

**Success Criteria:**
- All tests still pass
- Code quality improved
- No behavior changes

**Recovery if Failed:**
- Revert changes
- Smaller refactor scope
- Add tests first

---

## Feature Sizing Reference

| Size | Description | Sessions | Max Duration | Action |
|------|-------------|----------|--------------|--------|
| **S** | Single-file, isolated | 1 | 45 min | Direct implementation |
| **M** | Multi-file, clear boundaries | 2-3 | 2 hours | Plan then implement |
| **L** | Cross-cutting, integrations | 4-6 | 4 hours | **Decompose first** |
| **Epic** | Architectural changes | 7+ | 8+ hours | **Must decompose** |

### Decomposition Rules

**L features must be broken into:**
- Setup task (S)
- Core implementation tasks (M each)
- Integration task (M)
- Testing task (S)

**Epics must be broken into:**
- Multiple L features (which then decompose to S/M)
- Clear milestones between features
- Human checkpoint at each milestone

---

## Session Boundaries

### Time Limits

| Complexity | Maximum Duration |
|------------|------------------|
| Simple changes | 25 minutes |
| Standard features | 45 minutes |
| Complex integrations | 60 minutes |

**Rule:** If session exceeds time limit without progress, STOP and reassess.

### Context Limits

**DO load:**
- AGENTS.md (always)
- Relevant feature spec
- Directly related code
- Current tests

**DO NOT load:**
- Entire codebase
- Unrelated features
- Historical decisions already in ADR
- Verbose documentation

### Session Isolation

Each session should:
- Have ONE clear goal
- Start with fresh context
- Not carry assumptions from previous sessions
- End with committed code or documented blockers

---

## The 4-Attempt Rule

### Definition

If a logic problem isn't solved in 4 AI iterations, the architecture is wrong—not the prompt.

### What Counts as One Attempt

- One complete AI coding session on the same problem
- One red-green-refactor cycle that fails
- One focused conversation on a specific blocker

### What Does NOT Count

- Multiple prompts refining the same solution within one session
- Clarifying questions
- Adding context

### When Triggered

After 4 attempts:

1. **STOP coding**
2. **Assess:**
   - Is the feature sized correctly?
   - Is there a missing prerequisite?
   - Is the approach fundamentally wrong?
3. **Choose action:**
   - Decompose feature
   - Build prerequisite first
   - Change approach (document in ADR)
   - Reduce scope

---

## Recovery Procedures

### Session Failure

```
1. Document what was attempted
2. Document what failed and why
3. Update issue with blocker status
4. Do NOT continue in same session
5. Start fresh session with adjusted approach
```

### 4-Attempt Trigger

```
1. STOP immediately
2. Create "Architecture Review" task
3. Document all 4 attempts and outcomes
4. Identify root cause
5. Update ADR if approach changes
6. Decompose into smaller tasks
7. Resume with new approach
```

### Integration Failure

```
1. Isolate integration code
2. Create mock for external service
3. Verify internal logic works
4. Test integration separately
5. Check external service status
6. Escalate if API issue
```

---

## Session Execution Checklist

### Before Session

- [ ] Feature-Test Matrix entry reviewed
- [ ] AGENTS.md loaded
- [ ] Relevant code identified
- [ ] Session type selected
- [ ] Time limit set
- [ ] ONE clear goal defined

### During Session

- [ ] Start with tests (TDD)
- [ ] Implement to pass tests
- [ ] Stay within scope
- [ ] Track attempt count
- [ ] Stop if time exceeded

### After Session

- [ ] Tests passing?
- [ ] Code committed?
- [ ] Issue updated?
- [ ] Blockers documented?
- [ ] Ready for review (if complete)?

---

*Template Version: 1.0 | SEAD Framework*
