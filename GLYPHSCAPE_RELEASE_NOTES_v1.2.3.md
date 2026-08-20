# GLYPHSCAPE v1.2.3 Release Notes

## Fixed
- Corrected the persistent flat/squished world appearance at the geometry level.
- Increased the default hidden terrain vertical-scale factor from 0.24 to 0.42.
- Added an explicit **Vertical relief** control to ASCII Vision (0.18–0.80).
- Legacy projects using the old hidden 0.24 default are upgraded to 0.42 on normalization.
- Preserved camera composition during ordinary generation; **Frame** remains an explicit action.
- Preserved adaptive-resolution recovery fixes from v1.2.1/v1.2.2.
- Updated visible and internal version references consistently to v1.2.3.

## Not changed
- Procedural seed algorithm
- Terrain height arrays
- Climate/simulation arrays
- 360-degree camera orientation
- Scene depth testing
- Shaded/Semantic/Hybrid ASCII modes
