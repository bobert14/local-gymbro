# Local GymBro

Offline Android app for planning and logging gym and calisthenics workouts.
Open source (GPL-3.0). All data stays on the device. Built for every Android
user, including people with older or low-end phones.

## Who you are working with

The maintainer is a beginner programmer learning with your help.
- Chat with him in Romanian. Code, comments, commit messages, docs: English.
- Work in small steps, one feature at a time. Explain what you did and why in
  plain words, and tell him how to test it on his phone.
- Never add a dependency without explaining why and asking first.

## Decisions already made (do not reopen without asking)

- Language/UI: Kotlin, Jetpack Compose, Material 3.
- Storage: Room (SQLite). Architecture: MVVM (ViewModel + StateFlow).
- Android only. `minSdk = 24` (Android 7.0). No API above 24 without a fallback.
- No `INTERNET` permission, ever. No accounts, no analytics, no telemetry, no
  cloud code. Do not add libraries that need network access.
- License: GPL-3.0. Every dependency must be GPL-compatible (Apache-2.0 and MIT
  are fine). Do not copy code or text from other projects without checking its
  license; ideas are fine.
- Languages: English is the default (`res/values`), Romanian in
  `res/values-ro`. No hardcoded UI strings.
- No rest timer (explicit decision).
- Backup: export/import as one JSON file (with `schemaVersion`) through the
  Android file picker (Storage Access Framework). The user picks where it goes.
- Exercise types: weight (kg x reps), bodyweight (reps), timed (seconds).
- Exercise data: JSON files in `assets/`, starting from free-exercise-db
  (described as public domain; verify its LICENSE.md, including the images,
  before importing anything). Calisthenics progressions and Romanian
  translations are written by us. Images as WebP, loaded lazily; the app must
  work with images turned off. Keep the APK small.
- The app does not give medical advice; show a clear disclaimer.

## MVP, in this order

1. Exercise library: search, filters (muscle, equipment, type).
2. Manual program builder: days, exercises, target sets and reps.
3. Workout screen: log sets (reps, kg or seconds), optional notes.
4. History of sessions.
5. Progress chart per exercise (reps, kg or seconds over time).
6. English + Romanian strings complete.
7. Export / import JSON.

After the MVP: guided beginner program generator (rule-based, every rule cites a
source note in `docs/rules/`), and suggestions of new exercises over time.

## Data model (Room)

Exercise, Program, ProgramDay, PlannedExercise, Session, SetLog, Settings.
A SetLog belongs to one Session and one Exercise (reps, weight in kg or null for
bodyweight, seconds for timed exercises, optional note).

## Code layout

Package by feature under the app's package: `exercises`, `programs`, `workout`,
`history`, `progress`, `settings`, plus `data` (Room, repositories) and `ui`
(theme, shared components). Small files, clear names, comments explain the why.

## How to work

- Build with the Gradle wrapper only: `gradlew.bat assembleDebug` on Windows,
  `./gradlew assembleDebug` elsewhere. Do not use a global Gradle.
- After each step: build, then tell the maintainer how to run and check it on
  the phone.
- Unit-test the logic (progress calculation, generator rules, export/import
  round trip).
- Do not commit or push unless asked. Commit messages: Conventional Commits.
- Never paste text from books or articles into the repo. Notes go in his own
  words, with a citation.

## docs/

`docs/` is an Obsidian-compatible vault: `sources/` (one note per book or
article), `rules/` (one note per generator rule, linked to its sources),
`decisions/` (why we chose things).

## CodeGraph (optional)

Not enabled until the first features exist. If a `.codegraph/` directory exists,
use `codegraph_explore` for questions about structure, callers and impact before
grepping files. `.codegraph/` is git-ignored.
