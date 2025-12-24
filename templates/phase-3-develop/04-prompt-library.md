# Prompt Library

Pre-tested prompts for common SEAD development tasks.

---

## Phase 1: Specification Prompts

### PRD Generation

```
Based on the following requirements, generate a complete PRD using 
the SEAD Framework template structure.

Include:
1. Executive summary (one paragraph)
2. Problem statement with user pain points
3. Success metrics (quantifiable, measurable)
4. User types and permissions
5. Feature requirements with acceptance criteria
6. AI feature specifications (if applicable)
7. Integration requirements
8. Non-functional requirements (performance, security, scalability)
9. Compliance requirements
10. Out of scope items
11. Open questions
12. Timeline

Here are the inputs:

[Paste transcript/requirements]

Additional context:
[Any clarifications]
```

### Feature-Test Matrix Generation

```
Based on this PRD, create a Feature-Test Matrix.

For each feature include:
1. Feature ID (matching PRD)
2. Feature name
3. Acceptance criteria (Given/When/Then format)
4. Test scenarios covering:
   - Happy path
   - Validation errors
   - Edge cases
   - Error states
5. Priority (P0 = must have, P1 = should have, P2 = nice to have)
6. Risk classification (Critical/High/Medium/Low)
7. Size estimate (S = 1 session, M = 2-3 sessions)

Flag any features that are L or Epic size - these need decomposition.

PRD:
[Paste PRD]
```

### ADR Generation

```
Create an Architecture Decision Record for [decision topic].

Context: [describe the situation requiring a decision]

Options to consider:
A) [Option A with brief description]
B) [Option B with brief description]
C) [Option C if applicable]

Decision drivers:
- [Driver 1, e.g., performance]
- [Driver 2, e.g., team expertise]
- [Driver 3, e.g., cost]

For each option, provide:
- Pros (bullet list)
- Cons (bullet list)
- Estimated effort (Low/Medium/High)
- Risk level (Low/Medium/High)

Then recommend one option with clear rationale.
Include consequences (positive, negative, neutral).
Note any compliance impacts.
```

### AGENTS.md Generation

```
Create an AGENTS.md file for AI coding assistants.

Project context:
[One paragraph describing the project]

Tech stack:
- [List technologies with versions]

Based on this context and the PRD/ADR below, create AGENTS.md including:
1. Project context (one paragraph)
2. Tech stack with versions
3. Project structure (folder layout)
4. Coding standards (naming, style, imports)
5. Testing requirements (TDD, coverage threshold)
6. Security rules (DO NOT section is critical)
7. AI feature boundaries (if applicable)
8. Error handling patterns
9. Git conventions
10. Current focus

Keep under 150 lines total.

PRD summary:
[Paste key sections]

ADR decisions:
[List key decisions]
```

---

## Phase 2: Architecture Prompts

### Feature Decomposition

```
I need to decompose this feature for AI development sessions.

Feature: [Name]
Description: [Description]
Current size: L or Epic

Test scenarios from Feature-Test Matrix:
[List scenarios]

Break this into subtasks where each subtask is:
- S (small): 1 session, single file, < 5 test scenarios
- M (medium): 2-3 sessions, multi-file, 5-10 test scenarios

For each subtask provide:
1. Name
2. Size (S or M)
3. Dependencies (which subtasks must complete first)
4. Test scenarios it covers
5. Files it will create/modify

Ensure the subtasks cover ALL original test scenarios.
```

### Risk Assessment

```
Assess the risk level of this feature:

Feature: [Name]
Description: [Description]

Evaluate these risk factors (score 0-2 each):
- Handles PII/sensitive data: [0/1/2]
- Touches authentication: [0/1/2]
- Touches authorization: [0/1/2]
- Involves payments/money: [0/1/2]
- Uses AI for decisions: [0/1]
- Integrates external service: [0/1]
- Can delete/modify data: [0/1]

Based on total score:
- 4+ = Critical
- 2-3 = High  
- 1 = Medium
- 0 = Low

Provide the risk level and list which review requirements apply.
```

---

## Phase 3: Development Prompts

### TDD Test Writing

```
I need to write a test for this feature:

Feature: [Feature Name]
Acceptance Criterion: 
Given [context]
When [action]
Then [expected result]

Test Scenario: [Specific scenario, e.g., "valid input"]

Project context is in AGENTS.md.
Testing framework: [Jest/Vitest/Playwright]

Write a test that:
1. Sets up the preconditions (Given)
2. Performs the action (When)
3. Asserts the expected outcome (Then)

The test should FAIL right now because implementation doesn't exist.
Use [describe/it or test] syntax.
Follow AAA pattern (Arrange, Act, Assert).
```

### Implementation from Failing Test

```
The following test is failing:

[Paste test code]

Error message:
[Paste error]

Write the MINIMAL implementation to make this test pass.
Do not add features beyond what the test requires.
Follow the patterns in AGENTS.md.
```

### Bug Fix

