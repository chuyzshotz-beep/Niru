# Pump trade v2/v3 buyback-fee screen (2026-10-13)

**Disposition:** no distinct token-level entry edge. Treat the new fee fields as trade-accounting and decoder-version requirements, not evidence of a token buyback or predictive demand.

## Mechanism checked

Pump's current PumpSwap v2 and bonding-curve v3 trade docs define `buyback_fee` as the buyback portion of the protocol fee and direct that amount to one of eight fee-recipient accounts during the trade. The caller supplies the recipient account; the trade documentation does not describe an automatic purchase of the token being traded. The remaining protocol fee on v2/v3 stays in the pool or curve and is recorded for a later sweep. The v2 event reports the fee amount and a zero protocol-fee-recipient key for retained fees; the v3 event similarly reports the fee amount and fee-sweep accounting fields.

This does not support interpreting the `buyback_fee` event field as token-specific buy pressure, or treating recipient selection as an independent signal. Any apparent price effect would be confounded with ordinary swap size, the existing fee schedule, reserve changes, and the later sweep. The fee accounting also overlaps the existing global-fee-config and fee-sweep screens.

## Research disposition

- Do not add a buyback-flow feature or entry rule from this field.
- For any separately approved future trade-ledger study, version the v1/v2/v3 instruction path and reconcile each trade's protocol, creator, LP, and buyback fee fields against the contemporaneous pool/curve state and later sweep before measuring executable prices.
- The local scraper's current trade-row schema and active decoder version were not audited in this screen; the published IDL alone does not establish deployed-version coverage or historical activation.
- No RPC/provider request, capture, transaction, raw market row, outcome, holdout, wallet linkage, code, test, or strategy change was performed.

## Primary sources

- [PumpSwap Trades V2](https://github.com/pump-fun/pump-public-docs/blob/main/docs/instructions/PUMP_SWAP_TRADE_V2.md)
- [Bonding Curve Trades V3](https://github.com/pump-fun/pump-public-docs/blob/main/docs/instructions/TRADE_V3.md)
- [Fee sweeps](https://github.com/pump-fun/pump-public-docs/blob/main/docs/instructions/SWEEP_FEES.md)
- This overlaps the project's existing global fee-configuration and fee-sweep accounting screens; keep it folded into those mechanisms rather than opening a parallel signal family.
