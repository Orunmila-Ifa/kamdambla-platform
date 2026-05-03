# Feature: Phase 2 - Member Work Tracker

**Platform**: KamDamBla (www.KamDamBla.com)

## Summary

Implement AI-powered member work tracking system for KamDamBla with voice journaling, written entries, emotional analysis, progress scoring, and priest evaluation framework for spiritual development monitoring.

## User Story

As a KamDamBla spiritual development practitioner
I want to track my daily progress and receive AI-powered insights
So that I can measure my growth and stay motivated on my spiritual journey

## Problem Statement

Users lack a systematic way to track spiritual progress, analyze emotional patterns, and receive structured feedback on their development journey. Current manual journaling lacks AI analysis and progress metrics.

## Solution Statement

1. Implement multi-modal journal input system (voice, text, images)
2. Add AI analysis layer for emotional tone and growth pattern detection
3. Create progress scoring and milestone tracking system
4. Build priest evaluation framework with dashboard and alerts

## Metadata

| Field | Value |
|-------|-------|
| Type | NEW_CAPABILITY |
| Complexity | HIGH |
| Systems Affected | @archon/core, @archon/server, @archon/web, @archon/providers |
| Dependencies | Phase 0 (Identity), Phase 1 (Profiles), AI services |
| Estimated Tasks | 15 |
| Confidence | 7/10 — Requires AI integration but follows existing patterns |

---

## UX Design

### Before State
```
╔════════════════════════════════════════════════╗
║              BEFORE STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: Manual journaling only           ║
║   PAIN_POINT: No progress tracking or insights ║
║   DATA_FLOW: Unstructured text entries         ║
╚════════════════════════════════════════════════╝
```

### After State
```
╔════════════════════════════════════════════════╗
║               AFTER STATE                       ║
╠════════════════════════════════════════════════╣
║   USER_FLOW: Voice/text/image → AI analysis → Progress dashboard ║
║   VALUE_ADD: Automated insights, growth tracking, milestone rewards ║
║   DATA_FLOW: Structured analysis with emotional patterns and trends ║
╚════════════════════════════════════════════════╝
```

### Interaction Changes

| Location | Before | After | User Impact |
|----------|--------|-------|-------------|
| Journal entry | Text only | Voice, text, image uploads | Multi-modal expression |
| Progress tracking | None | Automated scoring and insights | Clear growth visibility |
| Feedback | Manual self-reflection | AI analysis + priest evaluation | Structured guidance |

---

## NOT Building (Scope Limits)

- Real-time voice transcription during journaling (offline processing only)
- Video journal entries (Phase 6 immersive environment)
- Advanced predictive analytics (basic pattern analysis only)

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
| `packages/core/src/db/journal-entries.ts` | CREATE | Journal entry storage |
| `packages/core/src/db/progress-tracking.ts` | CREATE | Progress metrics storage |
| `packages/core/src/types/journal.ts` | CREATE | Journal entry types |
| `packages/core/src/types/progress.ts` | CREATE | Progress tracking types |
| `packages/core/src/services/journal-analyzer.ts` | CREATE | AI analysis service |
| `packages/core/src/services/progress-scorer.ts` | CREATE | Progress calculation service |
| `packages/core/src/services/priest-evaluator.ts` | CREATE | Evaluation framework |
| `packages/server/src/routes/journal.ts` | CREATE | Journal API endpoints |
| `packages/server/src/routes/progress.ts` | CREATE | Progress API endpoints |
| `packages/web/src/components/journal/JournalEntry.tsx` | CREATE | Journal input component |
| `packages/web/src/components/journal/VoiceRecorder.tsx` | CREATE | Voice recording component |
| `packages/web/src/components/progress/ProgressDashboard.tsx` | CREATE | Progress visualization |
| `packages/web/src/components/progress/PriestEvaluation.tsx` | CREATE | Evaluation interface |
| `migrations/002_journal_progress.sql` | CREATE | Database schema |
| `packages/workflows/src/defaults/journal-analysis.yaml` | CREATE | Analysis workflow |

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
**Details**: Define progress tracking and evaluation types
**Mirror**: Journal types patterns
**Imports**: `z`, date handling
**Gotcha**: Support different progress metrics and milestones
**Validate**: Type validation for all progress scenarios

### Task 3: CREATE `migrations/002_journal_progress.sql`

