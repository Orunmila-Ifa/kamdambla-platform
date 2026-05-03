# Feature: Phase 3 - Dating + Community Mode

**Platform**: KamDamBla (www.KamDamBla.com)

## Summary

Implement integrated dating system for KamDamBla with spiritual level matching, community mode with red/green status tracking, and behavior-based reputation system while maintaining privacy controls and transparency requirements.

## User Story

As a KamDamBla spiritual development practitioner
I want to connect with like-minded individuals for dating and community
So that I can build meaningful relationships with people who share my spiritual journey

## Problem Statement

Users seeking spiritual connections lack a dedicated platform that matches based on spiritual compatibility and progress. Existing dating apps don't account for spiritual development levels or community engagement.

## Solution Statement

1. Implement spiritual level-based matchmaking system
2. Create red/green status tracking for lesson completion
3. Build community mode with transparency controls
4. Add reputation system based on behavior and engagement

## Metadata

| Field | Value |
|-------|-------|
| Type | NEW_CAPABILITY |
| Complexity | HIGH |
| Systems Affected | @archon/core, @archon/server, @archon/web |
| Dependencies | Phase 0 (Identity), Phase 1 (Profiles), Phase 2 (Work Tracker) |
| Estimated Tasks | 13 |
| Confidence | 8/10 — Builds on existing user management and progress systems |

---

## UX Design

### Before State
```
╔════════════════════════════════════════════════╗
║              BEFORE STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: No dating or community features    ║
║   PAIN_POINT: Isolated spiritual journey       ║
║   DATA_FLOW: Individual progress only           ║
╚════════════════════════════════════════════════╝
```

### After State
```
╔════════════════════════════════════════════════╗
║               AFTER STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: Matchmaking → Community interaction → Dating ║
║   VALUE_ADD: Spiritual compatibility, progress-based matching ║
║   DATA_FLOW: Shared progress data, reputation tracking ║
╚════════════════════════════════════════════════╝
```

### Interaction Changes

| Location | Before | After | User Impact |
|----------|--------|-------|-------------|
| Social features | None | Dating + community | Connection opportunities |
| Progress visibility | Private | Community mode transparency | Social accountability |
| Matching | None | Spiritual level based | Compatible connections |

---

## NOT Building (Scope Limits)

- Anonymous matching - all users require verified identity
- Cross-age dating - strict age segregation maintained
- Financial transactions between users - restricted in community mode

---

## Mandatory Reading

**The implementation agent MUST read these files before starting any task.**

| Priority | File | Lines | Why Read This |
|----------|------|-------|---------------|
| P0 | `packages/core/src/db/users.ts` | All | User profile patterns |
| P1 | `packages/core/src/db/progress-tracking.ts` | All | Progress data for matching |
| P2 | `packages/server/src/routes/conversations.ts` | All | Message handling patterns |
| P3 | `packages/web/src/components/` | All | UI component patterns |
| P4 | `packages/core/src/services/` | All | Service layer patterns |

---

## Patterns to Mirror

**User Relationship Pattern:**
```typescript
// SOURCE: packages/core/src/db/users.ts
export interface User {
  id: string;
  email: string;
  profile: UserProfile;
  createdAt: Date;
}
```

**Message Storage Pattern:**
```typescript
// SOURCE: packages/core/src/db/conversations.ts
export interface Message {
  id: string;
  conversationId: string;
  senderId: string;
  content: string;
  createdAt: Date;
}
```

**API Route Pattern:**
```typescript
// SOURCE: packages/server/src/routes/conversations.ts
export const conversationRoutes = {
  create: registerOpenApiRoute({
    method: 'post',
    path: '/conversations',
    responses: {
      200: { content: { 'application/json': { schema: conversationSchema }}},
    },
  }, createConversationHandler),
};
```

---

## Files to Change

| File | Action | Justification |
|------|--------|---------------|
| `packages/core/src/db/dating.ts` | CREATE | Dating system storage |
| `packages/core/src/db/community.ts` | CREATE | Community features storage |
| `packages/core/src/types/dating.ts` | CREATE | Dating system types |
| `packages/core/src/types/community.ts` | CREATE | Community system types |
| `packages/core/src/services/matchmaker.ts` | CREATE | Spiritual level matching |
| `packages/core/src/services/reputation-manager.ts` | CREATE | Reputation calculation |
| `packages/core/src/services/community-moderator.ts` | CREATE | Community moderation |
| `packages/server/src/routes/dating.ts` | CREATE | Dating API endpoints |
| `packages/server/src/routes/community.ts` | CREATE | Community API endpoints |
| `packages/web/src/components/dating/Matchmaker.tsx` | CREATE | Dating interface |
| `packages/web/src/components/dating/ProfileCard.tsx` | CREATE | User profiles for dating |
| `packages/web/src/components/community/CommunityFeed.tsx` | CREATE | Community activity feed |
| `packages/web/src/components/community/StatusIndicator.tsx` | CREATE | Red/green status display |
| `migrations/003_dating_community.sql` | CREATE | Database schema |

---

## Step-by-Step Tasks

### Task 1: CREATE `packages/core/src/types/dating.ts`

**Action**: CREATE
**Details**: Define dating system types including matches, preferences, and compatibility
**Mirror**: `packages/core/src/types/` patterns
**Imports**: `z` from `@hono/zod-openapi`
**Gotcha**: Handle different matching criteria and preferences
**Validate**: `bun run type-check`

### Task 2: CREATE `packages/core/src/types/community.ts`

**Action**: CREATE
**Details**: Define community system types including status, reputation, and moderation
**Mirror**: Dating types patterns
**Imports**: `z`, user types
**Gotcha**: Support different community roles and permissions
**Validate**: Type validation for all community scenarios

