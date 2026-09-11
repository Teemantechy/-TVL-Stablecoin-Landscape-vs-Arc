# -TVL-Stablecoin-Landscape-vs-Arc
A cross-chain comparison of TVL, stablecoin supply, real-world asset (RWA) activity, and daily active addresses across six major blockchains — built ahead of Circle's Arc mainnet launch (Sept 16, 2026) to establish the current benchmark Arc's institutional RWA positioning will be measured against.
## 🔗 Live Dashboard
[View the interactive dashboard on Tableau Public](https://public.tableau.com/app/profile/taiwo.adigun/viz/TVLStablecoinLandscapevsArc/TVLStablecoinLandscapevsArc?publish=yes)

## Chains covered
Ethereum, Solana, Base, Arbitrum, Optimism, Robinhood Chain

*(BSC was deliberately excluded — out of scope for this comparison.)*

## Key findings
- **Ethereum dominates RWA activity** — $14.8B RWA Active Mcap, more than 17x Base and 3x+ the next-closest chain (Solana). This is the specific bar Arc's institutional positioning will be judged against once it launches.
- **Robinhood Chain (7 weeks old) already outpaces Base (3 years old) on daily active addresses** — 470,859 vs 415,089 — suggesting real usage, not just idle capital.
- **Data-quality catch:** while pulling DEX volume in an earlier phase of this project, wash-trading transactions were found inflating Base's reported 30-day DEX volume by ~81% and Robinhood Chain's by ~56%, both via a handful of transactions trading obscure/illiquid tokens with each swap leg logged twice in the source table. See `scripts/dex_dominance_cleaned.sql` for the full diagnostic and fix.

## Data sources
- **TVL, Stablecoins Mcap, RWA Active Mcap, and most Active Addresses figures:** [DeFiLlama](https://defillama.com) chain overview pages
- **Active Addresses for Robinhood Chain and OP Mainnet** (not surfaced directly by DeFiLlama): pulled via Dune Analytics — see `scripts/active_addresses_24h.sql`
- **DEX volume diagnostics** (earlier project phase): Dune Analytics `dex.trades` table — see `scripts/dex_dominance_cleaned.sql`

## Methodology notes
- All figures reflect a snapshot near the time of writing; Arc is included as a pre-launch placeholder (no live data yet — mainnet launches Sept 16, 2026) with its founding validators (BlackRock, Visa, Mastercard, DTCC, Standard Chartered) and day-one native assets (USDC, USYC) noted for context.
- DEX volume figures were cross-checked against external published benchmarks (not just internal consistency) before being trusted — see the diagnostic queries for the full process of catching and correcting wash-trading inflation.
- Raw Dune text exports were reshaped into clean CSVs using `scripts/parse_dune_export.py`, which handles Dune's column-per-line export format and a known quirk where header rows can repeat mid-table.

## Repo structure
├── README.md
├── scripts/
│ ├── parse_dune_export.py # Reshapes raw Dune text exports into clean CSVs
│ ├── active_addresses_24h.sql # Pulls Active Addresses via Dune (Robinhood Chain, OP Mainnet)
│ └── dex_dominance_cleaned.sql # Full diagnostic + cleaned DEX volume query (wash-trade detection & fix)
├── data/
│ └── chain_metrics_comparison.xlsx # Final cleaned comparison table
└── dashboard/
└── (Tableau workbook / exported dashboard image)

## Tools used
Dune Analytics · DeFiLlama · Excel (Power Query) · Tableau

## Next steps
Once Arc's mainnet is live (Sept 16, 2026+), the placeholder row will be replaced with real TVL, stablecoin, RWA, and active address figures for a direct post-launch comparison against the established chains above.
