# Multi-Layer Review Process

**Project:** [Project Name]

**Version:** 1.0

---

## Overview

Never trust single-pass AI generation. This multi-layer review process catches errors through redundancy: AI generates, different AI reviews, automation scans, human decides.

---

## The Four Layers

```
┌──────────────────────────────────────────────────────────────┐
│                    REVIEW LAYERS                              │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  LAYER 1: GENERATION                                          │
│  ├── AI writes tests (TDD)                                    │
│  ├── AI implements solution                                   │
│  └── Output: PR with code                                     │
│                                                               │
│  LAYER 2: AI REVIEW                                           │
│  ├── Fresh context (new session)                              │
│  ├── Reviews for logic, security, edge cases                  │
│  └── Output: Review comments                                  │
│                                                               │
│  LAYER 3: AUTOMATED SCANS                                     │
│  ├── Linting and formatting                                   │
│  ├── Type checking                                            │
│  ├── Security scanning                                        │
│  ├── Test coverage                                            │
│  └── Output: Pass/fail gates                                  │
│                                                               │
│  LAYER 4: HUMAN DECISION                                      │
│  ├── Reviews AI review comments                               │
│  ├── Checks architecture alignment                            │
│  ├── Verifies business logic                                  │
│  └── Output: Approve/Request changes                          │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## Layer 1: Generation

**Actor:** AI Code Generator (Cursor, Factory.ai, Copilot, etc.)

**Process:**
1. Load AGENTS.md and relevant context
2. Follow TDD workflow
3. Write tests first
4. Implement to pass tests
5. Create PR

**Output:** Pull request with:
- Test files
- Implementation files
- Commit history

---

## Layer 2: AI Review

**Actor:** AI Thinking Partner with fresh context (Claude, GPT-4, etc.)

**Critical Rule:** NEVER use same session that generated code. Fresh context catches blind spots.

### Triggering Review

For all features:
- Automated AI review tool (if available)

For High/Critical features:
- Manual review in new AI conversation

### Review Prompts

#### General Code Review

```
Review this code for quality issues:

[Paste code]

Check for:
1. Logic errors
2. Edge cases not handled
3. Error handling gaps
4. Performance issues
5. Code clarity/maintainability

For each issue: severity (High/Medium/Low), location, suggested fix.
```

#### Security Review (Critical/High Risk)

```
Review this code for security vulnerabilities:

[Paste code]

Check for:
1. OWASP Top 10 vulnerabilities
2. Input validation gaps
3. Output encoding issues
4. Authentication/authorization flaws
5. Sensitive data exposure
6. Injection vulnerabilities

For each issue: CVSS severity estimate, location, remediation.
```

#### AI Feature Review

```
Review this AI feature for boundary enforcement:

[Paste code]

Check:
1. Can AI modify data directly? (Should: NO)
2. Is human confirmation required? (Should: YES for actions)
3. Is reasoning/explanation provided? (Should: YES)
4. How is missing data handled?
5. How is AI service failure handled?
6. Are rate limits implemented?

For each issue: severity, location, suggested fix.
```

#### Integration Review

```
Review this integration code for reliability:

[Paste code]

Check:
1. Error handling for all failure modes
2. Timeout handling
3. Retry logic appropriateness
4. Circuit breaker (if applicable)
5. Rate limit handling
6. Data validation on receive

For each issue: severity, location, suggested fix.
```

### Documenting Review

Create review comment in PR:

```markdown
## AI Review - [Date]

### Summary
[Overall assessment]

### Issues Found

#### High Severity
- **Issue:** [Description]
  - Location: [File:Line]
  - Fix: [Suggested fix]

#### Medium Severity
- **Issue:** [Description]
  - Location: [File:Line]
  - Fix: [Suggested fix]

#### Low Severity
- **Issue:** [Description]
  - Location: [File:Line]
  - Fix: [Suggested fix]

