# Veeting — Planning & Brainstorm

> Captured 2026-08-13 from initial idea dump. This is the raw material for the
> upcoming brainstorm session — nothing here is final.

## The Pitch (as stated)

A mobile app for appointments, meetings, and notes via voice and text.

- So simple, so minimal
- Focused product
- Mainly for connecting with **calendar** and **email** to book time slots and arrange meetings
- Can run on **voice commands**
- Can take **notes**
- Any other tools to help someone working on their phone get the job done

## Candidate Feature Areas

### 1. Scheduling (the core)
- Calendar connection (Google Calendar first? Outlook later?)
- See free/busy, propose time slots
- Book appointments and confirm meetings
- Email integration: parse "can we meet next week?" threads into bookings

### 2. Voice
- Voice commands for booking: "schedule 30 min with Alex on Friday"
- Voice capture for notes with transcription
- Hands-free flow for when you're walking/driving

### 3. Notes
- Quick capture: voice or text
- Attach notes to a meeting (prep notes, follow-up notes)
- Standalone notes for ideas on the go

### 4. "Get the job done" extras (brainstorm later)
- Meeting reminders / smart nudges
- Share availability link
- Action items extracted from notes
- Daily agenda glance

## Open Questions (for brainstorm)

- UNCONFIRMED: Platform — iOS first, Android first, or cross-platform (React Native / Flutter / Expo)?
- UNCONFIRMED: Calendar provider priority — Google only for v1?
- UNCONFIRMED: Voice — on-device speech recognition vs cloud (Whisper API etc.)?
- UNCONFIRMED: Does v1 need accounts/backend, or can it be device + provider APIs only?
- UNCONFIRMED: Email integration scope for v1 — read-only parsing, or send invites too?
- Name check: is "Veeting" available on the app stores?

## Non-Goals (keep it minimal)

- Not a full calendar replacement
- Not a general note-taking app competing with Notion/Obsidian
- Not a video-call product (despite the name sounding like "meeting")

## Next Steps

1. [x] Create repo + capture initial ideas
2. [ ] Brainstorm session: settle open questions above
3. [ ] Pick tech stack
4. [ ] Define v1 scope (smallest lovable product)
5. [ ] Wireframes for the 2–3 core screens
6. [ ] Build

## MVP Sketch (strawman for discussion)

**One screen, three actions:**

- Big mic button → speak a command or note, app figures out which
- Today's agenda strip (from connected calendar)
- Recent notes list

That's it. Everything else is settings.
