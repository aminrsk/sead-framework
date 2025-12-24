# TDD Workflow Guide

**Project:** [Project Name]

**Version:** 1.0

---

## Overview

Test-Driven Development (TDD) is mandatory for SEAD projects. Tests become your verification layer when you can't read every line of AI-generated code.

---

## The TDD Cycle

```
┌──────────────────────────────────────────────────────────────┐
│                        TDD CYCLE                              │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│    ┌─────────┐                                                │
│    │  RED    │  Write test that fails                         │
│    │         │  (Based on acceptance criteria)                │
│    └────┬────┘                                                │
│         │                                                     │
│         ▼                                                     │
│    ┌─────────┐                                                │
│    │ VERIFY  │  Run test → Must FAIL                          │
│    │  FAIL   │  (If passes, test is wrong)                    │
│    └────┬────┘                                                │
│         │                                                     │
│         ▼                                                     │
│    ┌─────────┐                                                │
│    │  GREEN  │  Write minimal code to pass                    │
│    │         │  (Only enough to pass, no more)                │
│    └────┬────┘                                                │
│         │                                                     │
│         ▼                                                     │
│    ┌─────────┐                                                │
│    │ VERIFY  │  Run test → Must PASS                          │
│    │  PASS   │  (All tests should pass)                       │
│    └────┬────┘                                                │
│         │                                                     │
│         ▼                                                     │
│    ┌─────────┐                                                │
│    │REFACTOR │  Improve code quality                          │
│    │         │  (Tests still pass)                            │
│    └────┬────┘                                                │
│         │                                                     │
│         ▼                                                     │
│    ┌─────────┐                                                │
│    │ COMMIT  │  Save progress                                 │
│    └────┬────┘                                                │
│         │                                                     │
│         └──────────────► Next acceptance criterion            │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## Step-by-Step Process

### Step 1: Prepare

Before starting:

1. Open Feature-Test Matrix
2. Find the feature you're implementing
3. Read all acceptance criteria
4. Read all test scenarios

### Step 2: Write First Test (RED)

**Prompt for AI:**

```
I need to write a test for this feature:

Feature: [Feature Name]
Acceptance Criterion: [Given/When/Then statement]
Test Scenario: [Specific scenario]

Project context is in AGENTS.md.

Write a test that:
1. Sets up the preconditions (Given)
2. Performs the action (When)
3. Asserts the expected outcome (Then)

The test should FAIL right now because the implementation doesn't exist yet.
```

**Example Test:**

```typescript
describe('User Registration', () => {
  it('should create account with valid email and password', async () => {
    // Given
    const validInput = {
      email: 'user@example.com',
      password: 'SecurePass123!',
    };

    // When
    const result = await registerUser(validInput);

    // Then
    expect(result.success).toBe(true);
    expect(result.user.email).toBe('user@example.com');
  });
});
```

### Step 3: Verify Failure

Run the test:

```bash
npm test -- --grep "should create account"
```

**Expected:** Test FAILS because `registerUser` doesn't exist.

**If test passes:** Your test is wrong. It's not testing what you think.

### Step 4: Implement (GREEN)

**Prompt for AI:**

```
The following test is failing:

[Paste test code]

Error message:
[Paste error]

