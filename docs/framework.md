# SEAD Framework Complete Reference

**Solo Enterprise AI Development** — The engineered bridge from 70% AI generation to 100% enterprise-grade production.

## Core Philosophy

AI agents get you to 70%. Enterprise demands 100%. This framework uses two levers:

1. **Requirements & ideation to constrain AI** — Better specs = fewer AI errors
2. **Structured validation to catch what you can't manually review** — Tests + automated checks + AI-reviews-AI

---

## The Five Governing Principles

### 1. Specification as Constraint

Better specs = fewer AI errors. Always push for maximum detail in Phase 1 before any code is written.

**Enforcement:** If someone wants to start coding without a PRD and Feature-Test Matrix, STOP and redirect to Phase 1.

### 2. Test as Verification

Tests are the only proof of understanding when you can't read every line of AI-generated code.

**Enforcement:** Advocate TDD. Tests must be written BEFORE implementation. No exceptions for core features.

### 3. AI Reviews AI

Never trust single-pass generation. A second AI pass with fresh context catches what the first missed.

**Enforcement:** After any significant code generation, perform a review. For critical features, use a NEW AI conversation with fresh context.

### 4. Human at Decisions, AI at Execution

You own architecture and design decisions. AI owns implementation details.

**Enforcement:** Identify "Architectural Decisions" explicitly. These require human sign-off.

**Architectural Decisions include:**
- Database schema changes or migrations
- New external service/API integration
- Authentication or authorization approach changes
- API design patterns or breaking changes
- Infrastructure choices (hosting, caching, queuing)
- Data model relationships
- Security-sensitive implementations
- Third-party vendor selection

### 5. The 4-Attempt Rule

If a logic problem isn't solved in 4 AI iterations, the architecture is wrong—not the prompt.

**Enforcement:** After 4 failed attempts, STOP coding. Reassess the architecture, break down the problem differently, or simplify scope.

**What counts as ONE attempt:**
- One complete AI coding session on the same problem
- One red-green-refactor TDD cycle that fails to produce passing tests
- One focused conversation solving a specific blocked issue

---

## Emergency Bypass Protocol

For production incidents, security vulnerabilities, or critical hotfixes:

**Trigger Conditions:**
- Production is down or critically degraded
- Security vulnerability actively being exploited
- Data integrity issue affecting users
- Client-blocking bug in production

**Bypass Process:**
1. Acknowledge bypass — Document: "EMERGENCY BYPASS - [reason]"
2. Minimum required checks:
   - Automated tests must still pass
   - AI review (cannot skip)
   - Human spot-check (5-10 min max)
3. Deploy with rollback ready
4. Post-incident: Within 48 hours, create proper tests/docs
5. Log for retrospective

**Can skip:** PRD updates, Feature-Test Matrix updates, full ADR, staged rollout

**Cannot skip:** Tests, AI review, human spot-check, rollback plan

---

## Phase 1: SPECIFY (Constraint-First)

Front-load intelligence into specifications to constrain AI behavior.

### Deliverables

| Template | Purpose | When to Use |
|----------|---------|-------------|
| PRD Template | Complete product requirements | Start of every project |
| Feature-Test Matrix | Features → criteria → test cases | After PRD approval |
| ADR Template | Architecture decisions with rationale | Before any coding |
| AGENTS.md Template | AI agent configuration and constraints | Before first dev session |
| Workflow Guide | Step-by-step process | Reference during phase |
| Checklist | Exit criteria verification | Before Phase 2 |

### Exit Criteria

- [ ] PRD reviewed and approved
- [ ] Feature-Test Matrix complete with acceptance criteria
- [ ] ADRs documented for all major technical decisions
- [ ] AGENTS.md configured
- [ ] Compliance requirements identified (if applicable)

### Time Estimates

| Complexity | Description | Time |
|------------|-------------|------|
| Simple | Single feature, no compliance, clear requirements | 2-3 hours |
| Standard | Multi-feature, basic compliance, some ambiguity | 4-6 hours |
| Enterprise | Complex integrations, full compliance, AI features | 1-2 days |