```
There's a bug in this feature:

Feature: [Feature Name]

Expected behavior:
[What should happen]

Actual behavior:
[What's happening]

Error message (if any):
[Paste error]

Related code:
[Paste relevant code]

1. First, write a test that reproduces this bug (should fail now)
2. Then provide the fix
3. Explain what was wrong
```

### Refactoring

```
Refactor this code to improve [quality aspect]:

[Paste code]

Quality aspect to improve: [readability/performance/testability/etc.]

Requirements:
1. Behavior must remain identical
2. All existing tests must still pass
3. Follow patterns from AGENTS.md
4. Explain each change made

Provide the refactored code and a summary of changes.
```

---

## Review Prompts

### General Code Review

```
Review this code for quality issues:

[Paste code]

Acceptance criteria it should meet:
[Paste criteria]

Check for:
1. Logic errors and bugs
2. Edge cases not handled
3. Error handling gaps
4. Performance issues
5. Code clarity and maintainability
6. Adherence to acceptance criteria

For each issue found:
- Severity: High/Medium/Low
- Location: File and line
- Problem: What's wrong
- Fix: Suggested solution
```

### Security Review

```
Review this code for security vulnerabilities:

[Paste code]

This is a [Critical/High] risk feature because: [reason]

Check for OWASP Top 10:
1. Injection (SQL, NoSQL, Command, etc.)
2. Broken Authentication
3. Sensitive Data Exposure
4. XML External Entities (if applicable)
5. Broken Access Control
6. Security Misconfiguration
7. Cross-Site Scripting (XSS)
8. Insecure Deserialization
9. Using Components with Known Vulnerabilities
10. Insufficient Logging & Monitoring

Also check:
- Input validation present and correct
- Output encoding where needed
- Authentication required where needed
- Authorization checks correct
- Sensitive data not logged
- Secrets not hardcoded

For each issue:
- Severity: Critical/High/Medium/Low
- Location: Specific line/function
- Vulnerability type
- Remediation steps
```

### AI Feature Review

```
Review this AI feature implementation:

[Paste code]

AI Feature requirements from PRD:
[Paste AI feature spec]

Check these AI boundaries:
1. Can AI modify data directly? (Should: NO)
2. Is human confirmation required before actions? (Should: YES)
3. Does AI provide reasoning/explanation? (Should: YES)
4. Is confidence level shown if applicable?
5. What happens if AI service is unavailable?
6. What happens if AI returns low confidence?
7. Are rate limits implemented?
8. Is input validated before sending to AI?
9. Is output validated/sanitized after receiving?

For each issue:
- Severity: High/Medium/Low
- What's wrong
- How to fix
```

### Integration Review

```
Review this integration code:

[Paste code]

Integration with: [External service name]

Check for:
1. All failure modes handled
   - Service unavailable
   - Timeout
   - Rate limit exceeded
   - Authentication failure
   - Partial success
   - Malformed response
2. Retry logic appropriate (exponential backoff?)
3. Circuit breaker if applicable
4. Request timeout configured
5. Response validation
6. Sensitive data handling (API keys, etc.)
7. Logging (without sensitive data)

For each issue:
- Severity
- Location
- Problem
- Suggested fix
```

---

## Debugging Prompts

### Error Analysis

```
I'm getting this error:

Error message:
[Paste full error with stack trace]

Context:
- Feature: [Feature name]
- What I was trying to do: [Action]
- When it happens: [Trigger condition]

Related code:
[Paste relevant code]

Please:
1. Explain what the error means
2. Identify the root cause
3. Provide the fix
4. Explain why the fix works
```

### Test Failure Analysis

```
This test is failing unexpectedly:

Test code:
[Paste test]

Error:
[Paste error]

Implementation being tested:
[Paste implementation]

Please:
1. Identify why the test is failing
2. Determine if it's a test issue or implementation issue
3. Provide the fix
```

---

## Documentation Prompts

### README Generation

```
Generate a README.md for this project:

Project name: [Name]
Description: [One paragraph]
Tech stack: [List]

Include:
1. Project title and description
2. Features list
3. Tech stack
4. Prerequisites
5. Installation steps
6. Environment variables needed
7. Running locally
8. Running tests
9. Deployment
10. Contributing
11. License
```

### API Documentation

```
Generate API documentation for these endpoints:

[Paste route handlers or API code]

For each endpoint include:
1. HTTP method and path
2. Description
3. Request headers
4. Request body (with example)
5. Response codes and bodies (with examples)
6. Error responses
7. Authentication requirements

Use OpenAPI/Swagger format or Markdown table format.
```

---

## Quick Reference

| Task | Prompt Category |
|------|-----------------|
| Starting a project | PRD Generation, AGENTS.md |
| Planning features | Feature-Test Matrix, Decomposition |
| Architectural decision | ADR Generation |
| Writing tests | TDD Test Writing |
| Implementing feature | Implementation from Test |
| Fixing bugs | Bug Fix, Error Analysis |
| Reviewing code | Review Prompts (by type) |
| Improving code | Refactoring |
| Writing docs | Documentation Prompts |

---

*Template Version: 1.0 | SEAD Framework*
