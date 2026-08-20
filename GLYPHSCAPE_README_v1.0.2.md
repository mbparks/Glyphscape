# GLYPHSCAPE v1.0.2

GLYPHSCAPE is a local-first browser instrument for generating, shaping, simulating, observing, and capturing three-dimensional worlds rendered as American Standard Code for Information Interchange (ASCII) art.

Version 1.0.2 is the Batch 2 project-safety and verification release. It retains the unrestricted 360-degree yaw, pitch, and roll introduced in version 1.0.1 while adding a versioned project schema, strict import validation, a complete local project library, explicit destructive workflows, damaged-project recovery, and tested save–close–reopen behavior.

## Open the application

Open `GLYPHSCAPE_v1.0.2.html` in a current desktop browser. The application is a self-contained HyperText Markup Language (HTML) file. Its current primary workflow does not require an account, backend, database server, analytics service, telemetry service, or network connection.

Ordinary static hosting also works: upload the HTML file and open it through a normal website address. No server-side program is required.

## First launch

GLYPHSCAPE opens as a genuinely blank project.

Choose generation settings and select **Generate world**, or intentionally select **Load demo** to open the editable Highland Reach demonstration. Demonstration content is never silently inserted as the user’s project.

World-only controls are disabled while the project is blank so that visible controls accurately reflect the current state.

## Core workflow

**GENERATE → SHAPE → SIMULATE → OBSERVE → CAPTURE**

1. Generate a deterministic world from a seed and terrain controls.
2. Rotate, pan, zoom, inspect, and focus the world.
3. Sculpt terrain or paint world properties.
4. Play, pause, stop, single-step, reset, or introduce a creative event.
5. Save the editable project locally or export a durable project file.
6. Capture the current ASCII view as text, Scalable Vector Graphics (SVG), Portable Network Graphics (PNG), or standalone HTML.

## Full 360-degree rotation

The world view supports continuously wrapping yaw, pitch, and roll.

### Pointer controls

- **Left drag:** tumble through yaw and pitch.
- **Right drag:** roll the world.
- **Alt/Option + left drag:** roll without a secondary mouse button.
- **Shift + left drag:** pan.
- **Middle drag:** pan.
- **Mouse wheel or trackpad scroll:** zoom.
- **Double-click a visible cell:** select and focus it.

### Keyboard controls

- **Left/Right Arrow:** yaw.
- **Up/Down Arrow:** pitch.
- **Alt/Option + Left/Right Arrow:** roll.
- **O:** Orbit mode.
- **I:** Inspect mode.
- **S:** Sculpt mode.
- **P:** Paint mode.
- **Space:** play or pause.
- **Control/Command + S:** save the current project.
- **Control/Command + Z:** undo.
- **Control/Command + Shift + Z** or **Control/Command + Y:** redo.
- **Escape:** close a non-recovery dialog or return to Orbit mode.

Keyboard shortcuts are ignored while typing in a text field, selection field, or text area.

## Project commands

Version 1.0.2 separates commands that previously could be confused with one another.

### New

Creates a separate blank project with a new identity, default generation controls, and reset camera.

### Load demo

Creates a separate editable Highland Reach demonstration project. It does not silently replace an empty startup state.

### Clear current world

Removes terrain, structures, agents, simulation state, event history, and undo history while retaining the current project identity and generation controls.

### Reset simulation

Restores the world to its captured simulation baseline while preserving the project identity, generation controls, and current camera.

### Stop

Pauses the simulation without restoring the baseline.

### Delete saved project

Permanently removes one selected project from the local project library. If the deleted project is currently open, GLYPHSCAPE opens a new unsaved blank project.

### Clear all local data

Removes every GLYPHSCAPE project, active-project fallback, compact preference record, and session-library record owned by the application in the current browser profile.

Destructive commands are visually distinct and confirmed. Where recoverable work exists, the confirmation offers a local recovery download before proceeding.

## Local project library

Open **Projects** to manage browser-local project records.

The project library supports:

- Save current project
- Open another project
- Rename a project
- Duplicate a project as a separate branch
- Delete one saved project
- Back up the raw content of an unreadable project
- Delete an unreadable project after confirmation
- Clear all GLYPHSCAPE local data

The current project is clearly marked and cannot be opened redundantly from its own row.

## Autosave and storage

GLYPHSCAPE autosaves after meaningful changes.

The preferred persistence path is the Indexed Database Application Programming Interface (IndexedDB API). A compact active-project copy is also maintained in local storage when available. An in-memory session copy remains available when persistent storage is blocked or fails.

Visible save states include:

