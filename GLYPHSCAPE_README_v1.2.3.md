# GLYPHSCAPE v1.2.3

Visual-relief correction release for the 3D ASCII World Simulator.

## Key change
Terrain vertical relief is now an explicit render/scene control instead of a hidden constant. The default changed from 0.24× world size to 0.42× world size so generated terrain retains clear three-dimensional relief through the character-cell renderer.

Use **ASCII Vision → Vertical relief** to tune the world from 0.18× to 0.80×. Existing projects that still contain the old unexposed 0.24 default are normalized to 0.42 when loaded.

Camera composition, seed determinism, world arrays, simulation grids, project safety, and ASCII render modes remain unchanged.
