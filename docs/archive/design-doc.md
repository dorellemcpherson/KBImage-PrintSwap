# Design Doc: KBImage Print Swap

Owner: Dorelle McPherson, AI Creative Technologist

Created on: 10/15/2026

Status: [WIP]

Approved on: TBD

| Name | Status: [approved | commented] |
|---|---|
|  |  |
|  |  |
|  |  |

## Overview

Print swap is a regular retouching job at Komar: the same garment photo is shown in a new print, so a style can be sold in every colorway without a new shoot. Today the retouching team builds each swap by hand in a layered Photoshop file. It is skilled, repetitive work, and most of the time goes into masking the garment, its parts and its trims, not into the creative decisions.

KBImage Print Swap is a Photoshop panel that builds that same file for the retoucher. It follows the team's own steps, layer names and layer order, and uses AI only where it saves time: finding the garment, the hands, the trims and the parts, and removing the old print. Every step is checked and accepted by the retoucher before the next one runs, and every result stays editable in Photoshop.

## Stakeholders

| Role | Person / team |
|---|---|
| Owner, build and support | Dorelle McPherson (AI Enablement) |
| Primary users | Retouching team |
| Process owner and sign off on output quality | Retouching lead (TBD) |
| Deployment, security review, Fal account | IT (TBD) |
| Sponsor | TBD |

## RACI Matrix

R = responsible, A = accountable, C = consulted, I = informed. Draft for review.

| Task / Activity | AI Enablement | Retouching team | Retouching lead | IT | Leadership |
|---|---|---|---|---|---|
| Panel build, fixes and releases | A/R | C | C | I | I |
| Supply original photos, layered files and part names | C | R | A | – | – |
| Test runs and quality feedback | R | R | A | – | I |
| Output quality sign off | C | C | A/R | – | I |
| Security review and Fal key / billing | C | – | – | A/R | I |
| Install on retouching machines | C | I | I | A/R | – |
| User training and guide | A/R | C | C | – | – |
| Go / no go | C | C | R | C | A |

## User Stories

* As a retoucher, I want the garment, hands, trims and parts masked for me, so I spend my time on checking and fine tuning instead of selecting.
* As a retoucher, I want the file built with our own layer names and order, so I can open it, read it and finish it the way I always do.
* As a retoucher, I want to accept, re-run or discard every step, so nothing the AI does is kept without my say.
* As a retoucher, I want piping, buttons and lace kept in their own color and on top, so trims are never printed over.
* As a retoucher, I want to swap to another print without starting over, and compare it with the last one.
* As a retouching lead, I want every swap to follow the same steps, so results are consistent across the team.
* As IT, I want one plug-in that talks to one vendor with one key, so the review and the billing are simple.

## Current Method

The team's print swap file (reviewed layer by layer, 111 layers) is built by hand:

* A pure white background and the model cut out (hair handled by hand).
* The old print removed from the garment, then a neutral gray base (GREY group: Brightness/Contrast 7/19, Exposure 0.10 / -0.0026 / 0.96, Linear Burn 10%).
* Each garment part masked on its own (LEFT TOP, RIGHT HAND, LEFT PANT TRIM and so on) and the print placed into each part.
* Piping and buttons kept on top in their own groups and recolored (Color Fill in Color mode, Hue/Saturation).
* Shading brought back over the print, a 10% veil, a merged stamp, and hair over the collar.

Pain points: masking every part and trim is slow; quality depends on who does it; there is no checklist, so steps can be missed.

## Proposed Solution

### How it works

A Photoshop panel with nine steps. Each step adds layers or masks to the open document and waits for Accept, Re-run or Discard.

