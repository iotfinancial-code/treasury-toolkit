# Custody model rules

The logic behind the [custody questionnaire](https://iotfinancial.net/guides/custody/#tool) in the [custody guide](https://iotfinancial.net/guides/custody/). Seven answers lead to one of four custody models, using six rules checked in order. The guide sets out the same rules under [how the questionnaire decides](https://iotfinancial.net/guides/custody/#logic) and explains each model under [custody models](https://iotfinancial.net/guides/custody/#models).

The result is a starting point for a discussion with the company's own advisers, not a recommendation.

## Questions

| Key | Question | Answers |
| --- | --- | --- |
| `exposure` | Does the company need to hold and move bitcoin itself, or only want exposure to its price? | `hold`, `only` |
| `thirdParty` | Does an auditor, lender, investor agreement or the board require a regulated third party to hold the asset? | `no`, `yes` |
| `comfort` | How comfortable is the team with hardware wallets, backups and recovery tests? | `low`, `medium`, `high` |
| `approvers` | How many people should approve a transfer? | `1`, `2`, `3` (three or more) |
| `size` | How large is the planned holding relative to the company? | `small`, `large` (a loss would be material) |
| `keyPerson` | Is it acceptable that one person being unavailable could block access? | `no`, `yes` |
| `frequent` | Will the company move funds more than once a month? | `no`, `yes` |

## Rules

The first rule that matches decides.

| Rule | Condition | Model |
| --- | --- | --- |
| R1 | `exposure` is `only` | Exchange-traded product (a spot bitcoin ETF or a crypto ETN, held in a brokerage account) |
| R2 | `thirdParty` is `yes` | Regulated custodian |
| R3 | `comfort` is `low` | Regulated custodian |
| R4 | `comfort` is `medium` | Collaborative multisig (2 of 3): the company holds two keys, a specialist key agent holds one |
| R5 | `comfort` is `high` and (`approvers` is not `1`, or `size` is `large`, or `keyPerson` is `no`) | Self-managed multisig (2 of 3): the company holds all three keys on separate devices and people |
| R6 | otherwise (high comfort, one approver, small holding, key-person risk accepted) | Collaborative multisig (2 of 3) |

A single-signature wallet is never an outcome. One device or one person would be a single point of failure for loss, theft or a device flaw. See the guide's section on [why not a single key](https://iotfinancial.net/guides/custody/#single).

## Notes added to the result

| When | Note |
| --- | --- |
| Model is the exchange-traded product | The company would own a security, not bitcoin. It cannot withdraw bitcoin or move it on chain, shares trade only during exchange hours, and an ongoing fee is taken from the product. |
| `frequent` is `yes` and the model is not the exchange-traded product | Consider keeping a small operating balance separate from the main reserve, so routine transfers never touch the reserve keys. |
| Rule R6 | A single-signature wallet is not suggested even with one approver. Collaborative multisig keeps a provider-held recovery key, so one unavailable person does not lock the company out. |
| `size` is `large` and the model holds keys (either multisig) | Ask the insurer and auditor what evidence they expect about key storage and access controls. |
| `approvers` is `1` | Write down who can act if that person is unavailable, and how. |

## Sources

- BIP 11, M of N standard transactions (multisig): https://github.com/bitcoin/bips/blob/master/bip-0011.mediawiki
- BIP 39, recovery words: https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki
- BIP 174, partially signed bitcoin transactions: https://github.com/bitcoin/bips/blob/master/bip-0174.mediawiki
- SEC, Investor Bulletin on exchange-traded funds: https://www.investor.gov/introduction-investing/general-resources/news-alerts/alerts-bulletins/investor-bulletins-24
- SEC, Investor Bulletin on exchange-traded products, September 2024: https://www.investor.gov/introduction-investing/general-resources/news-alerts/alerts-bulletins/investor-bulletins/ETPBulletinSeptember2024
- FCA, retail access to crypto ETNs: https://www.fca.org.uk/news/press-releases/fca-opens-retail-access-crypto-etns
- FCA, cryptoassets for firms: https://www.fca.org.uk/firms/cryptoassets
- FCA, Financial Services Register: https://register.fca.org.uk/s/
- FSCS, cryptocurrencies and cover: https://www.fscs.org.uk/news/protection/cryptocurrencies-risk-cover/
- FDIC, crypto fact sheet: https://www.fdic.gov/news/fact-sheets/crypto-fact-sheet-7-28-22.html
- SEC, Staff Accounting Bulletin 122: https://www.sec.gov/rules-regulations/staff-guidance/staff-accounting-bulletins/staff-accounting-bulletin-122
- SEC custody rule, 17 CFR 275.206(4)-2: https://www.law.cornell.edu/cfr/text/17/275.206(4)-2
- NCSC, small business guide: https://www.ncsc.gov.uk/collection/small-business-guide
- NIST SP 800-57 Part 1 Rev. 5, key management: https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final

Source of the logic: `site/assets/tools.js` on iotfinancial.net, checked 3 November 2026.
