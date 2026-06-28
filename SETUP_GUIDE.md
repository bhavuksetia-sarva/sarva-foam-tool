# Sarva Foam Tool v2 — Setup Guide

## Files in this package

| File | Purpose | Update when... |
|------|---------|----------------|
| `index.html` | The tool itself | New features added |
| `worker.js` | Cloudflare Worker (AI proxy) | Rarely |
| `block_master.xlsx` | Your BOM / Block Master | BOM changes |
| `config.json` | Column mapping for your unit | Report format changes |

---

## Step 1: Upload all files to GitHub (2 min)

1. Create repo `sarva-foam-tool` on github.com (Public)
2. Upload ALL 4 files: `index.html`, `block_master.xlsx`, `config.json`, `worker.js`
3. Settings → Pages → Deploy from branch → main → Save
4. Your URL: `https://YOUR-USERNAME.github.io/sarva-foam-tool`

---

## Step 2: Deploy Cloudflare Worker (3 min)

1. cloudflare.com → Workers & Pages → Create Worker → name: `sarva-foam` → Deploy
2. Edit code → paste contents of `worker.js` → Deploy
3. Settings → Variables → Add secret: `ANTHROPIC_API_KEY` = your key from console.anthropic.com

Your Worker URL: `https://sarva-foam.YOUR-NAME.workers.dev`

---

## Step 3: First-time tool setup (1 min)

Open your GitHub Pages URL. You'll see 3 setup boxes:

1. **Worker URL** → paste your Cloudflare Worker URL → Save
2. **Config** → paste: `https://raw.githubusercontent.com/YOU/REPO/main/config.json` → Load
3. **BOM** → paste: `https://raw.githubusercontent.com/YOU/REPO/main/block_master.xlsx` → Load

Click **"Start using the tool"** — done! Settings are remembered in the browser.

---

## For multiple units

Each unit needs its own:
- `block_master.xlsx` — their BOM file
- `config.json` — their column mapping

**Option A:** One repo per unit (`sarva-foam-unit5`, `sarva-foam-unit6`)
**Option B:** One repo, subfolders (`/unit5/block_master.xlsx`, `/unit6/block_master.xlsx`)
  → Users pick their unit by loading the right config/BOM URL

---

## Updating the BOM (when formulations change)

1. Open your GitHub repo
2. Click `block_master.xlsx` → Delete → Upload new file → Commit
3. Users click "Reload BOM" in the tool — done. No code changes.

## Updating config.json (when report format changes)

1. Open `config.json` in GitHub → Edit → update column names → Commit
2. Users click "Reload Config" in the tool.

---

## config.json — what to edit

```json
{
  "unit_name": "Sarva Foam Industries — Unit V",
  "foaming_report": {
    "height_mm": 820,
    "scrap_columns": {
      "imported":  "Imp (Imported scrap)",
      "local":     "Local (PU Scrap Local)",
      "rebonded":  "RB (Rebonded scrap)",
      "memory":    "Memory scrap (may be absent)"
    },
    "binder_columns": {
      "hard1519":  "Hard / 1519 Binder",
      "soft1513":  "Soft / 1513 Binder"
    }
  },
  "bom_columns": {
    "sku":             "Block SKU Name",
    "grade_code":      "Grade Code",
    "density":         "Density",
    "L":               "L (mm)",
    "W":               "W (mm)",
    "total_wt":        "Total Wt\\n(KG)",
    "local_pct":       "Local Scrap",
    "imported_pct":    "Imported Scrap",
    "hard1519_pct":    "Hard Binder 1519",
    "soft1513_pct":    "Soft Binder 1513",
    "total_binder_pct":"Total Binder %"
  }
}
```

Change the **values** (right side) to match your Excel column headers exactly.
