# GLYPHSCAPE v1.2.1 — Visual Regression Hotfix

This hotfix corrects presentation regressions introduced in v1.2.0 without changing the deterministic terrain-generation algorithm.

## Fixed

- Adaptive character resolution no longer treats idle time between event-driven renders as poor frame rate.
- Interaction timing resets when camera movement begins, avoiding misleading low frame-rate measurements after idle periods.
- Reduced frame-budget resolution now schedules a recovery render and returns to full detail after the scene settles.
- Orbit now restores a perspective Orbit composition after Top Down or Isometric views.
- New world generation escapes stale orthographic Top/Isometric state and recenters/fits the world in perspective Orbit.
- Added a **Frame** command to center and fit the complete world in perspective Orbit without resetting the world.
- New projects use neutral rendering defaults.
- The built-in Highland Reach demonstration explicitly resets to neutral exposure and perspective Orbit.
- Renamed **Randomize** to **Randomize Seed** to clarify that it changes only the deterministic seed, not terrain parameters.
- Added the missing `hasMeaningfulWork()` lifecycle guard used by replacement and recovery flows.
- Updated visible versioning consistently to v1.2.1.

## Deliberately unchanged

- Terrain-generation formulas
- World normalization
- Seed determinism
- Scene geometry architecture
- ASCII Shaded, Semantic, and Hybrid algorithms
- Project schema version 4
- Existing project import/export compatibility

## Verification

A targeted Chromium regression suite passed 17 of 17 checks, including same-seed determinism, neutral demo state, Isometric-to-Orbit restoration, generation auto-framing, adaptive-resolution recovery, idle-time behavior, and zero page/console errors.
