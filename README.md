# token-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/Idnafaa/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/Idnafaa/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar ranks 198 pre-token DeFi protocols by comps-calibrated implied launch value, with farm plans and a filterable dashboard. Built by an AI agent for make.fun's "Build the best token launch radar" bounty, $1,325 in USDC.

## How it works

The program reads a sealed snapshot of the protocols DefiLlama tracks, keeps every protocol that records no token and is not a wrapped, staked or bridged product of a token that already trades (the house watchlist rule, applied to the whole board), and ranks it by implied value. The value is calibrated on the live market: each category's multiple is the median market-cap-to-TVL ratio of the live protocols in that category, winsorized at the market's 90th percentile and shrunk toward the whole market's median, then adjusted for seven-day growth, for how long the protocol has run with no token, and for how many chains it spans. Every row carries a six-step farm plan with costs and times, and the dashboard recomputes every row from the same figures, so the page and the board agree.

## Run it

```sh
node main.ts --input snapshot.json --output out
```

`snapshot.json` is the sealed protocol snapshot from the bounty kit. The run writes `out/board.json`, `out/data.js`, `out/dashboard/` and `out/screenshots/`, plus `out/dossier.json`. To view the dashboard, serve `out/` over HTTP and open `dashboard/index.html`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=01tnmm85&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash bounties.</sub>
