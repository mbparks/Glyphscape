# GLYPHSCAPE v1.0.2 — Batch 2 Release Notes

## Release objective

Version 1.0.2 turns the stabilized world instrument from Batch 1 into a safer local project system. The release focuses on data durability, explicit lifecycle commands, defensive import, schema migration, recoverable failure states, and complete browser workflow verification.

## Added: project schema version 2

- Added explicit `schemaVersion: 2` to the top-level record and project metadata.
- Added serialized simulation speed and fixed-step metadata.
- Added a simulation baseline world and baseline event log.
- Added a deterministic world fingerprint using 32-bit Fowler–Noll–Vo 1a (FNV-1a) hashing.
- Added a schema 1 to schema 2 migration function.
- Rejects unsupported future schemas rather than silently guessing.
- Preserves project identity, timestamps, camera orientation, render settings, world state, simulation time, event history, and metadata through save and import round trips.

## Added: strict import validation

- Added a 32-megabyte import limit.
- Added clear JavaScript Object Notation (JSON) parsing errors.
- Requires the `GLYPHSCAPE_PROJECT` format marker.
- Validates world resolution from 8 through 256.
- Strictly decodes all Base64 world arrays.
- Requires exact byte lengths for every typed array.
- Rejects malformed height, moisture, temperature, water, vegetation, fire, and biome data.
- Normalizes camera, generation, tool, structure, agent, and event values to safe bounds.
- Verifies the optional world-integrity fingerprint.
- Leaves the current project untouched when validation fails.
- Skips unnecessary replacement confirmation when the current project is genuinely empty.

## Added: complete local project library

- Save current project.
- Open a saved project.
- Rename a saved project.
- Duplicate a project as a new branch with a new identifier and timestamps.
- Delete a selected saved project.
- Identify the currently open project.
- Detect and label unreadable project records.
- Download an unreadable record without opening it.
- Delete an unreadable record through the protected destructive flow.
- Display Indexed Database, local-fallback, schema, quota, and recovery-hold status.

## Added: explicit project and simulation lifecycle

The release now distinguishes:

- **New** — a separate blank project with new identity and default settings.
- **Load demo** — an intentionally selected editable demonstration project.
- **Clear current world** — remove world content while retaining project identity and generation controls.
- **Reset simulation** — restore the stored simulation baseline without changing project or camera.
- **Stop** — pause without resetting.
- **Delete saved project** — remove one library record.
- **Clear all local data** — remove all GLYPHSCAPE-owned local project and preference records.

## Added: recovery-first destructive actions

- Added a common safety dialog for destructive replacement and deletion workflows.
- Added an enabled-by-default recovery-download option when work exists.
- Added clear action-specific titles and confirmation labels.
- Added a damaged-active-project recovery screen.
- Added readable error summary and copyable technical details.
- Added Download recoverable data, Retry, Continue session only, and Back up and replace actions.
- Prevents autosave and page-unload handling from overwriting the damaged active record while recovery hold is active.
- Back up and replace downloads the damaged value before writing a valid blank project.

## Improved: persistence and deterministic generation

- Maintains the active project in IndexedDB, local fallback, and session memory according to browser availability.
- Retains the existing IndexedDB database name so earlier local project libraries remain discoverable.
- Migrates earlier active-project keys after successful recovery.
- Detects quota, security, invalid-state, and timeout failures.
- Continues in a clearly labeled session-only mode when persistent storage cannot be used.
- Made generated structure and agent identifiers deterministic so identical seeds and settings reproduce identical initial world fingerprints.
- Added project-level integrity information to saved and exported records.

## Improved: history and simulation reset

- History snapshots now include the event log, simulation baseline, and baseline event log.
- Undo and redo restore the world and its associated evidence consistently.
- Completed editing strokes remain grouped as one undoable transaction.
- Simulation reset restores the captured baseline while preserving project identity and camera orientation.

## Improved: interface clarity

- Disabled world-only controls in a blank project.
- Disabled Stop when the simulation is already paused.
- Added clear project-library storage status.
- Added damaged-project styling and actions.
- Shortened the header description so it remains readable without clipping.
- Limited concurrent notifications to three to prevent avoidable interface obstruction.
- Preserved the compact viewport, visible version, and zero document-level horizontal overflow at a 390 × 844 viewport.

## Verification result

The final build passed **64 of 64** static and Chromium workflow checks.

Verified behaviors include:

- blank cold start
- explicit demonstration load
- deterministic repeated generation
- viewport sculpting
- undo and redo
- yaw, pitch, roll, and zoom persistence
- simulation step and reset
- event-history preservation
- explicit save
- save–close–reopen recovery
- project duplicate, rename, open, and delete
- JSON export and import round trip
- malformed typed-array rejection
- schema 1 migration
- clear-all local data
- damaged-project recovery
- recovery download before replacement
- session-only fallback
- PNG capture
- compact-width rendering
- no page errors
- no browser-console errors

## Compatibility and boundaries

The build remains a self-contained, local-first HTML application without remote scripts, remote style sheets, account requirements, telemetry, advertising, or a mandatory backend.

This release completes Batch 2, not the entire GLYPHSCAPE roadmap. The current scene remains a projected three-dimensional height-field representation. Free-fly navigation, sparse voxel or block regions, object transformation, cinematic camera paths, advanced ASCII render passes, checkpoint branching, and animated recording remain future batches.
