# Bitcoin supply and halvings

The maths behind the [supply curve](https://iotfinancial.net/learn/bitcoin-supply/) chart, the live counters on [by the numbers](https://iotfinancial.net/learn/by-the-numbers/), and the halving countdown on the [market context](https://iotfinancial.net/guides/market-context/) page.

Bitcoin's supply is set by a schedule in the software: each block pays a subsidy that started at 50 BTC and halves every 210,000 blocks, rounded down to whole satoshis (1 BTC = 100,000,000 satoshis).

## Subsidy and supply

```
era(h)     = floor(h / 210000)
subsidy(h) = (era(h) >= 64) ? 0 : floor(5,000,000,000 / 2^era(h))      in satoshis

supplyAt(h) = sum of subsidy(b) for every block b from 0 to h inclusive
            computed era by era:
            for each era e while e * 210000 <= h and subsidy(e * 210000) > 0:
                end = min(h, e * 210000 + 209999)
                add (end - e * 210000 + 1) * subsidy(e * 210000)
```

Results the page states, which follow from the schedule:

- There are 33 eras in which the subsidy is at least one satoshi. Era 0 pays 5,000,000,000 satoshis (50 BTC) per block.
- The last block with a subsidy is block 6,929,999.
- Summing every era gives 2,099,999,997,690,000 satoshis, which is 20,999,999.9769 BTC, just under 21 million.

The live counters use the current block height `h` from mempool.space:

```
issued         = supplyAt(h) / 100,000,000                   BTC
share issued   = supplyAt(h) / 2,100,000,000,000,000 * 100   per cent of 21 million
left to issue  = (2,100,000,000,000,000 - supplyAt(h)) / 100,000,000   BTC
blocks         = h + 1                                        (block 0 is the genesis block)
```

## Halvings

```
next halving height = (era(h) + 1) * 210000
blocks to go        = next halving height - h
days to go (about)  = blocks to go * 10 / 1440
```

The halving date is an estimate from the 10 minute block target. Real block times vary, so the date moves. This is a schedule estimate, not a forecast of anything else.

The halvings so far, from the block explorer:

| Halving | Block | Date (UTC) | Subsidy after |
| --- | --- | --- | --- |
| First | 210,000 | 28 November 2012 | 25 BTC |
| Second | 420,000 | 9 July 2016 | 12.5 BTC |
| Third | 630,000 | 11 May 2020 | 6.25 BTC |
| Fourth | 840,000 | 20 April 2024 | 3.125 BTC |
| Fifth | 1,050,000 | not yet reached | 1.5625 BTC |

## Dates on the chart

The chart places each block on a date by straight-line interpolation between known points: the genesis block (3 January 2009, 18:15:05 UTC), the four halvings above, and the current tip at the current time. Beyond the tip it assumes 600 seconds (10 minutes) per block.

## Sources

- Bitcoin Core, `src/validation.cpp`, `GetBlockSubsidy`: https://github.com/bitcoin/bitcoin/blob/master/src/validation.cpp
- Bitcoin Core, `src/consensus/amount.h`, `COIN` and `MAX_MONEY`: https://github.com/bitcoin/bitcoin/blob/master/src/consensus/amount.h
- Bitcoin Core, `src/kernel/chainparams.cpp`, halving interval, block target and genesis block: https://github.com/bitcoin/bitcoin/blob/master/src/kernel/chainparams.cpp
- mempool.space, block 210,000: https://mempool.space/block/210000
- mempool.space, block 420,000: https://mempool.space/block/420000
- mempool.space, block 630,000: https://mempool.space/block/630000
- mempool.space, block 840,000: https://mempool.space/block/840000
- mempool.space REST API (current height): https://mempool.space/docs/api/rest

Source of the maths: `site/assets/explore.js` and `site/assets/market.js` on iotfinancial.net, checked 3 November 2026.
