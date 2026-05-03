# Feature: Phase 2 - Member Work Tracker

**Platform**: KamDamBla (www.KamDamBla.com)

## Summary

Implement AI-powered member work tracking system for KamDamBla with Ọ̀rúnmìlà-led assignments, music-based member identification, journaling system, power dynamics analysis, community agreement tracking, emotional analysis, progress scoring, and priest evaluation framework for Christ Unity Consciousness development.

## User Story

As a KamDamBla way-shower following Ọ̀rúnmìlà's guidance
I want to complete the 6 member work assignments with music-based identification and journaling
So that I can understand my inner members, establish community agreements, and stand in my Christ Unity Consciousness power

## Problem Statement

KamDamBla members lack a systematic way to complete Ọ̀rúnmìlà's 6 assignments: music-based member identification, detailed member documentation, community agreement establishment, power dynamics analysis, role responsibility mapping, and integrity accountability tracking. Current systems don't support this specific spiritual work methodology.

## Solution Statement

1. Implement music-based member identification system with playlist meditation
2. Create structured journaling system for 6 Ọ̀rúnmìlà assignments
3. Build power dynamics analysis tools for 5 power types
4. Add community agreement tracking and integrity accountability
5. Implement AI analysis for emotional patterns and member conflicts
6. Create progress scoring for Christ Unity Consciousness development
7. Build priest evaluation framework with dashboard and alerts

## Metadata

| Field | Value |
|-------|-------|
| Type | NEW_CAPABILITY |
| Complexity | HIGH |
| Systems Affected | @archon/core, @archon/server, @archon/web, @archon/providers |
| Dependencies | Phase 0 (Identity), Phase 1 (Profiles), AI services |
| Estimated Tasks | 20 |
| Confidence | 7/10 — Requires AI integration but follows existing patterns |

---

## UX Design

### Before State
```
╔════════════════════════════════════════════════╗
║              BEFORE STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: Basic journal entry creation        ║
║   PAIN POINT: No Ọ̀rúnmìlà assignment structure ║
║   DATA_FLOW: Unstructured text entries only     ║
╚════════════════════════════════════════════════╝
```

### After State
```
╔════════════════════════════════════════════════╗
║               AFTER STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: Playlist meditation → Member ID → 6 Assignments → Power Analysis ║
║   VALUE_ADD: Complete Ọ̀rúnmìlà methodology, CUCGC progress tracking     ║
║   DATA_FLOW: Structured assignments with AI analysis and community tracking ║
╚════════════════════════════════════════════════╝
```

### Interaction Changes

| Location | Before | After | User Impact |
|----------|--------|-------|-------------|
| Member identification | None | Music playlist meditation | Discover inner members |
| Assignment tracking | Manual journaling | Structured 6 assignments | Complete Ọ̀rúnmìlà methodology |
| Power analysis | No framework | 5 power types analysis | Understand dynamics |
| Community building | Individual work | Agreement tracking | Collective integrity |
| Progress tracking | None | CUCGC development scoring | Christ Unity Consciousness growth |

---

## NOT Building (Scope Limits)

- Automated music selection (manual playlist creation required)
- Real-time voice transcription during journaling (offline processing only)
- Video journal entries (Phase 6 immersive environment)
- Advanced predictive analytics (basic pattern analysis only)
- External music service integration (manual upload only)

---

## Mandatory Reading

**The implementation agent MUST read these files before starting any task.**

| Priority | File | Lines | Why Read This |
|----------|------|-------|---------------|
| P0 | `packages/core/src/db/conversations.ts` | All | Message storage patterns |
| P1 | `packages/providers/src/claude/` | All | AI provider integration patterns |
| P2 | `packages/server/src/routes/` | All | API route patterns to extend |
| P3 | `packages/web/src/components/` | All | UI component patterns |
| P4 | `packages/workflows/src/` | All | Workflow engine for analysis |

---

## Patterns to Mirror

**Message Storage Pattern:**
```typescript
// SOURCE: packages/core/src/db/conversations.ts
export interface Message {
  id: string;
  conversationId: string;
  content: string;
  role: 'user' | 'assistant';
  createdAt: Date;
  metadata?: Record<string, any>;
}
```