### Recommendations
- [Optional improvements]
```

---

## Layer 3: Automated Scans

**Actor:** CI/CD Pipeline

### Checks

| Check | Tool | Failure Behavior |
|-------|------|------------------|
| Linting | ESLint | Block merge |
| Formatting | Prettier | Block merge |
| Type checking | TypeScript | Block merge |
| Unit tests | Jest/Vitest | Block merge |
| Coverage | Jest | Block if < threshold |
| Security | npm audit/Snyk | Block if critical |
| Build | Next.js/Vite | Block merge |

### Configuration Example

```yaml
# .github/workflows/pr-checks.yml
name: PR Checks

on: [pull_request]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      
      - run: npm ci
      - run: npm run lint
      - run: npm run typecheck
      - run: npm run test:coverage
      - run: npm run build
      - run: npm audit --audit-level=high
```

---

## Layer 4: Human Decision

**Actor:** You (for Critical/High) or auto-merge (for Medium/Low)

### When Human Review Required

| Risk Level | Human Review |
|------------|--------------|
| Critical | Always, full review |
| High | Always, focused review |
| Medium | Optional, spot-check |
| Low | Not required |

### Human Review Focus

For Critical/High features:

1. **Architecture alignment**
   - Does this match our ADR decisions?
   - Are patterns consistent?

2. **Business logic**
   - Does this meet requirements?
   - Are edge cases handled correctly?

3. **AI review issues**
   - Were all High issues addressed?
   - Are Medium issues acceptable?

4. **Security**
   - For auth/data features specifically
   - Double-check AI security review

### Review Checklist

```markdown
## Human Review Checklist

### Architecture
- [ ] Matches ADR decisions
- [ ] Follows established patterns
- [ ] No unexpected dependencies

### Business Logic
- [ ] Meets acceptance criteria
- [ ] Edge cases handled
- [ ] Error states handled

### AI Review Response
- [ ] All High issues resolved
- [ ] Medium issues reviewed
- [ ] Low issues acknowledged

### Security (if applicable)
- [ ] No auth bypasses
- [ ] Input validation present
- [ ] No sensitive data exposure

### Decision
- [ ] APPROVE
- [ ] REQUEST CHANGES (list issues)
```

---

## Review by Risk Level

### Critical Features

```
Layer 1: AI Generation
    ↓
Layer 2: AI Security Review (mandatory, fresh context)
    ↓
Layer 3: Automated Scans + Security Scan
    ↓
Layer 4: Full Human Review
    ↓
Merge (with human approval)
```

### High Features

```
Layer 1: AI Generation
    ↓
Layer 2: AI Review (mandatory, fresh context)
    ↓
Layer 3: Automated Scans
    ↓
Layer 4: Human Spot-Check
    ↓
Merge (with human approval)
```

### Medium Features

```
Layer 1: AI Generation
    ↓
Layer 2: Automated AI Review (if available)
    ↓
Layer 3: Automated Scans
    ↓
Layer 4: Optional human review
    ↓
Merge (auto or human)
```

### Low Features

```
Layer 1: AI Generation
    ↓
Layer 3: Automated Scans
    ↓
Merge (auto)
```

---

## Review Metrics

Track to improve review effectiveness:

| Metric | Target | Meaning |
|--------|--------|---------|
| Issues caught in Layer 2 | > 0.5/PR | AI review is finding issues |
| Issues caught in Layer 4 | < 0.2/PR | Earlier layers catching most |
| Post-merge bugs | < 1/month | Reviews are effective |
| Review turnaround | < 4 hours | Not bottlenecking |

---

## Quick Reference

```
LAYER 1: AI GENERATION
- AI writes tests + code
- Creates PR

LAYER 2: AI REVIEW  
- Fresh context (new session!)
- Use review prompts
- Document findings

LAYER 3: AUTOMATED
- CI/CD runs checks
- All must pass

LAYER 4: HUMAN
- Critical/High: Full review
- Medium: Optional
- Low: Skip
```

---

*Template Version: 1.0 | SEAD Framework*
