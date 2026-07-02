# FoldLab - 2D Dieline to 3D

A browser-only challenge solution that reads a color-coded carton dieline, builds a Three.js panel hierarchy, and visibly folds the net into a closed box.

## Run locally

```bash
npm install
npm run dev
```

Open `http://localhost:5173`. The app accepts PNG, JPG, SVG, and single-page PDF inputs. Use **Load sample carton** for the built-in straight tuck-end demo.

## How it works

1. `dieline-parser.js` rasterizes the source and classifies red cut lines, green crease lines, and blue score lines.
2. The detected line density and source proportions produce a normalized carton panel specification.
3. `box-scene.js` creates each panel as a thin mesh attached to a `THREE.Group` hinge positioned on its crease.
4. Folding is rotation around those local hinge axes. For example, the right wall uses `Ry(-pi/2 * t)`, and its child front panel applies a second `Ry(-pi/2 * t)` to close the opposite face.
5. Top, bottom, glue, and tuck flaps fold in later phases so the closing sequence stays readable. The timeline directly controls `t` from `0` (flat) to `1` (closed).

## Structure

- `src/dieline-parser.js` - file loading, PDF rasterization, line classification, panel estimates
- `src/box-scene.js` - renderer, OrbitControls, materials, hinge graph, fold transforms
- `src/main.js` - upload flow, state, metrics, playback, timeline controls
- `src/styles.css` - responsive dark glass interface

## Learning documentation

- [`docs/BEGINNER_GUIDE.md`](docs/BEGINNER_GUIDE.md) - concepts, architecture, data flow, and fold math
- [`docs/CODE_WALKTHROUGH.md`](docs/CODE_WALKTHROUGH.md) - file-by-file and line-by-line explanation
- [`docs/MODIFICATION_GUIDE.md`](docs/MODIFICATION_GUIDE.md) - safe recipes for changing the parser, box, animation, and UI
- [`docs/PRESENTATION_GUIDE.md`](docs/PRESENTATION_GUIDE.md) - demo script, code walkthrough, and likely questions

## Production

```bash
npm run build
npm run preview
```