- Unsaved
- Saving
- Saved locally
- Session only
- Recovery needed
- Save failed

A **Session only** state means that the current tab remains usable, but work may be lost when it closes. Export the project as JavaScript Object Notation (JSON) for a durable backup.

## Project schema version 2

Version 1.0.2 introduces project schema 2.

Schema 2 adds:

- Explicit simulation speed and fixed-step metadata
- A serialized simulation baseline
- A baseline event log
- A world-integrity fingerprint
- Strict world-array validation
- Explicit migration from schema 1

Schema 1 projects are migrated in memory and normalized to schema 2 before use. Projects from a future unsupported schema are rejected with a clear message rather than guessed at.

See `GLYPHSCAPE_PROJECT_SCHEMA_v2.md` for the complete field reference.

## Import validation

Project import performs the following checks before replacing the current project:

1. File size is within the 32-megabyte import limit.
2. JSON syntax is valid.
3. The project format marker is correct.
4. The schema can be migrated safely.
5. World resolution is an integer from 8 through 256.
6. Every Base64-encoded typed array decodes successfully.
7. Every array has the exact byte length required by the world resolution and data type.
8. Structures, agents, event entries, camera values, and generation settings are normalized to safe limits.
9. The optional world-integrity fingerprint matches the imported world.

A failed import leaves the current project unchanged.

Importing into a genuinely empty project proceeds directly. Importing over meaningful work uses the recovery-capable replacement confirmation.

## Damaged-project recovery

If an active local project cannot be migrated or validated, GLYPHSCAPE does not overwrite it.

The recovery screen provides:

- A readable error summary
- The application and schema version
- Copyable technical details
- Download recoverable data
- Retry
- Continue in a temporary session
- Back up and replace the damaged active record

The damaged local value remains untouched until the user explicitly chooses a replacement or deletion action.

## Import and export formats

The current release supports:

- Full editable project JSON import and export
- Plain-text ASCII export
- SVG text-row export
- PNG capture
- Standalone HTML capture
- On-screen ASCII text preview and clipboard copy

Exports are created locally. Nothing is uploaded or transmitted by the application.

## Privacy

All world generation, simulation, rendering, editing, persistence, and export processing occurs locally in the browser. GLYPHSCAPE contains no analytics, advertising, behavioral profiling, tracking pixels, accounts, or intentional project-data transmission.

## Verification status

The packaged build passed 64 of 64 automated and browser-driven checks in Chromium. The tested workflows include blank startup, explicit demonstration loading, deterministic generation, viewport sculpting, undo and redo, full camera orientation, simulation reset, save, simulated close and reopen, project branching, rename, deletion, JSON round trip, schema migration, malformed typed-array rejection, clear-all behavior, damaged-project recovery, blocked-storage fallback, PNG capture, and compact-width rendering.

The container blocked navigation to local and locally served addresses. Testing therefore loaded the unmodified self-contained application with Chromium `page.set_content()` and injected test-only in-memory implementations of local storage and IndexedDB before startup. Native persistent-origin IndexedDB behavior, Firefox, WebKit, assistive-technology, and long-duration stress testing remain outside this release verification.

See `GLYPHSCAPE_VERIFICATION_v1.0.2.md` and `GLYPHSCAPE_v1.0.2_QA.json` for details.

## Current scope

Version 1.0.2 is a hardened vertical slice, not the final implementation of every capability in the original specification. It currently uses a height-field world with projected structures and agents. Free-fly navigation, sparse voxel regions, object transformation, cinematic paths, advanced ASCII render passes, checkpoints, and animated recording remain later roadmap work.

## Release files

- `GLYPHSCAPE_v1.0.2.html` — complete self-contained application
- `GLYPHSCAPE_README_v1.0.2.md` — operating guide
- `GLYPHSCAPE_SHORTCUTS_v1.0.2.md` — controls and keyboard reference
- `GLYPHSCAPE_RELEASE_NOTES_v1.0.2.md` — Batch 2 change record
- `GLYPHSCAPE_VERIFICATION_v1.0.2.md` — human-readable verification evidence
- `GLYPHSCAPE_PROJECT_SCHEMA_v2.md` — project-format reference and migration notes
- `GLYPHSCAPE_v1.0.2_QA.json` — machine-readable quality-assurance results
- `GLYPHSCAPE_Batch_2_Persistence_World_v1.0.2.glyphscape.json` — editable sample and round-trip project
- `GLYPHSCAPE_v1.0.2_CHECKSUMS-SHA256.txt` — release-file hashes
- `GLYPHSCAPE_SOURCE_SPEC.md` — original application specification

## Copyright

Green Shoe Garage, 2026.
