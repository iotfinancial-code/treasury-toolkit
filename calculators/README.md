# Calculators

The maths behind the calculators on [iotfinancial.net](https://iotfinancial.net/tools/), written out from the site's own scripts so anyone can check it, rebuild it in a spreadsheet, or spot a mistake.

| File | Site tool | What it computes |
| --- | --- | --- |
| [allocation-sizing.md](allocation-sizing.md) | [Sizing tool](https://iotfinancial.net/guides/sizing/#tool) | Protected reserve, excess cash, allocation within the company's own limits, and a stress test |
| [custody-model-rules.md](custody-model-rules.md) | [Custody questionnaire](https://iotfinancial.net/guides/custody/#tool) | Six ordered rules from seven answers to one of four custody models |
| [custody-cost.md](custody-cost.md) | [Custody cost calculator](https://iotfinancial.net/learn/bitcoin-custody-cost-calculator/) | Yearly cost of four custody models from the user's own figures |
| [network-fees.md](network-fees.md) | [Fees and UTXOs](https://iotfinancial.net/learn/bitcoin-fees-and-utxos/) | Transaction size and fee, and consolidating now against spending later |
| [bitcoin-supply.md](bitcoin-supply.md) | [Supply curve](https://iotfinancial.net/learn/bitcoin-supply/) and [by the numbers](https://iotfinancial.net/learn/by-the-numbers/) | Block subsidy, total issued, and the next halving |

Each file lists its inputs, the formulas exactly as the site computes them, a worked example using the site's default inputs, and its sources.

Every default figure is an example only, not a quote, a typical price or a suggestion. The tools run in the browser and nothing typed into them leaves it.

Not covered here, because they are not formulas:

- The [readiness quiz](https://iotfinancial.net/learn/readiness-quiz/) counts how many of its ten questions were not answered yes and lists the matching pages.
- The [2 of 3 multisig simulator](https://iotfinancial.net/learn/multisig-2-of-3/) shows fixed scenarios (a lost key, a departing keyholder and so on), not a calculation.
- The [policy generator](https://iotfinancial.net/guides/policy/#tool) assembles clauses; its text is in [policy-template](../policy-template/).
- The [market context](https://iotfinancial.net/guides/market-context/) page shows live public data from third parties. Only its halving countdown is covered, in bitcoin-supply.md.

The formula blocks are shared under the MIT licence so they can be reused in code; the explanations are under CC BY 4.0. See the [README](../README.md#licences).

Education, not advice. The calculators show arithmetic on the user's own inputs. They are not a recommendation and do not take account of any company's circumstances.
