# GLYPHSCAPE Project Schema Version 2

## Purpose

GLYPHSCAPE project files are JavaScript Object Notation (JSON) documents that preserve an editable world, camera, tool state, simulation baseline, event history, and project metadata.

Schema version 2 is used by GLYPHSCAPE v1.0.2.

## Top-level record

| Field | Type | Purpose |
|---|---|---|
| `format` | string | Must equal `GLYPHSCAPE_PROJECT` |
| `version` | string | Application version that wrote the record |
| `schemaVersion` | integer | Project schema; must migrate to `2` |
| `project` | object | Identity, name, timestamps, sample flag, and schema metadata |
| `generation` | object | Seed and procedural-generation controls |
| `view` | object | Camera orientation, projection, glyph style, palette, and layer visibility |
| `tool` | object | Current interaction mode and editing settings |
| `simulation` | object | Speed, fixed-step duration, baseline world, and baseline event log |
| `world` | object | Current world arrays, entities, clock, weather, and blank-state flag |
| `eventLog` | array | Current project event history |
| `integrity` | object | Optional world fingerprint and algorithm name |

## Project metadata

```json
{
  "id": "unique-project-id",
  "name": "Project name",
  "createdAt": "2026-08-19T23:00:00.000Z",
  "updatedAt": "2026-08-19T23:05:00.000Z",
  "schemaVersion": 2,
  "isSample": false
}
```

Rules:

- `id` is limited to 120 characters.
- `name` is limited to 80 characters and cannot normalize to an empty value.
- Timestamps are normalized to valid International Organization for Standardization (ISO) date-time strings.
- `isSample` identifies intentionally loaded demonstration content.

## Generation settings

| Field | Accepted value |
|---|---|
| `seed` | string, maximum 64 characters |
| `preset` | `highlands`, `archipelago`, `canyon`, `plateau`, `plains`, or `crater` |
| `resolution` | numeric world resolution from 8 through 256 |
| `seaLevel` | number from 0 through 0.7 |
| `roughness` | number from 0.1 through 1 |
| `climate` | `temperate`, `arid`, `tropical`, `polar`, or `continental` |
| `settlements` | number from 0 through 50 |

Unrecognized optional values use safe defaults after migration and validation.

## View and camera

Camera angles are stored in radians.

| Field | Purpose |
|---|---|
| `yaw` | horizontal world rotation |
| `pitch` | vertical world rotation without a fixed top or underside clamp |
| `roll` | rotation around the viewing axis |
| `zoom` | view magnification, normalized from 0.1 through 10 |
| `panX`, `panY` | viewport offsets |
| `projection` | `perspective` or `orthographic` |
| `glyphSet` | built-in glyph-ramp identifier |
| `palette` | built-in palette identifier |
| `detail` | render-detail value from 0.1 through 1 |
| `color` | biome-color enable state |
| `shadow` | depth-shading enable state |
| `layers` | visibility flags for terrain, water, vegetation, structures, agents, and weather |

Yaw, pitch, and roll are normalized to continuously wrapping angles when a project is read.

## Tool state

| Field | Accepted value |
|---|---|
| `mode` | `orbit`, `inspect`, `sculpt`, or `paint` |
| `sculptAction` | `raise`, `lower`, or `smooth` |
| `radius` | 1 through 20 |
| `strength` | 0.01 through 1 |
| `paintLayer` | `moisture`, `temperature`, `vegetation`, `water`, or `fire` |
| `paintValue` | 0 through 1 |
| `paintRadius` | 1 through 20 |

## World representation

`world.n` is the width and depth of the square simulation grid. Valid values are integers from 8 through 256. Every grid array contains exactly `n × n` elements.

### Encoded typed arrays

Arrays are serialized as Base64 strings containing the raw typed-array bytes.

