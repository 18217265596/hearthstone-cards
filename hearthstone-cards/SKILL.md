---
name: hearthstone_cards
description: Build or refine original Hearthstone-style golden collectible card animations from user-provided reference art, using procedural browser graphics, synchronized effects, and seamless looping.
---

# Hearthstone Golden Card Animation

Create a self-contained, polished golden-card animation around the reference art supplied for the current task. Typical deliverables are a single offline-ready index.html using Canvas 2D, WebGL, GLSL, or a practical combination of them. Keep the source readable, the card recognizable, and motion restrained enough to preserve its illustrated focal points.

The skill applies to requests to build or revise collectible-card animations, animated golden card showcases, or their effects. Follow the user's requested framework, file format, style, and loop duration when provided.

## Work from supplied art

- First inspect the attachment dimensions and locate the actual illustration within the canvas. Account for borders and flat margins before establishing logical drawing coordinates.
- Treat provided card art as a visual reference and potential source input. Determine what the user requests. For procedural coding, it is valid to sample colors, silhouettes, and details offline to construct a vector or parametric reconstruction. Do not make the runtime depend on the reference file if the user requests a self-contained file or zero external assets.
- When the user requires original procedural drawing or prohibits image reuse, construct and render the picture from code. A mesh, traced contours, sampled palette, derived masks, or brush paths fitted to the reference are still derived from the reference. Say this plainly if asked. Do not claim the artwork was independently invented or that it used no reference-derived data.
- Never conceal an embedded raster behind a claim of procedural authorship. When no source image is allowed in the output, keep runtime assets to code-generated Canvas, shader, and inline vector or numeric data, and make the asset pipeline clear.
- Match composition before detail. Set up a reference-coordinate system and record the key anchors for the silhouette, eyes, joints, waterline, and foreground frame.

## Build the image and material

Use a small number of layers with explicit ownership, ordered back to front:

1. Atmosphere and distant background.
2. Main silhouette and large forms.
3. Secondary mechanisms, eyes, panels, and appendages.
4. Water, liquid, smoke, and the foreground ledge.
5. Relighting, particles, foreground occlusion, and card hardware.

For code-painted illustration, combine broad color planes or a triangulated color mesh with contours and directional, locally shaded brush paths. Use higher detail density around eyes, seams, joints, rivets, and other focal landmarks. Add metal shading with broad glazes, bevel highlights, scratches, and subtle deterministic grain. Keep texture aligned to the shape. Avoid clean flat fills or ornamental details that obscure the original silhouette.

Prefer WebGL when per-pixel warping, lighting, fluid distortion, or large-resolution playback merits a shader. Use Canvas 2D for paths, sprites, masks, and particles. Keep the renderer simple, separate static drawing from animated passes, use cached textures or atlases where drawing them each frame would be wasteful, and limit device-pixel-ratio scaling when necessary for frame rate.

## Design the animation as a cycle

- Define normalized loop phase t = mod(elapsed, duration) / duration. Express every continuous oscillation, emitter path, flicker, water wave, mist drift, and periodic impact using integer multiples of 2πt or a phase function that is periodic over the complete loop.
- Give non-sinusoidal events smooth, deterministic periodic envelopes. A burst must fade to zero before a wrapped trajectory changes direction or resets. Rotate stable, seeded particle parameters across the cycle. Never rely on Math.random() inside frame rendering or wall-clock time for appearance.
- Use an art-directed cue timeline for impacts, charging, release, and settling. Use smooth periodic envelopes or periodic spline curves so the first and last frame match in content and lighting. Keep event counts and recurrence compatible with the selected cycle duration.
- Animate articulated appendages with a few visible joints, phase lag, and restrained overlapping motion. Keep high-value features registered to their surfaces.
- Shape the focal-eye animation, auxiliary eyes, power source, water reflection, and light response into an intentional buildup, release, and decay. Let the eye remain readable when effects overlap it.
- When screen-space particles should follow warped character parts, expose the same pose calculation or an anchor function from the shader rig. Evaluate emitter positions at the event's correct phase.

## Compose effects with a clear visual hierarchy

Build effects as independent passes that can be tuned without changing the illustration:

- Lightning may use midpoint displacement, branched paths, cached variants, and layered emission. Coordinate its route with real contact points. Pair major discharges with localized metal and mist illumination.
- Use sparks for short, high-speed contact effects and embers for warmer, slower drifting motion. Add readable tails, varied scale, and directional motion. Give large hero fragments enough size and contrast to read at the card's displayed size.
- Water can combine refracted texture, interrupted reflections, foam, droplets, impact wakes, and spreading rings. Use masks to keep spray behind submerged metal, appendages, or the foreground rim.
- Build fog from soft, irregular procedural density maps rather than a stack of identical translucent discs. Advect it smoothly and preserve contrast at the focal point.
- If the user says effects are excessive, reduce the simultaneous bright electrical area and branching density first. Reassign emphasis to compatible effects such as hot-metal glints, tumbling sparks, heat shimmer, caustics, steam, water splash, or localized reflections. Do not fill the freed visual space with another blanket overlay.
- Calibrate at final card size. Count competing focal events, maintain darker rests between peaks, and keep bloom from erasing illustrated detail.

## Deliver and verify

- Follow the user's exact requested output format. If they request one HTML file, inline executable code and generated numeric or vector data within that file. Do not bundle temporary source inputs, source rasters, external fonts, or dependencies unless requested.
- Keep only controls that serve preview or art review. For loop previews, a small seekable progress control and pause/replay affordance are useful when requested.
- Give the first recognizable preview as soon as it runs. Continue improving the requested effect level and composition rather than treating the first render as final.
- When a fidelity, smooth-loop, performance, or browser requirement is material to the request, validate the actual browser render at representative phases, including immediately before and after the loop seam. Check desktop and narrow layouts when both matter.
- Report measured results accurately. Separate procedural runtime drawing from reference-derived offline drawing data. Mention the playback device, rendering size, or fallback mode when a performance measurement depends on it.
