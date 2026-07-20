# ERP Supply Chain — Parameter Timeline

Interactive reference for the AD Parameter Small Group: the supplier-to-production
parameter flow, plus TL transit times to the Laredo, TX crossing.

**Live site:** `https://<your-username>.github.io/<repo-name>/`

## Contents

| File | Purpose |
|---|---|
| `index.html` | The full interactive page (self-contained — no build step, no dependencies) |
| `data_TL_Transit_to_Laredo.xlsx` | Source data for the transit map |

## Sections

1. **Parameter Timeline** — the EDI → Production Build Date flow. Click any stage or
   parameter pin to see its detail.
2. **TL Transit Time to Laredo** — transit days by state, from a 3-point mileage
   average (closest / central / furthest city) using the **500 miles = 1 day** rule.
3. **Parameter Reference** — glossary with pros, cons, and owner per parameter.
   Click a card to expand.

## Notes on the transit map

Transit days are **transportation time only**. They exclude warehousing, kitting,
sequencing, and line-feeding time. Border crossings add **+1 day**. Add these
buffers on top to arrive at total Safety Time.

## Publishing to GitHub Pages

1. Push these files to the repository root (on `main`).
2. Repo **Settings → Pages**.
3. Under **Source**, select **Deploy from a branch**.
4. Branch: `main`, folder: `/ (root)` → **Save**.

The site is live in ~1 minute. Because `index.html` is fully self-contained,
nothing else is required.

## Updating the transit data

The state data lives in the `TL_DATA` array inside `index.html` (near the bottom,
under the `── TL TRANSIT MAP ──` comment). Each entry:

```js
{"abbr":"AL","state":"Alabama","closestCity":"Bayou La Batre","closestMi":708,
 "centralCity":"Maplesville","centralMi":840,"furthestCity":"Bridgeport",
 "furthestMi":962,"avgMi":836.7,"rangeMi":254,"days":1.67,"x":628,"y":438}
```

`days` = `avgMi / 500`. `x` / `y` are map positions on a 960×600 grid — leave them
as-is unless you are repositioning a state.
