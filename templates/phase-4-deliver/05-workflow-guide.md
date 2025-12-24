# Phase 4: DELIVER - Workflow Guide

This guide walks you through completing Phase 4 step-by-step.

---

## Overview

**Goal:** Safely deploy to production with staged rollout, complete documentation, and transition to support.

**Duration:** 1-6 weeks depending on complexity

**Inputs:** Phase 3 outputs (tested code on staging)

**Outputs:**
- Production deployment
- Complete documentation
- Client handoff
- Support transition

---

## Pre-Delivery Checklist

Before starting Phase 4, verify:

- [ ] All Phase 3 exit criteria met
- [ ] Code deployed and stable on staging
- [ ] All tests passing
- [ ] No open P0/P1 issues
- [ ] Client available for rollout coordination

---

## Step 1: Prepare for Rollout (Week -2)

### 1.1 Finalize Rollout Plan

Complete the Staged Rollout Plan template:
- Define stages and audiences
- Set success criteria per stage
- Document rollback triggers
- Assign responsibilities

### 1.2 Prepare Documentation

Use Delivery Documentation Checklist:
- User documentation
- Technical documentation  
- Operations documentation
- Handoff materials

### 1.3 Configure Monitoring

Ensure production monitoring is ready:
- Error tracking (Sentry, etc.)
- Performance monitoring
- Alerting configured
- Dashboards created

### 1.4 Verify Rollback Capability

Test that you can:
- Instantly revert deployment
- Disable feature flags
- Restore database if needed

---

## Step 2: Knowledge Transfer (Week -1)

### 2.1 Schedule Sessions

Book time with client for:
- Technical walkthrough (2-4 hours)
- Operations training (1-2 hours)
- Support handoff (1 hour)

### 2.2 Conduct Technical Walkthrough

**Prepare:**
- Architecture diagrams
- Key code areas identified
- Database schema
- Integration documentation

**Cover:**
- System architecture
- Codebase structure
- Data model
- Integrations
- Deployment process

### 2.3 Conduct Operations Training

**Prepare:**
- Runbook
- Monitoring access
- Log access

**Cover:**
- How to monitor system health
- How to read logs
- Common issues and solutions
- Escalation procedures

### 2.4 Complete Support Handoff

**Prepare:**
- Support procedures document
- SLA document
- Contact list

**Cover:**
- Support tiers and responsibilities
- Response time expectations
- Communication channels

---

## Step 3: Stage 1 - Internal Testing (1-2 days)

### 3.1 Deploy to Production

```bash
# Deploy via your pipeline
npm run deploy:production

# Or trigger via CI/CD
```

### 3.2 Verify Deployment

- [ ] Application accessible
- [ ] Core features working
- [ ] Monitoring receiving data
- [ ] No errors in logs

### 3.3 Internal Testing

Test all critical paths:
- [ ] Authentication flows
- [ ] Core business workflows
- [ ] Integrations
- [ ] Edge cases

### 3.4 Go/No-Go Decision

**GO if:**
- [ ] No critical bugs
- [ ] No security issues
- [ ] Core flows work
- [ ] Performance acceptable

**NO-GO if:**
- Critical bug found
- Security issue found
- Major functionality broken

---

## Step 4: Stage 2 - Pilot (1-2 weeks)

### 4.1 Enable for Pilot Users

Via feature flag or user selection:
```
- 5-10% of users
- OR selected user group
- OR specific department
```

### 4.2 Communicate to Pilot Users

Send pilot start notification:
- What's new
- How to access
- How to report issues
- Who to contact

### 4.3 Daily Monitoring

Check each day:
- Error rates
- Performance metrics
- User feedback
- Support tickets

### 4.4 Weekly Status Update

Send client weekly update:
- Metrics summary
- Issues found/resolved
- User feedback
- Recommendation

### 4.5 Go/No-Go Decision

**GO if:**
- [ ] Error rate < 1%
- [ ] No critical bugs
- [ ] Positive feedback
- [ ] Support load manageable