**AI Provider Pattern:**
```typescript
// SOURCE: packages/providers/src/claude/claude-provider.ts
export class ClaudeProvider implements IAgentProvider {
  async sendQuery(options: SendQueryOptions): Promise<AsyncIterable<MessageChunk>> {
    // Implementation
  }
}
```

**API Route Pattern:**
```typescript
// SOURCE: packages/server/src/routes/conversations.ts
export const conversationRoutes = {
  createMessage: registerOpenApiRoute({
    method: 'post',
    path: '/conversations/{id}/messages',
    responses: {
      200: { content: { 'application/json': { schema: messageSchema }}},
    },
  }, createMessageHandler),
};
```

---

## Files to Change

| File | Action | Justification |
|------|--------|---------------|
| `packages/core/src/db/journal-entries.ts` | CREATE | Journal entry storage with metadata |
| `packages/core/src/db/assignments.ts` | CREATE | Ọ̀rúnmìlà assignment tracking |
| `packages/core/src/db/music-members.ts` | CREATE | Music-based member identification |
| `packages/core/src/types/journal.ts` | CREATE | Journal entry type definitions |
| `packages/core/src/types/assignments.ts` | CREATE | 6 assignment structure types |
| `packages/core/src/types/power-dynamics.ts` | CREATE | 5 power types analysis |
| `packages/core/src/services/journal-manager.ts` | CREATE | Journal CRUD operations |
| `packages/core/src/services/assignment-tracker.ts` | CREATE | Assignment progress tracking |
| `packages/core/src/services/music-member-identifier.ts` | CREATE | Music meditation member ID |
| `packages/core/src/services/emotion-analyzer.ts` | CREATE | AI emotion analysis service |
| `packages/core/src/services/power-dynamics-analyzer.ts` | CREATE | Power dynamics analysis |
| `packages/core/src/services/progress-scorer.ts` | CREATE | CUCGC progress calculation |
| `packages/core/src/services/priest-evaluator.ts` | CREATE | Priest evaluation and alerts |
| `packages/server/src/routes/journal.ts` | CREATE | Journal API endpoints |
| `packages/server/src/routes/assignments.ts` | CREATE | Assignment tracking endpoints |
| `packages/server/src/routes/music-members.ts` | CREATE | Music member ID endpoints |
| `packages/web/src/components/journal/JournalEntry.tsx` | CREATE | Journal entry UI |
| `packages/web/src/components/assignments/AssignmentTracker.tsx` | CREATE | 6 assignments UI |
| `packages/web/src/components/assignments/MusicMemberIdentifier.tsx` | CREATE | Music meditation UI |
| `packages/web/src/components/assignments/PowerDynamics.tsx` | CREATE | Power analysis UI |
| `packages/web/src/components/progress/ProgressDashboard.tsx` | CREATE | CUCGC progress visualization |
| `packages/web/src/components/progress/PriestEvaluation.tsx` | CREATE | Priest evaluation UI |
| `packages/web/src/hooks/useJournal.ts` | CREATE | Frontend journal hook |
| `packages/web/src/hooks/useAssignments.ts` | CREATE | Frontend assignments hook |
| `migrations/002_journal_assignments.sql` | CREATE | Database schema for assignments |

---

## Step-by-Step Tasks

### Task 1: CREATE `packages/core/src/types/journal.ts`

**Action**: CREATE
**Details**: Define journal entry types with multi-modal support
**Mirror**: `packages/core/src/types/` patterns
**Imports**: `z` from `@hono/zod-openapi`
**Gotcha**: Handle different content types (text, audio, image)
**Validate**: `bun run type-check`

### Task 2: CREATE `packages/core/src/types/progress.ts`

**Action**: CREATE
**Details**: Define 6 Ọ̀rúnmìlà assignment structures and member types
**Mirror**: Journal types patterns
**Imports**: `z`, journal types
**Gotcha**: Support all 6 assignments with proper validation
**Validate**: Assignment types support complete methodology

### Task 3: CREATE `packages/core/src/types/power-dynamics.ts`

