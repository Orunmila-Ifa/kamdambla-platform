# Feature: Phase 0 - Legal, Safety, and Ethics Layer

**Platform**: KamDamBla (www.KamDamBla.com)

## Summary

Implement the foundational legal, safety, and ethics infrastructure for the KamDamBla spiritual development platform, including identity verification, age segregation, consent tracking, and financial compliance systems.

## User Story

As a platform operator
I want robust legal, safety, and ethics infrastructure
So that I can provide a safe, compliant environment for spiritual development

## Problem Statement

Current Archon-dev framework lacks specialized legal compliance, identity verification, age segregation, and consent tracking systems required for a spiritual development platform handling sensitive user data and community interactions.

## Solution Statement

1. Extend the existing user management system with identity verification integration
2. Implement age-based access controls and data segregation
3. Add consent tracking and privacy management systems
4. Integrate financial compliance for payment processing

## Metadata

| Field | Value |
|-------|-------|
| Type | NEW_CAPABILITY |
| Complexity | HIGH |
| Systems Affected | @archon/core, @archon/server, @archon/web |
| Dependencies | Identity verification provider APIs |
| Estimated Tasks | 12 |
| Confidence | 8/10 — Leverages existing Archon patterns but requires new integrations |

---

## UX Design

### Before State
```
╔════════════════════════════════════════════════╗
║              BEFORE STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: Basic signup → Profile creation   ║
║   PAIN_POINT: No identity verification         ║
║   DATA_FLOW: All users access same features     ║
╚════════════════════════════════════════════════╝
```

### After State
```
╔════════════════════════════════════════════════╗
║               AFTER STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: KYC verification → Age gating → Profile ║
║   VALUE_ADD: Legal compliance, age-appropriate content ║
║   DATA_FLOW: Segregated access by age/verification status ║
╚════════════════════════════════════════════════╝
```

### Interaction Changes

| Location | Before | After | User Impact |
|----------|--------|-------|-------------|
| Registration | Basic email/password | KYC verification flow | Higher friction but compliant |
| Profile access | All features available | Age-gated features | Safe, appropriate content |
| Settings | Basic preferences | Privacy controls, consent management | User control over data |

---

## NOT Building (Scope Limits)

- Anonymous-only access modes — all users require verified identity
- Cross-age community interactions — strict segregation enforced
- Unverified payment processing — all financial activity requires KYC

---

## Mandatory Reading

**The implementation agent MUST read these files before starting any task.**

| Priority | File | Lines | Why Read This |
|----------|------|-------|---------------|
| P0 | `packages/core/src/db/users.ts` | All | Existing user management patterns |
| P1 | `packages/server/src/routes/auth.ts` | All | Authentication patterns to extend |
| P2 | `packages/web/src/components/auth/` | All | Frontend auth patterns to mirror |
| P3 | `packages/core/src/types/` | All | Type definitions to extend |

---

## Patterns to Mirror

**User Management Pattern:**
```typescript
// SOURCE: packages/core/src/db/users.ts
export interface User {
  id: string;
  email: string;
  createdAt: Date;
  updatedAt: Date;
}
```

**Database Schema Pattern:**
```typescript
// SOURCE: packages/core/src/db/schema.ts
export const userSchema = z.object({
  id: z.string().uuid(),
  email: z.string().email(),
  createdAt: z.date(),
  updatedAt: z.date(),
});
```

**API Route Pattern:**
```typescript
// SOURCE: packages/server/src/routes/auth.ts
export const authRoutes = {
  login: registerOpenApiRoute({
    method: 'post',
    path: '/auth/login',
    responses: {
      200: {
        description: 'Login successful',
        content: {
          'application/json': {
            schema: loginResponseSchema,
          },
        },
      },
    },
  }, loginHandler),
};
```

---

## Files to Change

| File | Action | Justification |
|------|--------|---------------|
| `packages/core/src/db/users.ts` | UPDATE | Add identity verification fields |
| `packages/core/src/types/user.ts` | CREATE | Define extended user types |
| `packages/server/src/routes/identity.ts` | CREATE | Identity verification endpoints |
| `packages/server/src/routes/consent.ts` | CREATE | Consent management endpoints |
| `packages/web/src/components/auth/IdentityVerification.tsx` | CREATE | KYC verification UI |
| `packages/web/src/components/auth/AgeGate.tsx` | CREATE | Age verification UI |
| `packages/web/src/components/settings/PrivacyControls.tsx` | CREATE | Privacy management UI |
| `migrations/001_identity_verification.sql` | CREATE | Database schema changes |
| `packages/core/src/services/identity-verification.ts` | CREATE | Third-party integration service |
| `packages/core/src/services/age-segregation.ts` | CREATE | Age-based access control |
| `packages/core/src/services/consent-manager.ts` | CREATE | Consent tracking service |
| `packages/web/src/hooks/useIdentityVerification.ts` | CREATE | Frontend hook for verification |

---

## Step-by-Step Tasks

### Task 1: CREATE `packages/core/src/types/user.ts`

**Action**: CREATE
**Details**: Define extended user types with identity verification fields
**Mirror**: `packages/core/src/types/` — follow existing type patterns
**Imports**: `z` from `@hono/zod-openapi`
**Gotcha**: Ensure all new fields have proper validation
**Validate**: `bun run type-check`

### Task 2: UPDATE `packages/core/src/db/users.ts`

