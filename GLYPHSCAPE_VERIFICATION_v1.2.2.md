# GLYPHSCAPE v1.2.2 Verification

Targeted regression verification: **17 / 17 passed**.

Verified:
- visible v1.2.2 version
- demo begins in Perspective Orbit
- deliberate 1.75x Orbit zoom can be established
- Isometric -> Orbit restores Perspective
- Isometric -> Orbit restores prior zoom
- generation from Isometric restores prior Perspective composition
- generation from Isometric preserves prior zoom
- normal Perspective generation preserves deliberate zoom
- Frame deliberately returns to a fitted 1.00x view
- full-size ASCII resolution recovers after idle time
- no page errors
- no browser-console errors
- JavaScript syntax passes Node syntax checking
- no stale v1.2.1 application version remains
- scene vertical scale remains unchanged
- generation no longer contains the v1.2.1 forced zoom-reset path

The terrain generator was not modified by this hotfix.
