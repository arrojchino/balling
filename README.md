# Balling

Still Balling — an interactive Three.js sculpture generated from an ASCII silhouette.

Live: https://arrojchino.github.io/balling/
Source: https://github.com/arrojchino/balling

## What it does

An ASCII silhouette is traced into contours, extruded as real geometry and rendered
as a rotating metallic sculpture. No models, no textures, no build step.

## Controls

- Drag to rotate the sculpture.
- Scroll or pinch to zoom.
- Use the export control to save a 2048px PNG.

## Verification

Tested in Chromium: the WebGL scene loads, drag rotation and zoom respond, and the
export control writes a PNG. The page is a single HTML file with one inline script.
