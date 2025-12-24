# The Five Governing Principles

These principles are the foundation of SEAD. Enforce them consistently.

## 1. Specification as Constraint

> Better specs = fewer AI errors. Always push for maximum detail in Phase 1 before any code is written.

### Why This Matters

AI coding assistants work from context. Vague requirements produce vague code. Precise specifications constrain the solution space, reducing the chance of AI going off-track.

### Enforcement

**If someone wants to start coding without a PRD and Feature-Test Matrix, STOP and redirect to Phase 1.**

### Practical Application

- Never start a coding session without clear acceptance criteria
- If requirements are ambiguous, clarify before coding
- Document edge cases explicitly—AI won't guess them correctly
- Include "what NOT to do" in specifications

### Red Flags

- "Just build something and we'll iterate"
- "The requirements are obvious"
- "We'll figure out the edge cases later"
- Starting with code before PRD exists

---

## 2. Test as Verification

> Tests are the only proof of understanding when you can't read every line of AI-generated code.

### Why This Matters

AI can generate hundreds of lines of code in seconds. You cannot meaningfully review all of it. Tests become your verification layer—if the tests pass and they cover the acceptance criteria, the implementation is correct *enough*.

### Enforcement

**Advocate TDD. Tests must be written BEFORE implementation. No exceptions for core features.**

### Practical Application

- Write tests based on Feature-Test Matrix acceptance criteria
- Verify tests fail before implementing
- One test per acceptance criterion minimum
- Cover happy path, validation, edge cases, errors
- For AI features: test boundaries, reasoning requirements, failure modes

### The TDD Cycle

```
1. Write test (from acceptance criteria)
2. Run test → Must FAIL
3. Implement minimum code
4. Run test → Must PASS
5. Refactor if needed
6. Commit
```

### Red Flags

- "We'll add tests later"
- "It's a simple change, no tests needed"
- Tests written after implementation
- Low coverage on AI-generated code

---

## 3. AI Reviews AI

> Never trust single-pass generation. A second AI pass with fresh context catches what the first missed.

### Why This Matters

AI coding assistants develop "blind spots" within a session. They become attached to their approach and miss obvious issues. A fresh context—new conversation, different prompt—catches errors the first pass missed.

### Enforcement

**After any significant code generation, trigger a review. For critical features, perform a review in a NEW AI conversation with fresh context.**

### The Multi-Layer Review Process

| Layer | Actor | What It Catches |
|-------|-------|-----------------|
| 1. Generation | AI Coder | Initial implementation |
| 2. AI Review | Different AI/Fresh Context | Logic errors, edge cases |
| 3. Automated Scans | CI/CD | Linting, type errors, vulnerabilities |
| 4. Human Decision | You | Architecture alignment, business logic |

### Critical Review Prompts

For security-sensitive code:
```
Review this code for security issues:
[paste code]

Check for:
1. OWASP Top 10 vulnerabilities
2. Authentication bypasses
3. Authorization failures
4. Input validation gaps
5. Sensitive data exposure

For each issue: severity, location, suggested fix.
```

For AI features:
```
Review this AI feature for boundary enforcement:
[paste code]

Check:
1. Can AI modify data directly? (Should: NO)
2. Is user confirmation required? (Should: YES)
3. Does AI provide reasoning? (Should: YES)
4. How does it handle missing data?
5. What if AI service times out?
```

### Red Flags

- "It works, ship it"
- Skipping review for "simple" changes
- Same AI session reviewing its own code
- No fresh context between generation and review

---

## 4. Human at Decisions, AI at Execution

> You own architecture and design decisions. AI owns implementation details.

### Why This Matters

AI is excellent at implementing solutions but poor at making strategic decisions. Architecture decisions compound—a wrong choice early creates exponentially more work later. These decisions require human judgment.

### Enforcement

**Identify "Architectural Decisions" explicitly. These require human sign-off before proceeding.**

### What Counts as an Architectural Decision

- Database schema changes or migrations
- New external service/API integration
- Authentication or authorization approach changes
- API design patterns or breaking changes
- Infrastructure choices (hosting, caching, queuing)
- Data model relationships
- Security-sensitive implementations
- Third-party vendor selection

### Practical Application

- Document every architectural decision in an ADR
- Never let AI make these decisions autonomously
- Review AI suggestions for hidden architectural implications
- Create explicit checkpoint gates before architectural changes

### The Decision Flow

```
AI suggests approach
       ↓
Is it architectural? ──NO──→ Proceed with implementation
       │
      YES
       ↓
Document in ADR
       ↓
Human reviews options
       ↓
Human approves approach
       ↓
AI implements approved approach
```

### Red Flags

- AI choosing database schema without review
- New packages/services added without ADR
- "The AI suggested it, so we went with it"
- Authentication changes without explicit approval

---

## 5. The 4-Attempt Rule

> If a logic problem isn't solved in 4 AI iterations, the architecture is wrong—not the prompt.

### Why This Matters

When AI struggles repeatedly with a problem, the instinct is to write better prompts. But usually the issue is that the problem is structured wrong, the architecture doesn't support the solution, or the scope is too large.

### Enforcement

**After 4 failed attempts, STOP coding. Reassess the architecture, break down the problem differently, or simplify scope.**

### What Counts as ONE Attempt

- One complete AI coding session on the same problem
- One red-green-refactor TDD cycle that fails to produce passing tests
- One focused conversation solving a specific blocked issue

**NOT separate attempts:** Multiple prompts within the same session refining the same solution.

### When the Rule Triggers

After 4 attempts, ask:
1. Is the feature sized correctly? (L/Epic needs decomposition)
2. Is there a missing prerequisite?
3. Is the approach fundamentally flawed?
4. Is the scope too ambitious?
5. Is there a simpler solution?

### Recovery Actions

| Diagnosis | Action |
|-----------|--------|
| Feature too large | Decompose into S/M features |
| Missing prerequisite | Build the prerequisite first |
| Wrong approach | Document in ADR, choose alternative |
| Scope creep | Reduce to MVP, defer additions |
| Fundamental complexity | Consider different architecture |

### Red Flags

- "Just one more prompt will fix it"
- 6+ attempts on the same problem
- Refining the same broken approach
- Blaming the AI instead of the structure

---

## Principle Interactions

The principles reinforce each other:

```
Better Specs (1) → Clearer Tests (2) → Fewer AI Errors
                                              ↓
AI Reviews AI (3) ← Catches remaining issues ←┘
       ↓
Human Decision (4) → Approves approach
       ↓
4-Attempt Rule (5) → Stops bad directions early
       ↓
Back to Better Specs (1) if needed
```

## Enforcement Checklist

Use this to verify principle adherence:

- [ ] PRD and Feature-Test Matrix exist before coding
- [ ] Tests written before implementation
- [ ] AI review performed on all significant code
- [ ] Fresh context used for critical feature reviews
- [ ] All architectural decisions documented in ADR
- [ ] Human approved all architectural decisions
- [ ] No feature in 4+ attempt loop
- [ ] L/Epic features decomposed before development

## When to Override

Principles can be bent (never broken) in specific circumstances:

**Emergency Bypass Protocol** allows faster process for:
- Production outages
- Active security exploits
- Data integrity issues
- Critical client-blocking bugs

Even then, tests and AI review cannot be skipped.
