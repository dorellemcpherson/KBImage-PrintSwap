# KBImage Print Swap: user guide

How to install the panel and swap a print, step by step. For the rules and what to check before each Accept, see [Rules and best practices](print-swap-guide.md). Garment types and part names are in [parts-list.md](parts-list.md).

Screenshots live in `docs/screenshots/`. Ones still to be taken are marked like this: 📷 `00-name.png`.

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

The panel has a **Print Swap | Settings** toggle under the title (the view shown is the highlighted side). With no key saved, the panel opens on Settings with "Add the Fal key to start"; once a key is saved it opens on Print Swap.

1. Open the **Settings** tab.
2. Paste the key into **Fal API key**. Click **Show** to check it.
3. Type an **admin PIN** (4 or more characters). It locks the key.
4. Click **Test Connection**. It should say the key works.
5. Click **Save**.
6. Click the **Print Swap** tab.

The key is stored in Photoshop's secure storage on this computer and is only sent to Fal.

**Locked by admin.** Once the key is saved, Settings shows "Key saved ✓, locked by admin": the key can't be shown, edited, saved or tested, and the spend warning, edge bleed and rates are read-only. Retouchers still see the session cost and its Reset on Print Swap. To change settings, click **Admin** and type the PIN: Settings stays unlocked until the panel reloads. The PIN itself is never stored, only a one-way hash of it, in Photoshop's secure storage. **Forgot the PIN?** **Reset key** (click it twice) clears the key and the PIN, and the panel asks for a new key. It never shows the old key.

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

### Step 0 · Upscale (optional)

Step 0 never runs by itself. Step 1 stays locked until you Accept an upscale or click **Skip**.

1. Read the size line: **Document: W × H px**, with a note on the long edge. Under 3000 px: "Small: upscale recommended". 3000 to 3999 px: "OK". 4000 px or more: "Good: no upscale needed".
2. Click **Upscale** (Topaz on Fal; the cost is shown under the button) or **Skip**.
3. Upscale makes the photo ×2 (×4 for a very small photo), then fits the document between 4000 and 6000 px on the long edge. The result is the layer **UPSCALE**, right above the original photo; the original stays below it, hidden. Every later step uses UPSCALE as the photo. Check it at 100%.
4. **Accept** keeps it and opens step 1. **Discard** puts the original back at its original size. **Re-run** upscales the original again.

Once step 1 is done, step 0 is locked ("Start over to upscale"): Print Swap never upscales under finished steps.

**After Start over, UPSCALE is kept.** The status line says what was kept, for example "Started over. UPSCALE kept (Topaz ×2, 998 × 2048 → 1996 × 4096). Steps 1 to 9 reset." Step 0 shows **done ✓ · UPSCALE kept** with:

* **Keep and continue**: step 1 opens.
* **Upscale again**: deletes UPSCALE, shows the original again, sizes the document back to the original size and upscales the original. UPSCALE itself is never upscaled.
* **Remove upscale**: deletes UPSCALE, shows the original again at its original size, and sets step 0 back to ready.

### Step 1 · Background

