# Technofunda Dhruva Explorer

An interactive, single-page explorer for the **Technofunda Dhruva Platform** — a
rules-based NSE equity strategy that buys on every first "1G" signal and sells on
every "3R" signal, rebalanced on the first Tuesday of each month.

**Live:** https://sureshtumu.github.io/dhruva-explorer

## What it shows

Pick any start month between **Jan 2024 and early 2026** and the page recomputes the
whole run from a fresh start at that month — buys, sells, cumulative P&L, XIRR, and
peak capital — measured against the Nifty 50 over the exact same window.

The headline result: **the process beat the Nifty in all 27 of 27 start months.**
Even the worst case (starting Jun 2024, a clean 2.09-year window) still came in at
**27.7% XIRR vs 5.3% Nifty** — a ~22 percentage-point-a-year edge.

Two views:

- **Explorer** — headline cards, a per-month rhythm chart (buys / sells / cumulative
  P&L vs a Nifty-on-same-capital line), and a table of every start month you can click
  to select or play.
- **Movie** — a ~60-second animated month-by-month replay of any run, with scrubbing,
  speed controls, and a manual step-through mode.

## Design notes

- **Self-contained.** Everything — data, styling, and logic — lives in `index.html`.
  There are no external data files, no build step, and no runtime fetches. The only
  external calls are the (optional) GoatCounter stats script.
- **Fresh-extract model.** Every month's figures are baked into the page as of the last
  pipeline run. There is no stored series or server; the page reflects one snapshot.

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
*Designed & developed using Claude — Anthropic AI skills.*