**NO-GO if:**
- Error rate > 2%
- Critical bugs unresolved
- Negative user feedback
- Support overwhelmed

---

## Step 5: Stage 3 - Expanded (1-2 weeks)

### 5.1 Enable for 25%

Expand feature flag to larger audience.

### 5.2 Monitor for Scale Issues

Watch for:
- Performance degradation
- Resource utilization
- New error patterns

### 5.3 Finalize Documentation

Complete all remaining documentation:
- User guides
- Admin guides
- API documentation

### 5.4 Train Support Team

Ensure support is ready for GA:
- All documentation accessible
- Common issues understood
- Escalation paths clear

### 5.5 Go/No-Go Decision

**GO if:**
- [ ] Error rate < 1%
- [ ] Infrastructure handles load
- [ ] Documentation complete
- [ ] Support trained

---

## Step 6: Stage 4 - General Availability

### 6.1 Prepare GA Communication

Draft announcements:
- Client communication
- User announcement
- Internal notification

### 6.2 Enable for 100%

Remove feature flags, enable for all users.

### 6.3 Send Announcements

- Notify client
- Announce to users
- Update team

### 6.4 Intensive Monitoring (48 hours)

First 48 hours:
- Check metrics every 2 hours
- Be ready for immediate rollback
- Support on high alert

### 6.5 Stabilization

First 2 weeks:
- Address issues quickly
- Collect feedback
- Fine-tune if needed

---

## Step 7: Project Close

### 7.1 Deliver Final Documentation

Complete handoff of all materials:
- Documentation package
- Access and credentials
- Runbooks and procedures

### 7.2 Conduct Final Review

Meet with client to:
- Confirm all deliverables received
- Answer remaining questions
- Define support transition

### 7.3 Get Sign-off

Obtain formal acceptance:
- Deliverables accepted
- Project complete
- Support terms agreed

### 7.4 Retrospective

Document within 1 week:
- What worked well
- What didn't work
- Process improvements
- Lessons learned

### 7.5 Close Project

- Mark project complete in tracking tool
- Archive project materials
- Final billing if applicable
- Update portfolio/case studies

---

## Timeline Summary

| Week | Phase | Key Activities |
|------|-------|----------------|
| -2 | Preparation | Rollout plan, documentation, monitoring |
| -1 | Knowledge Transfer | Walkthroughs, training, handoff prep |
| 0 | Internal + Pilot Start | Deploy, internal test, pilot begin |
| 1-2 | Pilot | Monitor, feedback, iterate |
| 3-4 | Expanded | 25% rollout, finalize docs, train support |
| 5 | GA | 100% rollout, intensive monitoring |
| 6 | Close | Documentation, sign-off, retrospective |

---

## Emergency Procedures

### Production Issue During Rollout

```
1. ASSESS: Determine severity
   - P0: Rollback immediately
   - P1: Fix within hours or rollback
   - P2: Fix in next release

2. COMMUNICATE: Notify client
   - Use Issue Notification template
   - Provide updates regularly

3. RESOLVE: Fix or rollback
   - Follow rollback procedure
   - Or deploy hotfix

4. REVIEW: Post-incident
   - Root cause analysis
   - Prevention measures
   - Update procedures
```

### Client Concerns During Rollout

```
1. LISTEN: Understand the concern fully

2. ASSESS: Determine if it's:
   - Bug: Follow issue process
   - Misunderstanding: Clarify/train
   - Scope creep: Document for future
   - Legitimate concern: Address

3. RESPOND: Provide clear plan

4. FOLLOW UP: Ensure resolution
```

---

## Success Metrics

| Metric | Target |
|--------|--------|
| Rollout completion | 100% within timeline |
| Error rate at GA | < 1% |
| User satisfaction | > 7/10 |
| Documentation complete | 100% |
| Client satisfaction | Positive |
| Issues at GA | 0 P0, < 2 P1 |

---

*Workflow Guide Version: 1.0 | SEAD Framework*
