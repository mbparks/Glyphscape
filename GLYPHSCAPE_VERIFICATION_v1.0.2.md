# GLYPHSCAPE v1.0.2 — Batch 2 Verification

Generated: 2026-08-19T23:46:01Z

**Batch 2 result: PASS — 64 of 64 checks**

Version 1.0.2 passed static integrity checks, JavaScript syntax verification, real Chromium rendering and interaction, deterministic generation, save–close–reopen recovery, complete local project-library workflows, JavaScript Object Notation (JSON) round trips, schema migration, malformed-array rejection, recovery-first destructive behavior, storage-failure handling, Portable Network Graphics (PNG) capture, and compact-width review.

## Release artifact

| Property | Result |
|---|---:|
| Application | `GLYPHSCAPE_v1.0.2.html` |
| Size | 133,479 bytes |
| Secure Hash Algorithm 256-bit (SHA-256) | `3761a09445f156e505f45eda2f1ef2d39dd146025f79174008f88c56548b4574` |
| HyperText Markup Language (HTML) identifiers | 143 |
| Unique identifiers | 143 |
| Inline JavaScript blocks | 1 |
| Remote scripts | 0 |
| Remote style sheets | 0 |
| Visible version | `v1.0.2` |
| Project schema | `2` |

## Static verification

| Result | Check |
|---|---|
| PASS | Complete self-contained HTML document exists |
| PASS | All 143 element identifiers are unique |
| PASS | Inline JavaScript parses with `node --check` |
| PASS | Visible version and document title report `v1.0.2` |
| PASS | Schema constant reports version 2 |
| PASS | No remote script or style-sheet dependency is declared |
| PASS | No runtime network address is embedded; the World Wide Web Consortium SVG namespace is declarative only |
| PASS | Explicit New, Load Demo, Clear Current World, Reset Simulation, Stop, Delete Project, and Clear All Local Data controls exist |
| PASS | Recovery dialog and all recovery actions exist |

## Cold-start and deterministic-generation verification

| Result | Workflow evidence |
|---|---|
| PASS | Cold start opened a genuinely blank, non-demonstration project |
| PASS | World-only controls were disabled in the blank state |
| PASS | Stop was disabled while the simulation was paused |
| PASS | Load Demo generated the editable Highland Reach project only after explicit selection |
| PASS | Demonstration generation created terrain, structures, and agents |
| PASS | Repeated generation with identical seed and settings produced the same world fingerprint |

## Editing, history, camera, and simulation verification

| Result | Workflow evidence |
|---|---|
| PASS | Pointer-driven Sculpt changed the world through the visible canvas |
| PASS | One completed sculpt stroke created one history transaction |
| PASS | Undo restored the pre-sculpt world fingerprint |
| PASS | Redo restored the edited world fingerprint |
| PASS | Yaw accepted and retained `175°` |
| PASS | Pitch accepted and retained `-150°` |
| PASS | Roll accepted and retained `-152°` |
| PASS | Zoom accepted and retained `1.37×` |
| PASS | Step One Day advanced simulation time |
| PASS | Rainstorm event was recorded in the event log |
| PASS | Reset Simulation restored baseline day zero |
| PASS | Reset Simulation preserved project identity and full camera orientation |

## Save, reopen, and project-library verification

| Result | Workflow evidence |
|---|---|
| PASS | Control/Command + S reached Saved locally state |
| PASS | Saved record used schema 2 and contained a matching world fingerprint |
| PASS | Active project was stored in the local fallback and IndexedDB project library paths |
| PASS | A fresh Chromium document restored the saved project identifier and name |
| PASS | Reopen preserved world fingerprint, simulation day, event log, yaw, pitch, roll, and zoom |
| PASS | Project library duplicated the current project with a new identity |
| PASS | Project library renamed the duplicate |
| PASS | Project library duplicated and deleted a selected branch |
| PASS | Project library opened the renamed branch through the recovery-capable replacement flow |
| PASS | New created a separate blank project identity rather than merely clearing content |

## Import, export, and migration verification

