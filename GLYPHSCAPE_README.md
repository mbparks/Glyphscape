# GLYPHSCAPE v1.0.0

GLYPHSCAPE is a local-first, self-contained browser instrument for generating, shaping, simulating, observing, and capturing three-dimensional (3D) American Standard Code for Information Interchange (ASCII) worlds.

## Open the application

Open `GLYPHSCAPE_v1.0.0.html` in a modern desktop browser. No installation, account, network connection, telemetry, or server is required for the core workflow.

## Core workflow

**GENERATE → SHAPE → SIMULATE → OBSERVE → CAPTURE**

1. Generate a deterministic world from a seed and terrain controls.
2. Navigate the world with the camera and inspect its terrain, climate, water, vegetation, structures, and agents.
3. Shape terrain and paint world properties with contextual tools.
4. Run, pause, step, or reset the fixed-step simulation and introduce creative events.
5. Capture the current result as text, an image, Scalable Vector Graphics (SVG), project data, or a standalone browser artifact, depending on the selected export.

## Included capabilities

- Deterministic seeded height-field generation
- Climate, biome, water, vegetation, fire, weather, structures, and agents
- Perspective and orthographic camera behavior
- Real-time glyph rendering with parallel canvas and text frames
- Explicit editing and navigation modes
- Fixed-step simulation controls and creative world events
- Undo and redo history
- Local project persistence with autosave and recovery behavior
- Indexed Database API (IndexedDB) persistence with local-storage fallback
- Blank-start and reproducible sample-world behavior
- JavaScript Object Notation (JSON) project import and export
- Plain-text, SVG, image, and standalone HyperText Markup Language (HTML) capture paths
- Responsive, keyboard-aware, high-contrast interface
- Visible semantic version number

## Data and privacy

Worlds and settings remain in the browser unless you explicitly export or download them. The application contains no analytics, advertising, behavioral tracking, or silent data transmission.

## Browser notes

The application is designed for current Chromium-, Firefox-, and WebKit-based desktop browsers. Browser privacy settings can limit persistent local storage. Exported project files remain the most portable backup.

## Recovery

If a session is interrupted, reopen the file in the same browser profile. The application attempts to restore the latest autosaved state. Use project export for durable backups or transfer between browsers.

## Release contents

- `GLYPHSCAPE_v1.0.0.html` — complete self-contained application
- `GLYPHSCAPE_README.md` — operating notes
- `GLYPHSCAPE_VERIFICATION.md` — generated release checks
- `GLYPHSCAPE_SOURCE_SPEC.md` — original project specification, when packaged

## Copyright

Green Shoe Garage, 2026.
