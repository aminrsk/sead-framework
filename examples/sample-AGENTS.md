# AGENTS.md

This file configures AI coding assistants. Keep under 150 lines.

---

## Project Context

This is a sample customer portal application for managing client accounts 
and support requests. Built with Next.js 14 and PostgreSQL. Currently in 
Phase 3: Development. Focus on authentication and core CRUD features.

---

## Tech Stack

```
Framework:     Next.js 14 with App Router
Language:      TypeScript 5.x (strict mode)
Styling:       Tailwind CSS 3.x
Database:      PostgreSQL via Neon
ORM:           Prisma
Auth:          Clerk
Testing:       Jest + React Testing Library + Playwright
Hosting:       Vercel
```

---

## Project Structure

```
/app                 # Next.js App Router pages
  /api               # API routes
  /(auth)            # Auth pages (login, register)
  /(dashboard)       # Main application
/components          # React components
  /ui                # Reusable UI (buttons, cards, etc.)
  /features          # Feature-specific components
/lib                 # Utilities
  /db                # Database utilities
  /utils             # Helper functions
/prisma              # Database schema
/tests               # All tests
```

---

## Coding Standards

### Naming
- Components: PascalCase (`UserProfile.tsx`)
- Files: kebab-case or match component
- Functions: camelCase (`getUserById`)
- Types: PascalCase (`UserProfile`)

### Style
- TypeScript strict mode
- Prefer const over let
- Use async/await
- Destructure imports
- Max function length: 50 lines

---

## Testing Requirements

### TDD Mandatory
1. Write tests FIRST
2. Verify tests FAIL
3. Implement to pass
4. Refactor
5. Commit

### Coverage
- Minimum: 80%
- Critical features: 100%

---

## Security Rules

### DO NOT
- ❌ Commit secrets or API keys
- ❌ Access production DB directly
- ❌ Skip input validation
- ❌ Bypass auth checks
- ❌ Log sensitive data
- ❌ Use `any` for user input

### DO
- ✅ Use environment variables
- ✅ Validate with Zod
- ✅ Use Prisma (parameterized)
- ✅ Check authorization

---

## Current Focus

### In Progress
- [F001] User Registration

### Next
- [F002] User Login
- [F003] Password Reset

### Blocked
- None

---

## Human Checkpoints

Require approval before:
- [ ] Database schema changes
- [ ] New API integrations
- [ ] Auth flow changes
- [ ] Authorization changes

---

*Updated: [Date]*
