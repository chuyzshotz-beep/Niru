# PumpSwap global fee-config change screen

**Status:** unapproved, future-only accounting/regime hypothesis. This is not a predictive entry signal, a strategy change, or authorization for RPC, capture, or outcome access.

## Question and distinction

If PumpSwap emits a verified fee-configuration update that changes applicable rates, does the rate change alter the fee-adjusted net utility of the existing fixed paper policy? This is a protocol-wide cost-regime question, distinct from the existing per-transaction 420-SOL fee-tier transition screen and fee-recipient throughput screen. A rate update may improve cost accounting without creating predictive alpha.

The pinned [official PumpSwap documentation](https://github.com/pump-fun/pump-public-docs/blob/639b87fb45c3adeffa6f7c4a1bf0cb85e392bf22/docs/PUMP_SWAP_README.md) describes `update_fee_config` as changing the global config's LP/protocol rates and recipients. The matching [IDL](https://github.com/pump-fun/pump-public-docs/blob/639b87fb45c3adeffa6f7c4a1bf0cb85e392bf22/idl/pump_amm.json) defines `UpdateFeeConfigEvent` with a timestamp and LP, protocol, and creator fee-rate fields. The local IDL has the same event. These are documented-schema facts only; they do not prove which fields a deployed instruction version changes, the activation boundary, or that a historical rate change occurred.

## Measurement and identification gate

The current scraper subscribes to PumpSwap logs at `processed` commitment, but its decoder accepts only BuyEvent and SellEvent discriminators and the scraper persists only decoded trades. It therefore does not provide a finalized fee-config event history or prove which config applied to any historical swap. Do not infer a rate change from an IDL, current fee page, market-cap tier, or a creator/recipient address.

Before any study, a separately authorized outcome-blind source review must establish a complete finalized sequence of fee-config events, each event's actual effective time, and transaction-level reconciliation that the reported rates match the fees users paid. Exclude the event's admin, authority, and fee-recipient addresses from analysis and output.

A single global before/after transition is not causal evidence: market regime, slot duration, protocol upgrades, launch mix, and other fee or routing changes can move at the same time. Continue only if there are multiple usable changes with distinct timing or a credible unaffected comparison group and sufficient independent time blocks. Otherwise stop at accounting feasibility and do not describe a pre/post difference as an edge.

If those gates pass, compare the existing fixed paper policy with identical entry/exit rules, fills, latency, fee, slippage, and finite-capital assumptions before and after each verified rate transition. The primary result is the change in net policy utility after applying the observed rate schedule; fixed-window downside or activity changes are secondary diagnostics. Keep the frozen Oct 9-22 cohort and holdout untouched. Any outcome test requires a separately reviewed, hash-locked prospective cohort after `2026-10-23T01:05:00Z`.

## Kill conditions

Drop the lead if no verified effective rate change exists, event coverage or finality is incomplete, event fields do not reconcile to actual trade fees, the change is perfectly confounded with a regime or protocol transition, there are too few independent transitions/time blocks, or any apparent benefit disappears under identical net-cost assumptions. No event capture, RPC/provider request, raw outcome inspection, holdout access, wallet linkage, or live trading is authorized by this screen.

