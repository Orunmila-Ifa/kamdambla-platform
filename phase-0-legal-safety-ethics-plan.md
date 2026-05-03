# Feature: Phase 0 - Legal, Safety, and Ethics Layer

**Platform**: KamDamBla (www.KamDamBla.com)

## Summary

Implement the foundational legal, safety, and ethics infrastructure for the KamDamBla Sovereign Religious State and Faith-Based Private Members Association, including sovereign legal framework, member verification, bylaws access, consent tracking, and PMA compliance systems under UCC 1.308 and US 26 508c1a tax exemption.

## User Story

As a KamDamBla Sovereign Religious State operator
I want robust sovereign legal framework and PMA compliance infrastructure
So that I can provide a protected, sovereign environment for Christ Unity Consciousness spiritual development

## Problem Statement

Current Archon-dev framework lacks specialized sovereign religious state compliance, PMA legal framework, member verification systems, bylaws access control, and faith-based governance structures required for a Sovereign Religious State operating under UCC 1.308 and US 26 508c1a tax exemption.

## Solution Statement

1. Implement KamDamBla Sovereign Religious State legal framework under UCC 1.308
2. Create Faith-Based Private Members Association governance structure
3. Build member verification system for CUCGC Christ Unity Consciousness Priesthood
4. Add bylaws and legal statement access control for PMA members
5. Implement consent tracking and sovereign privacy management
6. Integrate tax-exempt financial compliance under US 26 508c1a

## Metadata

| Field | Value |
|-------|-------|
| Type | NEW_CAPABILITY |
| Complexity | HIGH |
| Systems Affected | @archon/core, @archon/server, @archon/web |
| Dependencies | Sovereign legal framework, PMA governance, Identity verification |
| Estimated Tasks | 15 |
| Confidence | 8/10 — Leverages existing Archon patterns but requires new integrations |

---

## UX Design

### Before State
```
╔════════════════════════════════════════════════╗
║              BEFORE STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: Basic signup → Profile creation   ║
║   PAIN_POINT: No sovereign legal framework      ║
║   DATA_FLOW: No PMA governance or bylaws access ║
╚════════════════════════════════════════════════╝
```

### After State
```
╔════════════════════════════════════════════════╗
║               AFTER STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: PMA member verification → Bylaws access → Profile ║
║   VALUE_ADD: Sovereign legal compliance, CUCGC priesthood access ║
║   DATA_FLOW: Protected member data, sovereign governance structure ║
╚════════════════════════════════════════════════╝
```

### Interaction Changes

| Location | Before | After | User Impact |
|----------|--------|-------|-------------|
| Registration | Basic email/password | PMA member verification flow | Sovereign compliance, CUCGC access |
| Profile access | All features available | Bylaws-gated features | Protected PMA member content |
| Settings | Basic preferences | Sovereign controls, legal statement access | Member control over sovereign data |

---

## NOT Building (Scope Limits)

- Anonymous-only access modes — all members require PMA verification
- Non-sovereign legal frameworks — only UCC 1.308 and US 26 508c1a compliance
- Public access to bylaws — restricted to verified PMA members only
- Non-CUCGC priesthood access — membership limited to Christ Unity Consciousness practitioners

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
| `packages/core/src/db/users.ts` | UPDATE | Add PMA member verification fields |
| `packages/core/src/types/user.ts` | CREATE | Define sovereign member types |
| `packages/core/src/db/bylaws.ts` | CREATE | Bylaws access control system |
| `packages/core/src/types/pma.ts` | CREATE | PMA governance structure types |
| `packages/server/src/routes/identity.ts` | CREATE | PMA member verification endpoints |
| `packages/server/src/routes/bylaws.ts` | CREATE | Bylaws access endpoints |
| `packages/server/src/routes/sovereign.ts` | CREATE | Sovereign legal framework endpoints |
| `packages/web/src/components/auth/PMAVerification.tsx` | CREATE | PMA member verification UI |
| `packages/web/src/components/auth/BylawsAccess.tsx` | CREATE | Bylaws access control UI |
| `packages/web/src/components/settings/SovereignControls.tsx` | CREATE | Sovereign privacy management UI |
| `packages/web/src/components/legal/LegalStatement.tsx` | CREATE | Legal statement display UI |
| `migrations/001_pma_sovereign.sql` | CREATE | Database schema for PMA structure |
| `packages/core/src/services/pma-verifier.ts` | CREATE | PMA member verification service |
| `packages/core/src/services/bylaws-manager.ts` | CREATE | Bylaws access management service |
| `packages/core/src/services/sovereign-governance.ts` | CREATE | Sovereign legal framework service |
| `packages/core/src/services/consent-manager.ts` | CREATE | Consent tracking service |
| `packages/web/src/hooks/usePMAVerification.ts` | CREATE | Frontend hook for PMA verification |

