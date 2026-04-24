# GameChanger Architecture Project

## What This Is

A set of standalone HTML architecture diagrams for the GameChanger youth sports app. Each file opens directly in a browser — no server needed.

## Files

| File | Description |
|------|-------------|
| `architecture-current.html` | Current-state functional map |
| `architecture-future.html` | Future state v1 (three pillars: Athlete Profile, Team Experience, Celebrate) |
| `architecture-future-v2.html` | Future state v2 (added League/Tournament as peer entity) |
| `architecture-future-v3.html` | Future state v3 — current working version (four pillars: Organize, Connect, Celebrate, Grow) |

## What GameChanger Is

Youth sports app originally built for baseball/softball scoring. Now centered on helping families follow games via livestreaming and live play-by-play. 100% free for coaches. Covers millions of youth sports games.

## Current Architecture (architecture-current.html)

**Dual entry point:** Join/create a team OR create a league/tournament — two peer paths from the start.

**Organizational hierarchy:** League/Tournament sits above Team. L/T creates schedules, can score games for participating teams. Teams belong to L/T optionally — they can also schedule independently. Only teams (not L/T admins) can livestream.

**Team-level functional areas:**
- Team Management — roster, schedule, RSVP, staff/community members
- Game Coverage — live (livestream, scoring, play-by-play) + post-game (replays, highlights, AI recaps, stats)
- Team Communication — single group chat, members only
- Athlete Profile — parent-created, cross-team hub for one child. NOT first-class today; you have to drill into a team or game to find a player's content. Roster records across teams are not unified — Athlete Profile manually bridges them.

**Access control (three tiers):**
- Public: team profile, schedule, results, L/T profiles
- Team-controlled: stats (3 sub-tiers), livestreams & replays (open or members-only)
- Members only: chat, roster details, RSVP

**User roles:** League/Tournament Admin (org-level); Coach/Staff, Community Member, Viewer/Follower (team-level)

## Future Vision — Four Pillars (architecture-future-v3.html)

**Home Screen** is the primary entry point — a standalone aggregator/router, not one of the pillars.

**Role-based onboarding** (order matters — Parent, Player, Coach, Fan):
- Parent → set up child's Athlete Profile first, then join a team
- Player → create own profile, team membership follows
- Coach → create/join a team (team is still their primary context)
- Fan → directed to Celebrate to discover teams and athletes

### Pillar 1: Organize
Teams and Leagues/Tournaments as peer entities. Teams can exist independently or associate optionally with a League/Tournament. The organizational scaffolding everything else runs on.

**Functional areas (as shown in the diagram):** Team Management, League Management, Club Management, Tournament Management, Registration

### Pillar 2: Connect
Game coverage — the source of truth. Live and post-game. This is a first-class consumer experience, not just infrastructure.

**Functional areas (as shown in the diagram):** Livestream, Score and Track Stats, Watch Live, See Game Results, Watch Replays and Clips

**Content flows out of Connect:**
- Athlete content (clips, stats, moments) → Grow
- Public content → Celebrate

### Pillar 3: Celebrate (👏, NEW)
Public feed of youth sports moments — the #ItsOnGameChanger concept brought to life. Content types: Top Plays, Highlight Reels, Standout Statlines, Photo Galleries. Positive and inclusive UX: reactions are allowed, but no comments. Supports social sharing back to feed. NOT a social network — no user posts outside of game coverage. Discovery destinations: team public page, athlete Grow profile.

**Key Concepts (as shown in diagram):**
- Public, non-restricted content feed sourced from coverage and direct contributions
- Positive and inclusive UX (reactions, but no comments)
- Support social sharing back to feed

### Pillar 4: Grow (ELEVATED)
Athlete Profile elevated to first-class. The first destination to see a player's clips, stats, moments, and photos — not something you drill to from a team. Aggregates across all teams and sports. Private by default, opt-in public profile discoverable in Celebrate.

**Sections (as shown in diagram):**
- **The Profile** — Multi-sport career view, directly connected to all teams, private by default / opt-in public
- **Coverage-Driven Content** — Player clips & highlights, stats across all teams & seasons, fed automatically from game coverage
- **Optional User Contributions** — Photos & videos, milestones & achievements, gear

## Key Naming & Design Decisions

- "Explore/Watch" was renamed to **Celebrate**
- 👏 icon for Celebrate (not ✨) — chosen to convey "helping those moments be seen"
- Follower user-team relationship is **not new** — it already exists; never label it as new
- Persona order in onboarding is fixed: **Parent, Player, Coach, Fan**
- Four pillars: **Organize, Connect, Celebrate, Grow**
- Celebrate has **reactions** (positive UX) but **no comments** — not a fully social-free experience, but not a social network
- Grow header does **not** carry a "Primary for most users" label — removed
- Org-level user role is called **Org Admin** (not "League/Tournament Admin")
- User relationship order in the diagram: **Parent/Athlete → Staff/Coach → Community Member → Follower → Org Admin**
- Content Visibility & Access Control band is **commented out** in v3 (preserved for potential revival)

## Open Question: Pregame

A potential new feature bucket called **Pregame** covering team registration, league registration, and league/club management. Two placement options discussed:

- **Option A** — Fourth equal pillar alongside the others
- **Option B (preferred)** — Layer above the four pillars, between Home Screen and the pillars, representing organizational scaffolding. Visually communicates hierarchy and chronology.

**Key unresolved question:** Does Pregame introduce a new user role — league/club administrator? If yes, it needs to appear in onboarding and the user relationship model gets a new tier. Confirm this before touching the diagram.

## Diagram Conventions

- Standalone HTML/CSS — no frameworks, no JavaScript
- CSS Grid for multi-column layouts (`repeat(4, 1fr)` for the four-pillar row)
- Per-card color theming via CSS custom properties (`--accent`, `--rc`, `--rbg`)
- Badge system: Public / Team-controlled / Members only / Elevated / New
- Content flow shown as labeled pill-shaped bands below the pillars
- System font stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`
- Save prior versions before making breaking changes (v1, v2, v3 naming)
- Pillar bodies use **high-level functional area tiles** (not granular feature lists) — CSS classes: `.func-area-grid`, `.func-area-tile`
- Section description subheaders use `.section-desc` (italic, 10.5px, no border)
