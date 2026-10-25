# Annual update checklist

The app's logic doesn't go stale, but its dollar figures do. Once a year (November, after the IRS publishes next year's numbers, is a good time), update the items below in `index.html`, then bump `DATA.year` and `DATA.reviewed`. If the app is opened in a year later than `DATA.year`, it shows a banner telling people some figures may be out of date.

Everything is in the block marked `ANNUAL UPDATE` near the top of the script.

| What | Where in index.html | Source |
|---|---|---|
| `DATA.year`, `DATA.reviewed` | `var DATA=` | — |
| 401(k)/403(b), 457(b), IRA, HSA family, dependent care FSA limits; 401(a)(17) pay cap and 415(c) total limit; Social Security wage base | `var LIM=` | IRS cost-of-living announcement (Oct/Nov); SSA wage base (Oct) |
| Federal brackets and standard deduction (joint, single, and married filing separately — `mfs`, used by the Loans tab) | `var FED=` | IRS Revenue Procedure for the coming tax year |
| SALT cap and phase-down, child tax credit | `taxCalc()` | IRS / current tax law |
| New Jersey brackets | `var NJBR=` | NJ Division of Taxation (change only when the law changes) |
| Specialty salaries | `var SPECS=` | Doximity Physician Compensation Report (published each summer) |
| Federal student loan rates, RAP / IBR / PSLF rules | Student Loans tab text, `calcLoans()` | studentaid.gov (rates set each July) |
| NJ seller "mansion tax" tiers | `mansionRate()` | NJ Division of Taxation |
| NJ treatment of HSA contributions (taxed as of 2026; a bill to conform is pending) | HSA step text in `calcPlay()` | NJ Division of Taxation |
| Catch-up limits (`catch50`, `catch6063`) and the Roth-catch-up wage threshold ($150,000 in 2026, in the `catch-hint` text and the Playbook step) | `var LIM=`, `catch-hint`, `calcPlay()` | IRS cost-of-living announcement (Oct/Nov) |
| Pre-retirement card facts: ACA subsidy rules (enhanced credits expired after 2025), Social Security ages, RMD ages; college costs (College Board averages, published each fall: all-in private ~$61k / in-state public ~$26k for 2025–26; selective private ~$90–105k, 16 schools over $100k for 2026–27 per Princeton Review/CNBC — also the `col-amt` default of $90k and its hint) and the NJ 529 deduction income limit | `calcPlay()` — `pb-pre` and `pb-col` text | healthcare.gov / Congress; ssa.gov; IRS; College Board Trends in College Pricing; NJ Division of Taxation |
| Fixed-costs card facts: Social Security max benefit at 67 (~$45–50k/yr; $4,152/mo max at FRA in 2026), NJ property tax appeal deadline (April 1 in most towns) | `calcPlay()` — `pb-stuck` text | ssa.gov; NJ Division of Taxation |
| Gift tax annual exclusion and lifetime exemption (`giftExcl`, `giftLife`) | `var LIM=` | IRS cost-of-living announcement (Oct/Nov) |
| Physician mortgage rate premium over conventional | `var PHYS=` | Quotes from physician-loan lenders |
| Mortgage rate and property tax defaults | Rent vs Buy sliders `rvb-rate`, `rvb-tax` | Freddie Mac PMMS; NJ property tax averages |
| Childcare cost hint, living-cost estimates | `daymo` slider hint, `var EST=` | Local daycare rates; household spending |

After editing: open the app, check every tab for errors, and spot-check one known case (e.g. $600k salary, age 34, net worth −$150k, $200k retirement spending, 403(b) + 457(b) + both Roths + $4,000/mo brokerage → work optional ~51, full retirement ~60 at 2026 figures).
