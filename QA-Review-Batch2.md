# QA Review — Batch 2 (11 Reports)
**Reviewer:** Claude Code (QA Session)
**Date:** 2026-03-23
**Reports Reviewed:** Elite-LP-Columbus-OH, Elite-LP-Jacksonville, Elite-LP-Lake-City, Elite-LP-Northwest-Ohio, Elite-LP-Sarasota, Elite-LP-Savannah, Elite-Passion-Pools, Integrity-Built-Pools, LP-Austin, LP-Boston-North, LP-DFW

---

## 1. Elite – Leisure Pools Columbus OH
**ISSUES FOUND**

**Issue 1 — Device Enum Error: Code 3 labeled "Connected TV" instead of "Tablet"**
The device performance table labels device code 3 as "Connected TV" with 6 clicks, 39 impressions, $18 spend. In the Google Ads API, device enum 3 = TABLET, not Connected TV (which is enum 6). This is a device enum mislabeling. The data itself may be correct tablet data displayed under the wrong label.
> Specific text: `<tr><td>Connected TV</td><td>3</td><td>Main</td><td>6</td><td>39</td><td>$18</td><td>0</td><td>$2.99</td></tr>`

**Issue 2 — "Desktop/Tablet" combined under code 4**
The report groups "Desktop/Tablet" under code 4, but code 4 = DESKTOP only. Tablet is code 3 (mislabeled as Connected TV above). This means the desktop numbers may include tablet data, or the tablet row is getting its own (mislabeled) entry while desktop is also mislabeled. Inconsistent either way.

**Issue 3 — Match type code mapping states "2 = EXACT, 3 = PHRASE" — verify against Google Ads API**
The report says "Match type codes: 2 = EXACT, 3 = PHRASE." In the Google Ads API, the actual mapping is: 2=EXACT, 3=PHRASE, 4=BROAD. This is correct. No issue here — noted for completeness.

**Everything else checks out:** CPA math ($2,163 / 14 = $154.50, report says $154 — rounding OK). Total spend ($2,163 + $242 = $2,405 — matches). Total clicks (338 + 18 = 356 — matches). Geo targeting correctly identified as PRESENCE (enum 7). Shared negative list distinction between "Master Exclusion List 3.18" (unlinked) and "Master Negative Keywords 3.18" (linked) is clearly explained. Duplicate call tracking finding is well-documented with specific conversion action names and counting types.

---

## 2. Elite – Leisure Pools Jacksonville
**ISSUES FOUND**

**Issue 1 — Click count discrepancy: Scorecard says 966, campaign table totals 758**
The scorecard at the top shows 966 total clicks. The campaign performance summary table shows: Primary = 454 clicks + Pool Builder = 304 clicks = 758 total. That's a 208-click discrepancy (27%).
> Scorecard text: `<div class="value">966</div> <div class="label">Clicks</div>`
> Table totals: `Total | $1,650.66 | 758 | 7,320 | 10.4% | 37 | $44.61`

The impressions (7,320) and spend ($1,650.66) and conversions (37) all match between scorecard and table. Only clicks are inconsistent. The 758 figure produces a 10.4% CTR (758/7320 = 10.35%). The 966 figure would produce 13.2% CTR — which is what the scorecard shows. So the scorecard CTR (13.2%) is calculated from the 966 click number, not the 758 from the detailed table. One of these numbers is wrong.

**Everything else checks out:** CPA math is clean ($1,650.66 / 37 = $44.61). Geo targeting correct (PRESENCE, enum 7). Broad match finding on "fiberglass pool builders" is well-documented with spend and CPA impact. QS findings are specific with real keyword names. Conversion action API failure is correctly reported as "Unable to Verify" rather than claiming missing conversions. Device enums correct (Mobile=2, Desktop=4, Tablet=3). Callouts listed (8 items but says "7 per campaign" — 8 listed: Top-Rated Builder, Fast Installation, Low Maintenance Pools, Lifetime Warranty, Serving Jacksonville Area, 30+ Pool Designs, Free Estimates, Financing Available — this is 8, not 7).

**Issue 2 — Callout count: Text says "7 per Campaign" but lists 8 callouts**
> Text: `Callout Extensions — 7 per Campaign (field_type=11)` but then lists: Top-Rated Builder, Fast Installation, Low Maintenance Pools, Lifetime Warranty, Serving Jacksonville Area, 30+ Pool Designs, Free Estimates, Financing Available = 8 items.

---

## 3. Elite – Leisure Pools Lake City
**ISSUES FOUND**

