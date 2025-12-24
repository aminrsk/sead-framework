# Context Management Plan

**Project:** [Project Name]

**Version:** 1.0

**Last Updated:** [Date]

---

## Overview

This document defines strategies to prevent context rot across AI sessions and ensure consistent, high-quality output throughout development.

---

## The Context Problem

AI coding assistants have limited context windows and no persistent memory between sessions. Without management:
- Previous decisions are forgotten
- Code patterns become inconsistent
- Errors repeat across sessions
- Quality degrades over time

---

## Context Management Strategies

### Strategy 1: AGENTS.md as Anchor

**Purpose:** Provide consistent base context for every session

**Implementation:**
- AGENTS.md loaded at start of every session
- Contains project context, standards, rules
- Updated when decisions change
- Kept under 150 lines

**Update Triggers:**
- New ADR decision
- Tech stack change
- New pattern established
- Security rule added

---

### Strategy 2: Session Isolation

**Purpose:** Prevent contaminated context from previous work

**Implementation:**
- Start fresh session for each feature
- Don't carry forward assumptions
- Load only relevant code for current task
- Clear session when switching contexts

**Rules:**
- One feature per session
- Fresh start after breaks
- New session for reviews
- Clean context for debugging

---

### Strategy 3: Minimal Context Loading

**Purpose:** Maximize useful context by excluding irrelevant information

**DO Load:**
```
- AGENTS.md (always)
- Current feature's test file
- Current feature's implementation file
- Directly imported modules
- Feature-Test Matrix entry
```

**DO NOT Load:**
```
- Entire codebase
- Unrelated features
- Verbose documentation
- Historical chat logs
- Full ADR collection
```

---

### Strategy 4: Progress Tracking (PROGRESS.md)

**Purpose:** Maintain state across sessions

**File Location:** `/docs/PROGRESS.md` or project root

**Format:**

```markdown
# Progress Log

## Current Sprint

### In Progress
- [F001] User Registration - 80% complete
  - Tests: Done
  - Implementation: In progress
  - Blocker: None

### Blocked
- [F010] External API - Waiting for credentials

### Completed This Sprint
- [F000] Project Setup - Done

## Session Log

### [Date] Session 3
- Goal: Complete F001 implementation
- Outcome: Success, PR created
- Next: F002 User Login

### [Date] Session 2
- Goal: F001 tests
- Outcome: Success
- Next: Implementation
```

**Update Frequency:** End of each session

---

### Strategy 5: Handoff Artifacts

**Purpose:** Enable clean context transfer between sessions

**Session End Artifact:**

```markdown
## Session Summary

**Feature:** F001 User Registration
**Goal:** Write tests for registration flow
**Outcome:** Complete

**Files Changed:**
- `/tests/auth/registration.test.ts` (created)

**Tests Status:**
- 5 tests written
- All currently failing (expected - TDD)

**Next Session Goal:**
- Implement registration to pass tests

**Blockers:** None

**Notes:**
- Using Zod for validation
- Following pattern from F000
```

---

## Session Protocols

### Session Start Protocol

```
1. Review PROGRESS.md
2. Identify session goal
3. Load AGENTS.md
4. Load relevant files only:
   - Current feature test file
   - Current feature implementation file
   - Related utilities (if needed)
5. State goal clearly to AI
6. Set timer
```

### Session End Protocol

```
1. Verify tests pass
2. Commit changes
3. Update PROGRESS.md:
   - Mark session complete
   - Note outcome
   - Document blockers
   - Set next goal
4. Update issue status
5. Create handoff artifact if complex
```

### Context Refresh Protocol

Use when context seems "stale":

```
1. End current session
2. Take 5-minute break
3. Start fresh session
4. Load only AGENTS.md
5. Explicitly state current state
6. Resume work
```

---

## Context Templates

### Feature Development Session

```
I'm working on [Feature ID]: [Feature Name]

Project context is in AGENTS.md.

Current state:
- Tests: [written/not written/passing/failing]
- Implementation: [not started/in progress/complete]

Session goal: [specific goal]

Relevant files:
[Paste only relevant code]

Acceptance criteria:
[Paste from Feature-Test Matrix]
```

### Review Session

```
I need to review code for [Feature ID]: [Feature Name]

This is a FRESH review session - not the session that wrote this code.

Review focus:
- [Security/Logic/AI boundaries/Performance]

Acceptance criteria this should meet:
[Paste criteria]

Code to review:
[Paste code]
```

### Debug Session

```
I'm debugging an issue with [Feature ID]: [Feature Name]

Project context is in AGENTS.md.

Expected behavior:
[What should happen]

Actual behavior:
[What's happening]

Error message (if any):
[Paste error]

Relevant code:
[Paste minimal relevant code]
```

---

## Context Limits Reference

| AI Model | Approx Context | Practical Limit |
|----------|----------------|-----------------|
| Claude | 100-200K tokens | ~50K tokens useful |
| GPT-4 | 8-128K tokens | ~30K tokens useful |
| Gemini | 1M+ tokens | ~50K tokens useful |

**Practical guidance:** Even with large contexts, limit to ~50K tokens for best results. Quality degrades with more context, even when technically supported.

---

## Warning Signs

Context may be degraded when:

🚩 AI repeats mistakes from earlier in session

🚩 AI forgets coding standards defined in AGENTS.md

🚩 AI suggests patterns that contradict ADR decisions

🚩 Quality noticeably drops compared to session start

🚩 AI seems "confused" about project structure

**Response:** End session, refresh context, start new session.

---

## Metrics

Track these to assess context management effectiveness:

| Metric | Target | Action if Missed |
|--------|--------|------------------|
| Session success rate | > 80% | Reduce session scope |
| Context refresh frequency | < 2 per day | Improve AGENTS.md |
| 4-Attempt triggers | < 1 per week | Improve decomposition |
| Inconsistency reports | 0 | Update AGENTS.md |

---

*Template Version: 1.0 | SEAD Framework*