Write the MINIMAL implementation to make this test pass.
Do not add features beyond what the test requires.
```

### Step 5: Verify Success

Run the test again:

```bash
npm test -- --grep "should create account"
```

**Expected:** Test PASSES.

**If test fails:** Debug. Don't write more code until this test passes.

### Step 6: Refactor (Optional)

If code can be improved:

1. Identify improvement
2. Make change
3. Run tests
4. Verify still passing

### Step 7: Commit

```bash
git add .
git commit -m "[F001] feat: User registration - valid email/password"
```

### Step 8: Next Criterion

Repeat for next acceptance criterion in Feature-Test Matrix.

---

## Test Categories

### Unit Tests

**What:** Individual functions, components, utilities

**Location:** Next to source or in `/tests/unit/`

**Example:**
```typescript
// /lib/auth/validation.test.ts
describe('validatePassword', () => {
  it('should reject passwords under 8 characters', () => {
    expect(validatePassword('short')).toBe(false);
  });
});
```

### Integration Tests

**What:** Multiple components working together

**Location:** `/tests/integration/`

**Example:**
```typescript
// /tests/integration/auth-flow.test.ts
describe('Authentication Flow', () => {
  it('should allow login after registration', async () => {
    await registerUser({ email, password });
    const session = await loginUser({ email, password });
    expect(session).toBeDefined();
  });
});
```

### E2E Tests

**What:** Full user flows in browser

**Location:** `/tests/e2e/`

**Example:**
```typescript
// /tests/e2e/registration.spec.ts
test('user can register and access dashboard', async ({ page }) => {
  await page.goto('/register');
  await page.fill('[name="email"]', 'user@example.com');
  await page.fill('[name="password"]', 'SecurePass123!');
  await page.click('button[type="submit"]');
  await expect(page).toHaveURL('/dashboard');
});
```

---

## Test Scenarios by Feature Type

### Standard Feature

```
Happy path
├── Valid input → Success
└── Complete flow → Expected outcome

Validation
├── Missing required field → Error message
├── Invalid format → Error message
└── Out of range → Error message

Edge cases
├── Boundary values → Correct handling
├── Empty input → Correct handling
└── Maximum values → Correct handling

Errors
├── Network failure → Graceful handling
├── Database error → Graceful handling
└── Timeout → Graceful handling
```

### AI Feature

```
Standard scenarios (above)
+
AI-specific
├── AI provides reasoning → Visible to user
├── Low confidence → Appropriate handling
├── AI timeout → Fallback behavior
├── Rate limit → Queue or error
└── Human confirmation → Required before action

Boundary enforcement
├── AI cannot modify data directly → Blocked
├── AI cannot skip confirmation → Blocked
└── AI scope limited → Enforced
```

### Integration Feature

```
Standard scenarios (above)
+
External service
├── Service available → Success
├── Service timeout → Graceful handling
├── Service error → Graceful handling
├── Rate limited → Backoff/retry
├── Auth failure → Re-authenticate or error
└── Partial success → Appropriate handling
```

---

## Common Patterns

### Arrange-Act-Assert

```typescript
it('should do something', () => {
  // Arrange
  const input = setupTestData();
  
  // Act
  const result = functionUnderTest(input);
  
  // Assert
  expect(result).toBe(expectedValue);
});
```

### Async Testing

```typescript
it('should handle async operations', async () => {
  const result = await asyncFunction();
  expect(result).toBeDefined();
});
```

### Mocking

```typescript
it('should handle external dependency', () => {
  // Mock the external dependency
  jest.spyOn(externalService, 'method').mockResolvedValue(mockData);
  
  const result = functionThatUsesExternalService();
  
  expect(result).toBe(expected);
});
```

### Error Testing

```typescript
it('should throw on invalid input', () => {
  expect(() => functionUnderTest(invalidInput)).toThrow('Expected error');
});
```

---

## Coverage Requirements

| Risk Level | Line Coverage | Branch Coverage |
|------------|---------------|-----------------|
| Critical | 100% | 100% |
| High | 90% | 85% |
| Medium | 80% | 75% |
| Low | 70% | 65% |

### Checking Coverage

```bash
npm test -- --coverage
```

### Viewing Report

```bash
open coverage/lcov-report/index.html
```

---

## TDD Anti-Patterns

### ❌ Writing implementation first

Tests should drive implementation, not document it.

### ❌ Testing implementation details

Test behavior, not internal workings.

### ❌ Tests that always pass

If a test can't fail, it's not testing anything.

### ❌ Skipping the "verify fail" step

Always confirm test fails before implementing.

### ❌ Multiple assertions per test

One test = one behavior = one assertion (when possible).

### ❌ Brittle tests

Tests shouldn't break when implementation changes if behavior stays same.

---

## Quick Reference

```
1. Pick acceptance criterion from Feature-Test Matrix
2. Write test (should fail)
3. Run test → MUST FAIL
4. Write minimal implementation
5. Run test → MUST PASS
6. Refactor if needed
7. Commit
8. Repeat
```

---

*Template Version: 1.0 | SEAD Framework*