**Issue 1 — Device table: Mobile CPA of $459.41 on 1 conversion seems extreme but math checks out**
Mobile: $459.41 spend / 1 conv = $459.41 CPA. Desktop: $62.25 / 1 conv = $62.25 CPA. Math is internally consistent. The recommendation to "bid down -35% on mobile" is reasonable given the data, though with only 2 total conversions the sample size is very small. This is not an error per se but worth noting the low-confidence data.

**Issue 2 — Total spend adds up approximately: $435.54 + $64.10 + $17.03 + $4.95 + $4.04 = $525.66 from landing page table; report header says $526. Also device table: $459.41 + $62.25 + $4.00 = $525.66.** Matches within rounding — OK.

**No major issues.** Report is thorough for a small-market account. Correctly identifies structural problems (homepage absorbing 82.9% of spend at $435 CPA vs. /download-brochure/ at $64 CPA). Geo targeting correct (PRESENCE, enum 7). Conversion tracking is clean — no duplicate counting. Shared negative list confirmed linked. Campaign-level negatives correctly flagged as missing (P1). Rebuild spec uses real, reasonable pool model names — none fabricated.

**PASS** (with the minor caveat that small sample size recommendations should be taken directionally)

---

## 4. Elite – Leisure Pools Northwest Ohio
**ISSUES FOUND**

**Issue 1 — Shared negative list member count inconsistency: says 99 keywords**
The report states the shared set 12012201802 has "99 exact-match terms." Every other report in this batch (Jacksonville, Savannah, Columbus, Lake City, etc.) identifies the same shared set ID as having 162 keywords. The 3/20 audit is cited as the source of the 99 count. This is likely stale data from a prior audit — the list has since been updated to 162.
> Text: `Shared set 12012201802 is attached to the campaign (status ENABLED). This is the Explore-wide negative keyword list (99 exact-match terms per 3/20 audit).`
> Also: `<tr><td>Shared Negatives</td><td>List 12012201802</td><td>1</td><td>99 exact-match terms, campaign-attached</td></tr>`

**Issue 2 — Structured snippet recommendation includes potentially fabricated pool model name "The Wave"**
The recommended structured snippet values are: "The Eclipse, The Supreme, The Pinnacle, The Allure, The Wave." The Eclipse, Supreme, Pinnacle, and Allure are verified Leisure Pools models. **"The Wave" is not a known Leisure Pools model.** Known LP models include: Elegance, Tuscany, Palladium, Monaco, Limitless, Esprit, Acclaim, Eclipse, Supreme, Pinnacle, Allure, etc. "The Wave" does not appear in any other report's model listing across the fleet.
> Text: `STRUCTURED SNIPPET – header "Pool Styles": The Eclipse, The Supreme, The Pinnacle, The Allure, The Wave`

**Everything else checks out:** Health score of 36/100 is well-supported by findings. CPA math ($523 / 3 = $174.33, report says $174 — rounding OK). Geo targeting correct (PRESENCE, enum 7). Max CPC cap of $250 flagged as P1 — appropriate finding. Zero manual assets finding is clearly documented. Search term waste analysis is specific with dollar amounts.

---

## 5. Elite – Leisure Pools Sarasota
**PASS**

CPA math: $540 / 11 = $49.09 (report says $49 — rounding OK). Keyword-level CPAs all check out: leisure pools $47.91/5.0 = $9.58, fiberglass pools $151.83/4.0 = $37.96, pool designs $152.03/1.0 = $152.03. Geo targeting correctly identified as PRESENCE (enum 7). Business Name asset PAUSED finding is appropriately documented with asset ID and audit history. Call asset 631 area code flag is a legitimate finding. Shared negative set attached. Keywords shown as BROAD — report correctly identifies waste from broad match but does not flag this as a match type violation (unlike Jacksonville where there is a "no broad match rule"). The audit treats broad match as context-appropriate for this account, which may or may not be correct depending on fleet policy, but the report is internally consistent.

The impression share analysis is sound: 11.6% IS with 73.1% rank-lost and 15.2% budget-lost. Growth roadmap is logical (QS cleanup first, then budget increase).

No math errors, no fabricated model names, no enum inversions, no contradictions found.

---

## 6. Elite – Leisure Pools Savannah
**PASS**

CPA math: $479 / 6 = $79.83 (report says $80 — rounding OK). Geo targeting is correctly handled — positive geo is PRESENCE (enum 7), negative geo is PRESENCE_OR_INTEREST (enum 5), and the report explicitly explains that negative geo using PRESENCE_OR_INTEREST is standard/acceptable. The "RESOLVED" finding about prior geo targeting issue is well-documented with explanation that prior audits were wrong (reported PRESENCE_OR_INTEREST when it was actually PRESENCE/enum 7). Brochure downloads correctly treated as real conversions. Match types compliant (Exact + Phrase only, no broad). Shared negative list "Master Exclusion List 3.18" confirmed linked with 162 keywords. RSA headline/description correctly reported as unverifiable via API.

