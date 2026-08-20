# GLYPHSCAPE v1.2.1 Verification

## Targeted regression focus

The v1.2.1 verification concentrated on the defects observed after v1.2.0:

1. Perceived flattening and reduced world detail.
2. Adaptive resolution remaining at reduced detail.
3. Orthographic Isometric/Top state persisting into later generations.
4. Orbit failing to restore perspective framing.
5. Demonstration/render styling carrying unintended exposure or camera state.
6. Replacement-flow lifecycle errors.

## Results

17 / 17 targeted browser checks passed.

- Visible version is v1.2.1.
- **Randomize Seed** label is explicit.
- Built-in demonstration opens in Perspective Orbit.
- Demonstration exposure is 0.0 EV.
- Same seed/settings produce the same world fingerprint.
- Isometric uses orthographic projection as intended.
- Selecting Orbit after Isometric restores perspective projection.
- Orbit preset state is restored.
- Generating from an Isometric state automatically returns to Perspective Orbit.
- Generation recenters the world target.
- Generation restores fitted zoom.
- Adaptive resolution returns to full scale after motion.
- Adaptive reason returns to `full` after settling.
- An idle interval does not cause a frame-budget reduction on the next render.
- **Frame** restores Perspective Orbit framing.
- No page errors occurred.
- No browser-console errors occurred.

## Test environment

Chromium was run headlessly using the system browser executable. The application was loaded with `page.set_content()` because local persistent-origin navigation is restricted in the build environment. Persistent IndexedDB refresh/reopen behavior was not requalified in this hotfix; project schema and storage architecture are unchanged from v1.2.0.
