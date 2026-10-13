# Jupiter quote API terms screen (2026-10-13)

**Disposition:** do not call Jupiter's Swap API for the proposed Jupiter-versus-CEX research comparison unless Jupiter first gives written permission for that use.

The official [SDK & API License Agreement](https://developers.jup.ag/docs/legal/sdk-api-license-agreement) grants use for internal development, including informational, comparison, or testing purposes (section 2.1). But section 3.2(f) also prohibits accessing the API for competitive analysis, and section 3.2(g) prohibits combining API content with content from scraping or other means. The queued lead would compare Jupiter quote output against an independent CEX reference, so its fit under the agreement is ambiguous and may fall within both restrictions. The terms reviewed do not establish a right to retain the quote data for the proposed research period.

Treat this as a hard operational gate, not a legal conclusion: make no `/order` call, do not combine any Jupiter output with external market data, and do not start capture unless written permission expressly covers comparative research and the needed data retention. If permission is unavailable, drop this source path. Reconsider only a non-Jupiter quote source whose documented terms allow the intended use and retention, subject to a separate novelty and feasibility screen.

No API request, account/key setup, RPC/provider request, capture, or market/outcome-data access was made. This screen is based on the published agreement and does not interpret other contracts or jurisdiction-specific law.
