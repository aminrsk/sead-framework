# Product Requirements Document (PRD)

**Project Name:** [Project Name]

**Version:** 1.0

**Last Updated:** [Date]

**Author:** [Your Name]

**Status:** Draft | In Review | Approved

---

## 1. Executive Summary

[One paragraph describing the project, its purpose, and expected outcome]

---

## 2. Problem Statement

### 2.1 Current Situation

[Describe the current state and pain points]

### 2.2 User Pain Points

| User Type | Pain Point | Impact |
|-----------|------------|--------|
| [User Type 1] | [Pain point] | [Business/user impact] |
| [User Type 2] | [Pain point] | [Business/user impact] |

### 2.3 Business Impact

[Describe the business cost of not solving this problem]

---

## 3. Success Metrics

| Metric | Current | Target | Measurement Method |
|--------|---------|--------|-------------------|
| [Metric 1] | [Value] | [Goal] | [How measured] |
| [Metric 2] | [Value] | [Goal] | [How measured] |

---

## 4. User Types & Permissions

| User Type | Description | Key Permissions |
|-----------|-------------|-----------------|
| [Admin] | [Description] | Full access, user management |
| [Manager] | [Description] | Read/write, reporting |
| [User] | [Description] | Read/limited write |

---

## 5. Feature Requirements

### 5.1 Phase 1 Features (MVP)

| ID | Feature | Description | Priority | Notes |
|----|---------|-------------|----------|-------|
| F001 | [Feature Name] | [Brief description] | P0 | [Any notes] |
| F002 | [Feature Name] | [Brief description] | P0 | |
| F003 | [Feature Name] | [Brief description] | P1 | |

### 5.2 Phase 2 Features (Post-MVP)

| ID | Feature | Description | Priority | Notes |
|----|---------|-------------|----------|-------|
| F010 | [Feature Name] | [Description] | P2 | |

### 5.3 Feature Details

#### F001: [Feature Name]

**Description:** [Detailed description]

**User Story:** As a [user type], I want to [action] so that [benefit].

**Acceptance Criteria:**
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

**Edge Cases:**
- [Edge case 1]
- [Edge case 2]

---

## 6. AI Features (if applicable)

### 6.1 AI Capabilities

| Feature | AI Role | Human Role | Boundary |
|---------|---------|------------|----------|
| [Feature] | Suggest/recommend | Approve/reject | AI cannot [action] |

### 6.2 AI Feature Details

#### [AI Feature Name]

**Purpose:** [What the AI does]

**Data Sources:**
- [Data source 1]
- [Data source 2]

**AI Outputs:**
- [Output type 1]
- [Output type 2]

**Human Confirmation Required:** Yes/No

**What AI Does NOT Do:**
- [Restriction 1]
- [Restriction 2]

**Fallback Behavior:**
- If AI service unavailable: [behavior]
- If AI returns low confidence: [behavior]

---

## 7. Integration Requirements

| System | Integration Type | Data Exchanged | Direction |
|--------|-----------------|----------------|-----------|
| [System 1] | API | [Data types] | Inbound/Outbound/Both |
| [System 2] | Webhook | [Data types] | Inbound |

### 7.1 Integration Details

#### [System Name] Integration

**Purpose:** [Why this integration]

**API/Method:** [REST/GraphQL/Webhook/etc.]

**Authentication:** [OAuth/API Key/etc.]

**Data Flow:**
1. [Step 1]
2. [Step 2]

**Error Handling:**
- [Error scenario]: [Response]

---

## 8. Non-Functional Requirements

### 8.1 Performance

| Metric | Requirement |
|--------|-------------|
| Page load time | < 3 seconds |
| API response time | < 500ms (p95) |
| Concurrent users | [Number] |

### 8.2 Security

| Requirement | Implementation |
|-------------|----------------|
| Authentication | [Method] |
| Authorization | [Method] |
| Data encryption | [At rest/In transit] |
| Audit logging | [What to log] |

### 8.3 Scalability

| Metric | Initial | Growth Target |
|--------|---------|---------------|
| Users | [Number] | [Number] |
| Data volume | [Size] | [Size] |

---

## 9. Compliance Requirements

| Standard | Applicable | Requirements |
|----------|------------|--------------|
| SOC2 | Yes/No | [Specific requirements] |
| GDPR | Yes/No | [Specific requirements] |
| ISO27001 | Yes/No | [Specific requirements] |
| HIPAA | Yes/No | [Specific requirements] |
| WCAG 2.1 | Yes/No | [Level: A/AA/AAA] |

---

## 10. Out of Scope

The following are explicitly NOT included in this project:

- [Item 1]
- [Item 2]
- [Item 3]

---

## 11. Open Questions

| # | Question | Owner | Due Date | Resolution |
|---|----------|-------|----------|------------|
| 1 | [Question] | [Name] | [Date] | [Pending/Resolved: answer] |

---

## 12. Timeline

| Phase | Start | End | Key Deliverables |
|-------|-------|-----|------------------|
| Specify | [Date] | [Date] | PRD, Feature-Test Matrix, ADR |
| Architect | [Date] | [Date] | Agent Harness, Quality Gates |
| Develop | [Date] | [Date] | Working application |
| Deliver | [Date] | [Date] | Production deployment |

---

## 13. Stakeholders

| Role | Name | Responsibility |
|------|------|----------------|
| Product Owner | [Name] | Requirements approval |
| Technical Lead | [Name] | Architecture decisions |
| Client Sponsor | [Name] | Budget, final approval |

---

## Approval

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Product Owner | | | |
| Client Sponsor | | | |

---

*Template Version: 1.0 | SEAD Framework*
