# Human Checkpoint Map

**Project:** [Project Name]

**Version:** 1.0

**Last Updated:** [Date]

---

## Overview

This document identifies all decision points requiring human approval before AI proceeds. These checkpoints prevent AI from making architectural or high-risk decisions autonomously.

---

## Risk Classification

| Category | Definition | Required Review |
|----------|------------|-----------------|
| **Critical** | Security, auth, payments, data deletion | Full human review + security scan |
| **High** | AI features, external integrations, PII | AI review + human spot-check |
| **Medium** | Core business logic | AI review + automated tests |
| **Low** | UI, styling, copy changes | Automated tests only |

---

## Checkpoint Types

### Type 1: Architecture Checkpoint

**Trigger:** Any change that affects system structure

**Examples:**
- Database schema changes
- New API endpoints
- New external service integration
- Changes to authentication flow
- New data models

**Review Process:**
1. AI proposes change
2. Human reviews implications
3. ADR created/updated
4. Human approves
5. AI implements approved design

**Artifacts Required:**
- ADR documenting decision
- Impact analysis
- Rollback plan

---

### Type 2: Security Checkpoint

**Trigger:** Any change touching security-sensitive code

**Examples:**
- Authentication changes
- Authorization rule changes
- Encryption implementation
- Secret management
- Input validation changes

**Review Process:**
1. AI implements with tests
2. AI review for security (fresh context)
3. Automated security scan
4. Human reviews all security-touching code
5. Sign-off before merge

**Artifacts Required:**
- Security review checklist completed
- Test coverage report
- OWASP check results

---

### Type 3: AI Feature Checkpoint

**Trigger:** Any AI-powered feature implementation

**Examples:**
- New AI prompt implementation
- AI boundary changes
- AI error handling
- AI-to-database interactions
- AI decision points

**Review Process:**
1. AI implements feature
2. Verify human confirmation in flow
3. Test boundary enforcement
4. Human reviews AI behavior
5. Sign-off before merge

**Artifacts Required:**
- Prompt documentation
- Boundary test results
- Edge case documentation

---

### Type 4: Integration Checkpoint

**Trigger:** Any external system integration

**Examples:**
- New API integration
- Webhook implementations
- Third-party SDK usage
- Data sync implementations

**Review Process:**
1. ADR documents integration approach
2. AI implements with mocks
3. Integration tests pass
4. Human reviews error handling
5. Staged rollout for live testing

**Artifacts Required:**
- Integration ADR
- Error scenario coverage
- Rollback procedure

---

### Type 5: Data Checkpoint

**Trigger:** Any change affecting user data

**Examples:**
- Data model changes
- Migration scripts
- Data deletion logic
- PII handling changes
- Backup/restore procedures

**Review Process:**
1. AI proposes schema/migration
2. Human reviews data impact
3. Test on staging data
4. Backup verification
5. Human approves migration

**Artifacts Required:**
- Migration script review
- Rollback script
- Data backup confirmation

---

## Feature Risk Classification

Use this table to classify each feature:

| Feature ID | Feature Name | Risk Level | Checkpoint Type | Reviewer |
|------------|--------------|------------|-----------------|----------|
| F001 | User Registration | Critical | Security | [Name] |
| F002 | User Login | Critical | Security | [Name] |
| F003 | Password Reset | Critical | Security | [Name] |
| F010 | [Feature] | High | AI Feature | [Name] |
| F020 | [Feature] | Medium | None | Auto |
| F030 | [Feature] | High | Integration | [Name] |

---

## Checkpoint Procedures

### Before AI Implementation

```
For Critical/High features:
1. Review feature specification
2. Identify checkpoint type(s)
3. Assign reviewer
4. Document expected review criteria
5. Notify reviewer of incoming work
```

### During AI Implementation

```
For features with checkpoints:
1. AI completes implementation
2. AI generates tests
3. All automated checks pass
4. PR created with checkpoint label
5. Reviewer notified
```

### Checkpoint Review

```
1. Reviewer receives notification
2. Review within [X] hours SLA
3. Use checkpoint-specific checklist
4. Document any issues
5. Approve or request changes
6. Sign-off recorded
```

---

## Checkpoint Checklists

### Security Review Checklist

- [ ] No hardcoded secrets
- [ ] Input validation present
- [ ] Output encoding/sanitization
- [ ] Authentication required where needed
- [ ] Authorization checks correct
- [ ] No sensitive data in logs
- [ ] HTTPS for external requests
- [ ] SQL injection prevention (parameterized queries)
- [ ] XSS prevention
- [ ] CSRF protection where needed

### AI Feature Checklist

- [ ] Human confirmation in flow
- [ ] AI cannot modify data directly
- [ ] Reasoning/explanation included
- [ ] Fallback for AI failure
- [ ] Rate limiting implemented
- [ ] Input validation before AI
- [ ] Output validation after AI
- [ ] Confidence thresholds working

### Integration Checklist

- [ ] Error handling for all failure modes
- [ ] Timeout handling
- [ ] Rate limit handling
- [ ] Authentication secure
- [ ] Data validation on receive
- [ ] Retry logic appropriate
- [ ] Circuit breaker if applicable
- [ ] Rollback procedure documented

### Data Change Checklist

- [ ] Backup created
- [ ] Rollback script tested
- [ ] No data loss possible
- [ ] PII handling correct
- [ ] Audit log updated
- [ ] Performance impact assessed
- [ ] Indexes appropriate

---

## Escalation Path

### If Reviewer Unavailable

1. Wait up to [X] hours
2. Escalate to backup reviewer: [Name]
3. If backup unavailable, escalate to [Name]
4. Document delay reason

### If Disagreement

1. Document disagreement
2. Escalate to [Name]
3. Meeting within 24 hours
4. Decision recorded in ADR

---

## Red Flags

Stop and escalate immediately if:

🚩 AI modifies security code without checkpoint

🚩 AI adds new external service without ADR

🚩 AI changes data model without review

🚩 AI implements AI feature without boundaries

🚩 AI deletes or modifies production data

🚩 Reviewer not assigned for Critical/High feature

---

*Template Version: 1.0 | SEAD Framework*
