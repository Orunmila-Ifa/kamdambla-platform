# Feature: Phase 1 - User Profile System

**Platform**: KamDamBla (www.KamDamBla.com)

## Summary

Implement the sovereign member profile system for KamDamBla, including CUCGC Christ Unity Consciousness Priesthood levels, warrior tribe heritage integration, AI-powered avatar generation with ancestral elements, and sovereign privacy controls for PMA member data protection.

## User Story

As a KamDamBla sovereign member and CUCGC practitioner
I want a comprehensive profile that reflects my spiritual journey, warrior heritage, and Christ Unity Consciousness level
So that I can connect authentically with fellow way-showers and stand in my power within the sovereign community

## Problem Statement

Current Archon-dev framework lacks specialized profile structures for sovereign religious state members, CUCGC priesthood level tracking, warrior tribe heritage integration, and AI avatar generation with ancestral spiritual elements.

## Solution Statement

1. Create sovereign member profile structure with CUCGC priesthood level tracking
2. Implement warrior tribe heritage integration (Creek Moscogee Nation, Olmec lineage)
3. Build AI avatar generation system with spiritual and ancestral elements
4. Add sovereign privacy controls for PMA member data protection
5. Create profile discovery and connection features for way-showers

## Metadata

| Field | Value |
|-------|-------|
| Type | NEW_CAPABILITY |
| Complexity | HIGH |
| Systems Affected | @archon/core, @archon/server, @archon/web |
| Dependencies | Phase 0 (PMA verification), AI avatar services |
| Estimated Tasks | 18 |
| Confidence | 8/10 — Builds on Archon patterns with sovereign extensions |

---

## UX Design

### Before State
```
╔════════════════════════════════════════════════╗
║              BEFORE STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: Basic profile creation              ║
║   PAIN_POINT: No spiritual level tracking       ║
║   DATA_FLOW: Generic profile data only          ║
╚════════════════════════════════════════════════╝
```

### After State
```
╔════════════════════════════════════════════════╗
║               AFTER STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: PMA verification → CUCGC level → Warrior heritage → AI avatar ║
║   VALUE_ADD: Sovereign identity, ancestral connection, spiritual progression ║
║   DATA_FLOW: Protected sovereign data with CUCGC level tracking ║
╚════════════════════════════════════════════════╝
```

### Interaction Changes

| Location | Before | After | User Impact |
|----------|--------|-------|-------------|
| Profile creation | Basic fields | Sovereign verification, CUCGC level, heritage | Authentic spiritual identity |
| Avatar generation | Upload only | AI-powered with warrior/ancestral elements | Meaningful visual representation |
| Privacy settings | Basic controls | Sovereign data protection levels | PMA member sovereignty |

---

## NOT Building (Scope Limits)

- Non-sovereign profile templates - only PMA member profiles
- Generic avatar generation - must include warrior tribe and CUCGC elements
- Public profile discovery - member-only access to sovereign profiles
- Cross-platform profile sync - sovereign data stays within KamDamBla

---

## Mandatory Reading

**The implementation agent MUST read these files before starting any task.**

| Priority | File | Lines | Why Read This |
|----------|------|-------|---------------|
| P0 | `packages/core/src/db/users.ts` | All | Existing user management patterns |
| P1 | `packages/core/src/types/pma.ts` | All | PMA governance structure types |
| P2 | `packages/server/src/routes/identity.ts` | All | PMA verification patterns |
| P3 | `packages/web/src/components/auth/PMAVerification.tsx` | All | Verification UI patterns |
| P4 | `phase-0-legal-safety-ethics-plan.md` | All | Sovereign legal framework context |

---

## Patterns to Mirror

**User Management Pattern:**
```typescript
// SOURCE: packages/core/src/db/users.ts
export interface User {
  id: string;
  email: string;
  profile: UserProfile;
  createdAt: Date;
}
```

**PMA Verification Pattern:**
```typescript
// SOURCE: packages/core/src/types/pma.ts
export interface PMAMember {
  id: string;
  verificationLevel: VerificationLevel;
  cucgcStatus: CUCGCStatus;
  warriorHeritage: WarriorHeritage;
}
```

**API Route Pattern:**
```typescript
// SOURCE: packages/server/src/routes/identity.ts
export const identityRoutes = {
  verify: registerOpenApiRoute({
    method: 'post',
    path: '/identity/verify',
    responses: {
      200: { content: { 'application/json': { schema: verificationSchema }}},
    },
  }, verificationHandler),
};
```

---

## Files to Change

