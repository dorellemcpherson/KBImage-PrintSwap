# KBImage Print Swap: user guide

How to install the panel and swap a print, step by step. For the rules and what to check before each Accept, see [Rules and best practices](print-swap-guide.md). Garment types and part names are in [parts-list.md](parts-list.md).

Screenshots are marked like this: 📷 `00-name.png`. They live in `docs/screenshots/`.

---

## 1. Before you start

You need:

* Photoshop 2022 (version 23.3) or newer
* The UXP Developer Tool (from Adobe Creative Cloud), until IT installs the panel for you
* A Fal API key (ask your admin)
* The **original** garment photo from the shoot: TIFF or PSD, 4000 px or more on the long edge, 8 or 16 bit RGB
* The **print file** at full resolution (the PDRF TIF), big enough to cover the garment without enlarging it

Small or web size photos give soft, pasted on results. See section 1 of the rules.

## 2. Install the panel

1. Open Photoshop.
2. Open the **UXP Developer Tool**.
3. Click **Add Plugin** and choose `manifest.json` in the KBImage Print Swap folder.
4. On the new row, click **•••** and choose **Load**.
5. In Photoshop, open **Plugins > KBImage Print Swap**. Dock the panel on the right, about 360 px wide.

📷 `02-install-udt.png` (UDT with the plug-in row loaded)

**After an update:** in UDT click **•••** > **Remove**, then **Add Plugin** again. The Reload button does not always pick up changes.

## 3. Add the Fal key (once per computer)

1. Click the **gear** at the top right of the panel.
2. Paste the key into **Fal API key**. Click **Show** to check it.
3. Click **Test Connection**. It should say the key works.
4. Click **Save**.
5. Click the **⇄** button to go back to Print Swap.

The key is stored in Photoshop's secure storage on this computer and is only sent to Fal.

📷 `03-settings.png` (Settings with the key saved)

**Other settings:**

* **Spend warning ($):** the running total turns red past this amount.
* **Edge bleed (px):** how far masked results reach past their edge. Leave at the default.
* **Per-action rates:** Fal's prices, used for the cost shown on each button. **Reset to defaults** puts them back.

## 4. How every step works

Each step has a header row with its number, name and state:

| State | Meaning |
|---|---|
| locked | An earlier step is not done yet |
| ready | You can run it |
| done ✓ | Accepted |

To work a step:

1. Click the step header to open it.
2. Click the step's main button.
3. A **progress bar** shows Queued, Rendering (with a timer) and Downloading while Fal works.
4. Check the result **at 100% zoom**.
5. Click one of:
   * **Accept:** keep it. The next step opens.
   * **Re-run:** delete it and run again with the current settings. This costs again.
   * **Discard:** delete it and stop. No cost.

📷 `04-accept-bar.png` (a step with Accept, Re-run and Discard showing)

The bar under the header shows the money spent this session. **Reset** starts it at $0.00.

## 5. The steps

### Step 1 · Background

