# Staged Rollout Plan

**Project:** [Project Name]

**Version:** 1.0

**Last Updated:** [Date]

---

## Overview

Never deploy 0→100. This plan defines how to progressively roll out to users while monitoring for issues.

---

## Rollout Stages

```
┌──────────────────────────────────────────────────────────────┐
│                    ROLLOUT STAGES                             │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  STAGE 1: INTERNAL                                            │
│  ├── Audience: Team only                                      │
│  ├── Duration: 1-2 days                                       │
│  └── Goal: Catch obvious issues                               │
│                                                               │
│  STAGE 2: PILOT                                               │
│  ├── Audience: 5-10% of users (selected)                      │
│  ├── Duration: 1-2 weeks                                      │
│  └── Goal: Validate with real usage                           │
│                                                               │
│  STAGE 3: EXPANDED                                            │
│  ├── Audience: 25% of users                                   │
│  ├── Duration: 1-2 weeks                                      │
│  └── Goal: Scale validation                                   │
│                                                               │
│  STAGE 4: GENERAL AVAILABILITY                                │
│  ├── Audience: 100% of users                                  │
│  ├── Duration: Ongoing                                        │
│  └── Goal: Full production                                    │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## Stage 1: Internal Testing

### Audience
- You (developer)
- Key client stakeholder (if applicable)
- Total: 1-3 people

### Duration
1-2 days

### Success Criteria
- [ ] No critical bugs
- [ ] No security issues
- [ ] Core flows work correctly
- [ ] Performance acceptable
- [ ] UI/UX as expected

### Activities
1. Deploy to production environment
2. Test all critical paths manually
3. Verify monitoring/alerting works
4. Confirm rollback capability
5. Document any issues found
6. Fix blockers before proceeding

### Go/No-Go Checklist
- [ ] All critical paths tested
- [ ] No P0 bugs open
- [ ] Monitoring confirmed working
- [ ] Rollback tested
- [ ] Client stakeholder approved (if applicable)

---

## Stage 2: Pilot

### Audience
- Selected pilot users
- 5-10% of total user base
- OR specific user group (e.g., power users, one department)

### Selection Criteria
- Users who can provide feedback
- Not critical operations (in case of issues)
- Representative of broader user base

### Duration
1-2 weeks

### Success Criteria
- [ ] Error rate < 1%
- [ ] No critical bugs reported
- [ ] Positive user feedback (NPS > 7)
- [ ] Performance within SLA
- [ ] Support load manageable

### Activities
1. Enable feature flags for pilot users
2. Monitor error rates closely
3. Collect user feedback
4. Daily check on metrics
5. Weekly sync with pilot users
6. Fix issues as they arise

### Metrics to Track
| Metric | Target | Alert Threshold |
|--------|--------|-----------------|
| Error rate | < 1% | > 2% |
| Response time p95 | < 2s | > 3s |
| User complaints | < 2 | > 5 |
| Support tickets | < 5 | > 10 |

### Go/No-Go Checklist
- [ ] Error rate < 1% sustained
- [ ] No P0/P1 bugs open
- [ ] User feedback positive
- [ ] Support load acceptable
- [ ] Metrics stable for 3+ days

---

## Stage 3: Expanded Rollout

### Audience
- 25% of total users
- OR additional departments/regions

### Duration
1-2 weeks

### Success Criteria
- [ ] Error rate < 1%
- [ ] No new critical bugs
- [ ] Metrics stable at scale
- [ ] Support team ready for GA
- [ ] Documentation complete

### Activities
1. Expand feature flag to 25%
2. Monitor for scale-related issues
3. Finalize documentation
4. Train support team
5. Prepare GA communication

### Metrics to Track
| Metric | Target | Alert Threshold |
|--------|--------|-----------------|
| Error rate | < 1% | > 1.5% |
| Response time p95 | < 2s | > 2.5s |
| CPU usage | < 60% | > 80% |
| Memory usage | < 70% | > 85% |

### Go/No-Go Checklist
- [ ] Error rate < 1% sustained
- [ ] No new P0/P1 bugs
- [ ] Infrastructure handles load
- [ ] Support team trained
- [ ] Documentation complete
- [ ] GA communication ready

---

## Stage 4: General Availability (GA)

### Audience
- 100% of users

### Duration
Ongoing

### Success Criteria
- [ ] All KPIs met
- [ ] Support process working
- [ ] Monitoring active
- [ ] Team transitioned to maintenance mode

### Activities
1. Remove feature flags / enable for all
2. Send GA communication
3. Monitor intensively for 48 hours
4. Transition to normal monitoring
5. Close project formally

### Post-GA Monitoring (First 48 hours)
- Check metrics every 2 hours
- Be ready for immediate rollback
- Support team on high alert

---

## Rollback Plan

### Rollback Triggers

**Automatic Rollback:**
- Error rate > 5%
- Critical security issue detected
- Data integrity issue detected
- Performance degradation > 50%

**Manual Rollback Decision:**
- Error rate > 2% for 1+ hour
- Multiple user complaints
- Critical bug without quick fix
- Performance degradation > 20%

### Rollback Procedure

```
1. DECIDE: Confirm rollback needed
   - Check metrics
   - Assess user impact
   - Consult stakeholder if time permits