### Task 3: CREATE `migrations/003_dating_community.sql`

**Action**: CREATE
**Details**: Database schema for dating and community features
**Mirror**: Existing migration patterns
**Imports**: N/A
**Gotcha**: Proper indexing for matching queries
**Validate**: Test migration with sample data

### Task 4: CREATE `packages/core/src/db/dating.ts`

**Action**: CREATE
**Details**: Database operations for dating system
**Mirror**: `packages/core/src/db/users.ts` patterns
**Imports**: Database connection, dating types
**Gotcha**: Efficient matching queries and relationship tracking
**Validate**: CRUD operations and matching algorithms work

### Task 5: CREATE `packages/core/src/db/community.ts`

**Action**: CREATE
**Details**: Database operations for community features
**Mirror**: Dating patterns
**Imports**: Community types, aggregation functions
**Gotcha**: Real-time status updates and reputation calculations
**Validate**: Community features update correctly

### Task 6: CREATE `packages/core/src/services/matchmaker.ts`

**Action**: CREATE
**Details**: Service for spiritual level-based matching
**Mirror**: Service layer patterns
**Imports**: Progress data, user profiles, matching algorithms
**Gotcha**: Fair and unbiased matching algorithm
**Validate**: Matching produces compatible pairs

### Task 7: CREATE `packages/core/src/services/reputation-manager.ts`

**Action**: CREATE
**Details**: Service for calculating and managing user reputation
**Mirror**: Matchmaker patterns
**Imports**: User activity data, progress metrics
**Gotcha**: Transparent reputation calculation with clear criteria
**Validate**: Reputation scores reflect actual behavior

### Task 8: CREATE `packages/core/src/services/community-moderator.ts`

**Action**: CREATE
**Details**: Service for community moderation and status management
**Mirror**: Reputation manager patterns
**Imports**: Community guidelines, user reports
**Gotcha**: Consistent and fair moderation
**Validate**: Moderation actions are appropriate

### Task 9: CREATE `packages/server/src/routes/dating.ts`

**Action**: CREATE
**Details**: API endpoints for dating features
**Mirror**: `packages/server/src/routes/conversations.ts` patterns
**Imports**: OpenAPI, dating services
**Gotcha**: Secure handling of sensitive matching data
**Validate**: All dating operations work via API

### Task 10: CREATE `packages/server/src/routes/community.ts`

**Action**: CREATE
**Details**: API endpoints for community features
**Mirror**: Dating routes patterns
**Imports**: Community services, real-time updates
**Gotcha**: Efficient community data streaming
**Validate**: Community features update in real-time

### Task 11: CREATE `packages/web/src/components/dating/Matchmaker.tsx`

**Action**: CREATE
**Details**: React component for dating interface and matching
**Mirror**: `packages/web/src/components/` patterns
**Imports**: React hooks, API client, matching UI
**Gotcha**: Intuitive matching interface with clear preferences
**Validate**: Component handles all matching scenarios

### Task 12: CREATE `packages/web/src/components/dating/ProfileCard.tsx`

**Action**: CREATE
**Details**: React component for displaying user profiles in dating context
**Mirror**: Matchmaker component patterns
**Imports**: User data, profile components
**Gotcha**: Appropriate profile information display
**Validate**: Profile cards show relevant information

### Task 13: CREATE `packages/web/src/components/community/CommunityFeed.tsx`

**Action**: CREATE
**Details**: React component for community activity feed
**Mirror**: Dating component patterns
**Imports**: Community data, feed components
**Gotcha**: Real-time feed updates and filtering
**Validate**: Community feed displays relevant activities

### Task 14: CREATE `packages/web/src/components/community/StatusIndicator.tsx`

**Action**: CREATE
**Details**: React component for red/green status display
**Mirror**: Community feed patterns
**Imports**: Status data, visual indicators
**Gotcha**: Clear status communication
**Validate**: Status indicators are accurate and clear

---

## Testing Strategy

### Tests to Write

| Test File | Test Cases | Validates |
|-----------|-----------|-----------|
| `packages/core/src/services/matchmaker.test.ts` | Matching algorithms, compatibility | Match quality |
| `packages/core/src/services/reputation-manager.test.ts` | Reputation calculation, edge cases | Fair scoring |
| `packages/core/src/services/community-moderator.test.ts` | Moderation actions, consistency | Fair moderation |
| `packages/web/src/components/dating/Matchmaker.test.tsx` | UI states, matching flow | User experience |

### Edge Cases Checklist

- [ ] No available matches
- [ ] Reputation manipulation attempts
- [ ] Community mode abuse
- [ ] Inappropriate matching requests
- [ ] Status indicator conflicts
- [ ] Cross-age interaction attempts

---

## Validation Commands

**Detect project runner**: bun

**Levels:**

1. **Type check**: `bun run type-check`
2. **Lint**: `bun run lint`
3. **Unit tests**: `bun run test`
4. **Full validation**: `bun run validate`
5. **Database validation**: Run migration and verify relationships
6. **Manual verification**: Test matching and community features

## Acceptance Criteria

- [ ] Users can set dating preferences and receive matches
- [ ] Spiritual level matching produces compatible pairs
- [ ] Red/green status system accurately reflects progress
- [ ] Community mode provides appropriate transparency
- [ ] Reputation system rewards positive behavior
- [ ] All validation commands pass
- [ ] No regressions in existing user or progress systems

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Matching algorithm bias | Medium | High | Regular algorithm audits, user feedback |
| Community harassment | High | High | Strong moderation, clear guidelines |
| Privacy concerns in community mode | Medium | High | Granular privacy controls, user consent |
| Reputation gaming | Medium | Medium | Transparent calculation, abuse detection |