| Field | Runtime type | Required decoded byte length |
|---|---|---:|
| `height` | 32-bit floating-point array | `n × n × 4` |
| `moisture` | 32-bit floating-point array | `n × n × 4` |
| `temperature` | 32-bit floating-point array | `n × n × 4` |
| `water` | 32-bit floating-point array | `n × n × 4` |
| `vegetation` | 32-bit floating-point array | `n × n × 4` |
| `fire` | 32-bit floating-point array | `n × n × 4` |
| `biome` | unsigned 8-bit integer array | `n × n` |

Import rejects a field when:

- it is not a Base64 string;
- Base64 decoding fails;
- the decoded byte length does not exactly match the expected data type and world resolution; or
- reconstruction cannot produce the required typed array.

Malformed arrays are not silently replaced with empty terrain.

### Other world fields

| Field | Type | Purpose |
|---|---|---|
| `structures` | array | Normalized structure entities with bounded coordinates and values |
| `agents` | array | Normalized lightweight agents with bounded coordinates and values |
| `day` | number | Current simulation day |
| `weather` | string | Current stylized weather state |
| `weatherDays` | number | Remaining duration or transition state used by weather logic |
| `isBlank` | boolean | Whether the world contains generated or imported content |

## Simulation record

```json
{
  "speed": 1,
  "stepMs": 550,
  "baselineWorld": { "...": "serialized world" },
  "baselineEventLog": []
}
```

- `speed` is normalized from 0.25 through 100.
- `stepMs` is normalized from 50 through 5000 milliseconds.
- `baselineWorld` uses the same strict world representation as `world`.
- `baselineEventLog` is normalized using the same rules as the current event log.

Reset Simulation restores `baselineWorld` and `baselineEventLog` while retaining project identity, generation controls, and camera state.

## Event log

Each event entry is normalized to:

```json
{
  "at": "2026-08-19T23:05:00.000Z",
  "day": 1,
  "message": "A sustained rainstorm crossed the world.",
  "kind": ""
}
```

The imported record retains at most 500 entries. Messages are limited to 500 characters and kind labels to 30 characters.

## Integrity fingerprint

A schema-2 record may contain:

```json
{
  "algorithm": "FNV-1A-32",
  "worldHash": "d1565073"
}
```

The fingerprint covers:

- schema-specific world marker
- resolution
- every encoded grid array
- structures
- agents
- simulation day
- weather
- weather duration
- blank-state flag

This fingerprint is a corruption and consistency check. It is not a cryptographic signature and does not prove authorship or protect against intentional modification.

## Migration from schema 1

The schema 1 to schema 2 migration:

1. Copies the existing world into `simulation.baselineWorld`.
2. Copies the normalized event log into `simulation.baselineEventLog`.
3. Adds default simulation speed `1`.
4. Adds fixed-step duration `550` milliseconds.
5. Sets the top-level and project schema versions to `2`.
6. Runs the complete schema-2 validator and normalizer.
7. Recomputes the world-integrity fingerprint.

A future schema greater than 2 is rejected because this release cannot safely infer fields or migration behavior it does not understand.

## Local storage keys

| Storage | Name | Purpose |
|---|---|---|
| IndexedDB database | `glyphscape-projects-v1` | Project library; database name retained for compatibility |
| IndexedDB object store | `projects` | Project records keyed by `project.id` |
| Local storage | `glyphscape.active.v2` | Active-project fallback |
| Local storage | `glyphscape.settings.v1` | Compact interface preferences |
| Legacy active key | `glyphscape.active.v1` | Read-only migration candidate; removed after successful save to v2 |

The application also maintains in-memory session maps. These preserve operation during the current tab session when persistent browser storage is unavailable.

## Import replacement safety

Validation and migration occur before the current project is replaced.

- Importing into an empty `Untitled World` proceeds directly.
- Importing over meaningful work opens the recovery-capable replacement confirmation.
- A failed parse, migration, array validation, or integrity check leaves the current project unchanged.
- A damaged active local record enters recovery hold and is not overwritten by autosave or page-unload handling.
