# Balling

Still Balling — an interactive Three.js sculpture generated from an ASCII silhouette.

Live: https://arrojchino.github.io/balling/
Source: https://github.com/arrojchino/balling

## What it does

An ASCII silhouette is traced into contours, extruded as real geometry and rendered
as a floating metallic sculpture. The scene adds a fresnel rim glow, an orbiting
particle field, a soft contact shadow, bloom and a vignette. Drag to rotate,
scroll to zoom, and export a 2048px PNG.

## Controls

- Drag to rotate the sculpture.
- Scroll or pinch to zoom.
- Use the export control to save a 2048px PNG.

## Verification

Tested in Chromium: the WebGL scene loads with no errors, the rim, particles,
shadow and post-processing are visible, and the export control writes a PNG.