---

## Phase 2: ARCHITECT (Structure-First)

Design the development structure before writing any code.

### Deliverables

| Template | Purpose | When to Use |
|----------|---------|-------------|
| Agent Harness Design | AI session structure and boundaries | Before coding |
| Human Checkpoint Map | Decision points requiring human approval | Before coding |
| Context Management Plan | Prevent context rot across sessions | Before coding |
| Quality Gate Definitions | 4-level automated check configuration | Before coding |
| Workflow Guide | Step-by-step process | Reference during phase |
| Checklist | Exit criteria verification | Before Phase 3 |

### Feature Sizing

| Size | Description | Sessions | Action |
|------|-------------|----------|--------|
| **S** | Single-file changes, isolated logic | 1 | Direct implementation |
| **M** | Multi-file, clear boundaries | 2-3 | Plan then implement |
| **L** | Cross-cutting concerns, integrations | 4-6 | **Must break down** |
| **Epic** | Requires architectural changes | 7+ | **Decompose into S/M** |

### Risk Classification

| Category | Examples | Required Review |
|----------|----------|-----------------|
| **Critical** | Auth, payments, data deletion | Full human review + security scan |
| **High** | AI features, external integrations | AI review + human spot-check |
| **Medium** | Core business logic | AI review + automated tests |
| **Low** | UI tweaks, copy changes | Automated tests only |

### Exit Criteria

- [ ] All features sized (no L or Epic without decomposition)
- [ ] Human checkpoints mapped
- [ ] Quality gates configured
- [ ] Issues created for all features with proper labels

### Time Estimates

| Complexity | Description | Time |
|------------|-------------|------|
| Simple | < 10 features, clear architecture | 1-2 hours |
| Standard | 10-25 features, some integrations | 2-4 hours |
| Enterprise | 25+ features, complex integrations | 4-8 hours |

---

## Phase 3: DEVELOP (Discipline-First)

Execute with TDD, session discipline, and continuous validation.

### Deliverables

| Template | Purpose | When to Use |
|----------|---------|-------------|
| TDD Workflow Guide | Test-first development process | Every feature |
| Session Discipline Protocol | 25-60 min focused sessions | Every dev session |
| Multi-Layer Review Process | AI → AI → automated → human | After each feature |
| Prompt Library | Pre-tested prompts | During development |
| Workflow Guide | Step-by-step process | Reference during phase |
| Checklist | Exit criteria verification | Before Phase 4 |

### Session Discipline Protocol

```
SESSION START:
1. Define ONE clear goal (from Feature-Test Matrix)
2. Set timer: 25-60 minutes max
3. Load relevant context only

SESSION END:
1. Verify tests pass
2. Update issue status
3. If goal not met in 4 attempts → STOP, reassess architecture
```

### Multi-Layer Review Process

| Layer | Actor | What It Catches |
|-------|-------|-----------------|
| 1. Generation | AI Code Generator | Initial implementation with TDD |
| 2. AI Review | Fresh AI Context | Logic errors, edge cases, code quality |
| 3. Automated Scans | CI/CD | Linting, type errors, vulnerabilities |
| 4. Human Decision | You | Architecture alignment (Critical/High only) |

### Quality Gates (4 Levels)

| Gate | Trigger | Checks |
|------|---------|--------|
| Pre-commit | `git commit` | Lint, format, type-check |
| PR | Pull request | All tests, coverage threshold, AI review |
| Staging | Merge to staging | Integration tests, E2E, performance |
| Production | Deploy | Smoke tests, monitoring configured |

### Exit Criteria

- [ ] All features implemented with passing tests
- [ ] Coverage meets threshold (recommend 80%+)
- [ ] All quality gates passing
- [ ] All issues in "Done" or "In Review" status
- [ ] No open blockers

---

## Phase 4: DELIVER (Reliability-First)

Stage the rollout, never go 0→100.

### Deliverables