**Action**: CREATE
**Details**: Define 5 power dynamics types and analysis structures
**Mirror**: Assignment types patterns
**Imports**: `z`, power dynamics data
**Gotcha**: Support reward, coercive, expert, referent, legitimate power types
**Validate**: Power dynamics types support all analysis scenarios

### Task 4: CREATE `migrations/002_journal_assignments.sql`

**Action**: CREATE
**Details**: Database migration for journal entries, assignments, and music members
**Mirror**: Existing migration patterns
**Imports**: N/A
**Gotcha**: Proper indexing for assignment progress queries
**Validate**: Test migration with sample assignment data

### Task 5: CREATE `packages/core/src/db/journal-entries.ts`

**Action**: CREATE
**Details**: Database operations for journal entries with metadata
**Mirror**: `packages/core/src/db/conversations.ts` patterns
**Imports**: Database connection, journal types
**Gotcha**: Efficient indexing for date-based queries
**Validate**: CRUD operations work correctly

### Task 6: CREATE `packages/core/src/db/assignments.ts`

**Action**: CREATE
**Details**: Database operations for 6 Ọ̀rúnmìlà assignments tracking
**Mirror**: Journal database patterns
**Imports**: Assignment types, progress tracking
**Gotcha**: Support assignment completion and progress tracking
**Validate**: Assignment database maintains accurate progress

### Task 7: CREATE `packages/core/src/db/music-members.ts`

**Action**: CREATE
**Details**: Database operations for music-based member identification
**Mirror**: Assignment database patterns
**Imports**: Music member types, playlist data
**Gotcha**: Support member identification through music meditation
**Validate**: Music member database tracks identification accurately

### Task 8: CREATE `packages/core/src/services/journal-manager.ts`

**Action**: CREATE
**Details**: Service for managing journal entries and media processing
**Mirror**: `packages/core/src/services/` patterns
**Imports**: Journal database, media processing, file storage
**Gotcha**: Handle large media files efficiently
**Validate**: Journal management provides accurate storage

### Task 9: CREATE `packages/core/src/services/assignment-tracker.ts`

**Action**: CREATE
**Details**: Service for tracking 6 Ọ̀rúnmìlà assignments progress
**Mirror**: Journal manager patterns
**Imports**: Assignment database, progress algorithms
**Gotcha**: Track completion of all 6 assignments systematically
**Validate**: Assignment tracker maintains accurate progress

### Task 10: CREATE `packages/core/src/services/music-member-identifier.ts`

**Action**: CREATE
**Details**: Service for music-based member identification through meditation
**Mirror**: Assignment tracker patterns
**Imports**: Music member database, playlist analysis
**Gotcha**: Support member discovery through music meditation
**Validate**: Music identifier provides meaningful member insights

### Task 11: CREATE `packages/core/src/services/emotion-analyzer.ts`

**Action**: CREATE
**Details**: AI service for analyzing emotional tone in journal entries
**Mirror**: Music identifier patterns
**Imports**: AI provider, text processing, emotion schemas
**Gotcha**: Handle multiple languages and cultural contexts
**Validate**: Emotion analysis provides meaningful insights

### Task 12: CREATE `packages/core/src/services/power-dynamics-analyzer.ts`

**Action**: CREATE
**Details**: Service for analyzing 5 power dynamics in member relationships
**Mirror**: Emotion analyzer patterns
**Imports**: Power dynamics types, relationship analysis
**Gotcha**: Support all 5 power types with accurate analysis
**Validate**: Power dynamics analyzer provides meaningful insights

### Task 13: CREATE `packages/core/src/services/progress-scorer.ts`

**Action**: CREATE
**Details**: Service for calculating CUCGC progress scores and milestones
**Mirror**: Power dynamics analyzer patterns
**Imports**: Progress algorithms, assignment data, CUCGC criteria
**Gotcha**: Ensure scoring reflects Christ Unity Consciousness growth
**Validate**: Progress scoring maintains consistency

### Task 14: CREATE `packages/core/src/services/priest-evaluator.ts`

**Action**: CREATE
**Details**: Service for priest evaluation and alert system
**Mirror**: Progress scorer patterns
**Imports**: Evaluation criteria, alert system, user permissions
**Gotcha**: Balance privacy with priest oversight
**Validate**: Priest evaluation provides appropriate guidance

