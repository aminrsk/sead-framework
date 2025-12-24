# Quality Gate Definitions

**Project:** [Project Name]

**Version:** 1.0

**Last Updated:** [Date]

---

## Overview

Quality gates are automated checkpoints that verify code quality before it progresses through the development pipeline. This document defines four levels of gates.

---

## Gate Levels

| Level | Trigger | Purpose | Bypass Policy |
|-------|---------|---------|---------------|
| 1 | Pre-commit | Catch issues before commit | Never |
| 2 | Pull Request | Validate before merge | Never |
| 3 | Staging | Verify integration | Emergency only |
| 4 | Production | Confirm deploy readiness | Never |

---

## Level 1: Pre-commit Gate

**Trigger:** `git commit`

**Tools:** Husky, lint-staged, pre-commit

### Checks

| Check | Tool | Failure Action |
|-------|------|----------------|
| Linting | ESLint | Block commit |
| Formatting | Prettier | Auto-fix or block |
| Type check | TypeScript | Block commit |
| Secrets scan | gitleaks | Block commit |

### Configuration

**package.json:**
```json
{
  "scripts": {
    "lint": "eslint . --ext .ts,.tsx",
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "typecheck": "tsc --noEmit"
  },
  "lint-staged": {
    "*.{ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  }
}
```

**Husky pre-commit hook:**
```bash
#!/bin/sh
npx lint-staged
npm run typecheck
```

### Bypass

**Policy:** Never bypass Level 1.

If pre-commit blocks you:
1. Fix the issues
2. If legitimate exception, update ESLint config
3. Document exception reason

---

## Level 2: Pull Request Gate

**Trigger:** Pull request opened/updated

**Tools:** GitHub Actions, GitLab CI, etc.

### Checks

| Check | Tool | Failure Action |
|-------|------|----------------|
| All Level 1 checks | CI runner | Block merge |
| Unit tests | Jest/Vitest | Block merge |
| Integration tests | Jest/Playwright | Block merge |
| Coverage threshold | Jest | Block merge |
| AI code review | PR Review tool | Add comments |
| Security scan | Snyk/npm audit | Block if critical |
| Build | Next.js/Vite | Block merge |

### Configuration

**.github/workflows/pr.yml:**
```yaml
name: PR Checks

on:
  pull_request:
    branches: [main, develop]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Lint
        run: npm run lint
      
      - name: Type check
        run: npm run typecheck
      
      - name: Test with coverage
        run: npm run test:coverage
      
      - name: Check coverage threshold
        run: |
          COVERAGE=$(cat coverage/coverage-summary.json | jq '.total.lines.pct')
          if (( $(echo "$COVERAGE < 80" | bc -l) )); then
            echo "Coverage $COVERAGE% is below 80% threshold"
            exit 1
          fi
      
      - name: Build
        run: npm run build
      
      - name: Security audit
        run: npm audit --audit-level=high
```

### Coverage Requirements

| Feature Risk | Minimum Coverage |
|--------------|------------------|
| Critical | 100% |
| High | 90% |
| Medium | 80% |
| Low | 70% |

### Bypass

**Policy:** Never bypass Level 2.

If PR checks fail:
1. Fix the issues
2. If flaky test, mark as known issue and fix
3. If genuine exception, get written approval

---

## Level 3: Staging Gate

**Trigger:** Merge to staging branch / deploy to staging

**Tools:** CI/CD, Playwright, k6

### Checks

| Check | Tool | Failure Action |
|-------|------|----------------|
| E2E tests | Playwright | Block production |
| Integration tests | Jest | Block production |
| Performance tests | k6/Lighthouse | Warning if degraded |
| Visual regression | Percy/Chromatic | Review required |
| API contract tests | Pact/Hurl | Block production |
| Database migrations | Prisma | Verify success |

### Configuration

