# Allocation sizing

The maths behind the [sizing tool](https://iotfinancial.net/guides/sizing/#tool) in the [allocation sizing guide](https://iotfinancial.net/guides/sizing/). It turns a company's own figures and limits into a bitcoin allocation that leaves the cash the business needs untouched. The guide explains [why reserves come first](https://iotfinancial.net/guides/sizing/#why), [the formulas](https://iotfinancial.net/guides/sizing/#formulas) and [how to choose the limits](https://iotfinancial.net/guides/sizing/#choosing).

This is the site's own worked method for illustration. It is not a rule from a regulator or a standard, and it is not a recommended allocation. Every input is the company's own choice.

## Inputs

| Input | Meaning |
| --- | --- |
| `cash` | Total cash today |
| `monthly` | Monthly operating costs (the burn) |
| `months` | Months of costs to keep as a reserve |
| `obligations` | Known payments due (tax, payroll, loans and similar) |
| `pct` | Most of the excess the policy allows in bitcoin, in per cent (held between 0 and 100) |
| `hardCap` | Optional fixed maximum amount. 0 or blank means no fixed cap |
| `fall` | A price fall to test, in per cent (held between 0 and 100). A stress test the user chooses, not a forecast |

Inputs are read as plain numbers: anything other than digits and a decimal point (commas, currency signs, minus signs) is ignored, and a blank input counts as 0.

## Formulas

```
protected   = monthly * months + obligations
excess      = max(0, cash - protected)
byPct       = excess * pct / 100
allocation  = (hardCap > 0) ? min(byPct, hardCap) : byPct
limitedBy   = (hardCap > 0 and hardCap < byPct) ? "hard cap" : "percentage cap"

shareOfCash     = allocation / cash * 100          (0 if cash is 0)
scenarioLoss    = allocation * fall / 100
runwayAfterLoss = (cash - scenarioLoss - obligations) / monthly
                  (not shown if monthly is 0)
shortfall       = (cash < protected) ? protected - cash : 0
```

When `shortfall` is above 0, the company has less cash than its own protected reserve. The excess is then 0, so the allocation is 0, and the tool shows the size of the gap.

## Worked example

These are the tool's default inputs. They are example figures only.

| Input | Value |
| --- | --- |
| cash | 500,000 |
| monthly | 40,000 |
| months | 6 |
| obligations | 60,000 |
| pct | 10 |
| hardCap | none |
| fall | 50 |

| Output | Value |
| --- | --- |
| protected | 40,000 x 6 + 60,000 = 300,000 |
| excess | 500,000 - 300,000 = 200,000 |
| allocation | 200,000 x 10% = 20,000 (limited by the percentage cap) |
| shareOfCash | 4% |
| scenarioLoss | 20,000 x 50% = 10,000 |
| runwayAfterLoss | (500,000 - 10,000 - 60,000) / 40,000 = 10.75 months |

## Currency

Neither market is the default. If a country is chosen, US shows US dollars and UK shows pounds. Otherwise the browser region decides: GB, UK, GG, JE or IM shows pounds, US shows US dollars, and anything else shows plain numbers. The maths is the same in any currency, and amounts are shown rounded to whole units.

## Sources

The formulas are the site's own. The guide cites these primary sources for the accounting and tax context around an allocation (see [the guide's accounting section](https://iotfinancial.net/guides/sizing/#accounting)):

- FASB, ASU 2023-08, crypto assets at fair value: https://storage.fasb.org/ASU%202023-08.pdf
- FRC, FRS 102: https://www.frc.org.uk/library/standards-codes-policy/accounting-and-reporting/uk-accounting-standards/frs-102-the-financial-reporting-standard-applicable-in-the-uk-and-republic-of-ireland/
- FRC, FRS 105: https://www.frc.org.uk/library/standards-codes-policy/accounting-and-reporting/uk-accounting-standards/frs-105/
- IFRS Interpretations Committee, holdings of cryptocurrencies, June 2019: https://www.ifrs.org/content/dam/ifrs/supporting-implementation/agenda-decisions/2019/holdings-of-cryptocurrencies-june-2019.pdf
- IRS, Notice 2014-21: https://www.irs.gov/pub/irs-drop/n-14-21.pdf
- IRS, Digital assets: https://www.irs.gov/businesses/small-businesses-self-employed/digital-assets
- IRS, About Form 1099-DA: https://www.irs.gov/forms-pubs/about-form-1099-da
- IRS, Instructions for Form 1099-DA: https://www.irs.gov/instructions/i1099da
- HMRC, Cryptoassets Manual CRYPTO40100: https://www.gov.uk/hmrc-internal-manuals/cryptoassets-manual/crypto40100
- HMRC, Cryptoassets Manual CRYPTO41000: https://www.gov.uk/hmrc-internal-manuals/cryptoassets-manual/crypto41000
- HMRC, Cryptoassets Manual CRYPTO41050: https://www.gov.uk/hmrc-internal-manuals/cryptoassets-manual/crypto41050
- HMRC, Cryptoassets Manual CRYPTO41200: https://www.gov.uk/hmrc-internal-manuals/cryptoassets-manual/crypto41200
- HMRC, International Exchange of Information Manual IEIM8000050: https://www.gov.uk/hmrc-internal-manuals/international-exchange-of-information/ieim8000050
- HMRC, Information you'll need to give to UK cryptoasset service providers: https://www.gov.uk/guidance/information-youll-need-to-give-to-uk-cryptoasset-service-providers

Source of the maths: `site/assets/tools.js` on iotfinancial.net, checked 3 November 2026.
