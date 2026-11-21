# Balling

Still Balling: an ASCII silhouette inflated into a real 3D sculpture you can restyle, light, poke and throw basketballs at.

Live: https://arrojchino.github.io/balling/
Source: https://github.com/arrojchino/balling

## What it does

The page reads a braille ASCII drawing and builds the sculpture from it in the browser. There are no models, no image files and no build step. The only download is Three.js r170, pinned on jsDelivr.

1. **Smooth outline.** Each braille dot becomes a soft Gaussian splat on a grid three times finer than the dots. The outline is the iso-line of that field, so the stair-steps of the source turn into continuous curves. Dots are spaced equally in x and y, which keeps the ball in the drawing round.
2. **Inflation.** The shape is inflated by solving a Poisson equation inside the outline (red-black SOR, with the boundary placed exactly on the smooth outline) and taking the square root of the result. Thin limbs come out as round tubes, the ball as a sphere and the body as a rounded mass.
3. **Mesh.** Front and back surfaces are triangulated over the outline with marching squares, with normals taken from the analytic surface, so nothing is faceted. The result is about 47k vertices and 94k triangles.

## Finishes, light and effects

- **Seven finishes:** Chrome, Gold, Shiny (holographic chrome), Lava (animated crust with glowing cracks), Glass (refraction with dispersion), Obsidian and Neon (hologram scan lines). Switching finishes dissolves from one to the other along a noise edge.
- **Four lighting looks:** Studio, Sunset, Club and Noir. Each look sets the key, rim and fill lights, the backdrop, the reflections and the exposure, and cross-fades to the next one. Reflections come from a procedural photo studio: a dark room with softboxes, rendered once into an environment map.
- **Effects you can toggle:** Glow (bloom), Sparkles, Embers, Halo rings, Spotlights (sweeping beams with visible cones), Ball rain and Film (grain, chromatic aberration and vignette).
- **Random:** Shuffle picks a new finish, look and effect mix, and the sculpture hops and spins. Auto shuffles every seven seconds.

## Physics

- Drag to spin. A flick keeps it turning with inertia, then it settles back to face the viewer. Pitch springs back to rest.
- Clicking the sculpture pokes it: a ripple travels across the surface, the body squashes and stretches, and the hit adds spin.
- Clicking empty space throws a basketball along a ballistic arc to the point you clicked.
- Basketballs collide with the sculpture's real inflated shape, with each other, the podium and the floor. A low lip on the floor keeps them in view. Hard hits make the sculpture ripple and turn a little. Fixed 120 Hz steps.

## Controls

- Drag to spin, click to poke or throw, scroll or pinch to zoom.
- Keys: `S` shuffle, `A` auto, `M` next finish, `L` next light, `B` drop balls, `Space` pause the sway, `R` reset.
- Save PNG renders a 2048 x 2048 image.
- The sculpture stays centred between the title and the control dock; Hide controls frees the whole screen.

## Security and performance

- The scene runs in a sandboxed `srcdoc` iframe (`allow-scripts` only) under a CSP that allows scripts from jsDelivr and nothing else: no `connect-src`, no workers, no external images.
- Shaders for every finish compile up front, and the light count never changes, so switching never stutters on a shader compile.
- A sanitize pass removes NaN or Inf pixels before bloom, so one bad pixel cannot black out the frame.
- Resolution adapts to the frame rate (0.75x to 1.75x pixel ratio). Rendering pauses while the tab is hidden.

## Verification

Checked in Chromium at 1600 x 900 and 390 x 844 against a local server:

- The scene reports `ready` with no errors or console warnings: 94,248 triangles and 56 fps in the test browser, and the sculpture stays inside the frame.
- Every finish, light look and effect was switched and captured in screenshots.
- Shuffle and Auto change the finish and look. Poke, throw and a 16-ball drop behave as described.
- Save PNG returns a 2048 x 2048 image.