1. Pick **White** (the team's final, default) or **Lighten**.
2. Tick **Hair** if the model's hair falls over the garment.
3. Click **Background**.
4. Check the edge of the model and the hair. Click **Accept**.

Settings: **Lighten opacity (%)**, **Edge softness**, **Refine in Photoshop**.

Hair is saved as a channel, **KBPS hair**. The HAIR layer is built in step 9.

![Step 1 Background](screenshots/05-step1-background.png)

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

![Step 2 Garment](screenshots/06-step2-garment.png)

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

![Step 3 Remove print (CLEAN)](screenshots/08-step3-clean.png)

### Step 4 · Trims

The step lists the trims of your type, e.g. "PAJAMA SET: PIPING, BUTTONS".

**Piping**

1. Check the mode: **Colored piping** (red, navy, pink) or **Neutral piping** (white, black, gray). It is picked for you; the line under the buttons says "Auto: …".
   For **Neutral**, Find piping keeps lines of one direction only: light lines (white piping on darker fabric) or dark lines. The pick shows next to it ("Neutral: light lines"); if it is wrong, click **Light** or **Dark** and Re-run.
2. Click **Find piping**. Check that every piping line is in the selection and no skin. For Neutral, the status line says how many line pieces were kept and dropped. The garment's outer edge, short bits, folds, heather texture, KBPS hands and the buttons from Find buttons are left out.
3. Fix with **+ Add selection** / **- Remove selection**, or change the mode or **Tolerance** and **Re-run**.
4. Click **Accept**. The **PIPING** group is built on top.

**Buttons**

1. Click **Find buttons**. SAM looks at 4 close-ups of the garment, read straight from CLEAN (or from the photo when there is no CLEAN). The canvas does not change while it works: no layer is shown or hidden, and the layer that was active stays active. Find piping, Find parts and the other trims work the same way.
2. Add any it missed with **+ Add selection**. Click **Accept**. The **BUTTON** group is built on top.

Other trims of the type (lace, drawcord, bow, zipper) work the same way.

Settings: Tolerance, Edge ring, Min line length, Edge margin, Button fit (Tight, Normal, Loose), Shrink button mask, Edge softness.

**Neutral piping and the garment edge.** Find piping leaves out a thin **Edge ring** only where the garment meets the background (outside KBPS person), so the cut-out edge never reads as piping. Where the garment meets skin, hair or the neckline there is no ring, so collar, lapel, cuff and hem piping on that edge is found. A long light line along the edge (more than about 3% of the garment height) is kept even inside the ring. In the collar area (the top 20% of the garment box) shorter pieces count as lines, because collar piping comes in short curved pieces. **Edge ring (px)** and **Min line length (px)** are filled with the automatic values for the image and shown in the status line; widen or tighten them and Re-run.

**Save piping test case** (in Settings) saves what Find piping reads on this document, with KBPS piping as the expected result, to the plug-in data folder. Use it once the piping is right, so later changes to piping detection can be checked against this garment.

Step 4 only finds the trims. When a trim is built, the status line ends with "Set trim colors in step 7."

The trim groups always sit above the GREY group and above GREY copy 3, so the veil never covers a trim.

![Step 4 Trims](screenshots/09-step4-trims.png)

### Step 5 · Gray

1. Pick the **Target gray** under the button: **Light** #D0D0D0, **Mid** #BABABA (default), **Dark** #8C8C8C, or **Custom…**. Custom… opens Photoshop's color picker; while it is open you can click the canvas to sample a color (for example the new print's ground). You can also type any hex in the box. A color that is not neutral becomes the gray of the same lightness, and the status line says "Converted to gray #…". The gray is saved with the document, and step 3 (Remove print) ends its prompt with "(target grey #…)".
2. Click **Make gray**. Result: **GREY exact**, the garment in neutral gray with its folds.
3. Check: even gray, folds visible, no old print showing. Click **Accept**.

**Changing the gray later.** Once step 5 is done, a new Target gray turns the button into **Update gray**. It makes GREY exact again with the new gray, in the same place, with no Accept bar. Parts, prints and trims stay. If step 8 is done, the shading (GREY group and GREY copy 3) is built again from the new gray with the step 8 values, and a MERGED from Finish is redone. The status line says "Gray updated to #…". **Redo** on step 5 still clears steps 5 to 9 as before.

![Step 5 Gray](screenshots/10-step5-gray.png)

### Step 6 · Parts

The step reads, top to bottom: garment type, **Find parts** and its cost, the parts list, **+ Add selection** / **- Remove selection**, **Show shapes**.

1. Before Find parts the list reads **Parts to find (N)**, all checked. Uncheck any part this garment does not have.
2. Click **Find parts**. SAM makes one mask per part. The parts then tile the garment exactly: every garment pixel belongs to one part (where two masks overlap, the stronger one keeps it; a gap goes to the nearest part). Where two parts meet, the border is hard with a 1 px overlap, so no light or dark hairline shows between them. A group is built under **PARTS** only for a part with a shape, never an empty one. The status line stays short, for example "12 of 19 parts found · $0.16. Check the parts, then Accept."; the line under the list gives the coverage ("Coverage: 100%, gaps 0 px") and which parts filled gaps, so a missed part that really is visible is easy to spot.
3. The list now has two groups:
   * **Parts found (N):** a checkbox and the name. Click the name to select the part (Layers follows). Unchecking a part moves it to the second group; steps 7 to 9 skip it.
   * **In this style, not in this photo (N):** the name in gray and **+ Add**. **+ Add** moves the part up (checked and selected) and the status line says "Select [PART] on the photo, then click + Add selection." Once you add a selection, its group is built in the team's order.
4. Fix a part with **+ Add selection** / **- Remove selection**. **Show shapes** shows every part at once.
5. Click **Accept**.

Settings: **Edge softness** (only on the garment's outer edge, never between two parts), **Apply to part**, **Refine in Photoshop**.

![Step 6 Parts](screenshots/11-step6-parts.png)

### Step 7 · Print and Color

1. Click **Choose print** and pick the print file. A thumbnail, the file name and its size show under it.
2. Set **Scale % (whole garment)**.
3. Click **Place print**. The print is tiled into every part.

**Continuous** (above SCALE, on by default) tiles every part in one shared grid: the same origin (the document's top-left), the whole garment's scale and the whole garment's angle. The pattern runs on across the seams, the pocket and the placket, as if the garment were cut from one piece of fabric. A part's own scale or angle (This part), when set, still overrides it for that part only. Turn it off to tile each part along its own direction, centred on the part. Changing it redoes the print in every part at once. It is saved with the document; Swap print, Reset scale and rotation, and Redo keep it.
4. Adjust:
   * **Rotate print (whole garment):** ↺ 15°, ↺ 1°, ↻ 1°, ↻ 15°, 0° (reset), or type an **Exact angle** and **Apply**.
   * **One part:** open **Adjust one part** (closed by default), pick the part (Part dropdown, its step 6 row, or its group in Layers), then use the **This part** rotate buttons, angle box and scale box. They change only that part's PRINT: every other part and the Whole garment angle stay as they are, and the part's group is selected in Layers afterwards. **Whole garment · Angle** shows the whole garment's value only; **This part · Angle** shows the part's own angle, or "same as whole garment" when it has none.
   * With **Continuous** on, a part with its own angle or scale is turned or scaled around its own centre, starting from where the shared grid puts it, so it still lines up as closely as it can. Clear its angle and scale boxes (empty, then Apply) to put it back on the shared grid.
5. Click **Accept**.

To try another print, click **Swap print**. It keeps every setting.

**Trim colors** (below the print controls, above Reset scale and rotation). Each trim of the type has a row: a swatch, a hex box, and **Original · White · Black · Custom…**. Original means no recolor. **Custom…** opens Photoshop's color picker; click the print on the canvas to match it. You can also type a hex value in the box, with or without "#" (FFFFFF or #FFFFFF): Enter, or leaving the box, applies it. An invalid value turns the box red and changes nothing. Under BUTTON, **Same as piping** gives the buttons the piping's color (and **Same as buttons** under PIPING). Each trim's color is saved with the document and comes back after a reload or a Swap print.

A color adds two layers in the trim's group, clipped to the trim layer:

* **Trim lightness** (Levels) moves the trim's median lightness, measured inside its channel, to the color's lightness. The texture, folds and edges around it stay.
* **Color Fill 1** (Color mode) gives the color's hue and saturation.

The color shows as a preview: **Accept** to keep it, or **Discard** to go back to the color before. Original hides both layers. A color works as soon as step 4 is done, even before a print is placed, and after Finish too: MERGED is hidden while the preview waits, and a new MERGED is built on Accept. Find does not need to run again. The color is saved with the document and put back if the trim group is built again. Black takes the trim to a very dark gray, not pure black, so its folds still show.


📷 `12-step7-print.png` · 📷 `13-step7-rotate.png`

### Step 8 · Shading

When step 8 opens, the panel measures the average lightness of the source garment (the photo, before Remove print) and of the placed print, inside the garment. Each is **Dark** under 40%, otherwise **Light**. The line under the toggles shows the pair, for example "Auto: dark garment → light print". Click **Garment** or **Print** Light / Dark to override. A click only fills the fields below: nothing is built and no layer changes, even with a preview waiting. Click **Build shading** or **Re-run** to use it; your pick is then kept with the document.

The pair fills the starting values. You can change any field:

| Garment → Print | Fold contrast | Fold smoothing | Highlights | Shading strength |
| --- | --- | --- | --- | --- |
| Dark → Light | 2.0 | 2 | 0 | 100 |
| Light → Light | 1.0 | 2 | 0 | 100 |
| Light → Dark | 1.2 | 2 | 25 | 100 |
| Dark → Dark | 1.6 | 2 | 15 | 100 |

* **Shading strength %**: the opacity of GREY copy (Multiply).
* **Fold contrast**: higher means deeper folds.
* **Fold smoothing (px)**: a Surface Blur on GREY copy that hides fabric noise and keeps the fold edges. Every pair starts at 2 px.
* **Highlights %**: the opacity of GREY highlights (Screen), which brings back the light side of folds on dark prints.
* **Warm shadows** (On by default): tints the shading map slightly (about 10% saturation) toward the print's ground color, measured when step 8 opens, so shadows on a cream ground read as deeper cream, not gray. Flat fabric is not changed. The line under the toggles names the ground color.

Before the Levels, a thin ring along the KBPS garment edge (about 0.15% of the long edge, 6 px on a 4000 px image) is filled with the median gray in GREY copy, GREY highlights and GREY copy 2. GREY exact is darkest where the cut-out meets the background; without the ring, Multiply prints that edge as a dark outline along the sleeves and side seams.

1. Click **Build shading**. **Levels shading** maps the median gray of GREY exact to white, so flat fabric does not darken the print and only folds and shadows do. Every adjustment in the GREY group (Levels shading, Brightness/Contrast 1, Exposure 1, Warm shadows, Levels highlights, Levels burn) is clipped to its own shading layer, so none of them changes the print's colors. The status line starts "Shading built: 1 veil". If Photoshop refuses Surface Blur, a Gaussian Blur at half the radius is used and the status line says "Fold smoothing: Gaussian fallback".
2. Check that the print follows the folds and keeps its colors. Click **Accept**, or change the fields and **Re-run**.

Every Build, Re-run, Discard and Redo first unlocks and deletes every step 8 layer (the GREY group, GREY copy 3 and any stray GREY highlights or Levels layer), so Re-run with the same values gives the same result. If one cannot be deleted, the run stops with an error instead of building on top. Only GREY inside the group is locked; GREY copy 3 and the copies are unlocked and checked after every build. GREY copy 3 sits straight above the GREY group, under the trims. When a document opens, extra GREY copy 3 layers left by older runs are deleted.

Settings: Brightness 7, Contrast 19, Exposure 0.10, Offset -0.0026, Gamma 0.96, Linear Burn 10% (the team's values) and Veil 0% (raise it if the team wants the veil).

📷 `14-step8-shading.png`

### Step 9 · Finish

1. Click **Finish**. The lighten layer is hidden, **MERGED** is stamped on top, and **HAIR** goes over it.
2. Check the whole image at 100%. Click **Accept**. Save the PSD.

![Step 9 Finish](screenshots/15-step9-finish.png)

![Layers panel after Finish](screenshots/16-layers-final.png)

**Swapping again after Finish:** while the new print is waiting for Accept, MERGED is hidden so you can see it. On **Accept** a new MERGED is built. The one before stays below it, hidden, so you can compare. Only the 2 newest are kept.

## The status line

The line at the top of Print Swap says the result and what to do next, in two lines at most. When there is more to say, **Details** opens the full message (it is also in the trace). Results are in normal text, things to look at or do first in orange, errors in red. The progress bar shows "Stopped" only on an error or a cancel.

## 6. Redo and Start over

* **Redo** (orange, on a done step): deletes that step and every later one, then sets that step to ready. Earlier steps stay.
* **Start over** (top of the steps): deletes every Print Swap layer and mask and the garment type. Your photo and your own layers stay, and so does UPSCALE (see step 0). It asks first; **Show details** lists everything it will delete. It also removes leftovers from earlier versions: extra GREY copy 3 layers, GREY copies at the top level, BUTTON THREAD, temp layers and every KBPS channel.

Every delete (Start over, Redo, Discard, Re-run, trim colors, MERGED versions) first unlocks the layer (Lock None), then deletes it by itself, so a locked layer never stops the run and no Photoshop dialog appears. If Photoshop still keeps a layer, the status line names it in red with Photoshop's reason, and the rest is deleted anyway.

📷 `17-start-over.png`

## 7. Troubleshooting

| Problem | Fix |
|---|---|
| "Add your Fal API key in Settings" | Settings tab > paste key > admin PIN > Save. |
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
