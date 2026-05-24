# Listing FDV Workflow (CMC/CG + DEXTools)

This document captures a reproducible workflow to compute **Listing FDV** for the provided token list.

## Formula

- `listing_fdv = listing_price * total_supply`

## Data sources

1. **CoinMarketCap / CoinGecko**: token contract address (CA) and total supply.
2. **DEXTools pair explorer (BSC / Pancake)**:
   - Find the Pancake pool with highest liquidity for the token CA.
   - In Trade History, sort ascending by time.
   - Find the first trade where `type = init`.
   - Use that trade price as `listing_price`.

## Example (provided)

- Project: EVAA
- CA: `0xaa036928c9c0df07d525b55ea8ee690bb5a628c1`
- Pair: `0x26deb24a2623cf54452ab5183e2c34551831d54d`
- init price: `$2`
- total supply: `50,000,000`
- listing FDV: `2 * 50,000,000 = 100,000,000`

## Batch execution template

For each project:

1. Resolve CA from CMC/CG by symbol and project name (avoid symbol collisions).
2. Pull total supply.
3. Open DEXTools pairs for that CA.
4. Choose highest-liquidity Pancake pair.
5. Read first `init` trade price.
6. Compute listing FDV.

## Output columns

- Symbol
- Project Name
- Chain
- CA
- Total Supply
- DEXTools Pair URL
- First `init` tx hash
- Listing Price (USD)
- Listing FDV (USD)
- Notes

