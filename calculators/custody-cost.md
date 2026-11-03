# Custody cost

The maths behind the [custody cost calculator](https://iotfinancial.net/learn/bitcoin-custody-cost-calculator/). It adds up the yearly cost of four ways to hold bitcoin exposure: hardware, fees, insurance and staff time.

The calculator only adds up the numbers the user enters. It does not know any provider's prices. Every default is a round number chosen to show how the sum works; none is a quote or a typical price. Cost is not risk: the cheapest model is not automatically the right one.

## Shared inputs

| Input | Meaning |
| --- | --- |
| `value` | Value of the holding |
| `hourly` | Staff cost per hour |

Any blank, non-numeric or negative input counts as 0. A device life of 0 counts as 1 year.

## Formulas, per year

```
(a) Self-managed 2 of 3 multisig
    devices * pricePerDevice / yearsBeforeReplacing
  + backupsAndSecureStorage
  + networkFees
  + insurance
  + staffHours * hourly

(b) Collaborative multisig
    devicesYouHold * pricePerDevice / yearsBeforeReplacing
  + serviceFee
  + networkFees
  + insurance
  + staffHours * hourly

(c) Regulated custodian
    max(value * custodyFeePct / 100, minimumFee)
  + withdrawalFees
  + extraInsurance
  + staffHours * hourly

(d) Exchange-traded fund or note
    value * ongoingChargePct / 100
  + platformAndDealing
  + insurance
  + staffHours * hourly

shareOfHolding = total / value * 100      (shown as n/a if value is 0)
```

Totals are shown rounded to whole pounds or dollars, and the share of the holding to two decimal places.

## Worked example with the default inputs

Example figures only: `value` 250,000 and `hourly` 50.

| Model | Inputs | Per year | Share of holding |
| --- | --- | --- | --- |
| (a) Self-managed 2 of 3 | 3 devices at 150 over 5 years (90), storage 200, network 30, insurance 0, 16 hours (800) | 1,120 | 0.45% |
| (b) Collaborative | 2 devices at 150 over 5 years (60), service fee 1,000, network 30, insurance 0, 10 hours (500) | 1,590 | 0.64% |
| (c) Custodian | 0.4% of value (1,000) or the 1,500 minimum, whichever is higher (1,500), withdrawals 50, insurance 0, 6 hours (300) | 1,850 | 0.74% |
| (d) Fund or note | 0.25% of value (625), platform and dealing 100, insurance 0, 2 hours (100) | 825 | 0.33% |

Percentage fees grow with the value of the holding. Fixed costs such as devices and staff time do not, so the comparison changes as the holding changes. A fund or note is a security, not bitcoin: the company holds no keys and cannot move bitcoin on chain.

## Sources

The formulas are the site's own sum of the user's inputs. The page cites these sources for how funds and notes work (checked 31 October 2026):

- SEC, Updated Investor Bulletin: Exchange-Traded Funds (ETFs): https://www.investor.gov/introduction-investing/general-resources/news-alerts/alerts-bulletins/investor-bulletins-24
- SEC, Investor Bulletin: exchange-traded products providing exposure to bitcoin and ether (September 2024): https://www.investor.gov/introduction-investing/general-resources/news-alerts/alerts-bulletins/investor-bulletins/ETPBulletinSeptember2024
- FCA, FCA opens retail access to crypto ETNs (in force 8 October 2025): https://www.fca.org.uk/news/press-releases/fca-opens-retail-access-crypto-etns

Source of the maths: the calculator script on https://iotfinancial.net/learn/bitcoin-custody-cost-calculator/, checked 3 November 2026.
