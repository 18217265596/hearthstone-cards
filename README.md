# Hearthstone Cards

This repository contains the hearthstone_cards Codex skill and a self-contained golden-card animation example based on the supplied Mechathun reference.

## Skill

hearthstone-cards/SKILL.md guides Codex through planning and producing polished, procedural golden-card animations. It covers reference-image analysis, layered Canvas and WebGL rendering, seamless cyclic motion, synchronized particles and environmental effects, and honest disclosure when procedural geometry or colors are derived from reference artwork.

The skill is useful for building or revising collectible-card animations from supplied artwork, especially when the result should run offline as a single HTML file.

## Example files

- 12s-golden-card.html is the first-round single-file animation preview. Open it in a modern browser.
- 12s-preview.mp4 is the rendered twelve-second animation preview.
- reference-mechathun.png is the supplied artwork used as the visual and procedural-painting reference.

The HTML runs without loading the PNG. Its painted scene was generated procedurally from offline-fitted mesh colors and vector brush strokes derived from the reference.