Competitor brand names mentioned (Pride Pools, Latham, Ambikun, Corinthian, Taylor Pools, Alaglas) — these appear to be real Savannah-area pool competitors. No fabricated names detected.

No math errors, no enum inversions, no contradictions found.

---

## 7. Elite – Passion Pools
**ISSUES FOUND**

**Issue 1 — Total spend discrepancy: Executive summary says "$9,267/mo total spend" but market breakdown totals $8,267**
The executive summary states: "3 markets, $9,267/mo total spend — Dayton ($3,762), NKY ($2,203), Cincinnati ($2,302)." But $3,762 + $2,203 + $2,302 = **$8,267**, not $9,267. That's a $1,000 discrepancy.
> Text: `3 markets, $9,267/mo total spend — Dayton ($3,762), NKY ($2,203), Cincinnati ($2,302)`
> Math: $3,762 + $2,203 + $2,302 = $8,267

The individual market numbers in the detailed table all check out individually (CPA, CPC, etc.), so the error is in the executive summary total only.

**Everything else checks out:** Individual market CPAs are correct: NKY $2,203/19 = $115.95 ($116), Dayton $3,762/24 = $156.75 ($156), Cincinnati $2,302/13 = $177.08 ($177). Geo targeting correct (PRESENCE, type 7) on all 3 campaigns. Bidding strategy correctly identified as TARGET_SPEND (enum 9 = Max Clicks), with a note that this differs from the label "Max Conversions." Change event timeline with specific timestamps and editor identity is well-documented. Competitor brand waste amounts are specific and reasonable. Shared negative list confirmed linked (162 keywords). Device enums not shown in detail so no inversion risk.

---

## 8. Integrity Built Pools
**ISSUES FOUND**

**Issue 1 — Report claims "Monaco" is not a Leisure Pools model — it IS**
Three separate sections of this report state that "Palazzo, Olympus, Monaco — none are Leisure Pools models." However, **Monaco IS a real Leisure Pools model.** The known LP lineup includes: Elegance, Tuscany, Palladium, Monaco, Limitless, Esprit, Acclaim, Eclipse, Supreme, Pinnacle, Allure. Palazzo and Olympus are indeed not real LP models, but Monaco should not be included in the "fabricated" list.
> Text (repeated 3x): `Prior audit flagged potential fabricated model names (Palazzo, Olympus, Monaco — none are Leisure Pools models).`

This means the action item to "Confirm Palazzo/Olympus/Monaco were removed" is partially wrong — Monaco should be kept if it was in the structured snippet.

**Everything else checks out:** CPA math ($2,057 / 8 = $257.13, report says $257 — OK). Bidding strategy correctly identified as Max Clicks (TARGET_SPEND, enum 9) with explicit note contradicting Obsidian records that said Max Conversions. PMax budget reactivation risk is a legitimate finding. Geo targeting correct (PRESENCE, enum 7). Keyword QS analysis is detailed and realistic. Conversion tracking flagged as unverifiable (API error) — correctly reported as "unable to verify" rather than asserting missing.

---

## 9. LP Austin
**ISSUES FOUND**

**Issue 1 — P1 heading says "$538 wasted" but body details total $812.08**
The P1 finding heading reads: "3 Ad Groups Spending Zero Conversions ($538 wasted)." But the body lists: Pool Contractor $227.96 + Fiberglass Pools Cost/Pricing $513.06 + Fiberglass vs Concrete $71.06 = **$812.08**. The body text itself also says "$812 spent in 30 days" and "26% of total spend." $812 / $3,087 = 26.3%, so the 26% matches the $812 figure. The $538 in the heading appears to be a different/earlier calculation that doesn't match the detailed numbers.
> Heading: `P1 — 3 Ad Groups Spending Zero Conversions ($538 wasted)`
> Body: `Pool Contractor ($227.96, 41 clicks, 0 conv), Fiberglass Pools Cost/Pricing ($513.06, 126 clicks, 0 conv), Fiberglass vs Concrete ($71.06, 17 clicks, 0 conv) — combined $812 spent`

**Everything else checks out:** Blended CPA $3,087/15 = $205.80 (report says $206 — OK). Geo targeting correct (PRESENCE, enum 7). Conversion actions properly configured (4 active, all ONE_PER_CLICK). Shared negative list confirmed linked (162 keywords). Competitor brand waste is documented with specific amounts. Bidding strategy correctly identified as Target Spend (Max Clicks) with $15 CPC ceiling. Speed score = 0 flagged as potential tracking issue rather than definitively stated as a problem — appropriate caution.

---

## 10. LP Boston North
**PASS**