1. Pick **White** (the team's final, default) or **Lighten**.
2. Tick **Hair** if the model's hair falls over the garment.
3. Click **Background**.
4. Check the edge of the model and the hair. Click **Accept**.

Settings: **Lighten opacity (%)**, **Edge softness**, **Refine in Photoshop**.

Hair is saved as a channel, **KBPS hair**. The HAIR layer is built in step 9.

📷 `05-step1-background.png`

### Step 2 · Garment

1. Open **Garment type** and pick the type (A to H). Not on the list? Pick **Other** (see 5a).
2. Click **Find garment**. SAM finds the garment and takes the hands out.
3. Check the marching ants at 100%: the whole garment, and nothing else.
4. Fix it if needed (see below), then click **Accept**.

**Fixing the garment.** Later steps use the saved channel **KBPS garment**, not the marching ants on screen. Use these buttons so your fix is saved:

* **+ Add selection:** select the missing area with any selection tool, then click it.
* **- Remove selection:** select what should not be garment, then click it.
* **Use selection as garment:** replaces the garment with your whole selection.

If the panel says "Your selection isn't saved to the garment", use one of these buttons.

Settings: **Grow into old-garment fringe (px)**, **Edge softness**, **Refine in Photoshop**.

📷 `06-step2-garment.png`

#### 5a. Other: a garment type that is not on the list

1. Pick **Other** in Garment type.
2. Tick the **trims** this garment has (piping, buttons, lace and so on).
3. Tick its **parts**. Missing one? Type it in **Add part** (ALL CAPS, 2 to 3 words, e.g. LEFT POCKET FLAP) and click **Add part**.
4. Run the whole swap. When it works, click **Save as type**, type a short name (e.g. Sleep shirt) and click **Save**. It shows in the list as I, J and so on.

📷 `07-step2-other.png`

**Changing the type after step 2** asks first and deletes steps 3 to 9. Click **Change type** or **Keep current type**.

### Step 3 · Remove print

1. Click **Remove old print**. Nano Banana Pro removes the print and keeps the type's trims. Result: the **CLEAN** layer.
2. Check at 100%: same shape, folds, seams and shadows. Lace and buttons still look like lace and buttons, in their own color.
3. Anything redrawn? Click **Re-run**. Otherwise **Accept**.

📷 `08-step3-clean.png`

### Step 4 · Trims

The step lists the trims of your type, e.g. "PAJAMA SET: PIPING, BUTTONS".

**Piping**

1. Check the mode: **Colored piping** (red, navy, pink) or **Neutral piping** (white, black, gray). It is picked for you; the line under the buttons says "Auto: …".
2. Click **Find piping**. Check that every piping line is in the selection and no skin.
3. Fix with **+ Add selection** / **- Remove selection**, or change the mode or **Tolerance** and **Re-run**.
4. Click **Accept**. The **PIPING** group is built on top.

**Buttons**

1. Click **Find buttons**. SAM looks at close-ups of the garment.
2. Add any it missed with **+ Add selection**. Click **Accept**. The **BUTTON** group is built on top.

Other trims of the type (lace, drawcord, bow, zipper) work the same way.

Settings and **Colors**: Tolerance, Edge margin, Button fit (Tight, Normal, Loose), Shrink button mask, Edge softness, **Piping color** (hex) and **Buttons** (Hue, Saturation, Lightness) to recolor trims.

📷 `09-step4-trims.png`

### Step 5 · Gray

1. Click **Make gray**. Result: **GREY exact**, the garment in neutral gray with its folds.
2. Check: even gray, folds visible, no old print showing. Click **Accept**.

Settings: **Target gray**.

📷 `10-step5-gray.png`

### Step 6 · Parts

1. Uncheck any part this garment does not have.
2. Click **Find parts**. SAM makes one mask per part.
3. Click a part's pill to select it. Fix it with **+ Add selection** / **- Remove selection**. **Show shapes** shows every part at once.
4. Click **Accept**. Each part gets its own group under **PARTS**.

Settings: **Edge softness**, **Apply to part**, **Refine in Photoshop**.

📷 `11-step6-parts.png`

### Step 7 · Print

1. Click **Choose print** and pick the print file. A thumbnail, the file name and its size show under it.
2. Set **Scale % (whole garment)**.
3. Click **Place print**. The print is tiled into every part, following each part's direction.
4. Adjust:
   * **Rotate print (whole garment):** ↺ 15°, ↺ 1°, ↻ 1°, ↻ 15°, 0° (reset), or type an **Exact angle** and **Apply**.
   * **One part:** click the part's pill in step 6, then use **Rotate print in this part** and **Scale % for this part**.
5. Click **Accept**.

To try another print, click **Swap print**. It keeps every setting.

📷 `12-step7-print.png` · 📷 `13-step7-rotate.png`

### Step 8 · Shading

1. Click **Build shading**. Folds and shadows come back over the print (the team's GREY group).
2. Check that the print follows the folds. Click **Accept**.

Settings: Brightness 7, Contrast 19, Exposure 0.10, Offset -0.0026, Gamma 0.96, Linear Burn 10%, Veil 10% (the team's values).

📷 `14-step8-shading.png`

### Step 9 · Finish

1. Click **Finish**. The lighten layer is hidden, **MERGED** is stamped on top, and **HAIR** goes over it.
2. Check the whole image at 100%. Click **Accept**. Save the PSD.

📷 `15-step9-finish.png` · 📷 `16-layers-final.png` (the Layers panel after Finish)

**Swapping again after Finish:** while the new print is waiting for Accept, MERGED is hidden so you can see it. On **Accept** a new MERGED is built. The one before stays below it, hidden, so you can compare. Only the 2 newest are kept.

## 6. Redo and Start over

* **Redo** (orange, on a done step): deletes that step and every later one, then sets that step to ready. Earlier steps stay.
* **Start over** (top of the steps): deletes every Print Swap layer and mask and the garment type. Your photo and your own layers stay. It asks first; **Show details** lists everything it will delete.

📷 `17-start-over.png`

## 7. Troubleshooting

| Problem | Fix |
|---|---|
| "Add your Fal API key in Settings" | Gear > paste key > Save. |
| A step will not run: "Accept or Re-run the preview that is waiting first" | Find the open step with Accept / Re-run and finish it. If none shows, use **Start over**. |
| The print, a rotation or a fix does not show | Check that an older MERGED is not on top. Hide it. |
| The print got onto the hands | Step 2: select the hands, **- Remove selection**, then **Redo** step 3. |
| White piping not found | Step 4: switch to **Neutral piping** and Re-run. |
| Remove print changed the garment shape or the trims | Re-run once. If it happens again, check the photo size and the garment type. |
| The result looks soft or pixelated | The photo or the print file is too small. Use the originals. |
| The panel looks stuck or out of date | UDT: Remove and Add the plug-in again, or close and reopen the document. |

## 8. Screenshot list

Take these at 100% panel zoom, panel docked about 360 px wide, Photoshop's dark theme. Save as PNG in `docs/screenshots/`.

| File | What to show |
|---|---|
| `01-panel-overview.png` | The whole panel, a few steps done |
| `02-install-udt.png` | UDT with the plug-in loaded |
| `03-settings.png` | Settings with the key saved |
| `04-accept-bar.png` | A step waiting with Accept, Re-run, Discard |
| `05-step1-background.png` | Step 1 open |
| `06-step2-garment.png` | Step 2 open, garment selected on the photo |
| `07-step2-other.png` | Step 2 with Other open |
| `08-step3-clean.png` | Photo after Remove print |
| `09-step4-trims.png` | Step 4 with piping found |
| `10-step5-gray.png` | Photo after Gray |
| `11-step6-parts.png` | Step 6 with part pills |
| `12-step7-print.png` | Step 7 with the print thumbnail |
| `13-step7-rotate.png` | Step 7 rotate controls with an angle set |
| `14-step8-shading.png` | Photo after Shading |
| `15-step9-finish.png` | Final image |
| `16-layers-final.png` | Layers panel after Finish |
| `17-start-over.png` | Start over confirm |
