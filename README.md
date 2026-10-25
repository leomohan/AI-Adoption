# From Deployment to Transformation — Companion Tools

A small static website of working tools that accompany the book
*From Deployment to Transformation* by Mohan Krishnamurthy (Leomohan Publications).
Built to run for free on **GitHub Pages** with no server, no database, and no build step.

## Tools

| Appendix | Tool | Status |
|---|---|---|
| **A** | AI Adoption Maturity Assessment — 50 questions, 5 weighted dimensions | **Live** |
| **B** | Executive Dashboard — editable board of health, value, and leading indicators | **Live** |
| **C** | AI Agent Reporting Templates — per-agent monthly reports across a portfolio | **Live** |
| **D** | Value Realization Framework — ROI calculator, J-curve, sensitivity, and tracker | **Live** |

Appendix A scores an organization across the book's five Maturity-Scorecard
dimensions — Leadership (20%), Adoption (25%), Usage (20%), Productivity (20%),
Governance (15%) — and reports a weighted composite mapped to four bands:
**Early (0–40) · Developing (40–59) · Advancing (60–79) · Mature (80–100).**

## How it works

- Pure HTML, CSS, and vanilla JavaScript — nothing to compile.
- Answers and saved results live in the visitor's browser (`localStorage`).
  **Nothing is uploaded anywhere.** This is deliberate: it is both the correct
  privacy posture for candid self-assessment and what static hosting allows.
- Results export to **PDF** (via the browser's print dialog), **JSON**, and **CSV**.

## Repository structure

```
.
├── index.html            # landing page linking to each appendix
├── assets/
│   └── style.css         # shared design system for every tool
├── appendix-a/
│   └── index.html        # the AI Adoption Maturity Assessment
└── README.md
```

Paths are relative, so the site works whether it is served from a project
page (`username.github.io/repo/`) or a custom domain.

## Deploy to GitHub Pages

1. Create a new repository and add these files at its root.
2. Push to the `main` branch.
3. In the repository, open **Settings → Pages**.
4. Under **Build and deployment**, set **Source: Deploy from a branch**, then
   choose **Branch: `main`** and **Folder: `/ (root)`**. Save.
5. Wait a minute; your site appears at `https://<username>.github.io/<repo>/`.

To use your own domain later, add it under Settings → Pages → Custom domain.

## Preview locally

Open `index.html` directly in a browser, or serve the folder so relative paths
resolve exactly as they will in production:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Customizing Appendix A

Everything is in `appendix-a/index.html`:

- **Questions** — edit the `QUESTIONS` array. Each entry is
  `["dimensionKey", "statement"]`. Keep ten per dimension for balanced scoring
  (or adjust freely; scoring uses each dimension's average, so counts can differ).
- **Dimensions and weights** — edit the `DIMS` array (`weight` values should sum
  to 1). The `advice` text appears when a dimension is one of the two lowest.
- **Bands and level names** — edit `BANDS` and `LEVELS`. Keep these aligned with
  Chapter 17 of the book so the tool and the text agree.

## Attribution and licence

Companion to *From Deployment to Transformation* by Mohan Krishnamurthy,
Leomohan Publications. Add your chosen licence here before publishing
(for example, a permissive licence for the code and an "all rights reserved"
notice for the book content and question set).

## Roadmap

- Appendix B — executive dashboard templates (mirrors the book's dashboard figure).
- Appendix C — agent reporting templates.
- Appendix D — ROI calculators and tracking sheets (cost of ownership, attribution,
  the investment J-curve, sensitivity analysis).

## Customizing Appendix B

Everything is in `appendix-b/index.html`:

- The opening board is the `sample()` object — edit it to change the default
  worked example, or just use the in-page **Edit dashboard** button.
- Metrics carry a value, unit, a change note, a direction (up/flat/down), and an
  optional comma-separated `history` that draws the sparkline.
- The dashboard reads the latest **Appendix A** score from the same browser and
  shows it in the maturity strip, so the two tools stay connected.
- **Import JSON** reloads any board you previously exported — useful for keeping a
  template you reuse each reporting period.

## Customizing Appendix C

Everything is in `appendix-c/index.html`:

- The portfolio opens with two sample agents (`sample()`). Use the chips at the top
  to switch agents, **+ Add agent** to create one, or **Edit report** to fill in a
  month's figures.
- Each agent report carries: header (owner, function, month), **risk tier** and
  **lifecycle stage** badges, a health pill, an executive summary, three editable
  metric sections, an **incidents** table, a **governance controls** checklist, and
  a **lifecycle recommendation** with next steps — mirroring the book's chapters on
  operational metrics, monitoring, governance, and agent lifecycle.
- **Download JSON** exports the whole portfolio; **portfolio CSV** gives one row per
  agent (risk, stage, health, recommendation, open incidents) for a roll-up; **Import
  JSON** reloads a saved portfolio.

## Customizing Appendix D

Everything is in `appendix-d/index.html`, split into two tabs:

- **Value calculator** — enter program inputs (users, adoption, hours saved,
  loaded cost, attribution) and costs (per-user licences, infrastructure, support,
  enablement, one-time implementation). It computes ROI, net value, payback, and
  full-run-rate benefit, plots a **J-curve** from the actual monthly series (so the
  break-even is calculated, not drawn), and runs a **tornado sensitivity** across a
  plausible range for each assumption. Edit `defaultModel()` to change the opening
  example, or `TORNADO` to change the sensitivity ranges.
- **Value tracker** — log planned vs actual benefit and cost by period; it totals
  the columns and shows net variance. Edit `sampleTracker()` for the seed rows.

Both tabs export to PDF, JSON, and CSV. If Appendix A (maturity) or Appendix B
(weekly active users) has been used in the same browser, a context strip appears and
can pre-fill the adoption rate from the dashboard figure.

## The suite is complete

All four appendices (A–D) are live. They share one design system and connect where it
helps: Appendix B reads Appendix A's maturity score, and Appendix D reads both.
