# Session Discipline Protocol

**Project:** [Project Name]

**Version:** 1.0

---

## Overview

Session discipline ensures consistent, high-quality AI coding sessions. Every session has a clear goal, time limit, and defined outcome.

---

## Session Structure

```
┌──────────────────────────────────────────────────────────────┐
│                     SESSION TIMELINE                          │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  START (5 min)                                                │
│  ├── Review PROGRESS.md                                       │
│  ├── Select ONE goal                                          │
│  ├── Load context (AGENTS.md + relevant files)                │
│  └── Set timer                                                │
│                                                               │
│  EXECUTE (20-50 min)                                          │
│  ├── TDD cycle                                                │
│  ├── Stay focused on single goal                              │
│  └── Track attempt count                                      │
│                                                               │
│  CLOSE (5 min)                                                │
│  ├── Verify tests pass                                        │
│  ├── Commit changes                                           │
│  ├── Update PROGRESS.md                                       │
│  └── Update issue status                                      │
│                                                               │
│  TOTAL: 30-60 minutes                                         │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## Session Start Protocol

### Step 1: Review Progress (2 min)

```bash
cat docs/PROGRESS.md
```

Check:
- What was completed last session?
- What's next in priority?
- Any blockers to address?

### Step 2: Select Goal (1 min)

Pick ONE of:
- One acceptance criterion to implement
- One bug to fix
- One refactor task
- One review to complete

**Rule:** Never multiple goals. One goal per session.

### Step 3: Load Context (2 min)

Always load:
- AGENTS.md

Load if relevant:
- Current feature's test file
- Current feature's implementation file
- Feature-Test Matrix entry
- Directly related utilities

**Do NOT load:**
- Entire codebase
- Unrelated features
- Historical discussions

### Step 4: Set Timer

| Session Type | Duration |
|--------------|----------|
| Simple change | 25 min |
| Standard feature | 45 min |
| Complex integration | 60 min |

**Rule:** When timer ends, go to Close Protocol even if not done.

---

## Session Execution

### Focus Rules

✅ **DO:**
- Work only on stated goal
- Follow TDD cycle
- Commit frequently
- Stop when timer rings

❌ **DO NOT:**
- Add "quick" unrelated fixes
- Refactor unrelated code
- Start new features
- Continue past time limit

### Attempt Tracking

Count attempts for the current problem:

| Attempt | Action |
|---------|--------|
| 1 | Try initial approach |
| 2 | Adjust based on failure |
| 3 | Try different angle |
| 4 | **STOP** - 4-Attempt Rule triggered |

### Progress Checkpoints

Every 15 minutes, verify:
- Am I still on goal?
- Are tests passing?
- Am I making progress?

If stuck for 15 min, consider:
- Simplify the problem
- Take a different approach
- End session and reassess

---

## Session Close Protocol

### Step 1: Verify Tests (1 min)

```bash
npm test
```

All tests must pass before committing.

### Step 2: Commit Changes (1 min)

```bash
git add .
git commit -m "[F001] feat: Brief description of what was done"
```

### Step 3: Update PROGRESS.md (2 min)

```markdown
### [Date] Session [N]
- Goal: [What you set out to do]
- Outcome: [Complete/Partial/Blocked]
- Files changed: [List]
- Next: [What should happen next]
- Blockers: [Any blockers]
```

### Step 4: Update Issue (1 min)

Update issue status:
- Add comment with session outcome
- Change status if complete
- Add blocker label if blocked

---

## Daily Rhythm

### Morning Block (Recommended)

```
09:00 - 09:10  Daily planning (review PROGRESS.md, prioritize)
09:10 - 10:00  Session 1
10:00 - 10:15  Break
10:15 - 11:00  Session 2
11:00 - 11:15  Break
11:15 - 12:00  Session 3 (or reviews/admin)
```

### Afternoon Block

```
13:00 - 13:45  Session 4
13:45 - 14:00  Break
14:00 - 14:45  Session 5
14:45 - 15:00  Break
15:00 - 15:45  Session 6
15:45 - 16:00  Daily wrap-up (update PROGRESS.md, plan tomorrow)
```

### Session Limits

| Per Day | Maximum |
|---------|---------|
| Focused coding sessions | 6 |
| Total coding time | 4.5 hours |
| Remaining time | Reviews, planning, communication |

---

## Session Types

### Type A: Feature Implementation

```
Goal: Implement [acceptance criterion]
Duration: 45 min
Context: AGENTS.md, Feature-Test Matrix entry, test file

Process:
1. Write test (RED)
2. Verify fail
3. Implement (GREEN)
4. Verify pass
5. Refactor
6. Commit
```

### Type B: Bug Fix

```
Goal: Fix [issue description]
Duration: 30 min
Context: AGENTS.md, failing test, related code

Process:
1. Write failing test that reproduces bug
2. Verify fail
3. Fix bug
4. Verify pass
5. Verify no regressions
6. Commit
```

### Type C: Review

```
Goal: Review [PR/feature]
Duration: 30 min
Context: AGENTS.md, code to review, acceptance criteria

Process:
1. Read acceptance criteria
2. Review code against criteria
3. Check for security issues
4. Check for edge cases
5. Document findings
6. Approve or request changes
```

### Type D: Refactor

```
Goal: Improve [specific code]
Duration: 30 min
Context: AGENTS.md, code to refactor, all tests

Process:
1. Ensure tests pass
2. Make incremental changes
3. Run tests after each change
4. Commit frequently
5. Final test run
```

---

## Interruption Handling

### If Interrupted

1. Note current state
2. Commit work-in-progress: `git commit -m "WIP: [state]"`
3. Handle interruption
4. Start fresh session when returning

### If Blocked

1. Document the blocker
2. Update issue with blocker label
3. Switch to different task
4. Create follow-up for blocker resolution

### If Timer Expires

1. Stop coding immediately
2. Commit current state (even if incomplete)
3. Document what's left
4. Take break before next session

---

## Anti-Patterns

### ❌ Marathon Sessions

Sessions over 60 min have diminishing returns. Take breaks.

### ❌ Multi-tasking

Working on multiple features in one session leads to incomplete work.

### ❌ Skipping Breaks

Breaks are part of the process. Quality degrades without them.

### ❌ Ignoring Timer

"Just 5 more minutes" becomes 30 minutes of unfocused work.

### ❌ No Clear Goal

Starting without a goal leads to wandering and incomplete work.

### ❌ Carrying Context

Starting new session with assumptions from old session causes errors.

---

## Metrics

Track these to improve session effectiveness:

| Metric | Target | Track How |
|--------|--------|-----------|
| Goal completion rate | > 80% | Goals achieved / sessions |
| Session overruns | < 10% | Sessions exceeding time |
| 4-Attempt triggers | < 1/week | Count in PROGRESS.md |
| Tests passing at close | 100% | Every session |

---

## Quick Reference Card

```
SESSION START (5 min)
□ Review PROGRESS.md
□ Select ONE goal
□ Load AGENTS.md + relevant files
□ Set timer

EXECUTE (20-50 min)
□ TDD: Red → Green → Refactor
□ Stay on goal
□ Count attempts (max 4)

CLOSE (5 min)
□ npm test (must pass)
□ git commit
□ Update PROGRESS.md
□ Update issue status
```

---

*Template Version: 1.0 | SEAD Framework*