| Step | What it does | AI or Photoshop |
|---|---|---|
| 1 Background | White (team default) or Lighten behind the model; optional hair mask | Photoshop Select Subject; SAM 3.1 for hair |
| 2 Garment | Pick the garment type, find the garment, take out the hands | SAM 3.1 |
| 3 Remove print | Remove the old print, keep folds, seams and the type's trims (CLEAN) | Nano Banana Pro |
| 4 Trims | Piping, buttons, lace and other trims in their own groups on top | Photoshop (piping); SAM 3.1 (buttons, lace) |
| 5 Gray | Neutral gray garment with its folds (GREY exact) | Photoshop |
| 6 Parts | One mask and group per part of the type | SAM 3.1 |
| 7 Print | Tile the print into every part; scale and rotate per garment or per part; swap prints | Photoshop |
| 8 Shading | The team's GREY group values bring the folds back over the print | Photoshop |
| 9 Finish | Hide the lighten layer, stamp MERGED, HAIR on top; keep the last 2 MERGED versions after swaps | Photoshop |

### Tools

* Adobe Photoshop 2022 (23.3) or newer, UXP plug-in (panel).
* Fal (one API key) for both AI models.
* SAM 3.1 (Meta, via Fal): finds the garment, hands, trims and parts. $0.005 per request.
* Nano Banana Pro (Google, via Fal): removes the old print. $0.15 per image, $0.30 at 4K.

### Garment types

Types A to H cover the current pajama sets, nightgowns, sleepers and tee sets. Each type lists its parts (ALL CAPS, viewer's left and right, the team's names) and its protected trims. Styles not on the list use Other, and a working setup can be saved as a new type. Part names will be updated from the retouching team's layered files.

### Data and security

* The Fal key is stored in Photoshop's secure storage on each computer and is sent only to Fal.
* The panel can only reach Fal addresses (listed in the manifest). No other network access.
* Only crops of the garment and small close ups are sent to Fal for each AI step. Fal's data retention terms to be confirmed by IT.
* A trace and a session log are written to the plug-in's own data folder on the computer.

### Costs

A full run on a 4480 × 6720 photo cost $0.35 to $0.55 in testing (one Nano Banana Pro call, a few to about twenty SAM calls). Every button shows its price, and the panel keeps a running total with a spend warning. Billing goes to the Fal account. Who sees costs (everyone, admin only, or nobody) is to be decided before rollout.

### Deliverables

* The KBImage Print Swap plug-in (clean repository, Komar owns it in full).
* User guide with screenshots, rules and best practices, garment types and part names.
* This design doc.

### Out of scope

* General image generation, generative fill, extend and upscale (Photoshop, Flora and Make the Dot already cover them).
* Batch processing of many photos at once.
* Matching stripes across parts (done by the retoucher).

### Risks and mitigations

| Risk | Mitigation |
|---|---|
| Low resolution input gives soft results and lets the AI redraw details | Use studio originals of 4000 px or more; input size check planned |
| Remove print changes trims or shape | Prompt names the type's trims; retoucher checks and re-runs; nothing kept without Accept |
| SAM misses small trims or parts | Manual + Add / - Remove on every mask; Redo per step |
| Garment styles not covered | Other and Save as type; part names from the team's files |
| Vendor or model change at Fal | One place in the code per model; models can be swapped without changing the steps |

### Roll out

1. Testing on studio originals from the retouching team (in progress).
2. Part names and types updated from the team's layered files.
3. Pilot with one or two retouchers; side by side comparison with hand built files; time per swap measured.
4. IT review, packaging and install on retouching machines; Fal key and billing set up.
5. Team rollout with the user guide and a short walkthrough.

### Status (10/15/2026)

* Built and tested in Photoshop: the full nine step run on a 4480 × 6720 pajama set (type A), hand removal, white and colored piping detection, rotation, Start over, Redo.
* Built, testing next: keeping 2 MERGED versions after a swap, live part by part placement, print size warning, Discard, Other and Save as type.

### Reference Documents

* README.md (repository overview)
* docs/user-guide.md (how to, every step and button)
* docs/print-swap-guide.md (rules and best practices)
* docs/parts-list.md (garment types, parts and trims)
* The retouching team's print swap file (reference for layers and order)