---

## Step-by-Step Tasks

### Task 1: CREATE `packages/core/src/types/user.ts`

**Action**: CREATE
**Details**: Define extended user types with PMA member verification fields and sovereign status
**Mirror**: `packages/core/src/types/` — follow existing type patterns
**Imports**: `z` from `@hono/zod-openapi`
**Gotcha**: Ensure all new fields have proper validation for sovereign compliance
**Validate**: `bun run type-check`

### Task 2: CREATE `packages/core/src/types/pma.ts`

**Action**: CREATE
**Details**: Define PMA governance structure types including bylaws access and member levels
**Mirror**: User types patterns
**Imports**: `z`, user types
**Gotcha**: Support different member levels (CUCGC Priesthood, Warrior Tribe, etc.)
**Validate**: Type validation for all PMA scenarios

### Task 3: CREATE `migrations/001_pma_sovereign.sql`

**Action**: CREATE
**Details**: Database migration for PMA member verification and sovereign legal framework
**Mirror**: Existing migration patterns
**Imports**: N/A
**Gotcha**: Proper indexing for member verification queries
**Validate**: Test migration with sample data

### Task 4: CREATE `packages/core/src/db/bylaws.ts`

**Action**: CREATE
**Details**: Database operations for bylaws access control and legal statement management
**Mirror**: `packages/core/src/db/users.ts` patterns
**Imports**: Database connection, PMA types
**Gotcha**: Secure bylaws storage with member-only access
**Validate**: CRUD operations work correctly

### Task 5: UPDATE `packages/core/src/db/users.ts`

**Action**: UPDATE
**Details**: Add PMA member verification fields to user interface and database operations
**Mirror**: Existing user field patterns in same file
**Imports**: Import new types from `./types/user.ts` and `./types/pma.ts`
**Gotcha**: Maintain backward compatibility for existing users
**Validate**: `bun run test packages/core`

### Task 6: CREATE `packages/core/src/services/pma-verifier.ts`

**Action**: CREATE
**Details**: Service for PMA member verification and CUCGC Priesthood validation
**Mirror**: `packages/core/src/services/` patterns
**Imports**: User verification, legal framework validation
**Gotcha**: Handle different member verification levels and requirements
**Validate**: PMA verification provides accurate member status

### Task 7: CREATE `packages/core/src/services/bylaws-manager.ts`

**Action**: CREATE
**Details**: Service for managing bylaws access and legal statement distribution
**Mirror**: PMA verifier patterns
**Imports**: Bylaws database operations, member verification
**Gotcha**: Strict access control - only verified PMA members can access bylaws
**Validate**: Bylaws access is properly restricted

### Task 8: CREATE `packages/core/src/services/sovereign-governance.ts`

**Action**: CREATE
**Details**: Service for sovereign legal framework management under UCC 1.308
**Mirror**: Bylaws manager patterns
**Imports**: Legal compliance, tax exemption management
**Gotcha**: Ensure compliance with US 26 508c1a tax exemption requirements
**Validate**: Sovereign governance maintains legal compliance

### Task 9: CREATE `packages/server/src/routes/identity.ts`

**Action**: CREATE
**Details**: API endpoints for PMA member verification
**Mirror**: `packages/server/src/routes/auth.ts` patterns
**Imports**: OpenAPI route registration, validation schemas
**Gotcha**: Secure handling of sensitive member verification data
**Validate**: `bun run dev:server` and test endpoints

### Task 10: CREATE `packages/server/src/routes/bylaws.ts`

**Action**: CREATE
**Details**: API endpoints for bylaws access and legal statement retrieval
**Mirror**: Identity routes patterns
**Imports**: OpenAPI, bylaws manager service
**Gotcha**: Member-only access enforcement
**Validate**: Bylaws endpoints properly restrict access

