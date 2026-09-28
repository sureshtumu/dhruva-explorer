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

## Architecture — data stays private

The raw dataset (per-stock monthly signals and prices) is **not** shipped to the
browser. It lives in a private Supabase Storage bucket, and the calculation runs in a
Supabase Edge Function server-side. The page sends only the user's inputs (₹ per stock,
pick mode, window) and receives only the computed results (profit, XIRR, Nifty
comparison, chart points). So a visitor can use the tool but cannot download the
underlying tickers, signals, or prices.

- **Page (`index.html`, this repo):** UI + chart only, no data, no strategy logic.
- **Compute + data:** Supabase project `dhruva-calculator` — Edge Function `dhruva-calc`
  reads `D.json` from the private `data` bucket and returns results.

## Updating the data after a new pipeline run

The pipeline runs irregularly (no fixed cadence). To refresh:

1. Regenerate the data as `D.json`.
2. In Supabase → Storage → `data` bucket, replace `D.json` (upload, overwrite).

That's it — the page and function are unchanged, and the Edge Function picks up the new
data (it caches per warm instance, so a new deploy or a short wait refreshes the cache).
The public URL stays the same.

## Stats

Visitor stats are collected via [GoatCounter](https://www.goatcounter.com/)
(account `sureshtumu`), the same setup used for the retirement corpus calculator.

---

*Suresh Tumu · AMFI-certified · TechnoFunda community*
*Prepared with Claude AI. Thanks to Vivek Mashrani & team.*
