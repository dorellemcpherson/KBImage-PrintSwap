# CLAUDE.md — KBImage Print Swap

Photoshop UXP panel (`manifest.json`, `index.html`, `src/app.js`). One view, Print Swap
(9 steps), plus Settings. All AI goes through Fal with one key: SAM 3.1
(`fal-ai/sam-3-1/image`) and Nano Banana Pro (`fal-ai/nano-banana-pro/edit`). Read
`README.md` for what the panel does and `docs/` for the retouchers' guide and part names.

## Build rules

1. **No ES modules, no top-level `require()`.** One non-module `<script src="src/app.js">`;
   every `require("uxp")` / `require("photoshop")` is inside a function. The delegated click
   listener attaches at the top of the IIFE, before anything that can throw.
2. **CSS stays inline** in `index.html`. No flexbox `gap`, no `position: fixed/sticky`, no
   pseudo elements, no `%` radii on pills. No inline `onclick=`, no Spectrum components.
3. **No `localStorage`, `TextEncoder` or `TextDecoder`.** Keys and settings live in
   `secureStorage` (`printswap.*`); strings ↔ bytes with `strToBytes` / `bytesToStr`.
4. **Every document change runs inside `core.executeAsModal`.**
5. **Every step runs through `runWithRecall`** (Accept / Re-run / Discard) and writes the
   session log. Nothing is kept without Accept.
6. **Layer names, groups and order match the team's print swap file.** Plug-in channels start
   with `KBPS`; temp layers and channels start with `kb_` / `KBPS_tmp`.

## Placing pixels (PNG route)

* `imaging.putPixels` / `putSelection` fail in real Photoshop ("The command “Get” is not
  currently available"). Pixels go in as a hand-built PNG → file in the plug-in data folder →
  `placeEvent` → fit to the target rect → rasterize.
* **Place OPAQUE PNGs for geometry.** A mostly transparent PNG lands shifted. Masks are placed
  as black / white images and read back as the composite's brightness.
* Every AI result uses the one placement routine (`plPlaceInModal`): target rect first, send
  padded to the model's REAL output size (Nano Banana's 9:16 at 2K is 1536 × 2752), place
  with one scale so it covers the frame, cut to the target, check the bounds.
* Photoshop fits a placed file INSIDE the canvas, and a placed smart object's bounds are
  rounded: read `smartObjectMore.transform` for the exact corners (`plSmartBounds`).
* In 16-bit documents the 8-bit `getPixels` of ONE layer is refused; `getLayerPixels8` falls
  back to the document's depth. Composite reads are fine.

## batchPlay limits

* A batchPlay `get` of a channel by name is refused. Use the DOM: `doc.channels` by name
  (`kbChannelObjs`), `channel.remove()`, `doc.selection.load(ch)`.
* Select and delete layers by `_target: [{ _ref: "layer", _id: id }]` — with the underscore.
  A bare `target` key is ignored and the command hits whatever is active.
* With a layer mask or alpha channel targeted, Delete reports "not currently available": call
  `selectRGBChannel()` first.
* A masked layer's DOM bounds are its MASK bounds.

## Testing

* Offline: `node tests/garment_types_test.js` and `node tests/placement_test.js` (they read
  the real functions out of `src/app.js`). The `tests/` folder is removed before handover.
* In Photoshop: after any change to `src/app.js` or `manifest.json`, **Remove the plug-in in
  UDT and Add it again** — Reload does not reliably pick up script changes. HTML / CSS-only
  changes may reload.
* Trace of the last SAM / Remove print run: `printswap-trace.txt` in the plug-in data folder.
  Session log: `printswap-session-<id>.jsonl` in the same folder.

## Git

Commit only when asked. Stage files by name.
