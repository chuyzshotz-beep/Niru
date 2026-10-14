# Capacity-adjusted illiquidity: short-horizon loss-filter screen

**Status:** unapproved research candidate only. No outcomes, raw tape, protected cohort, holdout, provider data, or wallet identities were inspected for this screen. This is not a trading rule or evidence of an edge.

## Candidate

At the existing five-minute post-migration decision `D`, use only complete 10-second bars in `[D-60s,D)`. Define short-window Amihud proxy as the sum of absolute adjacent-bar log returns divided by gross event quote volume in SOL. Scale it by the square root of `market_cap_SOL_at_D times distinct_active_addresses_in_window` to obtain one capacity-adjusted illiquidity feature. The count is per mint and window only; do not retain or join addresses across mints, and do not interpret addresses as people or independent traders. A zero/missing volume, invalid mark, incomplete bar window, or ambiguous timestamp/order makes the feature unknown.

The hypothesis is narrow: this joint measure of observed price movement, quote volume, market size, and within-window participation may improve the existing five-minute, 60-minute reserve-mark downside-risk screen at a fixed alert rate. Reuse the target, baseline, mint-disjoint chronological folds, and family-wise correction in [the scraper predictability plan](scraper-predictability-plan.md); do not create a second evaluation family. The direction is that greater adjusted illiquidity signals more downside risk; that sign is untested. It is a risk filter, not an entry signal or a survival classifier.

## Evidence and overlap

Chang Liu's September 2026 SSRN preprint defines capacity-adjusted illiquidity by scaling Amihud price impact by the square root of market capitalization times trader breadth. It reports weekly token-death prediction on a survivorship-complete Ethereum DEX panel, with only a partial Solana comparison, and explicitly describes predictive associations rather than causal effects. This is a mechanism lead, not evidence for a one-minute PumpSwap feature or a 60-minute NIRU outcome. [SSRN abstract](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7536975)

NIRU already records per-trade event quote amount, mark, and per-mint `user` in the raw tape; its 10-second bars store market-cap proxy, gross buy/sell quote flow, and unique buyer/seller counts. This makes the feature computable from the existing schema in principle, but does not establish complete windows, valid event amounts, finalized ordering, or sufficient prospective sample support. The proposed combination overlaps heavily with existing flow, volatility, market-cap, buyer/seller breadth, and depth controls. It merits only a single incremental-feature screen if outcome-blind feasibility shows adequate variation after those controls; it is not a new independent signal family.

## Falsification and gates

- Before any outcome access, verify schema/version coverage, non-overlapping 10-second bar construction, exact volume units, mark semantics, gaps/reconnects, and minimum independent mint and market-time-block support. Do not backfill missing intervals.
- Freeze one `D`, one 60-second feature window, and the existing fixed 60-minute downside target. Compare the existing baseline against that baseline plus this single feature in time-forward, mint-disjoint folds, with full-denominator unknown counts, a fixed matched alert rate, family correction, and uncertainty clustered by mint and market-time block.
- Report whether the term adds calibrated risk information beyond contemporaneous market cap, gross volume, absolute return/volatility, buyer/seller breadth, flow imbalance, pool age, depth, and market-time. If it adds nothing after these controls, drop it rather than tune a different window or scaling.
- A reserve-mark result is not execution utility. Any later policy evaluation must separately use the already-approved attainable paper entry/exit assumptions, fees, impact, failed exits, and locked forward cohort; this note does not authorize that test or any capture change.

**Kill conditions:** incomplete/selective bar coverage; unreliable volume or mark semantics; inadequate independent support; near-deterministic restatement of existing controls; no incremental time-forward calibration or matched-rate loss reduction; or no improvement after fixed execution costs. No live trading is authorized.
