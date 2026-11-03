# IoT Financial treasury toolkit

Open materials from [IoT Financial](https://iotfinancial.net): free education for small companies in the UK and the US that are thinking about holding bitcoin in their treasury.

IoT Financial explains how a small company can think about sizing an allocation, choosing custody, writing a treasury policy, and handling the accounting and tax, with every claim linked to a primary source. This repository publishes the open parts of that work so anyone can read them, check them and suggest corrections.

> **Education, not advice.** Everything here is general information and education only. It is not financial, investment, tax, accounting, legal or regulatory advice, and it is not a recommendation to buy, sell or hold bitcoin or any other asset. It does not take account of your company's circumstances. Get your own professional advice before acting. Rules change, and official sources take precedence. Bitcoin is volatile; a company that buys it could lose some or all of the money it puts in. IoT Financial is not authorised or regulated by the Financial Conduct Authority (FCA) and is not registered with the US Securities and Exchange Commission (SEC) as an investment adviser. Full disclaimer: https://iotfinancial.net/disclaimer/

## What is in this repository

| Folder | Contents |
| --- | --- |
| [policy-template/](policy-template/) | The bitcoin treasury policy template as plain Markdown, with matching US and UK clauses |
| [calculators/](calculators/) | The formulas behind the site's calculators, written out from the site's own scripts, with worked examples and sources |
| [data/](data/claims-register.md) | The claims register: every claim on the site that can go out of date, its primary source and when it was last checked, as Markdown and CSV |

The designed, fillable PDF versions of the templates are not in this repository. They are available free by email from the site.

## Guides on the site

- [Allocation sizing guide](https://iotfinancial.net/guides/sizing/): protect the cash the business needs first, then size within limits the company sets. Includes the [sizing tool](https://iotfinancial.net/guides/sizing/#tool).
- [Custody guide](https://iotfinancial.net/guides/custody/): regulated custodian, collaborative multisig, self-managed multisig and exchange-traded products compared. Includes the [custody questionnaire](https://iotfinancial.net/guides/custody/#tool).
- [Treasury policy guide](https://iotfinancial.net/guides/policy/): what a policy should contain and how to adopt it. Includes the [policy generator](https://iotfinancial.net/guides/policy/#tool).
- [Policy template](https://iotfinancial.net/template/), [all tools](https://iotfinancial.net/tools/) and [how the site is researched and checked](https://iotfinancial.net/methodology/).

## Principles

- Primary sources only: regulators, statutes, accounting standards, tax authority guidance, companies' own filings and projects' own documentation.
- UK and US treated side by side. Neither is the default.
- No price predictions, no product endorsements, no trading signals.
- Single-signature wallets are not suggested for a company treasury: one device or one person is a single point of failure.
- Claims that could not be confirmed against a primary source are marked **UNVERIFIED** in the [claims register](data/claims-register.md) rather than silently changed.

## Corrections and suggestions

Found something wrong, out of date or unclear? Please [open an issue](../../issues/new). Include the file or page, what it says, what you think it should say, and a link to the primary source. See [CONTRIBUTING.md](CONTRIBUTING.md).

For anything you would rather not post in public, email hello@iotfinancial.net.

## Licences

- **Content** (the Markdown text, the policy template, the explanations and the claims register): [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). See [LICENSE](LICENSE).
- **Code snippets** (the formula and code blocks in [calculators/](calculators/), and any code added later): [MIT](LICENSE-CODE).

A suitable credit: *Source: IoT Financial, [file or page title], github.com/iotfinancial-code/treasury-toolkit, licensed under CC BY 4.0.*

The IoT Financial name and logo are not covered by either licence. Linked third-party sources keep their own terms. The text on iotfinancial.net itself is published under the licence shown in the site's [terms](https://iotfinancial.net/terms/#copyright).

Snapshot date: 3 November 2026. The site may be newer than this repository.