| File | Action | Justification |
|------|--------|---------------|
| `packages/core/src/types/profile.ts` | CREATE | Sovereign member profile types |
| `packages/core/src/types/cucgc.ts` | CREATE | CUCGC priesthood level definitions |
| `packages/core/src/types/warrior-heritage.ts` | CREATE | Warrior tribe heritage types |
| `packages/core/src/db/profiles.ts` | CREATE | Profile database operations |
| `packages/core/src/db/cucgc-levels.ts` | CREATE | CUCGC level tracking |
| `packages/core/src/services/profile-manager.ts` | CREATE | Profile management service |
| `packages/core/src/services/avatar-generator.ts` | CREATE | AI avatar generation service |
| `packages/core/src/services/sovereign-privacy.ts` | CREATE | Privacy control service |
| `packages/server/src/routes/profiles.ts` | CREATE | Profile API endpoints |
| `packages/server/src/routes/avatars.ts` | CREATE | Avatar generation endpoints |
| `packages/web/src/components/profile/SovereignProfile.tsx` | CREATE | Profile creation/editing UI |
| `packages/web/src/components/profile/CUCGCLevel.tsx` | CREATE | CUCGC level display UI |
| `packages/web/src/components/profile/WarriorHeritage.tsx` | CREATE | Heritage selection UI |
| `packages/web/src/components/profile/AvatarGenerator.tsx` | CREATE | AI avatar generation UI |
| `packages/web/src/components/profile/PrivacyControls.tsx` | CREATE | Sovereign privacy settings UI |
| `migrations/002_profiles_cucgc.sql` | CREATE | Database schema for profiles |

---

## Step-by-Step Tasks

### Task 1: CREATE `packages/core/src/types/profile.ts`

**Action**: CREATE
**Details**: Define sovereign member profile types with CUCGC integration
**Mirror**: `packages/core/src/types/` patterns
**Imports**: `z` from `@hono/zod-openapi`
**Gotcha**: Ensure sovereign data protection fields are properly validated
**Validate**: `bun run type-check`

### Task 2: CREATE `packages/core/src/types/cucgc.ts`

**Action**: CREATE
**Details**: Define CUCGC Christ Unity Consciousness priesthood levels and progression
**Mirror**: Profile types patterns
**Imports**: `z`, profile types
**Gotcha**: Support different priesthood paths and advancement criteria
**Validate**: Type validation for all CUCGC scenarios

### Task 3: CREATE `packages/core/src/types/warrior-heritage.ts`

**Action**: CREATE
**Details**: Define warrior tribe heritage types (Creek Moscogee, Olmec lineage)
**Mirror**: CUCGC types patterns
**Imports**: `z`, heritage data structures
**Gotcha**: Support multiple heritage paths and ancestral connections
**Validate**: Heritage types support all warrior tribe variations

### Task 4: CREATE `migrations/002_profiles_cucgc.sql`

**Action**: CREATE
**Details**: Database migration for sovereign profiles and CUCGC level tracking
**Mirror**: Existing migration patterns
**Imports**: N/A
**Gotcha**: Proper indexing for profile discovery and CUCGC level queries
**Validate**: Test migration with sample sovereign profile data

### Task 5: CREATE `packages/core/src/db/profiles.ts`

**Action**: CREATE
**Details**: Database operations for sovereign member profiles
**Mirror**: `packages/core/src/db/users.ts` patterns
**Imports**: Database connection, profile types, CUCGC types
**Gotcha**: Secure storage of sovereign member data with PMA compliance
**Validate**: Profile CRUD operations work correctly

### Task 6: CREATE `packages/core/src/db/cucgc-levels.ts`

**Action**: CREATE
**Details**: Database operations for CUCGC level tracking and progression
**Mirror**: Profile database patterns
**Imports**: CUCGC types, progression algorithms
**Gotcha**: Immutable level progression records for audit trail
**Validate**: CUCGC level tracking maintains accuracy

### Task 7: CREATE `packages/core/src/services/profile-manager.ts`

**Action**: CREATE
**Details**: Service for managing sovereign member profiles and CUCGC progression
**Mirror**: `packages/core/src/services/` patterns
**Imports**: Profile database, CUCGC validation, warrior heritage
**Gotcha**: Ensure profile updates maintain sovereign compliance
**Validate**: Profile management provides accurate member representation

### Task 8: CREATE `packages/core/src/services/avatar-generator.ts`

**Action**: CREATE
**Details**: AI service for generating avatars with warrior tribe and CUCGC elements
**Mirror**: Profile manager patterns
**Imports**: AI provider, image processing, heritage elements
**Gotcha**: Incorporate warrior tribe symbols and CUCGC level indicators
**Validate**: Avatar generation produces meaningful spiritual representations

### Task 9: CREATE `packages/core/src/services/sovereign-privacy.ts`

**Action**: CREATE
**Details**: Service for managing sovereign privacy controls and data protection
**Mirror**: Avatar generator patterns
**Imports**: Privacy controls, PMA compliance, data encryption
**Gotcha**: Ensure UCC 1.308 sovereign data protection compliance
**Validate**: Privacy controls maintain member sovereignty

### Task 10: CREATE `packages/server/src/routes/profiles.ts`

**Action**: CREATE
**Details**: API endpoints for sovereign profile operations
**Mirror**: `packages/server/src/routes/identity.ts` patterns
**Imports**: OpenAPI, profile manager service
**Gotcha**: Member-only access to sovereign profile data
**Validate**: Profile endpoints enforce proper access controls

### Task 11: CREATE `packages/server/src/routes/avatars.ts`

