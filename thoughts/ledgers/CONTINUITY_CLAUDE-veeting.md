# Continuity Ledger: Veeting

## Goal
Ship a minimal mobile app ("Veeting") for appointments, meetings, and notes via
voice and text. Done for this phase = private GitHub repo exists with README +
planning doc, and open questions are settled in a brainstorm session.

## Constraints
- So simple, so minimal — resist feature creep
- Phone-first, voice as first-class input
- Core = calendar + email connection to book time slots and arrange meetings

## Key Decisions
- Name (working title): **Veeting**
- Repo: private, on bokiko's personal GitHub
- Planning docs live in `veeting/` (README.md + PLANNING.md), staged in
  continuous-claude-guide until the dedicated repo exists

## State
- Done:
  - [x] Phase 1: Capture initial idea dump in veeting/PLANNING.md
  - [x] Phase 1: Draft veeting/README.md (ready to seed new repo)
- Now: [→] Phase 2: Create private repo `bokiko/veeting` (BLOCKED: GitHub App
  token cannot create repos — user must create it at github.com/new, then
  grant the Claude GitHub App access to it)
- Next: Phase 3: Move veeting/ docs into the new repo as initial commit
- Remaining:
  - [ ] Phase 4: Brainstorm session — settle Open Questions in PLANNING.md
  - [ ] Phase 5: Pick tech stack, define v1 scope
  - [ ] Phase 6: Wireframes, then build

## Open Questions
- UNCONFIRMED: Platform choice (iOS/Android/cross-platform)
- UNCONFIRMED: Calendar provider priority (Google first?)
- UNCONFIRMED: Voice: on-device vs cloud transcription
- UNCONFIRMED: Backend needed for v1?
- UNCONFIRMED: "Veeting" name availability on app stores

## Working Set
- Branch: `claude/veeting-mobile-app-setup-aeip8j` (continuous-claude-guide)
- Files: `veeting/README.md`, `veeting/PLANNING.md`
- Target repo (to be created): `bokiko/veeting` (private)
