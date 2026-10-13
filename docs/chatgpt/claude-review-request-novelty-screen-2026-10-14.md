# Claude review request: find a genuinely new, testable edge

Read `AGENTS.md` first and obey every hard rule. This is a bounded, read-only novelty review. Do not edit files, run commands/tests, inspect raw data/outcomes/holdouts/ledgers/secrets, query RPC/provider services, or use paid APIs.

Read only:

- `docs/chatgpt/novelty-screen-pumpswap-events-and-pump-gold-2026-10-14.md`
- `docs/plans/` file names plus targeted relevant sections for any proposed candidate
- `CODEX_REPORT.md` candidate headings and relevant sections
- Official Pump documentation or primary research sources needed to verify the candidate mechanism

First assess this specific low-confidence lead: a point-in-time deviation in a fixed-size SOL sell quote on Solana DEX routes versus an external CEX reference, as a market-wide execution-stress modifier. Current related work includes static Coinbase SOL book imbalance, bid-removal resilience, and BTC shock; RED-ARB v1.1 is only mechanism/data context, not validation. Jupiter Swap V2 documents quote-only `/order` requests without `taker`, but its documented response has no quote timestamp/context slot; the free plan lists 1 request/second. Assess whether local request/response bracketing can support a sufficiently precise prospective observation or whether timing, quote/reference mismatch, transfer limits, and market overlap kill it. Decide whether a cost- and stablecoin-basis-adjusted quote deviation is materially distinct and plausibly incremental. If it fails, find at most one other idea that is materially distinct from the already-screened candidates and could plausibly improve a point-in-time paper decision after costs.

Do not use wallet linkage across tokens, copy-trading, identity resolution, creator/funder clusters, address-based attribution, or another trader's calls. Do not relabel a known risk/accounting mechanism as alpha.

For a candidate, report: mechanism; exact point-in-time observable and clock; comparator/null; confounds; current capture gap; outcome-blind feasibility gate; later time-forward test; and explicit kill condition. Cite primary sources. If no idea clears the gates, answer `none` and explain the decisive blockers. A documented mechanism or public prevalence result alone is not an NIRU edge.
