# GLYPHSCAPE v1.2.2 Release Notes

## Camera framing regression hotfix

v1.2.2 corrects a regression introduced by v1.2.1's automatic world-framing logic.

### Fixed
- Normal world generation no longer resets Orbit zoom to 1.00x.
- Normal world generation no longer resets the user's perspective focus point.
- Returning from Top or Isometric to Orbit restores the prior perspective Orbit composition, including zoom and target.
- Generating while Top/Isometric is active returns to the remembered perspective composition rather than force-framing the world.
- The explicit Frame command remains available when the user intentionally wants the whole world centered and fitted.
- v1.2.1 adaptive-resolution and idle-frame timing fixes remain intact.
- Terrain generation and vertical scale are unchanged.

### Verification
A targeted Chromium regression suite passed 17/17 checks with no page or console errors.
