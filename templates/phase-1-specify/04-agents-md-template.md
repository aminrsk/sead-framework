# AGENTS.md

This file configures AI coding assistants working on this project. Keep under 150 lines.

---

## Project Context

[One paragraph describing the project, its purpose, and current phase]

Example:
> This is a customer relationship management system for enterprise clients. We're building a Next.js application with AI-powered insights. Currently in Phase 3: Development. Focus on core CRUD features first.

---

## Tech Stack

```
Framework:     [e.g., Next.js 14 with App Router]
Language:      [e.g., TypeScript 5.x (strict mode)]
Styling:       [e.g., Tailwind CSS 3.x]
Database:      [e.g., PostgreSQL via Neon]
ORM:           [e.g., Prisma]
Auth:          [e.g., Clerk]
AI:            [e.g., Claude API via Anthropic SDK]
Testing:       [e.g., Jest + React Testing Library + Playwright]
Hosting:       [e.g., Vercel]
```

---

## Project Structure

```
/app                 # Next.js App Router pages
  /api               # API routes
  /(auth)            # Auth-related pages
  /(dashboard)       # Main app pages
/components          # React components
  /ui                # Reusable UI components
  /features          # Feature-specific components
/lib                 # Utilities and shared logic
  /ai                # AI-related code
  /db                # Database utilities
/prisma              # Database schema and migrations
/tests               # Test files
  /unit              # Unit tests
  /e2e               # End-to-end tests
```

---

## Coding Standards

### Naming Conventions

- **Components:** PascalCase (`UserProfile.tsx`)
- **Files:** kebab-case (`user-profile.tsx`) or match component
- **Functions:** camelCase (`getUserById`)
- **Constants:** UPPER_SNAKE_CASE (`MAX_RETRIES`)
- **Types/Interfaces:** PascalCase (`UserProfile`)

### Code Style

- Use TypeScript strict mode
- Prefer `const` over `let`
- Use async/await over .then()
- Destructure props and imports
- Keep functions under 50 lines
- One component per file

### Imports Order

```typescript
// 1. React/Next
import { useState } from 'react';
import { useRouter } from 'next/navigation';

// 2. Third-party
import { z } from 'zod';

// 3. Internal
import { Button } from '@/components/ui/button';
import { getUserById } from '@/lib/db/users';

// 4. Types
import type { User } from '@/types';
```

---

## Testing Requirements

### Test-Driven Development (TDD)

1. Write tests FIRST based on acceptance criteria
2. Verify tests FAIL before implementing
3. Implement minimal code to pass
4. Refactor if needed
5. Commit

### Coverage Requirements

- Minimum 80% coverage for new code
- 100% coverage for Critical/High risk features
- All acceptance criteria must have tests

### Test File Location

- Unit tests: `__tests__/` next to source OR `/tests/unit/`
- E2E tests: `/tests/e2e/`
- Name pattern: `*.test.ts` or `*.spec.ts`

---

## Security Rules

### DO NOT (Critical - Never Do These)

- ❌ Never commit secrets, API keys, or credentials
- ❌ Never access production database directly
- ❌ Never skip input validation
- ❌ Never bypass authentication checks
- ❌ Never log sensitive data (passwords, tokens, PII)
- ❌ Never use `any` type for user input
- ❌ Never trust client-side data without validation
- ❌ Never modify auth logic without human review

### DO (Always)

- ✅ Use environment variables for secrets
- ✅ Validate all inputs with Zod schemas
- ✅ Use parameterized queries (Prisma handles this)
- ✅ Apply proper authorization checks
- ✅ Sanitize data before display
- ✅ Use HTTPS for all external requests

---

## AI Feature Boundaries

### AI Can (Autonomously)

- Generate suggestions and recommendations
- Analyze data and provide insights
- Draft content for human review
- Answer questions from provided context

### AI Cannot (Requires Human Confirmation)

- Modify database records
- Send emails or notifications
- Make API calls to external services
- Delete any data
- Change user permissions

### AI Response Requirements

- Always include reasoning/explanation
- Always include confidence level if applicable
- Always provide source references if from context
- Never make claims without supporting data

---

## Error Handling

### Pattern

```typescript
try {
  // Operation
} catch (error) {
  if (error instanceof SpecificError) {
    // Handle specific error
  }
  // Log error (not sensitive data)
  console.error('Operation failed:', error.message);
  // Return user-friendly message
  throw new AppError('Something went wrong', 500);
}
```

### User-Facing Errors

- Never expose stack traces
- Never expose internal error details
- Provide actionable error messages
- Log details server-side for debugging

---

## Git Conventions

### Commit Messages

```
[FEATURE_ID] Type: Brief description

- Detail 1
- Detail 2
```

Types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`

Example: `[F001] feat: Add user registration with email verification`

### Branch Names

- Feature: `feature/F001-user-registration`
- Fix: `fix/F001-validation-error`
- Refactor: `refactor/auth-cleanup`

---

## Current Focus

### Active Features

- [F001] User Registration - In Progress
- [F002] User Login - Not Started

### Blocked

- [F010] External Integration - Waiting for API credentials

### Completed

- [F000] Project Setup

---

## Human Checkpoints

The following require human approval before proceeding:

- [ ] Any database schema changes
- [ ] Any new external API integration
- [ ] Any changes to authentication flow
- [ ] Any changes to authorization rules
- [ ] Any AI feature that affects user data

---

*File Version: 1.0 | Last Updated: [Date] | SEAD Framework*
