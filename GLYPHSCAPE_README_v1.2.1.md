# GLYPHSCAPE v1.2.1

GLYPHSCAPE is a local-first 3D ASCII world generator, editor, simulator, and capture studio.

Primary workflow:

**SEED → SHAPE → POPULATE → SIMULATE → OBSERVE → CAPTURE**

## v1.2.1 hotfix controls

- **Randomize Seed** changes the seed only; it does not change terrain parameters.
- **Orbit** returns to a perspective Orbit composition after Top or Isometric views.
- **Frame** centers and fits the complete world in Perspective Orbit.
- **Top** and **Iso** remain orthographic composition presets.
- Adaptive resolution may reduce detail while moving or during expensive renders, but returns automatically to full detail after the scene settles.

## Local-first behavior

Project data is processed locally. GLYPHSCAPE requires no account, telemetry, advertising, or backend service. Editable projects can be exported as JSON for durable backup and transfer.

## Run

Open `GLYPHSCAPE_v1.2.1.html` in a modern browser. Ordinary static hosting is also supported.