**.github/workflows/staging.yml:**
```yaml
name: Staging Deploy

on:
  push:
    branches: [staging]

jobs:
  deploy-staging:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Deploy to staging
        run: npm run deploy:staging
      
      - name: Wait for deployment
        run: sleep 60
      
      - name: Run E2E tests
        run: npm run test:e2e
      
      - name: Run performance tests
        run: npm run test:perf
      
      - name: Notify on failure
        if: failure()
        run: echo "Staging tests failed"
```

### Bypass

**Policy:** Emergency bypass with approval.

For emergency bypass:
1. Document reason
2. Get approval from [Role]
3. Deploy with enhanced monitoring
4. Create follow-up issue to add missing tests

---

## Level 4: Production Gate

**Trigger:** Deploy to production

**Tools:** CI/CD, monitoring, feature flags

### Checks

| Check | Tool | Failure Action |
|-------|------|----------------|
| Smoke tests | Playwright | Rollback |
| Health checks | Custom | Alert |
| Monitoring configured | Sentry/Datadog | Block deploy |
| Rollback ready | Vercel/K8s | Block deploy |
| Feature flags set | LaunchDarkly/etc | Verify |

### Configuration

```yaml
name: Production Deploy

on:
  workflow_dispatch:
    inputs:
      confirm:
        description: 'Type "deploy" to confirm'
        required: true

jobs:
  deploy-production:
    if: github.event.inputs.confirm == 'deploy'
    runs-on: ubuntu-latest
    steps:
      - name: Verify staging passed
        run: |
          # Check staging gate passed
          
      - name: Deploy to production
        run: npm run deploy:production
      
      - name: Run smoke tests
        run: npm run test:smoke
      
      - name: Verify monitoring
        run: |
          # Check Sentry is receiving events
          # Check key metrics are tracking
      
      - name: Notify success
        run: echo "Production deploy complete"
      
      - name: Rollback on failure
        if: failure()
        run: npm run rollback
```

### Rollback Triggers

Automatic rollback if:
- Smoke tests fail
- Error rate > 5%
- Health check fails
- Critical alert fires

### Bypass

**Policy:** Never bypass Level 4.

If production gate fails:
1. Investigate failure
2. Fix issue
3. Re-run deployment
4. Never deploy with failing checks

---

## Gate Summary

```
┌─────────────────────────────────────────────────────────────┐
│                    DEVELOPMENT FLOW                          │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  Code Changes                                                │
│       │                                                      │
│       ▼                                                      │
│  ┌─────────────┐                                             │
│  │   GATE 1    │  Pre-commit: lint, format, typecheck        │
│  │  (Local)    │  ✗ = Fix before commit                      │
│  └──────┬──────┘                                             │
│         │                                                    │
│         ▼                                                    │
│  ┌─────────────┐                                             │
│  │   GATE 2    │  PR: tests, coverage, build, security       │
│  │   (CI/CD)   │  ✗ = Fix before merge                       │
│  └──────┬──────┘                                             │
│         │                                                    │
│         ▼                                                    │
│  ┌─────────────┐                                             │
│  │   GATE 3    │  Staging: E2E, integration, performance     │
│  │  (Staging)  │  ✗ = Fix before production                  │
│  └──────┬──────┘                                             │
│         │                                                    │
│         ▼                                                    │
│  ┌─────────────┐                                             │
│  │   GATE 4    │  Production: smoke tests, monitoring        │
│  │(Production) │  ✗ = Rollback immediately                   │
│  └──────┬──────┘                                             │
│         │                                                    │
│         ▼                                                    │
│     DEPLOYED                                                 │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## Monitoring Post-Deploy

After production deploy, monitor:

| Metric | Alert Threshold | Action |
|--------|-----------------|--------|
| Error rate | > 1% | Investigate |
| Error rate | > 5% | Rollback |
| Response time p95 | > 2s | Investigate |
| Response time p95 | > 5s | Rollback |
| CPU usage | > 80% | Scale |
| Memory usage | > 80% | Investigate |

---

*Template Version: 1.0 | SEAD Framework*