### Task 11: CREATE `packages/server/src/routes/sovereign.ts`

**Action**: CREATE
**Details**: API endpoints for sovereign legal framework information
**Mirror**: Bylaws routes patterns
**Imports**: Sovereign governance service
**Gotcha**: Public legal statement access vs private member-only content
**Validate**: Sovereign endpoints provide appropriate access levels

### Task 12: CREATE `packages/web/src/components/auth/PMAVerification.tsx`

**Action**: CREATE
**Details**: React component for PMA member verification flow
**Mirror**: `packages/web/src/components/auth/` patterns
**Imports**: React hooks, API client, PMA verification UI
**Gotcha**: Handle different member verification levels (CUCGC, Warrior Tribe, etc.)
**Validate**: Component handles all PMA verification scenarios

### Task 13: CREATE `packages/web/src/components/auth/BylawsAccess.tsx`

**Action**: CREATE
**Details**: React component for bylaws access control interface
**Mirror**: PMA verification component patterns
**Imports**: Similar to PMAVerification
**Gotcha**: Clear indication of member-only access requirements
**Validate**: Bylaws access component enforces restrictions

### Task 14: CREATE `packages/web/src/components/settings/SovereignControls.tsx`

**Action**: CREATE
**Details**: React component for sovereign privacy and data management
**Mirror**: Settings component patterns
**Imports**: API client, form handling, sovereign controls
**Gotcha**: Clear indication of sovereign data protection
**Validate**: Sovereign controls provide member data protection

### Task 15: CREATE `packages/web/src/components/legal/LegalStatement.tsx`

**Action**: CREATE
**Details**: React component for displaying KamDamBla legal statements and sovereign status
**Mirror**: Settings component patterns
**Imports**: Legal data, display components
**Gotcha**: Proper formatting of UCC 1.308 and US 26 508c1a references
**Validate**: Legal statement displays accurate information

---

## Testing Strategy

### Tests to Write

| Test File | Test Cases | Validates |
|-----------|-----------|-----------|
| `packages/core/src/services/pma-verifier.test.ts` | PMA verification, member levels | Sovereign member verification |
| `packages/core/src/services/bylaws-manager.test.ts` | Bylaws access, member restrictions | PMA governance compliance |
| `packages/core/src/services/sovereign-governance.test.ts` | UCC 1.308 compliance, tax exemption | Legal framework integrity |
| `packages/web/src/components/auth/PMAVerification.test.tsx` | UI states, member verification flows | PMA verification interface |

### Edge Cases Checklist

- [ ] PMA verification system downtime
- [ ] Bylaws access manipulation attempts
- [ ] Sovereign legal framework compliance issues
- [ ] UCC 1.308 documentation updates
- [ ] US 26 508c1a tax exemption verification
- [ ] Member level privilege escalation attempts
- [ ] Database migration failures
- [ ] Concurrent PMA verification attempts
- [ ] Sovereign data privacy conflicts

---

## Validation Commands

**Detect project runner**: bun

**Levels:**

1. **Type check**: `bun run type-check`
2. **Lint**: `bun run lint`
3. **Unit tests**: `bun run test`
4. **Full validation**: `bun run validate`
5. **Database validation**: Run migration and verify schema
6. **Manual verification**: Test PMA verification and bylaws access flow end-to-end

## Acceptance Criteria

- [ ] PMA members can complete sovereign verification with CUCGC Priesthood validation
- [ ] Bylaws access control prevents non-members from accessing restricted content
- [ ] Sovereign legal framework maintains UCC 1.308 and US 26 508c1a compliance
- [ ] Consent tracking maintains immutable audit trail for PMA governance
- [ ] Sovereign privacy controls allow members to manage protected data
- [ ] All validation commands pass
- [ ] No regressions in existing authentication system

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| PMA verification provider changes | Medium | Medium | Multiple verification methods, sovereign compliance |
| Bylaws access manipulation attempts | High | High | Strict member verification, audit logging |
| UCC 1.308 legal framework updates | Medium | High | Flexible legal compliance system |
| US 26 508c1a tax exemption changes | Low | High | Legal monitoring, compliance updates |
| Database migration issues | Low | High | Comprehensive testing, rollback procedures |