### Task 15: CREATE `packages/server/src/routes/journal.ts`

**Action**: CREATE
**Details**: API endpoints for journal operations
**Mirror**: `packages/server/src/routes/conversations.ts` patterns
**Imports**: OpenAPI, journal manager service
**Gotcha**: Secure handling of sensitive journal data
**Validate**: `bun run dev:server` and test endpoints

### Task 16: CREATE `packages/server/src/routes/assignments.ts`

**Action**: CREATE
**Details**: API endpoints for 6 Ọ̀rúnmìlà assignments tracking
**Mirror**: Journal routes patterns
**Imports**: OpenAPI, assignment tracker service
**Gotcha**: Proper authorization for assignment data
**Validate**: Assignment endpoints provide accurate tracking

### Task 17: CREATE `packages/server/src/routes/music-members.ts`

**Action**: CREATE
**Details**: API endpoints for music member identification
**Mirror**: Assignment routes patterns
**Imports**: OpenAPI, music member identifier service
**Gotcha**: Secure handling of music meditation data
**Validate**: Music member endpoints provide accurate identification

### Task 18: CREATE `packages/web/src/components/journal/JournalEntry.tsx`

**Action**: CREATE
**Details**: React component for journal entry creation and editing
**Mirror**: `packages/web/src/components/` patterns
**Imports**: React hooks, API client, rich text editor
**Gotcha**: Handle voice recording and image uploads
**Validate**: Component handles all journal entry scenarios

### Task 19: CREATE `packages/web/src/components/assignments/AssignmentTracker.tsx`

**Action**: CREATE
**Details**: React component for 6 Ọ̀rúnmìlà assignments tracking
**Mirror**: Journal entry component patterns
**Imports**: Assignment data, progress tracking, UI components
**Gotcha**: Support all 6 assignments with clear progress indication
**Validate**: Assignment tracker handles complete methodology

### Task 20: CREATE `packages/web/src/components/assignments/MusicMemberIdentifier.tsx`

**Action**: CREATE
**Details**: React component for music-based member identification
**Mirror**: Assignment tracker component patterns
**Imports**: Music member data, playlist interface, meditation UI
**Gotcha**: Support music meditation and member discovery workflow
**Validate**: Music identifier provides meaningful member experience

---

## Testing Strategy

### Tests to Write

| Test File | Test Cases | Validates |
|-----------|-----------|-----------|
| `packages/core/src/services/journal-analyzer.test.ts` | AI analysis, content types | Analysis accuracy |
| `packages/core/src/services/progress-scorer.test.ts` | Scoring algorithms, edge cases | Progress calculation |
| `packages/core/src/services/priest-evaluator.test.ts` | Evaluation criteria, consistency | Evaluation fairness |
| `packages/web/src/components/journal/JournalEntry.test.tsx` | UI states, form submission | User interface |

### Edge Cases Checklist

- [ ] Empty journal entries
- [ ] Corrupted audio files
- [ ] AI service unavailability
- [ ] Progress calculation overflow
- [ ] Concurrent journal entries
- [ ] Large image file uploads

---

## Validation Commands

**Detect project runner**: bun

**Levels:**

1. **Type check**: `bun run type-check`
2. **Lint**: `bun run lint`
3. **Unit tests**: `bun run test`
4. **Full validation**: `bun run validate`
5. **Database validation**: Run migration and verify data integrity
6. **Manual verification**: Test journal entry and progress tracking flow

## Acceptance Criteria

- [ ] Users can create journal entries via text, voice, or images
- [ ] AI analysis provides emotional tone and growth insights
- [ ] Progress scores are calculated and displayed accurately
- [ ] Priest evaluation framework provides structured feedback
- [ ] All validation commands pass
- [ ] No regressions in existing conversation system

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| AI analysis accuracy | Medium | Medium | Multiple analysis models, human oversight |
| File storage costs | High | Medium | Efficient compression, cloud storage |
| Progress calculation bias | Medium | High | Transparent algorithms, user feedback |
| Privacy concerns | Medium | High | Strong encryption, user control |