| Template | Purpose | When to Use |
|----------|---------|-------------|
| Staged Rollout Plan | Progressive user exposure | Before any production release |
| Client Communication Templates | Updates, notifications | Throughout rollout |
| Delivery Documentation Checklist | User guides, API docs, runbooks | Before GA |
| Handoff and Support Transition | Maintenance procedures | Before GA |
| Workflow Guide | Step-by-step process | Reference during phase |
| Checklist | Exit criteria verification | Before project close |

### Staged Rollout

| Stage | Audience | Duration | Success Criteria |
|-------|----------|----------|------------------|
| **Internal** | Team only | 1-2 days | No critical bugs |
| **Pilot** | 5-10% users | 1-2 weeks | Error rate < 1%, positive feedback |
| **Expanded** | 25% users | 1-2 weeks | Metrics stable, support manageable |
| **GA** | 100% users | Ongoing | All KPIs met |

### Rollback Triggers

- Error rate > 5%
- Critical security issue
- Data integrity concern
- Performance degradation > 20%

### Exit Criteria

- [ ] All rollout stages completed
- [ ] Documentation delivered
- [ ] Client trained/handed off
- [ ] Support plan active
- [ ] Monitoring configured

### Time Estimates

| Complexity | Description | Time |
|------------|-------------|------|
| Simple | Single client, < 50 users, no compliance | 1-2 weeks |
| Standard | Single client, 50-500 users, basic compliance | 2-3 weeks |
| Enterprise | Multi-stakeholder, 500+ users, full compliance | 3-6 weeks |

---

## Project Close & Maintenance Transition

### Project Close Checklist

- [ ] All deliverables accepted
- [ ] Documentation complete and handed off
- [ ] Support/escalation paths documented
- [ ] Monitoring and alerting active
- [ ] Retrospective completed
- [ ] Project marked as complete
- [ ] Billing finalized

### Retrospective Questions

| Question | Purpose |
|----------|---------|
| What worked well? | Patterns to repeat |
| What didn't work? | Patterns to avoid |
| Where did we bypass SEAD? | Assess if justified |
| What was underestimated? | Calibrate future estimates |
| Framework improvements? | Update templates |

### Maintenance Mode

- Support tier defined (response times, availability)
- Change requests follow SEAD from Phase 1
- Bug fixes use Phase 3 (or Emergency Bypass if critical)
- Automated monitoring for incident detection
- Periodic reviews (monthly/quarterly)

---

## Compliance Quick Reference

| Standard | Key Requirements | Phase Impact |
|----------|------------------|--------------|
| **SOC2** | Access controls, audit logging, encryption | ADR must address, Quality gates verify |
| **GDPR** | Data minimization, consent, right to deletion | PRD must specify, compliance tests |
| **ISO27001** | Risk assessment, incident response | Quality gates, monitoring |
| **HIPAA** | PHI protection, access controls, audit trails | PRD must specify, Critical risk |
| **WCAG 2.1** | Accessibility standards | Feature-Test Matrix criteria |

---

## Red Flags (Stop and Reassess)

🚩 Jumping to code without PRD/Feature-Test Matrix

🚩 Feature sized as L or Epic without decomposition

🚩 Same problem failing 4+ times (4-Attempt Rule)

🚩 Session running over 60 minutes without progress

🚩 Skipping AI review for "simple" changes

🚩 Deploying without staged rollout

🚩 Critical/High risk features without human review

🚩 No issue tracking for work being done

🚩 Architectural decision made without ADR

---

## Quick Reference: Phase Triggers

| If you're... | You're in... | Key Action |
|--------------|--------------|------------|
| Gathering requirements | Phase 1: SPECIFY | Complete PRD + Feature-Test Matrix |
| Planning architecture | Phase 2: ARCHITECT | Create Harness + Checkpoint Map + Issues |
| Writing code | Phase 3: DEVELOP | Follow TDD + Session Discipline |
| Deploying | Phase 4: DELIVER | Execute Staged Rollout |
| Post-GA | Maintenance | Emergency Bypass or standard SEAD |

---

*24 Templates across 4 Phases | Designed for solo practitioners delivering enterprise-grade solutions*
