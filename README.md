# KBImage Print Swap

A Photoshop panel that replaces the print on a garment photo. It builds the same layers, in
the same order and with the same names, as the Photoshop team's print swap file, and uses AI
only where it saves time: SAM 3.1 finds the garment, its trims and its parts, and Nano Banana
Pro removes the old print. Every step lands as new layers or channels in your document, and
nothing is kept until you click **Accept**. All AI runs through Fal, so the panel needs one
key: a Fal API key.

![Print Swap panel](docs/screenshots/panel.png)

## What you need

* Photoshop 2022 (version 23.3) or newer, with 8-bit RGB documents
* The UXP Developer Tool (UDT, from Adobe Creative Cloud)
* A Fal account and a Fal API key (fal.ai, then Dashboard, then Keys)

## Install in the UXP Developer Tool

1. Open Photoshop.
2. Open the UXP Developer Tool.
3. Click **Add Plugin** and choose the `manifest.json` file in this folder.
4. Click the **•••** menu on the new row and choose **Load**.
5. In Photoshop, open **Plugins > KBImage Print Swap**.

After any change to `src/app.js` or `manifest.json`, **Remove** the plug-in in UDT and
**Add** it again. The Reload button does not reliably pick up script changes.

## Enter your Fal key

1. Click the gear icon at the top right of the panel.
2. Paste your Fal key into **Fal API key**.
3. Click **Save**.

The key is stored on this computer in Photoshop's secure storage and is sent only to Fal.
The panel talks to these addresses only (all Fal): `queue.fal.run`, `fal.run`, `*.fal.run`,
`rest.alpha.fal.ai`, `*.fal.ai`, `fal.media`, `*.fal.media`, and `storage.googleapis.com`
(where Fal hosts some results).

![Settings](docs/screenshots/settings.png)

## The 9 steps

Open one step at a time, run it, check the result at 100%, then click **Accept** (keep it),
**Re-run** (delete it and run again with the current settings) or **Discard** (delete it and
stop). Accept closes the step and opens the next.

| Step | What it does | AI |
|---|---|---|
| 1 Background | White (the team's final) or Lighten behind the model. Optional Hair mask. | Photoshop Select Subject; SAM 3.1 if that fails or for Hair |
| 2 Garment | Pick the garment type (A to H, or Other), then **Find garment**. Fix it with **+ Add selection**, **- Remove selection** or **Use selection as garment**. | SAM 3.1 |
| 3 Remove print | Removes the old print and keeps the type's trims. Result: CLEAN. | Nano Banana Pro |
| 4 Trims | Finds piping, buttons, lace and the other trims of the type; each gets its own group on top. | SAM 3.1 (piping: none) |
| 5 Gray | The garment made neutral gray, folds kept. Result: GREY exact. | none |
| 6 Parts | One mask and one shape layer per part of the type. Uncheck parts this garment does not have. | SAM 3.1 |
| 7 Print | Choose the print file; it is tiled into every part, following each part's direction. **Swap print** puts a new file in with the same settings. | none |
| 8 Shading | Brings the folds and shadows back over the print (the team's GREY group). | none |
| 9 Finish | Hides the lighten layer and stamps MERGED (plus HAIR on top). | none |

![Steps](docs/screenshots/steps.png)

* The garment type is saved with the document. Changing it after step 2 resets steps 3 to 9,
  after a confirm.
* **Redo** on a finished step deletes that step and every later one. **Start over** deletes
  every Print Swap layer and channel and the garment type, keeping your photo. Both ask first.
* For a style not in A to H, pick **Other**, check its trims and parts (or add a part), and
  click **Save as type** to keep it as I, J and so on.

The full guide is [docs/print-swap-guide.md](docs/print-swap-guide.md); the garment types and
part names are in [docs/parts-list.md](docs/parts-list.md).

## Costs

Every button shows its price, and the bar under the header keeps a running total for the
session (**Reset** starts it again). Nano Banana Pro is $0.15 per image ($0.30 at 4K); SAM
3.1 is $0.005 per request. Prices are Fal's list prices and can be changed in Settings. Set a
**Spend warning** in Settings and the total turns red past it. The money is charged to your
Fal account.

While Fal works, a thin bar under the button you clicked shows Queued, Rendering (with a
timer) and Downloading. It turns red if the run fails.

## Help

Set `HELP_URL` at the top of the Help section in `src/app.js` to your team's help page; a
**Help** link then shows in Settings.

## Screenshot slots

Add these files to `docs/screenshots/` (PNG, panel docked at about 360 px wide):

* `panel.png` — the panel with step 2 open
* `settings.png` — Settings with the key saved
* `steps.png` — all nine steps, a few done

## Files

* `manifest.json` — plug-in id `com.komar.kbimage.printswap`, version 0.19.0
* `index.html` — the panel (styles inline)
* `src/app.js` — all of the panel's code
* `icons/` — `logo.png` (header) and the panel / plug-in icons; replace them with your own
  artwork at the same sizes (logo 600 × 600, panel 23 and 46 px, plug-in 48 and 96 px)
* `docs/` — the guide and the parts list
