# Fumagalli Pricer

A single-page web app for pricing Fumagalli lighting products by component
build-up and direct supplier/stock matching. Everything runs client-side in the
browser — no server or build step required.

## Live site

Once GitHub Pages is enabled (see below), the app is served from:

```
https://<your-username>.github.io/<repo-name>/
```

## How to use

1. Open the page in a browser.
2. Load the **master catalogue** `.xlsx` first. Either layout works: one sheet
   per range (the tab name is the range name) or a single combined sheet with a
   `Range` column. Each range sheet needs a `Configuration` column; a
   `Key`/`notes` tab is ignored.
3. Load the **ECI**, **Magnalux**, and **Stock** lists (`.xlsx`).
4. Pick a range and click **Calculate prices**.
5. Review flagged items, override component picks if needed, and **Export** the
   results.

Use the **Colour** dropdown above the table to filter the view (and exports) to a
single finish, and **Export all ranges** to price every range in the master and
download them in one workbook (with a `Range` column). The colour filter applies
to all three export buttons.

### Match codes → supplier import template (step 3)

A separate, lookup-only tool. Load the **ECI** and **Magnalux** price lists, then
upload a list of **product codes** (a `Product Code` column, or column A). Each
code is searched in both price lists — by description first, code as backup — and
written to the supplier import template (`ProdSuppRecImport`) **duplicated per
supplier**: one row for **E18** (ECI) and one for **M68** (Magnalux), each with
the price found. No build-up or calculation — just the matched prices. Codes with
no match are still written with a blank price so nothing is dropped.

**Colour-fill:** codes are grouped by their colour-stripped base (e.g.
`AMELIA800BK`, `AMELIA800WH`, `AMELIA800GY` → `AMELIA800`). If one colour is found
in a price list but a sibling colour is not, the sibling inherits that price — per
supplier, so a price is only borrowed from the same supplier's matched colour.

Validated head families (ANNA, RUT, SALEM, GOLIA, CEFA) are priced by component
build-up; every other range is matched directly against the supplier and stock
lists by description (with product code as a backup).

## Enabling GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Select the branch (e.g. `main`) and the `/ (root)` folder, then **Save**.
5. Wait a minute, then visit the URL shown at the top of the Pages settings.

`index.html` is at the repository root, so GitHub Pages serves it automatically.

## Dependencies

Loaded from CDNs at runtime (no install needed):

- [SheetJS / xlsx](https://github.com/SheetJS/sheetjs) — reads and writes `.xlsx`
- Google Fonts (Mulish, DM Mono)