| Result | Workflow evidence |
|---|---|
| PASS | JSON export downloaded a complete schema-2 project |
| PASS | Exported integrity fingerprint matched the current world |
| PASS | JSON import reproduced the exported world fingerprint |
| PASS | Import preserved project identifier, name, creation time, camera, simulation time, and event log |
| PASS | A Base64 field with an incorrect decoded byte length was rejected |
| PASS | Rejected import left the current project unchanged |
| PASS | A schema-1 project migrated to schema 2 |
| PASS | Migrated project received a valid serialized simulation baseline |
| PASS | PNG capture produced a valid PNG signature |

## Destructive-action and recovery verification

| Result | Workflow evidence |
|---|---|
| PASS | Clear All Local Data opened a new blank unsaved session |
| PASS | Clear All Local Data removed GLYPHSCAPE active-project and preference keys |
| PASS | Clear All Local Data emptied the IndexedDB project store |
| PASS | A corrupted active project opened recovery mode instead of crashing |
| PASS | Recovery hold left the damaged raw value untouched |
| PASS | Recovery screen displayed a readable field-specific error and technical details |
| PASS | Back Up and Replace downloaded the damaged raw record first |
| PASS | Replacement wrote a valid schema-2 blank project and cleared recovery hold |

## Storage-failure verification

| Result | Workflow evidence |
|---|---|
| PASS | Unavailable IndexedDB plus quota-blocked local storage produced Session only state |
| PASS | Session-only mode still generated and rendered a usable world |
| PASS | No generic initialization failure occurred |

## Compact-width verification

The final build was tested at a 390 × 844 viewport.

| Result | Workflow evidence |
|---|---|
| PASS | Document horizontal overflow measured 0 pixels |
| PASS | The `v1.0.2` version chip remained visible |
| PASS | Left and right panels began collapsed |
| PASS | The rendered world viewport remained visible and larger than 250 × 250 pixels |
| PASS | No page or browser-console error occurred |

## Visual review

The final desktop, compact-width, and damaged-project recovery screens were inspected directly.

- The viewport remains the dominant workspace.
- The header description no longer clips at the tested desktop width.
- Project and simulation actions use direct labels rather than ambiguous icons.
- Destructive actions are visibly distinct.
- World-only controls accurately disable while no world exists.
- Concurrent notifications are limited to three.
- The recovery dialog presents the error before technical detail and offers both nondestructive and repair options.
- Compact width retains the version, viewport, mode controls, and panel access without document-level horizontal overflow.

## Browser and storage test method

The container administrator blocked direct navigation to local files, local HyperText Transfer Protocol (HTTP) origins, and external addresses. Automation therefore used system Chromium with `page.set_content()` to load the final unmodified self-contained HTML document.

The application’s local-storage and IndexedDB transaction paths were exercised using test-only in-memory shims injected before application startup. The shims exposed storage contents so the tests could simulate closing and reopening a browser document, inspect project records, inject corruption, trigger quota failure, and verify deletion. They were not inserted into or shipped with the application.

## Verification limitations

The following remain outside this Batch 2 verification:

- Native persistent-origin IndexedDB behavior in the container
- Firefox and WebKit execution
- Assistive-technology testing with screen readers
- Physical touch-device testing
- Long-duration simulation and storage-quota stress testing
- Cross-version testing beyond the implemented schema 1 to schema 2 migration

These limitations do not negate the passing Chromium workflows, but they should be addressed before a broader public compatibility claim.

## Exit-gate determination

Batch 2 is accepted because a user can:

1. Start from an intentional blank project.
2. Generate or explicitly load a deterministic world.
3. Edit and undo it.
4. Preserve full camera orientation and simulation evidence.
5. Save, close, and reopen the project.
6. Rename, duplicate, open, and delete local projects.
7. Export and reimport a complete project without data loss.
8. Migrate a schema-1 project safely.
9. Reject malformed array data without damaging current work.
10. Recover or replace damaged local data without silent overwrite.
11. Continue working in session-only mode when persistent storage is unavailable.
12. Use the compact viewport without document-level horizontal overflow.

No uncaught page error or browser-console error occurred during the tested workflows.