**Action**: CREATE
**Details**: Database schema for journal entries and progress tracking
**Mirror**: Existing migration patterns
**Imports**: N/A
**Gotcha**: Proper indexing for performance on large datasets
**Validate**: Test migration with sample data

### Task 4: CREATE `packages/core/src/db/journal-entries.ts`

**Action**: CREATE
**Details**: Database operations for journal entries
**Mirror**: `packages/core/src/db/conversations.ts` patterns
**Imports**: Database connection, journal types
**Gotcha**: Handle large media file storage efficiently
**Validate**: CRUD operations work correctly

### Task 5: CREATE `packages/core/src/db/progress-tracking.ts`

**Action**: CREATE
**Details**: Database operations for progress tracking
**Mirror**: Journal entries patterns
**Imports**: Progress types, aggregation functions
**Gotcha**: Efficient progress calculation queries
**Validate**: Progress metrics calculate correctly

### Task 6: CREATE `packages/core/src/services/journal-analyzer.ts`

**Action**: CREATE
**Details**: AI service for analyzing journal entries
**Mirror**: `packages/providers/src/claude/` patterns
**Imports**: AI provider, text processing
**Gotcha**: Handle different content types and error cases
**Validate**: Analysis provides meaningful insights

### Task 7: CREATE `packages/core/src/services/progress-scorer.ts`

**Action**: CREATE
**Details**: Service for calculating progress scores and milestones
**Mirror**: Analysis service patterns
**Imports**: Progress types, scoring algorithms
**Gotcha**: Fair and consistent scoring across different users
**Validate**: Scores reflect actual progress

### Task 8: CREATE `packages/core/src/services/priest-evaluator.ts`

**Action**: CREATE
**Details**: Service for priest evaluation framework
**Mirror**: Progress scorer patterns
**Imports**: Evaluation criteria, user data
**Gotcha**: Objective evaluation with clear criteria
**Validate**: Evaluations are consistent and helpful

### Task 9: CREATE `packages/server/src/routes/journal.ts`

**Action**: CREATE
**Details**: API endpoints for journal operations
**Mirror**: `packages/server/src/routes/conversations.ts` patterns
**Imports**: OpenAPI, journal services
**Gotcha**: Secure file upload handling
**Validate**: All journal operations work via API

### Task 10: CREATE `packages/server/src/routes/progress.ts`

**Action**: CREATE
**Details**: API endpoints for progress tracking
**Mirror**: Journal routes patterns
**Imports**: Progress services, aggregation
**Gotcha**: Efficient progress data retrieval
**Validate**: Progress data is accurate and timely

### Task 11: CREATE `packages/web/src/components/journal/JournalEntry.tsx`

**Action**: CREATE
**Details**: React component for journal entry input
**Mirror**: `packages/web/src/components/` patterns
**Imports**: React hooks, form handling, API client
**Gotcha**: Intuitive multi-modal input interface
**Validate**: Component handles all input types gracefully

### Task 12: CREATE `packages/web/src/components/journal/VoiceRecorder.tsx`

**Action**: CREATE
**Details**: React component for voice recording
**Mirror**: JournalEntry component patterns
**Imports**: Web Audio API, recording utilities
**Gotcha**: Cross-browser compatibility for recording
**Validate**: Voice recording and playback work

### Task 13: CREATE `packages/web/src/components/progress/ProgressDashboard.tsx`

**Action**: CREATE
**Details**: React component for progress visualization
**Mirror**: Dashboard component patterns
**Imports**: Charts library, progress data
**Gotcha**: Clear and inspiring progress visualization
**Validate**: Dashboard shows accurate progress trends

### Task 14: CREATE `packages/web/src/components/progress/PriestEvaluation.tsx`

**Action**: CREATE
**Details**: React component for priest evaluation interface
**Mirror**: Progress dashboard patterns
**Imports**: Evaluation data, feedback forms
**Gotcha**: Constructive and encouraging evaluation display
**Validate**: Evaluation interface is helpful and clear

### Task 15: CREATE `packages/workflows/src/defaults/journal-analysis.yaml`

**Action**: CREATE
**Details**: Workflow definition for automated journal analysis
**Mirror**: Existing workflow patterns in defaults/
**Imports**: N/A
**Gotcha**: Efficient batch processing of entries
**Validate**: Workflow processes entries correctly

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