**Action**: CREATE
**Details**: API endpoints for avatar generation and management
**Mirror**: Profile routes patterns
**Imports**: OpenAPI, avatar generator service
**Gotcha**: Secure handling of avatar generation requests
**Validate**: Avatar endpoints provide proper spiritual representations

### Task 12: CREATE `packages/web/src/components/profile/SovereignProfile.tsx`

**Action**: CREATE
**Details**: React component for sovereign profile creation and editing
**Mirror**: `packages/web/src/components/` patterns
**Imports**: React hooks, API client, profile forms
**Gotcha**: Integrate CUCGC level selection and warrior heritage options
**Validate**: Profile component handles all sovereign member scenarios

### Task 13: CREATE `packages/web/src/components/profile/CUCGCLevel.tsx`

**Action**: CREATE
**Details**: React component for CUCGC level display and progression tracking
**Mirror**: SovereignProfile component patterns
**Imports**: CUCGC data, progression visualization
**Gotcha**: Clear indication of spiritual advancement and way-shower status
**Validate**: CUCGC component accurately reflects member's spiritual journey

### Task 14: CREATE `packages/web/src/components/profile/WarriorHeritage.tsx`

**Action**: CREATE
**Details**: React component for warrior tribe heritage selection and display
**Mirror**: CUCGC level component patterns
**Imports**: Heritage data, cultural elements
**Gotcha**: Respectful representation of Creek Moscogee and Olmec traditions
**Validate**: Heritage component honors ancestral connections appropriately

### Task 15: CREATE `packages/web/src/components/profile/AvatarGenerator.tsx`

**Action**: CREATE
**Details**: React component for AI avatar generation with spiritual elements
**Mirror**: Warrior heritage component patterns
**Imports**: Avatar generation API, preview components
**Gotcha**: Include warrior tribe symbols and CUCGC level indicators
**Validate**: Avatar generator creates meaningful spiritual representations

### Task 16: CREATE `packages/web/src/components/profile/PrivacyControls.tsx`

**Action**: CREATE
**Details**: React component for sovereign privacy settings and data controls
**Mirror**: Avatar generator component patterns
**Imports**: Privacy settings, sovereign controls
**Gotcha**: Clear explanation of sovereign data protection options
**Validate**: Privacy controls maintain member sovereignty

### Task 17: CREATE `packages/web/src/components/profile/ProfileDiscovery.tsx`

**Action**: CREATE
**Details**: React component for discovering and connecting with fellow way-showers
**Mirror**: Privacy controls component patterns
**Imports**: Profile search, connection requests
**Gotcha**: Member-only access with appropriate filtering
**Validate**: Discovery component facilitates meaningful connections

### Task 18: CREATE `packages/web/src/hooks/useSovereignProfile.ts`

**Action**: CREATE
**Details**: Custom hook for sovereign profile state management
**Mirror**: Existing hook patterns in `packages/web/src/hooks/`
**Imports**: React hooks, profile API, CUCGC data
**Gotcha**: Handle profile state caching and sovereign data protection
**Validate**: Hook provides accurate sovereign profile state

---

## Testing Strategy

### Tests to Write

| Test File | Test Cases | Validates |
|-----------|-----------|-----------|
| `packages/core/src/services/profile-manager.test.ts` | Profile creation, CUCGC progression | Sovereign profile management |
| `packages/core/src/services/avatar-generator.test.ts` | Avatar generation, heritage elements | Spiritual representation accuracy |
| `packages/core/src/services/sovereign-privacy.test.ts` | Privacy controls, data protection | Sovereign data compliance |
| `packages/web/src/components/profile/SovereignProfile.test.tsx` | UI states, profile creation | Sovereign profile interface |

### Edge Cases Checklist

- [ ] CUCGC level progression validation failures
- [ ] Warrior heritage data inconsistencies
- [ ] Avatar generation service unavailability
- [ ] Sovereign privacy control conflicts
- [ ] Profile discovery access violations
- [ ] Database migration failures for sovereign data

---

## Validation Commands

**Detect project runner**: bun

**Levels:**

1. **Type check**: `bun run type-check`
2. **Lint**: `bun run lint`
3. **Unit tests**: `bun run test`
4. **Full validation**: `bun run validate`
5. **Database validation**: Run migration and verify sovereign profile schema
6. **Manual verification**: Test sovereign profile creation and avatar generation

## Acceptance Criteria

- [ ] Sovereign members can create profiles with CUCGC level tracking
- [ ] Warrior tribe heritage integration respects ancestral traditions
- [ ] AI avatar generation includes meaningful spiritual and warrior elements
- [ ] Sovereign privacy controls maintain PMA member data protection
- [ ] Profile discovery facilitates authentic way-shower connections
- [ ] All validation commands pass
- [ ] No regressions in existing PMA verification system

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| CUCGC level validation complexity | Medium | High | Clear progression criteria, audit trails |
| Warrior heritage cultural sensitivity | High | High | Cultural consultation, respectful representation |
| Avatar generation spiritual accuracy | Medium | Medium | Multiple generation models, member feedback |
| Sovereign data privacy breaches | Medium | High | Strong encryption, access controls |
| Profile discovery abuse | Medium | Medium | Member verification, reporting systems |