**Action**: UPDATE
**Details**: Add identity verification fields to user interface and database operations
**Mirror**: Existing user field patterns in same file
**Imports**: Import new types from `./types/user.ts`
**Gotcha**: Maintain backward compatibility for existing users
**Validate**: `bun run test packages/core`

### Task 3: CREATE `migrations/001_identity_verification.sql`

**Action**: CREATE
**Details**: Database migration for identity verification fields
**Mirror**: Existing migration patterns in migrations/ directory
**Imports**: N/A
**Gotcha**: Ensure proper indexes for performance
**Validate**: Run migration against test database

### Task 4: CREATE `packages/core/src/services/identity-verification.ts`

**Action**: CREATE
**Details**: Service for integrating with third-party KYC providers
**Mirror: `packages/core/src/services/` patterns
**Imports**: HTTP client, logger, error handling
**Gotcha**: Handle provider-specific error responses
**Validate**: Unit tests for provider integration

### Task 5: CREATE `packages/core/src/services/age-segregation.ts`

**Action**: CREATE
**Details**: Service for age-based access control and content filtering
**Mirror: `packages/core/src/services/` patterns
**Imports**: User types, database queries
**Gotcha**: Ensure strict segregation with no bypasses
**Validate**: Test age boundary conditions

### Task 6: CREATE `packages/core/src/services/consent-manager.ts`

**Action**: CREATE
**Details**: Service for tracking and managing user consent
**Mirror: `packages/core/src/services/` patterns
**Imports**: Database operations, audit logging
**Gotcha**: Immutable consent records for audit trail
**Validate**: Test consent tracking accuracy

### Task 7: CREATE `packages/server/src/routes/identity.ts`

**Action**: CREATE
**Details**: API endpoints for identity verification
**Mirror**: `packages/server/src/routes/auth.ts` patterns
**Imports**: OpenAPI route registration, validation schemas
**Gotcha**: Secure handling of sensitive verification data
**Validate**: `bun run dev:server` and test endpoints

### Task 8: CREATE `packages/server/src/routes/consent.ts`

**Action**: CREATE
**Details**: API endpoints for consent management
**Mirror:** `packages/server/src/routes/identity.ts` patterns
**Imports**: OpenAPI, consent manager service
**Gotcha**: Proper audit logging for consent changes
**Validate**: Test consent tracking endpoints

### Task 9: CREATE `packages/web/src/components/auth/IdentityVerification.tsx`

**Action**: CREATE
**Details**: React component for KYC verification flow
**Mirror:** `packages/web/src/components/auth/` patterns
**Imports**: React hooks, API client, UI components
**Gotcha**: Handle verification failures gracefully
**Validate**: Component renders and handles all states

### Task 10: CREATE `packages/web/src/components/auth/AgeGate.tsx`

**Action**: CREATE
**Details**: React component for age verification
**Mirror:** IdentityVerification component patterns
**Imports**: Similar to IdentityVerification
**Gotcha**: Enforce age gating with no workarounds
**Validate**: Test age boundary conditions

### Task 11: CREATE `packages/web/src/components/settings/PrivacyControls.tsx`

**Action**: CREATE
**Details**: React component for privacy and consent management
**Mirror:** Settings component patterns
**Imports**: API client, form handling
**Gotcha**: Clear indication of privacy implications
**Validate**: Test consent update flow

### Task 12: CREATE `packages/web/src/hooks/useIdentityVerification.ts`

**Action**: CREATE
**Details**: Custom hook for identity verification state management
**Mirror:** Existing hook patterns in `packages/web/src/hooks/`
**Imports:** React hooks, API client
**Gotcha**: Handle verification status caching
**Validate**: Hook provides correct state updates

---

## Testing Strategy

### Tests to Write

| Test File | Test Cases | Validates |
|-----------|-----------|-----------|
| `packages/core/src/services/identity-verification.test.ts` | Provider integration, error handling | KYC service functionality |
| `packages/core/src/services/age-segregation.test.ts` | Age boundary conditions, content filtering | Access control logic |
| `packages/core/src/services/consent-manager.test.ts` | Consent tracking, audit trail | Consent management |
| `packages/web/src/components/auth/IdentityVerification.test.tsx` | UI states, error handling | Verification UI |

### Edge Cases Checklist

- [ ] Identity verification provider downtime
- [ ] Age verification manipulation attempts
- [ ] Consent withdrawal with data deletion
- [ ] Database migration failures
- [ ] Concurrent verification attempts
- [ ] Privacy control conflicts

---

## Validation Commands

**Detect project runner**: bun

**Levels:**

1. **Type check**: `bun run type-check`
2. **Lint**: `bun run lint`
3. **Unit tests**: `bun run test`
4. **Full validation**: `bun run validate`
5. **Database validation**: Run migration and verify schema
6. **Manual verification**: Test KYC flow end-to-end

## Acceptance Criteria

- [ ] Users can complete identity verification with at least one provider
- [ ] Age-based access control prevents underage users from accessing adult content
- [ ] Consent tracking maintains immutable audit trail
- [ ] Privacy controls allow users to manage data visibility
- [ ] All validation commands pass
- [ ] No regressions in existing authentication system

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| KYC provider API changes | Medium | Medium | Multiple provider support, adapter pattern |
| Age verification bypass attempts | High | High | Multiple verification methods, strict enforcement |
| Consent regulation changes | Medium | High | Flexible consent tracking system |
| Database migration issues | Low | High | Comprehensive testing, rollback procedures |