CPA math: $1,019 / 10 = $101.90 (report says $101.93 — the 3-cent difference likely comes from more precise underlying spend figure). All keyword spend amounts are listed with specific dollar values. Health score decline from 48 to 41 is explained with specific structural reasons. Geo targeting correct (PRESENCE, enum 7, implied but not explicitly stated with enum number — the shared set and campaign structure confirm it). All 24 keywords confirmed as broad match with specific search term waste documented. Third-party user finding (jan.stevens@bizitconseil.fr) is well-documented with specific dates, operations, and asset IDs — this is either real API data or very elaborate fabrication, but the specificity of asset IDs and timestamps suggests real data.

No math errors, no fabricated model names, no enum inversions, no contradictions found.

---

## 11. LP DFW
**PASS**

CPA math all checks out: Blended $4,046/32 = $126.44 ($126). Primary $1,996/20 = $99.80 ($99.79). Pool Builder $2,050/12 = $170.83 ($170.87). Total spend $1,996 + $2,050 = $4,046. "swimming pool builder" keyword: $1,444/8 = $180 CPA, and $1,444/$4,046 = 35.7% of budget (report says 36% — OK). "fiberglass pool" $143/5 = $28.60 (report says $28.59 — rounding). Geo targeting correct (PRESENCE on both campaigns). Bidding strategy correctly identified as Max Clicks with $15 CPC cap. Conversion setup confirmed clean (4 actions, all ONE_PER_CLICK). Shared negative list linked (162 keywords + ~95 campaign-level). Homepage vs. design page CPA comparison is well-documented ($151 vs $72).

No math errors, no fabricated model names, no enum inversions, no contradictions found.

---

## Summary Table

| # | Dealer | Verdict | Issues |
|---|--------|---------|--------|
| 1 | Elite-LP-Columbus-OH | **ISSUES FOUND** | Device enum 3 mislabeled as "Connected TV" (should be Tablet) |
| 2 | Elite-LP-Jacksonville | **ISSUES FOUND** | Click count discrepancy (scorecard 966 vs table 758); callout count says 7 but lists 8 |
| 3 | Elite-LP-Lake-City | **PASS** | Clean |
| 4 | Elite-LP-Northwest-Ohio | **ISSUES FOUND** | Shared list says 99 KWs (other reports say 162 for same ID); "The Wave" is not a real LP model |
| 5 | Elite-LP-Sarasota | **PASS** | Clean |
| 6 | Elite-LP-Savannah | **PASS** | Clean |
| 7 | Elite-Passion-Pools | **ISSUES FOUND** | Total spend in exec summary says $9,267 but markets sum to $8,267 ($1,000 discrepancy) |
| 8 | Integrity-Built-Pools | **ISSUES FOUND** | Monaco IS a real LP model — report incorrectly flags it as fabricated (3 occurrences) |
| 9 | LP-Austin | **ISSUES FOUND** | P1 heading says "$538 wasted" but body details total $812 |
| 10 | LP-Boston-North | **PASS** | Clean |
| 11 | LP-DFW | **PASS** | Clean |

**Pass Rate:** 5 of 11 (45%)
**Issues Found:** 6 of 11 (55%)

### Issue Severity Assessment
- **High (would mislead decision-making):** Passion Pools $1,000 spend discrepancy; Jacksonville click count discrepancy; Austin $538 vs $812 waste figure
- **Medium (incorrect information but unlikely to cause harm):** Integrity Built "Monaco" misidentified as fake; NW Ohio "The Wave" fabricated model name; NW Ohio shared list count wrong
- **Low (cosmetic/labeling):** Columbus device enum label; Jacksonville callout count off by 1

### Known Error Pattern Check Results
1. **Geo targeting enum inversion:** NOT FOUND in this batch. All reports correctly identify PRESENCE as enum 7.
2. **Device enum inversion:** FOUND in Columbus (code 3 labeled "Connected TV" instead of "Tablet"). Other reports with device data (Jacksonville, Lake City) are correct.
3. **API failures reported as findings:** NOT FOUND. Reports consistently say "unable to verify" for API failures (Jacksonville conversion actions, NW Ohio conversion tracking, Savannah sitelink content, etc.)
4. **Fabricated model names:** FOUND — NW Ohio recommends "The Wave" (not a real LP model). Also, Integrity Built incorrectly calls "Monaco" fabricated when it IS real.
5. **Brochure downloads as real conversions:** CORRECTLY handled across all reports.
6. **Math errors:** FOUND in 3 reports (Jacksonville clicks, Passion Pools total spend, Austin waste figure heading).
7. **Cross-report inconsistencies:** FOUND — NW Ohio says shared list has 99 keywords while all others say 162 for the same set ID.
8. **Internal contradictions:** Minor — Austin heading vs body waste figure.
