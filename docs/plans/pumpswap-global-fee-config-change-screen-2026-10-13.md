# PumpSwap global fee-config change screen

**Status:** unapproved, future-only accounting/regime hypothesis. This is not a predictive entry signal, a strategy change, or authorization for RPC, capture, or outcome access.

## Question and distinction

If a verified PumpSwap fee-configuration change alters pools' effective rates, does quote turnover per active pool-minute change around that transition? This is a protocol-wide flow/regime question, distinct from the existing per-transaction 420-SOL fee-tier transition screen and fee-recipient throughput screen. It is descriptive accounting, not a predictive entry signal or proof that changing fees caused a flow change.

The pinned [official PumpSwap documentation](https://github.com/pump-fun/pump-public-docs/blob/639b87fb45c3adeffa6f7c4a1bf0cb85e392bf22/docs/PUMP_SWAP_README.md) describes `update_fee_config` as changing the global config's LP/protocol rates and recipients. The matching [IDL](https://github.com/pump-fun/pump-public-docs/blob/639b87fb45c3adeffa6f7c4a1bf0cb85e392bf22/idl/pump_amm.json) defines `UpdateFeeConfigEvent` with a timestamp and LP, protocol, and creator fee-rate fields. The local IDL has the same event. These are documented-schema facts only; they do not prove which fields a deployed instruction version changes, the activation boundary, or that a historical rate change occurred.

## Measurement and identification gate

The current scraper subscribes to PumpSwap logs at `processed` commitment, but its decoder accepts only BuyEvent and SellEvent discriminators and the scraper persists only decoded trades. It therefore does not provide a finalized fee-config event history or prove which config applied to any historical swap. Do not infer a rate change from an IDL, current fee page, market-cap tier, or a creator/recipient address.

Before any study, a separately authorized, outcome-blind source review must establish a version-pinned, complete timeline of every instruction or state transition that can change relevant global economics, with finalized effective times. `UpdateFeeConfigEvent` alone is not a complete regime log: unresolved event, schema, deployment, or capture coverage means the window is unknown. Independently validate each sampled pool's effective pre/post rate from transaction-level fees and pool state, including tier, creator-fee override, cashback/holder-reward mode, Mayhem status, and other applicable settings. Exclude admin, authority, and fee-recipient addresses from analysis and output.

A single global before/after transition is not causal evidence: market regime, slot duration, protocol upgrades, launch mix, and other fee or routing changes can move at the same time. Multiple changes or more pools do not by themselves solve this identification problem. The single primary descriptive outcome is PumpSwap quote turnover per active pool-minute in fixed windows around each verified transition; buy/sell split is secondary. Continue beyond description only if a valid contemporaneous comparison or independently validated differential pool exposure exists, with sufficient independent time blocks. Otherwise report descriptive pre/post variation only and do not call it an edge or causal effect.

Keep this screen outcome-blind until the source and coverage gates pass. Any later strategy or predictive test is a separate, separately reviewed question; it must use identical paper-policy rules, fills, latency, fee, slippage, and finite-capital assumptions. Keep the frozen Oct 9-22 cohort and holdout untouched. Any outcome test requires a separately reviewed, hash-locked prospective cohort after `2026-10-23T01:05:00Z`.

## Kill conditions

Drop the lead if no verified effective rate change exists; any economics-relevant state, event, or finality coverage is incomplete; per-pool effective rates cannot be validated; or the pool-minute denominator is not measurable. If no valid comparison or independently validated differential exposure exists, stop at descriptive accounting regardless of event count. No event capture, RPC/provider request, raw outcome inspection, holdout access, wallet linkage, or live trading is authorized by this screen.
