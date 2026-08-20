# GLYPHSCAPE v1.2.3 Verification

## Root-cause verification
The v1.1.0 and v1.2.2 Scene Core use the same world-to-geometry formula and both defaulted terrain relief to `world.n × 0.24`. Batch 4's more accurate character-cell renderer exposed this as visually too shallow.

## Controlled renderer test
A deterministic 64×64 synthetic radial mountain was rendered with identical camera, projection, grid (100×60), and viewport (1000×600).

| Vertical scale | World Y scale | Occupied character bbox | Screen-space height | Width |
| --- | ---: | --- | ---: | ---: |
| 0.24 | 15.36 | [10,18]–[84,59] | 42 rows | 75 cols |
| 0.42 | 26.88 | [10,7]–[84,59] | 53 rows | 75 cols |

The correction increases screen-space terrain relief by 11 rows (26.2%) without changing horizontal scale.

## Static verification
- Inline JavaScript syntax: PASS
- Visible version: v1.2.3
- Vertical Relief control present: PASS
- Default vertical relief 0.42: PASS
- Old hidden 0.24 default normalization path: PASS
- Procedural generator unchanged from v1.2.2: PASS by targeted edit scope

## Environment note
Direct headless Chromium screenshot generation from `file://` did not complete in this container. The renderer-level deterministic test above was executed directly against the shipped Scene Core and is the relevant verification for this defect.
