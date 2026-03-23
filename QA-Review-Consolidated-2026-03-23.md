# QA Review — All 32 Dealer Audit Reports (2026-03-23)

**Reviewed by:** 3 Opus agents in parallel
**Date:** 2026-03-23
**Result:** 19 PASS / 13 ISSUES

---

## High Severity — Fix Before Using

| # | Dealer | Issue | Details |
|---|--------|-------|---------|
| 1 | **Elite LP Coastal Mississippi** | Match type hallucination or unreported violation | Every keyword listed as "Broad" and report celebrates it. Fleet policy = zero broad match. Every other report flags broad as bad. **Verify in Google Ads UI.** |
| 2 | **Passion Pools** | Spend math error ($1,000 off) | Executive summary says "$9,267/mo total spend" but market breakdown ($3,762 + $2,203 + $2,302) = $8,267. |
| 3 | **Jacksonville** | Click count discrepancy (208 gap) | Scorecard says 966 clicks, campaign performance table totals 758. CTR matches 966 number. |
| 4 | **LP Austin** | Contradictory waste figure | P1 heading says "$538 wasted" but body text details three ad groups totaling $812. |
| 5 | **Integrity Built Pools** | Fabricated "not a real model" claim | Report says "Monaco is not a Leisure Pools model" — Monaco IS a real Leisure Pools model. Action item to remove it from structured snippets is wrong. |

## Medium Severity — Misleading Data

| # | Dealer | Issue | Details |
|---|--------|-------|---------|
| 6 | **Backyard Pool & Patio** | Ad strength enum error | Value 6 labeled "Poor" — enum 6 = GOOD in Google's system. |
| 7 | **NW Ohio** | Fabricated model name + neg list count | "The Wave" recommended in structured snippets — not a real LP model. Shared neg list says 99 keywords vs 162 in every other report (same list ID 12012201802). |
| 8 | **Elite LP Beaufort** | Shared neg list count wrong | Says 49 keywords in Master Exclusion List. Same list ID = 162 in every other report. |
| 9 | **Tri County Pools** | Shared neg list count wrong | Says ~95 keywords. Same list = 162 everywhere else. |
| 10 | **Columbus OH** | Device enum mislabel | Device code 3 labeled "Connected TV" — should be "Tablet" (3=TABLET, not Connected TV). |

## Low Severity — Minor Inconsistencies

| # | Dealer | Issue | Details |
|---|--------|-------|---------|
| 11 | **LP Front Range** | Health score math error | Category scores sum to 67/100 but report says 52/100. |
| 12 | **Cajun Pools** | Shared set ID recognition | Minor — shared set ID not properly recognized. |
| 13 | **Elite Aviva Terre Haute** | P1 misclassification | No-Exact-Match flagged as P1 — should be P2 at most. |

---

## Systemic Patterns

1. **Shared negative list count inconsistency** — 3 reports (Beaufort=49, Tri County=95, NW Ohio=99) disagree with the fleet standard of 162 for the same list ID. The 162 count appears in 20+ reports and is likely correct.
2. **Known enum errors still appearing** — Device enum (Columbus: 3=Connected TV instead of Tablet) and ad strength enum (Backyard: 6=Poor instead of Good) show the enum mapping issue isn't fully resolved.
3. **Pool model name fabrication** — "The Wave" (NW Ohio) is not a real model. Monaco was falsely called fake (Integrity Built).

## Clean Reports (19 PASS)

All American, Aqua Pools CC, Blue Orca, Bluefin, Aviva Nashville South, Elite LP Athens, LP Europe, LP Houston, LP OK, LP San Antonio, LP Waco, Poolux Builders, Precision Fiberglass, Pronto Pools, LP DFW, LP Boston North, Elite LP Sarasota, Elite LP Savannah, Lake City

---

*Generated 2026-03-23 by QA review agents (Opus 4.6)*
