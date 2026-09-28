# Dhruva — Core Stock Portfolio Performance Analysis with Monthly Trading Rules

An interactive **what-if calculator** for the **Technofunda Dhruva Platform** — a
rules-based NSE equity strategy that buys on every "1G" signal and sells on every
"3R" signal on the first Tuesday of each month, recycling the proceeds of every sale
back into the next buys.

**Live:** https://sureshtumu.github.io/dhruva-explorer

## What it does

Change two things and watch the whole result recompute live against the Nifty 50 over
the same ~2.5-year window:

- **Rupees per stock** — how much goes into each buy (₹1,000 / ₹5,000 / ₹10,000, or any
  amount).
- **How you pick stocks each month** — buy *all* green (1G) stocks (the full process),
  or cap it to the first N (e.g. alphabetically), to see how selection discipline
  changes the outcome.

Profit, XIRR and the Nifty comparison update instantly, with a chart tracking the run.

> Experimental study — not investment advice. Tickers and monthly signals were captured
> as accurately as the data allows, and figures are gross of brokerage, taxes and
> slippage. Consult the TechnoFunda / Dhruva team for access to the Dhruva portal.

## Design notes

- **Self-contained.** Everything — data, styling, and logic — lives in `index.html`.
  There are no external data files, no build step, and no runtime fetches. The only
  external call is the (optional) GoatCounter stats script.
- **Fresh-extract model.** The month-by-month figures are baked into the page as of the
  last pipeline run. There is no stored series or server; the page reflects one snapshot.

## Updating

The pipeline runs irregularly (no fixed cadence). To refresh the site after a new run:

1. Regenerate the HTML from the pipeline.
2. Rename it to `index.html`.
3. In this repo: **Add file → Upload files**, drop in the new `index.html`, and commit
   to `main`.

The URL stays the same and GitHub Pages redeploys automatically within a minute.

## Stats

Visitor stats are collected via [GoatCounter](https://www.goatcounter.com/)
(account `sureshtumu`), the same setup used for the retirement corpus calculator.

---

*Suresh Tumu · AMFI-certified · TechnoFunda community*
*Prepared with Claude AI. Thanks to Vivek Mashrani & team.*
