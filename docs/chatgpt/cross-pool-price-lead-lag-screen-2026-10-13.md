# Same-mint cross-pool price-lead screen (2026-10-13)

**Disposition:** distinct from alternate-route execution value, but low-confidence and not capture-ready. This is a prospective market-microstructure hypothesis, not a proven signal or authorization to collect data.

## Candidate

PumpSwap permits multiple pools for the same base/quote pair. Test whether a short-horizon price move in a noncanonical pool tends to precede a move in the canonical migration pool for the same mint. The plausible mechanism is price discovery across fragmented pools; the sign and useful horizon are unknown. This asks whether one pool's already-observed price innovation adds information about the canonical pool's *future* move. It is distinct from comparing current direct-pool sell quotes to find a better execution route, though the features may be correlated and must be tested against that control. [PumpSwap pool model](https://github.com/pump-fun/pump-public-docs/blob/main/docs/PUMP_SWAP_README.md)

## Point-in-time definition and comparison

At each predeclared decision time `D`, use a fixed 30-second lookback. Before the window begins, freeze the eligible alternative-pool set using same-mint, same-quote-mint pools that have a valid fixed-size quote and meet a predeclared depth rule at `D-30s`. Include only successful pool swaps first received by the observer no later than `D`. Compute each pool's marginal price from version-validated post-swap reserves and effective quote reserves. Define `alt_residual_D` as the median eligible noncanonical pool log return over `[D-30s,D]` minus the canonical pool log return over that interval. Use local monotonic first-receipt time for the feature window; do not substitute block time for observation time. Test whether `alt_residual_D` adds to the canonical pool's next 30-second return, versus the same-mint canonical return, activity/flow, depth, current exact-route quote advantage, and broad market controls. Treat direction as unknown until the time-forward test. A fixed-size executable sell-value endpoint may be secondary; do not tune the lookback, depth rule, or direction on outcomes.

This residual makes no claim about transaction order within a slot: Solana's `logsSubscribe` notification documents a slot, signature, error, and logs, but no transaction index, so never label a same-slot pool as the on-chain leader from notification arrival order. Processed events are provisional and may roll back. A later finalized-block reconciliation may validate an event but must not backdate it into the feature window. [logsSubscribe](https://solana.com/docs/rpc/websocket/logssubscribe) [commitment levels](https://solana.com/docs/rpc)

## Coverage gap and gates

Static inspection of `C:\Users\Jesus\Downloads\NIRU3_FINAL_AI_SNIPER_AUTO_WALLETS\arena\scraper.mjs` found that it subscribes to PumpSwap logs at `processed` commitment but keeps a trade only when `pools.has(ev.pool)`; the existing pool map is built for tracked graduate pools, and the decoder accepts only `BuyEvent`/`SellEvent`. The current tape therefore does not establish complete alternate-pool discovery, all-pool swap coverage, or event-state reconciliation. No RPC request, stream capture, data-row, outcome, or holdout was inspected.

Before any cohort, require an outcome-blind demonstration that eligible mints have multiple same-quote pools with enough fixed-size depth; the pool universe, depth rule, reserve/fee math, event versions, first-receipt timestamps, reconnect gaps, and rollback handling are complete; and the feature is available at the intended decision time. Keep missing/incomplete pools unknown. If this requires a new provider or RPC request, seek separate owner approval first. Compare the candidate inside the existing path/market-context feature family using a later mint-disjoint, time-forward paper test with identical fills, fees, slippage, fixed-cost utility, and multiplicity correction.

Drop it if multi-pool eligible coverage is sparse or activity-selected; event order, reserves, fees, or receipt times cannot be reconciled; apparent lead is only same-slot arbitrage or current price divergence; or it adds no stable out-of-sample utility beyond canonical price path, market controls, and executable route value. A documented ability to create multiple pools is not evidence that enough independent pools exist or that this effect predicts returns.

## Related project screen

The current same-pair route-advantage screen tests whether an alternate pool improves an executable quote; it explicitly does not claim that price predicts returns. Keep this candidate separate only if its temporal feature and future-return test survive the controls above. [Same-pair route-advantage screen](C:/Users/Jesus/Downloads/NIRU3_FINAL_AI_SNIPER_AUTO_WALLETS/docs/plans/same-pair-pumpswap-route-advantage-screen-2026-10-13.md)
