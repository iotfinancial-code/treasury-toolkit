# Network fees and UTXO consolidation

The maths behind the two calculators on [fees and UTXOs](https://iotfinancial.net/learn/bitcoin-fees-and-utxos/).

A bitcoin network fee does not depend on the amount sent. It depends on the size of the transaction in virtual bytes (vB) and on the fee rate in satoshis per virtual byte (sat/vB) that the sender chooses:

```
fee = size in vB * fee rate in sat/vB
```

## Size estimate

The calculator assumes native SegWit 2 of 3 multisig inputs. Real sizes vary by a few bytes, and other wallet types differ, so check with the wallet before sending.

```
IN  = 104.5   vB per input  (native SegWit 2 of 3 multisig)
OUT = 43      vB per output
OH  = 10.5    vB fixed overhead

vsize(inputs, outputs) = OH + IN * inputs + OUT * outputs
fee                    = ceil(vsize * rate)           in satoshis
```

Inputs and outputs are rounded to whole numbers with a minimum of 1. The fee rate has a minimum of 0.1 sat/vB. The size is shown rounded up to a whole vB.

Example with the defaults (example only): 3 inputs, 2 outputs, 5 sat/vB gives 410 vB and a fee of 2,050 sats (0.00002050 BTC).

## Consolidate now or spend later

Compares spending many small UTXOs later at a high fee rate with consolidating them into one now at a low rate, then spending that one later.

```
n  = number of small UTXOs  (whole number, minimum 2)
lo = fee rate now           (sat/vB, minimum 0.1)
hi = fee rate later         (sat/vB, minimum 0.1)

later       = ceil(vsize(n, 2) * hi)     spend all n later, payment plus change
consolidate = ceil(vsize(n, 1) * lo)     n inputs into 1 output now
after       = ceil(vsize(1, 2) * hi)     spend the single UTXO later
total       = consolidate + after
difference  = later - total              positive: consolidating saves; negative: it costs
```

Example with the defaults (example only): 20 UTXOs, 2 sat/vB now, 30 sat/vB later.

| Step | Sats |
| --- | --- |
| Spend all 20 later at 30 sat/vB | 65,595 |
| Consolidate now at 2 sat/vB | 4,287 |
| Then spend 1 input later at 30 sat/vB | 6,030 |
| Total | 10,317 |
| Difference | saves 55,278 |

The fee rates are inputs the user chooses. The calculator does not predict future fee rates. Consolidating also links the UTXOs together on chain, which the page discusses.

## Sources

- BIP 141, Segregated Witness (weight and virtual size): https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki
- BIP 11, M of N standard transactions: https://github.com/bitcoin/bips/blob/master/bip-0011.mediawiki
- BIP 125, opt-in replace by fee: https://github.com/bitcoin/bips/blob/master/bip-0125.mediawiki
- Bitcoin developer guide, transactions: https://developer.bitcoin.org/devguide/transactions.html
- Bitcoin Optech, transaction size calculator: https://bitcoinops.org/en/tools/calc-size/
- Bitcoin Optech, fee estimation: https://bitcoinops.org/en/topics/fee-estimation/
- Bitcoin Optech, coin selection: https://bitcoinops.org/en/topics/coin-selection/
- Bitcoin Optech, child pays for parent: https://bitcoinops.org/en/topics/cpfp/
- Bitcoin Optech, UTXO consolidation case study: https://bitcoinops.org/en/xapo-utxo-consolidation/
- Bitcoin white paper: https://bitcoin.org/bitcoin.pdf
- mempool.space REST API (live fee rates): https://mempool.space/docs/api/rest
- IRS, Digital assets (fees and records): https://www.irs.gov/businesses/small-businesses-self-employed/digital-assets
- eCFR, 26 CFR 1.1001-7 (digital asset transactions): https://www.ecfr.gov/current/title-26/section-1.1001-7

Source of the maths: the calculator script on https://iotfinancial.net/learn/bitcoin-fees-and-utxos/, checked 3 November 2026.
