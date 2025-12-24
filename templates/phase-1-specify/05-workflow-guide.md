# Phase 1: SPECIFY - Workflow Guide

This guide walks you through completing Phase 1 step-by-step.

---

## Overview

**Goal:** Create comprehensive specifications that constrain AI behavior during development.

**Duration:** 2-6 hours depending on complexity

**Outputs:**
1. Product Requirements Document (PRD)
2. Feature-Test Matrix
3. Architecture Decision Records (ADRs)
4. AGENTS.md

---

## Prerequisites

Before starting Phase 1, gather:

- [ ] Meeting recordings and/or transcripts
- [ ] Client-provided documents
- [ ] Access to existing systems (if applicable)
- [ ] Compliance requirements checklist
- [ ] Stakeholder contact information

---

## Step 1: Discovery (30-60 min)

### 1.1 Conduct Discovery

If not already done, gather answers to these questions:

**Users & Permissions:**
- Who are all user types?
- What can each user type do?
- Are there external users vs. internal users?

**Technical Context:**
- What existing systems must integrate?
- What data sources are involved?
- Are there performance requirements?

**Compliance:**
- What compliance standards apply? (SOC2, GDPR, ISO27001, HIPAA)
- Are there industry-specific regulations?
- What data sensitivity levels exist?

**Timeline:**
- What are the hard deadlines?
- Are there phases planned?
- What does success look like in 3 months?

### 1.2 Document Raw Inputs

Create a folder for all inputs:
```
/docs/discovery/
  - meeting-transcript-2024-01-15.txt
  - client-requirements.pdf
  - existing-system-docs.md
```

---

## Step 2: Generate PRD (45-60 min)

### 2.1 Prepare the Prompt

```
Based on the following requirements, generate a complete PRD using 
the SEAD Framework template structure.

Include:
1. Executive summary
2. Problem statement with user pain points
3. Success metrics (quantifiable)
4. User types and permissions
5. Feature requirements with acceptance criteria
6. AI feature specifications (if applicable)
7. Integration requirements
8. Non-functional requirements
9. Compliance requirements
10. Out of scope
11. Open questions
12. Timeline

Here are the inputs:

[Paste transcript and/or requirements]

Additional context:
[Any clarifications needed]
```

### 2.2 Generate and Refine

1. Run the prompt with your AI thinking partner
2. Review the output section by section
3. Add missing details
4. Clarify ambiguous items
5. Mark open questions

### 2.3 Save the PRD

Save as `docs/PRD.md` in your project.

---

## Step 3: Create Feature-Test Matrix (30-45 min)

### 3.1 Prepare the Prompt

```
Based on this PRD, create a Feature-Test Matrix with:

For each feature:
1. Feature ID and name (matching PRD)
2. Acceptance criteria (Given/When/Then format)
3. Test scenarios covering:
   - Happy path
   - Validation errors
   - Edge cases
   - Error states
   - For AI: boundary tests
   - For integrations: failure modes
4. Priority (P0/P1/P2)
5. Risk classification (Critical/High/Medium/Low)
6. Size estimate (S/M/L/Epic)

PRD:
[Paste your PRD]
```

### 3.2 Validate the Matrix

Check that:
- Every PRD feature has a matrix entry
- Critical features have comprehensive scenarios
- AI features have boundary tests
- Integration features have failure scenarios
- No L or Epic features (decompose if found)

### 3.3 Save the Matrix

Save as `docs/FEATURE-TEST-MATRIX.md` in your project.

---

## Step 4: Document Architecture Decisions (30-60 min)

### 4.1 Identify Decisions Needed

Common decisions to document:

**Tech Stack:**
- Frontend framework
- Backend approach
- Database selection
- Authentication provider
- Hosting platform

**Architecture:**
- API design (REST vs GraphQL)
- State management
- Caching strategy
- File storage

**Integrations:**
- External API approach
- Data sync strategy

**AI Features (if applicable):**
- AI provider
- Feature boundaries
- Error handling

### 4.2 Generate ADRs

For each decision:

```
Create an ADR for [decision topic]:

Context: [describe the situation]

Options to consider:
A) [Option A]
B) [Option B]
C) [Option C if applicable]

Decision drivers:
- [Driver 1]
- [Driver 2]

Include pros/cons, effort estimate, risk level, and recommendation.
```

### 4.3 Save ADRs

Save in `docs/adr/`:
```
docs/adr/
  - ADR-001-frontend-framework.md
  - ADR-002-database-selection.md
  - ADR-003-authentication.md
```

---

## Step 5: Create AGENTS.md (15-30 min)

### 5.1 Prepare the Prompt

```
Create an AGENTS.md file for AI coding assistants based on:
- PRD: [paste key sections]
- ADR decisions: [list key decisions]
- Tech stack: [list]

Include:
1. Project context (one paragraph)
2. Tech stack with versions
3. Project structure
4. Coding standards
5. Testing requirements
6. Security rules (DO NOT section is critical)
7. AI feature boundaries
8. Git conventions
9. Current focus

Keep under 150 lines.
```

### 5.2 Review Critical Sections

Pay special attention to:
- **Security Rules:** List everything AI should NOT do
- **AI Boundaries:** What requires human confirmation
- **Testing Requirements:** Enforce TDD

### 5.3 Save AGENTS.md

Save as `AGENTS.md` in project root (AI tools read from root).

---

## Step 6: Client Review (Variable)

### 6.1 Prepare for Review

Create a summary document or presentation:
- Key features and priorities
- Timeline overview
- Open questions
- Decisions that need input

### 6.2 Conduct Review

- Walk through PRD with stakeholders
- Confirm feature priorities
- Resolve open questions
- Get explicit sign-off

### 6.3 Update Documents

After review:
- Update PRD with feedback
- Resolve open questions
- Add any new requirements
- Mark as "Approved"

---

## Phase 1 Completion

### Final Checklist

Before moving to Phase 2, verify:

- [ ] PRD complete and approved
- [ ] Feature-Test Matrix covers all PRD features
- [ ] No L or Epic features (decomposed to S/M)
- [ ] ADRs document all major technical decisions
- [ ] AGENTS.md is in project root
- [ ] Compliance requirements identified
- [ ] Open questions resolved
- [ ] Documents saved in project and shared with team

### Output Files

```
/project-root/
  AGENTS.md
  /docs/
    PRD.md
    FEATURE-TEST-MATRIX.md
    /adr/
      ADR-001-*.md
      ADR-002-*.md
      ...
```

### Time Tracking

| Step | Simple | Standard | Enterprise |
|------|--------|----------|------------|
| Discovery | 30 min | 45 min | 90 min |
| PRD | 45 min | 60 min | 120 min |
| Feature-Test Matrix | 30 min | 45 min | 90 min |
| ADRs | 30 min | 45 min | 120 min |
| AGENTS.md | 15 min | 20 min | 30 min |
| Client Review | 30 min | 60 min | 120 min |
| **Total** | **~3 hrs** | **~5 hrs** | **~10 hrs** |

---

## Next Steps

With Phase 1 complete, proceed to **Phase 2: ARCHITECT** to:
- Size all features
- Map human checkpoints
- Configure quality gates
- Create issues for development

---

*Workflow Guide Version: 1.0 | SEAD Framework*
