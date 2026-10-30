# CampusSphere

*Build. Connect. Compete. Grow.*

A student project, collaboration and career-growth app built for the
**"Campus Life, Upgraded"** hackathon with **Flutter + Serverpod 4 + PostgreSQL**,
deployable to **Serverpod Cloud**.

| Module | What it does |
|---|---|
| **ProjectVerse** | Reels-style feed of student projects with match reasons, likes, comments, bookmarks and a Project DNA page |
| **TeamUp** | Open roles ranked by explainable skill match, applications, owner accept/decline, contributions |
| **CareerCompass** | Rubric-based skill-gap assessment per career goal, evidence labelled *verified / self-reported / inferred*, day-by-day roadmap, practice projects |
| **Opportunity Radar** | Hackathons, competitions, internships, workshops; Deadline Intelligence prep plans that replan as time runs out |
| **Profile** | Evidence-based profile: skills, linked coding profiles (with consent), owner-confirmed contributions |

## Project layout

```
campussphere_server/   Serverpod backend (models in lib/src/models, endpoints in lib/src/endpoints, logic in lib/src/logic)
campussphere_client/   Generated client (do not edit)
campussphere_flutter/  Flutter app (screens in lib/screens)
```

## Run locally

Requirements: Flutter 3.44.4+ and the Serverpod CLI (`dart install serverpod_cli`).
No Docker needed: Serverpod 4 runs an embedded PostgreSQL in development.

```bash
cd campussphere_server
serverpod start
```

This applies migrations, seeds sample data on first boot, starts the server and
opens the Flutter app. In development, email verification codes are printed in
the server log (press `C` in the Serverpod terminal UI to copy one).

To serve the web build from the server itself (http://localhost:8082):

```bash
cd campussphere_flutter
flutter build web --base-href /
```

then copy `campussphere_flutter/build/web` to `campussphere_server/web/app` and restart the server.

Logic tests (no database needed):

```bash
cd campussphere_server
dart test test/unit
```

## Demo script (about 3 minutes)

1. **Sign up** and onboard as a 2nd-year CSE student: skills Flutter, Dart, Python, Java, DSA, Git; goal *Software Development Engineer*.
2. **ProjectVerse**: swipe the feed; each card says *why* it is shown. Open a project to see its Project DNA.
3. **CareerCompass**: note the starting rubric % and the evidence counts (all self-reported).
4. **TeamUp**: apply to *Flutter developer* on LeafLens (100% match). In *My applications*, use the demo-mode **Owner accepts** button (sample projects have no real owner).
5. **CareerCompass** again: progress rises and two criteria are now **Verified**. The practice list updates.
6. **Radar**: filter Hackathons, **Save & plan** MLH Global Hack Week. Show the backward-scheduled checklist, "Do this next" with its reason, and **Replan**.
7. **Profile**: the accepted role appears as a verified contribution; add what you built.

## Honesty and privacy choices

- All seeded profiles, projects and listings are labelled **Sample**. Real programs link to their real homepages, but their dates are illustrative and marked as such.
- Progress percentages measure coverage of an explicit rubric, not hiring chances.
- Coding-profile links are optional, never scraped, and count only as *inferred* evidence, and only with the student's consent. No third-party passwords are collected.
- Profile → *Delete my data* removes the profile and everything attached to it.

## Deploy to Serverpod Cloud

1. Create an account and a project at https://console.serverpod.dev (enable the database).
2. From the project root:

```bash
serverpod cloud launch
```

This links the project and deploys the backend plus the web build. Run it again to redeploy.
