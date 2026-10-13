# PumpSwap volume-accumulator close: working-capital follow-up (2026-10-13)

**Disposition:** a protocol-accounting / capital-availability question, not a predictive entry or exit edge. The close path deserves a targeted static and versioned-semantics check because the current Pump AMM IDL includes `close_user_volume_accumulator`; the existing first-touch screen should treat close-instruction presence as known and rent-recipient behavior as unresolved.

## What the published schema establishes

The checked-in `arena/idl/pump_amm.json` and Pump's current public [Pump AMM IDL](https://github.com/pump-fun/pump-public-docs/blob/main/idl/pump_amm.json) list `close_user_volume_accumulator`. The instruction has no arguments; its account schema marks `user` writable and signer, and `user_volume_accumulator` writable. The accumulator PDA is seeded from the user, so the schema represents one user-scoped accumulator rather than one per mint. The IDL account list does not specify a close destination or encode a close constraint, so it cannot by itself prove that rent goes to `user`, when closure is permitted, or whether an outstanding balance/state prevents closure. The corresponding `CloseUserVolumeAccumulatorEvent` name is also present, but event presence alone does not prove deployed behavior.

## Narrow candidate and test

For one hypothetical paper wallet, measure only the wallet-level capital tied up in a required accumulator, any recoverable amount actually returned on a valid close, and the network/priority cost to close it. If closing requires recreating the accumulator for later trades, charge the next creation too. Keep this separate from token-level trade PnL and from any attribution of global incentive claims. It may change capital utilization for a multi-token paper portfolio; it does not predict which mint will rise or fall.

Before a prospective replay, require an authoritative, version-pinned confirmation of the deployed close handler, eligibility/state preconditions, exact rent destination, whether the account can be recreated, and whether the close event is emitted only after successful account closure. Then use a fixed wallet-level trade schedule and compare available capital with and without closing, net of all creation/close transaction costs. Report the maximum capital released and the realized recovery separately; do not count a refund until a successful close and balance delta are independently verified.

Drop the capital-efficiency case if the close path is unavailable for the relevant instruction version, the refund destination is not the modeled wallet, closure requires costly or impractical state changes, or net recovery is negligible against transaction costs. No transaction, RPC/provider request, raw event inspection, capture, outcome access, account creation, or strategy change was performed or authorized by this note.
