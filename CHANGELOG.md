# KBImage Print Swap: changelog

Newest first. Versions marked *Photoshop test pending* were built and checked offline but not yet confirmed in Photoshop.

## 0.20.14 (2026-10-22) · Photoshop test pending

* **Step 5, Highlights from photo %** (default 60, 0 = off): GREY exact keeps the satin sheen of the original photo, which Remove print had made matte. Sharp edges of the old print are left out. It is saved with the document, and **Update gray** applies a changed value.
* **Step 8:** Highlights % now starts at 25 on light prints (dark prints stay at 40).

## 0.20.13 (2026-10-22) · Photoshop test pending

* **Trim colors:** every trim row (PIPING, BUTTON and the other trims) has two chips, **Original** and **Custom…**. Original shows the cord uncolored and opaque. You can also type a hex and press Enter.
* **Version in the header:** the panel title shows the version, e.g. "KBImage Print Swap v0.20.13", read from the plug-in itself.

## 0.20.12 (2026-10-22) · Photoshop test pending

* **Custom… color picker fixed:** the picked color was read at the wrong scale and came out white. It now reads the color correctly, waits for the picker if Photoshop returns early, and writes what it read to the trace file at once.
* **Opaque piping and buttons:** PIPING and BUTTON now look like solid dyed fabric. They are masked to the found trim at full strength, with no see-through Blend If. A color adds a second, Multiply color layer (35%) so the cord keeps its roundness.
* **Piping opacity %** in step 4 › Adjust.
* White and Black chips removed.

## 0.20.11 (2026-10-22) · Photoshop test pending

* **Step 6, parts:**
  * New **Use selection as part** button.
  * Click a selected part again to deselect it.
  * Clicking a part loads its shape as the selection, ready to grow or trim with Quick Selection or Lasso.
* **Session total** at the top of the panel is shown in the same green as the other prices.
* **Custom… color picker** opens at the trim's current color. If a color can't be applied, the old one comes back.
* **Finish** always includes PB (piping, buttons and their colors) and SDW in MERGED, even if they were hidden. The trace lists what was visible at the moment of the stamp.

## 0.20.3 to 0.20.10 (2026-10-19 to 2026-10-20) · Photoshop test pending

* **Fewer crashes on large files:** images are read in strips, which avoids the graphics crashes.
* **Edges:** the Edge softness sliders are always visible.
* **Trims:** new "Use selection as piping / buttons" buttons. Accept warns when a selection hasn't been saved to the trim.
* **Hand-painted masks:** syncing them back was turned off because it broke the print clipping. Paint fixes with the panel's buttons instead.
* **Repairs:** print clipping is repaired before Apply print and Finish, and leftover temporary layers are removed before every stamp.
* **Step 7:** trim colors are back in step 7 and usable before a print is placed. Step 7 stays open after Apply print.

## 0.20.2 (2026-10-18) · untested

* **Step 8:** the shading layer holds only garment pixels. **Shading strength** goes up to 200% (a second SHADOW layer above 100%).

## 0.20.1 (2026-10-18) · tested in Photoshop (tag v0.20.1-tested)

* **Find piping** settings are saved with the document, and a regression test guards the piping detection.
* **Backup:** the PRINT source and PRINT tiled layers go into a hidden Backup group, and are never stamped into MERGED.
* **Step 8:** new **Highlights %** lightens the lit side of folds.

* **Layers:** all parts live in one PARTS folder. PIPING and BUTTON stay in PB.
* **Parts:** part masks are smoother, with no light fringe between parts.
* **Prices:** shown in green, with a Charged badge per step.
* **Fixes:**
  * A second Find parts no longer deletes the trims.
  * PIPING no longer goes missing after a rebuild.
  * Gray updates in place.
  * The panel puts back anything moved out of PB and says so.

## 0.20.0 (2026-10-17) · untested

* Layers follow the team's print swap file: a PS group holds PB (trims), SDW (shading kit) and the parts. SDW has SHADOW with Color Balance, Brightness/Contrast, Selective Color, Light and Levels layers, with automatic fold masks.

## 0.19 (2026-10-15 to 2026-10-17)

* **First version.** Steps 0 to 9: Upscale, Background, Garment, Remove print, Trims, Gray, Parts, Print and Color, Shading, Finish. Every step has Accept / Re-run / Discard and writes a session log.
* **Panel:**
  * Print Swap | Settings tabs.
  * An admin PIN locks the Fal key.
  * Short status lines: orange for warnings, red for errors.
* **Garment types** survive a reload. **Other** lets you build and save your own type.
* **Step 7:**
  * Swap print and Apply print, repeatable after Shading and Finish.
  * Continuous print across parts.
  * Per-part angle and scale.
  * Trim colors.
* **Step 8:** Light/Dark presets, edge ring, warm shadows.
* **Docs:** README, user guide, design doc and screenshots.
