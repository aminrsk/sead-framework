# Feature-Test Matrix

**Project:** [Project Name]

**Version:** 1.0

**Last Updated:** [Date]

---

## Overview

This matrix maps every feature to its acceptance criteria and test scenarios. It serves as:
1. The source of truth for what "done" means
2. The foundation for TDD (test-driven development)
3. The verification checklist during development

---

## Matrix Structure

| Column | Description |
|--------|-------------|
| Feature ID | Unique identifier matching PRD |
| Feature Name | Descriptive name |
| Acceptance Criteria | Given/When/Then statements |
| Test Scenarios | Specific test cases |
| Priority | P0 (must have), P1 (should have), P2 (nice to have) |
| Risk | Critical, High, Medium, Low |
| Size | S, M, L, Epic |

---

## Feature-Test Matrix

### Authentication Features

| ID | Feature | Acceptance Criteria | Test Scenarios | Priority | Risk | Size |
|----|---------|---------------------|----------------|----------|------|------|
| F001 | User Registration | **Given** a new user<br>**When** they submit valid registration<br>**Then** account is created and email sent | - Happy path: valid email, password<br>- Invalid email format<br>- Password too weak<br>- Duplicate email<br>- Email service failure | P0 | Critical | M |
| F002 | User Login | **Given** a registered user<br>**When** they enter correct credentials<br>**Then** they are authenticated | - Valid credentials<br>- Invalid password<br>- Non-existent user<br>- Account locked<br>- Session persistence | P0 | Critical | S |
| F003 | Password Reset | **Given** a user who forgot password<br>**When** they request reset<br>**Then** reset email is sent | - Valid email<br>- Non-existent email (same response)<br>- Expired token<br>- Token reuse prevention | P0 | Critical | M |

### Core Features

| ID | Feature | Acceptance Criteria | Test Scenarios | Priority | Risk | Size |
|----|---------|---------------------|----------------|----------|------|------|
| F010 | [Feature Name] | **Given** [context]<br>**When** [action]<br>**Then** [result] | - [Scenario 1]<br>- [Scenario 2]<br>- [Scenario 3] | P0 | High | M |
| F011 | [Feature Name] | **Given** [context]<br>**When** [action]<br>**Then** [result] | - [Scenario 1]<br>- [Scenario 2] | P1 | Medium | S |

### AI Features

| ID | Feature | Acceptance Criteria | Test Scenarios | Priority | Risk | Size |
|----|---------|---------------------|----------------|----------|------|------|
| F020 | [AI Feature] | **Given** [data context]<br>**When** AI analyzes<br>**Then** [output with reasoning] | - Valid input, clear output<br>- Missing data handling<br>- Low confidence response<br>- AI service timeout<br>- Rate limiting<br>- User confirmation required | P1 | High | L |

### Integration Features

| ID | Feature | Acceptance Criteria | Test Scenarios | Priority | Risk | Size |
|----|---------|---------------------|----------------|----------|------|------|
| F030 | [Integration] | **Given** connected system<br>**When** sync triggered<br>**Then** data updated | - Successful sync<br>- API authentication failure<br>- Rate limit exceeded<br>- Partial failure<br>- Rollback on error | P1 | High | M |

---

## Test Scenario Details

### F001: User Registration - Detailed Scenarios

#### Scenario 1: Happy Path

```gherkin
Given a new visitor on the registration page
When they enter a valid email "user@example.com"
And they enter a password meeting requirements
And they submit the form
Then an account should be created
And a verification email should be sent
And they should see a confirmation message
```

#### Scenario 2: Invalid Email Format

```gherkin
Given a new visitor on the registration page
When they enter an invalid email "not-an-email"
And they attempt to submit
Then they should see an error "Please enter a valid email"
And no account should be created
```

#### Scenario 3: Weak Password

```gherkin
Given a new visitor on the registration page
When they enter a valid email
And they enter a weak password "123"
Then they should see password requirements
And no account should be created
```

#### Scenario 4: Duplicate Email

```gherkin
Given an existing user with email "existing@example.com"
When a new visitor tries to register with "existing@example.com"
Then they should see "An account with this email already exists"
And no duplicate account should be created
```

---

## Test Categories

### By Type

| Category | Description | When to Run |
|----------|-------------|-------------|
| Unit | Individual function/component | Pre-commit |
| Integration | Multiple components together | PR |
| E2E | Full user flows | Staging |
| Performance | Load and speed | Pre-production |
| Security | Vulnerability scans | PR + Staging |

### By Feature Risk

| Risk Level | Test Coverage | Review Required |
|------------|---------------|-----------------|
| Critical | 100% of scenarios | Human review |
| High | 100% of scenarios | AI review + spot-check |
| Medium | 80% of scenarios | AI review |
| Low | Happy path + key errors | Automated only |

---

## Verification Checklist

Use this during development to verify completeness:

### Per Feature

- [ ] All acceptance criteria have corresponding tests
- [ ] Happy path tested
- [ ] Validation errors tested
- [ ] Edge cases tested
- [ ] Error states tested
- [ ] For AI features: boundaries tested
- [ ] For integrations: failure modes tested

### Before Phase 3 Exit

- [ ] All P0 features have 100% scenario coverage
- [ ] All P1 features have 80%+ scenario coverage
- [ ] Critical/High risk features have full coverage
- [ ] Coverage threshold met (recommend 80%+)
- [ ] All tests passing

---

## Notes

### Sizing Guidelines

| Size | Characteristics | Example |
|------|-----------------|---------|
| S | Single file, < 100 lines, no external deps | Form validation |
| M | Multi-file, clear boundaries, 1-2 sessions | CRUD feature |
| L | Cross-cutting, integrations, 4-6 sessions | **Decompose first** |
| Epic | Architectural changes, 7+ sessions | **Must decompose** |

### Risk Assessment

| Factor | Increases Risk |
|--------|----------------|
| Data | Handles sensitive/PII data |
| Auth | Touches authentication/authorization |
| Money | Involves payments/financial |
| AI | Uses AI for decisions |
| External | Integrates with external systems |
| Delete | Can delete/destroy data |

---

*Template Version: 1.0 | SEAD Framework*
