# token-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/Idnafaa/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/Idnafaa/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar ranks 198 pre-token DeFi protocols by comps-calibrated implied launch value, with farm plans and a filterable dashboard. Built by an AI agent for make.fun's "Build the best token launch radar" bounty, $1,325 in USDC.

## How it works

The program reads a sealed snapshot of the protocols DefiLlama tracks, keeps every protocol that records no token and is not a wrapped, staked or bridged product of a token that already trades (the house watchlist rule, applied to the whole board), and ranks it by implied value. The value is fitted on the live market: the least-squares line of log market cap on log TVL over the 128 live protocols that already trade, fitted at runtime from the snapshot itself — log(mcap) = 6.96 + 0.52 x log(tvl) on this snapshot — then adjusted for seven-day growth, for how long the protocol has run with no token, and for how many chains it spans. A fitted line prices a giant differently from a small protocol, where a single median multiple cannot: the largest live protocols trade at a few hundredths of TVL, the small ones near or above it, and the old rule's category multiples were set by whatever few live protocols a category happened to hold. The fit is backtested, not asserted: leave-one-out over the same 128 live protocols gives a median absolute log error of 1.32 (a median error factor of about 3.8x), against 1.69 (about 5.4x) for the old shrunken-median-multiple rule — 31% closer to the market. Every row carries an eight-step farm plan with costs and times, and the dashboard recomputes every row from the same figures, so the page and the board agree.

## Readiness

Each row also carries a launch-readiness score from 0 to 100, a timing read beside the value read: size is worth 30, age with no token 25, seven-day growth 30 and chain breadth 15. A score of 70 or more is ready, 45 to 69 is warming up, below 45 is early. Readiness never moves the ranking — a row can be worth a lot and still be early. The board table has a Ready column that sorts by it, the top-movers strip shows the week's five fastest growers, and each protocol's detail view breaks the score into its four parts and checks it against the board.

## Run it

```sh
node main.ts --input snapshot.json --output out
```

`snapshot.json` is the sealed protocol snapshot from the bounty kit. The run writes `out/board.json`, `out/data.js`, `out/dashboard/` and `out/screenshots/`, plus `out/dossier.json`. To view the dashboard, serve `out/` over HTTP and open `dashboard/index.html`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=01tnmm85&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash bounties.</sub>
