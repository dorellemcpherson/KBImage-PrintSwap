# KBImage Print Swap

A Photoshop panel that swaps the print on a garment photo for the retouching team. It builds the same layers, in the same order and with the same names, as the team's print swap file, and uses AI only where it saves time. Every step is checked and accepted by the retoucher before the next one runs.

![KBImage Print Swap panel](docs/screenshots/01-panel-overview.png)

**Version** 0.19.0 · **Plug-in id** `com.komar.kbimage.printswap` · **Photoshop** 2022 (23.3) or newer

## Quick start

1. In the UXP Developer Tool click **Add Plugin**, choose `manifest.json`, then **Load**.
2. In Photoshop open **Plugins > KBImage Print Swap**.
3. Click the gear, paste the **Fal API key**, click **Save**.
4. Open the garment photo and work through steps 1 to 9, clicking **Accept** after each.

## The 9 steps

Background · Garment · Remove print · Trims · Gray · Parts · Print · Shading · Finish

## AI used (all through one Fal key)

| Model | Used for | Cost |
|---|---|---|
| SAM 3.1 | Finding the garment, hands, trims and parts | $0.005 per request |
| Nano Banana Pro | Removing the old print (step 3) | $0.15 per image ($0.30 at 4K) |

A full run on a 4480 × 6720 photo costs about $0.35 to $0.55. Everything else is plain Photoshop.

## Documents

| Document | For |
|---|---|
| [User guide](docs/user-guide.md) | Retouchers: install, every step, every button, troubleshooting |
| [Rules and best practices](docs/print-swap-guide.md) | Retouchers: inputs, rules, what to check |
| [Garment types and part names](docs/parts-list.md) | Types A to H, parts and protected trims |
| [Design doc](docs/design-doc.md) | Review and approval: why, how, scope, risks |
| [CLAUDE.md](CLAUDE.md) | Developers: build rules |

## Files

`manifest.json` · `index.html` · `src/app.js` · `icons/` · `docs/`