2. EXECUTE: Trigger rollback
   - Via hosting platform (Vercel: instant revert)
   - OR via feature flag disable
   - OR via deployment pipeline

3. VERIFY: Confirm rollback complete
   - Check application is previous version
   - Check metrics stabilizing
   - Check user-facing functionality

4. COMMUNICATE: Notify stakeholders
   - Inform team
   - Inform client
   - Prepare user communication if needed

5. INVESTIGATE: Root cause analysis
   - What went wrong
   - How to prevent recurrence
   - When to retry rollout
```

### Rollback Responsibility

| Time | Person Responsible |
|------|-------------------|
| Business hours | [Primary contact] |
| After hours | [On-call contact] |
| Escalation | [Manager/Lead] |

---

## Communication Plan

### Internal Communication

| Stage | When | Channel | Message |
|-------|------|---------|---------|
| Pre-pilot | 1 day before | [Slack/Email] | "Pilot starting tomorrow" |
| Pilot start | Day 1 | [Slack/Email] | "Pilot live, monitoring" |
| Pilot end | End of pilot | [Slack/Email] | "Pilot results: [summary]" |
| GA | Go-live | [Slack/Email] | "GA complete, [status]" |

### Client Communication

| Stage | When | Method | Template |
|-------|------|--------|----------|
| Pre-pilot | 3 days before | Email | Pilot announcement |
| Pilot feedback | Weekly | Call/Email | Status update |
| Pre-GA | 1 week before | Email | GA announcement |
| GA | Go-live | Email | Launch announcement |

### User Communication

| Stage | When | Method | Message |
|-------|------|--------|---------|
| Pilot | If selected | In-app/Email | Feature preview invitation |
| GA | Go-live | In-app/Email | New feature announcement |
| Issues | As needed | In-app | Status/incident updates |

---

## Timeline Template

| Date | Stage | Activity | Owner |
|------|-------|----------|-------|
| [Date] | Internal | Deploy to production | [Name] |
| [Date] | Internal | Internal testing | [Name] |
| [Date] | Internal | Go/No-Go decision | [Name] |
| [Date] | Pilot | Enable for pilot users | [Name] |
| [Date] | Pilot | Daily monitoring | [Name] |
| [Date] | Pilot | Collect feedback | [Name] |
| [Date] | Pilot | Go/No-Go decision | [Name] |
| [Date] | Expanded | Enable for 25% | [Name] |
| [Date] | Expanded | Monitor and support | [Name] |
| [Date] | Expanded | Go/No-Go decision | [Name] |
| [Date] | GA | Enable for 100% | [Name] |
| [Date] | GA | Intensive monitoring | [Name] |
| [Date] | GA | Transition to maintenance | [Name] |

---

## Risk Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Critical bug in production | Medium | High | Staged rollout, instant rollback |
| Performance degradation | Medium | Medium | Load testing, monitoring |
| User resistance | Low | Medium | Pilot feedback, communication |
| Data issues | Low | High | Backup before deploy, validation |

---

*Template Version: 1.0 | SEAD Framework*
