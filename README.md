# Second Skin

Sci-fi makeup and masks for the face, in the browser. Every look adds something on top of the face; none of them smooth, slim or reshape it.

## Looks

- **Faceted chrome:** a low-poly mirror-metal mask whose reflections slide as you turn your head. The eyes and mouth stay open.
- **Circuit tattoo:** glowing traces along the brow, cheekbones and jaw, with points of light running along them.
- **Holo veil:** a scanning wireframe that floats over the skin, with a slight colour split.
- **Prism glam:** iridescent lids, a graphic wing, holographic lips and cheek gems.

Each look has intensity and hue sliders, and a Snapshot button that saves a still.

## Privacy

Face tracking runs entirely on the device. No image or landmark data leaves the browser.

## Run it

The camera only works from `https://` or `localhost`, so you can't open `index.html` straight from disk. Instead:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

To put it online, turn on **GitHub Pages** (Settings → Pages → Deploy from branch → `main` / root). It will then be live at `https://claudiamiranda.github.io/second-skin/` with the camera working.

## How it works

- Face landmarks come from MediaPipe Face Mesh (468 points plus irises). The files are copied into the repo, so nothing loads from Google at runtime.
- `fm_assets.js` holds the model graph and weights as base64. A small shim in `index.html` serves them to MediaPipe from that file instead of fetching them, so the page also runs on hosts that only serve common file types.
- Each look is a plain Canvas 2D function in `index.html` (`chrome`, `circuit`, `veil`, `prism`) that draws from the landmark positions. To add a look, write a new function and register it in `LOOKS` and `DRAW`.

## Credits

The MediaPipe Face Mesh files (`face_mesh*.js`, `*.wasm`, `fm_assets.js`) are © Google, Apache License 2.0, from the `@mediapipe/face_mesh` npm package (0.4.1633559619).
