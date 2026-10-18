# Print Swap: rules, instructions and best practices

Print Swap automates the Photoshop team's print swap file. It builds the same layers, in the same order, with the same names, and adds small AI steps where they save time. The retoucher stays in control: every step is checked and accepted before the next one runs.

## 1. Inputs decide the result

The steps can only be as good as the files that go in.

**The photo**
* Use the full-size original from the shoot, never a web or marketplace JPG.
* Long edge 4000 px or more is best. 3000 to 3999 px works, but fine detail softens. Under 3000 px results will look soft and pasted on.
* If only a small file exists, upscale it in **step 0 (Upscale)** before step 1, never at the end.
* One garment, shot front, back or side, on a plain background.

**The print**
* Use the full-resolution artwork file (the PDRF TIF), not a screenshot or a JPG.
* The print must be big enough to cover the garment without being enlarged. If it has to be scaled up past 100%, get a bigger file.

**The garment type**
* Know which type it is (A to H, see [parts-list.md](parts-list.md)) before you start. The type decides which parts are found and which trims are protected.

## 2. Rules

1. **Stay true to the team's file.** Layer names, groups and order match the team's print swap file. Do not rename or reorder them.
2. **Trims are never printed.** Piping, buttons, lace, ruffle lace, drawcord, bow and zipper keep their own color and sit on top of the parts. They are not cut out of the parts.
3. **White background is the default** (the team's final). Lighten is an option for checking masks.
4. **One step at a time.** Run a step, check it, click Accept, then move on. Never skip a step that is not marked done.
5. **Part names** are ALL CAPS, 2 to 3 words, and LEFT and RIGHT are the viewer's left and right. The same word always means the same thing (HAND is a sleeve, TRIM is a band or cuff).
6. **Do not change the Remove print prompt wording.** The trims for the garment type are added to it automatically.
7. **Nothing is stretched.** If a result does not fit, Re-run or Discard. Do not transform it by hand.
8. **MERGED is a snapshot.** If you change anything below MERGED, hide it or rebuild it, or your change will not show.
9. **Stripes are not matched across parts.** The retoucher lines them up by hand.

## 3. Step by step

| Step | What you do | What to check before Accept |
|---|---|---|
| 1 Background | Pick White (default) or Lighten. Tick Hair if hair falls over the garment (see 3b). | Background is clean white; the model edge is not cut into. |
| 2 Garment | Pick the garment type, then Find garment. Fix the selection with the step 2 buttons (see 3a). Hands over the garment are taken out (see 3e). | The whole garment is selected, nothing else (skin, hands, hair, background). |
| 3 Remove print | Run Remove old print. | The garment shape, folds, seams and shadows are the same as the original. Lace and buttons are still lace and buttons, in their own color. If anything was redrawn, Re-run. |
| 4 Trims | Check Colored / Neutral piping (picked for you, see 3f), then find piping, buttons, lace and other trims for this type. Trim colors are set in step 7. | Every trim is found and masked closely, and no skin is in KBPS piping. Fix edges with a brush on the mask. |
| 5 Gray | Run to build the gray base. | Even gray, folds still visible, no old print showing through. |
| 6 Parts | Uncheck any part this garment does not have, then Find parts. Parts not in the photo move to "In this style, not in this photo"; **+ Add** brings one back. | Each part found has its own group and mask (no empty groups); coverage 100%, no hairlines between parts. Parts sit below the trim groups. |
| 7 Print and Color | Swap print to load the print file, set the scale (a suggestion is filled in), then Apply print; set the trim colors (they apply at once). Keep **Continuous** on for all-over and ditsy prints (one fabric across all parts). | Print is at the right scale, sharp, and runs the right way on each part. With Continuous on, the pattern does not break at seams, the pocket or the placket. |
| 8 Shading | The garment → print pair (Light / Dark each) fills Fold contrast, Fold smoothing, Highlights and Shading strength; change any of them. Run to bring the folds and shadows back over the print. | The print keeps its colors, follows the folds and does not look flat, dark or pasted on. The status line says "Shading built: 1 veil". |
| 9 Finish | Run the final clean up and stamp. | Check the whole image at 100%. MERGED matches what is below it. |


## 3a. Fixing the garment selection (step 2)

If your selection differs from the saved garment, step 2 shows a note: "Your selection isn't saved to the garment."

Every step after step 2 uses the saved garment, a channel called **KBPS garment**. It does **not** use the marching ants you see on screen. If you only change the selection with a selection tool, nothing after step 2 will see it.

To change the garment, use one of these:

1. **+ Add:** select the missing area (Lasso or any selection tool), then click + Add in step 2.
2. **- Remove:** select the area that should not be garment, then click - Remove.
3. **Paint the channel:** in the Channels panel, click KBPS garment and paint with white to add or black to remove. Click RGB when you are done.
4. **Use selection as garment:** replaces the garment with your whole current selection.

Check it: Ctrl+click KBPS garment in the Channels panel to load it and look at the edges at 100%.

If steps 3 and later are already done, click **Redo** on step 3 after fixing the garment, so every mask is rebuilt from the corrected one.

## 3b. Hair

When Hair is ticked in step 1, the hair is saved as a channel called **KBPS hair**. You will not see a hair layer yet.

* Step 2 takes the hair out of the garment, so the print never goes over it.
* The **HAIR** layer is built in step 9 Finish and sits on top, like the team's file.
* To check or fix the hair, use KBPS hair in the Channels panel the same way as the garment channel.

## 3c. Redo, Start over and getting unstuck

* **Redo** (on a done step): deletes that step and every step after it, then sets that step back to ready. Your earlier steps stay.
* **Start over** (top of the steps): deletes every Print Swap layer, group and channel and keeps only Background and UPSCALE (step 0 then offers Keep and continue, Upscale again or Remove upscale).
* **Delete layers with the panel, not by hand.** If you delete a preview layer in the Layers panel, the panel can still think a preview is waiting and block the next step.
* **If the panel is stuck,** use Start over. If that does not work, Remove and Add the plug-in again in UDT, or close and reopen the document.
* **The garment type belongs to the document.** If a new file shows a type you did not pick, change it before step 3.

## 3d. Template, part or find: which one to use

Three different things, often confused:

| You want to | Use | Where | What it does |
|---|---|---|---|
| Set up a garment style that is not in the list, for this and future files | **Template** (garment type) | Step 2: Garment type > Other, pick trims and parts, then **Save as type** | Saves the list of trims and parts under a name (e.g. "Sleep shirt"). It does not select anything in the image. |
| Add one part this garment has that the list is missing | **Add part** | Step 2: Other > type the name > **Add part** (ALL CAPS, 2 to 3 words) | Adds a name to the parts checklist, so Find parts looks for it. |
| Get the actual pixels selected | **Find** | Step 2 **Find garment**, step 6 **Find parts** | SAM looks at the image and makes the masks (channels) for the garment or for each checked part. |
| Fix a mask that Find got wrong | **+ Add / - Remove** | Step 2 for the garment, step 6 for the selected part | Adds your selection to, or removes it from, the saved mask. |

In short: the template and Add part decide **what** to look for. Find decides **where** it is. + Add and - Remove fix **where** by hand.

Tips:
* Pick or build the template **before** Find garment. The template decides which trims the Remove print prompt protects.
* Only **Save as type** once a garment has worked from start to finish, so the saved template is one you trust.
* In step 6, click a part's pill to select it, then use + Add / - Remove to fix only that part. **Show shapes** lets you see every part at once.

## 3e. Hands over the garment

When the model's hands rest on the garment (holding the hem, in front of the top, at a pocket), they must not get the print.

* After it finds the garment, **Find garment** asks SAM for the **hands** and takes them out of KBPS garment. The hands are saved as a channel called **KBPS hands**.
* For long-sleeve types (the ones with a HAND TRIM part), when the hands are over the garment, it also asks SAM for the **arms**. Only arm pixels with the hands' skin color come out, so the sleeves stay in the garment.
* The step 2 line says how many pixels were taken out and what the extra SAM calls cost: one for the hands, one more for the arms ($0.005 each). If SAM finds no hands, the garment is not changed.
* Check the fingers at 100%. Fabric between the fingers can stay in or drop out. Fix it with + Add / - Remove, or paint KBPS hands (white = hand).
* Find piping uses KBPS hands to keep skin out (see 3f). If you change the hands after step 4, run Find piping again.

## 3f. White piping: Colored or Neutral

Find piping has two ways of looking, shown on the step 4 face above **Find piping**:

* **Colored piping** finds the trim by its color. CLEAN is gray, so color left in it is trim (red, navy, pink piping).
* **Neutral piping** finds long, thin lines of one direction: lighter than the fabric (white piping on gray) or darker. It compares each pixel only with the garment around it, leaves out a thin ring along the garment's outer edge, and drops short bits, blobs, folds and heather texture. **Light** / **Dark** next to it overrides the automatic pick.

You do not have to choose. The first time you click Find piping, it looks at the thin lines in CLEAN. If they still carry color it starts on **Colored**, and if they are white, gray or black it starts on **Neutral**. The line under the buttons says which it picked ("Auto: Neutral …"). If the pick is wrong, click the other one and Re-run. Your click is kept until you switch to another document.

Skin is never picked up as piping. Find piping leaves out:

* KBPS hands, with a small margin
* garment pixels with the hands' skin color, near the hands or near the garment's edge (wrists, the neckline)

Skin color in the middle of the garment is left alone, so a pink or peach trim there is still found. The status line says how many pixels of skin were left out. If it says "No KBPS hands", run Find garment again first.

## 4. Best practices

* **Check at 100% zoom** before every Accept. Problems that are invisible at fit to screen show up in print.
* **Clean masks with a brush** on the layer mask (white adds, black removes). It is faster than re-running.
* **Re-run costs money; Discard does not.** If a result is wrong, try Re-run once. If it is still wrong, check the input first.
* **Recolor trims with the Trim colors rows in step 7** (Original · White · Black · Custom…). A pick applies right away (no Accept) and Original undoes it. It adds Trim lightness and Color Fill 1 inside the trim's group, never on the photo, and follows MERGED after Finish.
* **After any change below MERGED,** hide MERGED or rebuild it, or the change will not show.
* **Garment not on the list?** Use "Other" in step 2 and build a template (see 3d). Do not pick the closest type; the wrong type protects the wrong trims.
* **Save the PSD after each accepted step** so you can go back without re-running.
* **Hair:** only use the Hair option when hair actually covers the garment. Every model's hair is different, so check the hair mask closely.
* **Keep the team's file as the reference.** When in doubt, open it and compare layer by layer.

## 5. Known limits

* AI steps can redraw details on low resolution photos. Use high resolution input (section 1).
* SAM can miss very small trims (tiny buttons, thin lace). Check step 4 closely and brush in what was missed.
* Not in this version: an input size check in step 1, a print size check in step 7, and a Rebuild MERGED button.
