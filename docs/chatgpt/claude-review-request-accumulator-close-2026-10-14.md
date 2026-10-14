# Claude review request: PumpSwap accumulator-close capital recovery

Read the project `AGENTS.md` first and obey its hard rules. This is a bounded, read-only protocol and accounting review. Do not edit project files, run commands/tests, inspect raw trades/outcomes/ledgers/holdouts, query RPC/provider services, use accounts or keys, or contact wallets.

Review only:

- `docs/chatgpt/pumpswap-volume-accumulator-close-screen-2026-10-13.md`
- `docs/plans/pumpswap-first-touch-rent-working-capital-screen-2026-10-13.md`
- Official Pump sources needed to check the claims: Pump AMM IDL, PumpSwap V2 trade docs, and the cashback documentation/issue cited from official Pump docs

Answer with source evidence:

1. Does the current official Pump AMM IDL include `close_user_volume_accumulator`; what do its accounts and PDA seeds establish, and what do they leave unknown?
2. Distinguish the accumulator account from any quote-token ATA owned by the accumulator. Keep legacy cashback rules separate from PumpSwap V2.
3. Do official sources establish the close preconditions, rent destination, treatment of outstanding incentives/cashback, or whether a later trade recreates the account? If not, say which facts remain unknown; do not infer them from SDK helper names or an event name.
4. Is a fixed, one-wallet capital-availability comparison a meaningful operational accounting test after all creation/close and priority costs, or is the possible recovery too small / unsupported to prioritize?
5. Confirm the disposition: capital availability or fee accounting only, not an entry/exit predictor and not an edge claim.

Do not use the public-data issue reporter's account as authoritative proof of deployed behavior. No transaction or RPC lookup is requested. `none` is an acceptable conclusion if source evidence cannot support the capital-recovery hypothesis.
