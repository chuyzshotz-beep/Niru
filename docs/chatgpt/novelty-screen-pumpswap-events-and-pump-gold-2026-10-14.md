# Novelty screen: PumpSwap event surface and Pump-Gold dataset (2026-10-14)

**Disposition:** no new, testable entry edge identified in this pass. This is an outcome-blind source and plan-catalog screen, not an endorsement of the existing strategy. No local market rows, outcomes, holdout, wallet identities, or keys were inspected; no RPC/provider request or capture was made.

## PumpSwap event surface

Compared the checked-in Pump AMM IDL's instruction/event names with the current plan and research-note catalog. The candidate families already represented include global fee/config changes, LP deposits/withdrawals, volume incentives, boost buys/burns, holder-reward/CTO transitions, creator-fee splits, fee sweeps, and multi-hop routing. The full event list is not itself evidence of a signal or complete event capture.

One apparent gap was the global `disable` instruction and `DisableEvent`. The current official PumpSwap README says `disable_flags` can disable operations but is **currently not used**. Therefore this does not support a live halt predictor or a current entry filter. Revisit only if version-pinned deployment evidence shows the flags became active; otherwise drop it. The IDL and README are schema/documentation evidence, not a historical deployment or event-frequency audit. [PumpSwap README](https://github.com/pump-fun/pump-public-docs/blob/main/docs/PUMP_SWAP_README.md) [Pump AMM IDL](https://github.com/pump-fun/pump-public-docs/blob/main/idl/pump_amm.json)

## Public Pump-Gold dataset

The [repository README](https://github.com/Solid-Sea/pump-gold-dataset/blob/master/README.md) advertises 1,306,082 tokens and 17,033,442 trades, but the released core table is one row per token with aggregate buy/sell counts, unique wallets, total quote, average swap size, and whole-path `pmin`/`pmax`. The labels are defined from those full-path extremes (`pmax >= 10 * pmin` and `pmin > 0` for `golden`; `pmax < 2 * pmin` for `dead`). The public evaluation script uses a random train/test split. Those artifacts do not preserve decision-time features or a chronological holdout; lifetime activity is unavailable at a fixed entry decision, and any use of path extrema as features would directly leak the label. It is not suitable to validate a point-in-time PumpSwap entry signal. The repository declares CC BY 4.0, but licensing does not fix the temporal-schema limitation. [Dataset license](https://github.com/Solid-Sea/pump-gold-dataset/blob/master/LICENSE) [Evaluation script](https://github.com/Solid-Sea/pump-gold-dataset/blob/master/rf_classifier_eval.py)

## Next gate

Do not add a feature or collect data from this screen. Ask Claude for an independent novelty pass over the named current plan/report catalog after its reported Pro reset. Require a specific mechanism, point-in-time observable and clock, comparator/null, confounds, current-capture gap, outcome-blind feasibility gate, time-forward test, and kill condition. Prohibit wallet linkage, copying another trader, identity resolution, raw outcome/holdout inspection, RPC/provider spend, or live execution. If no candidate survives those requirements, record `none` rather than minting another screen.
