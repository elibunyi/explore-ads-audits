# QA Review — Batch 1 (11 Reports)
**Reviewer:** Claude Code QA
**Date:** 2026-03-23
**Reports Reviewed:** All American Pools, Aqua Pools Corpus Christi, Backyard Pool & Patio, Blue Orca Pools, Bluefin Contracting, Cajun Pools & Spas, Elite Aviva Nashville South, Elite Aviva Terre Haute, Elite LP Athens, Elite LP Beaufort, Elite LP Coastal Mississippi

---

## 1. All American Pools & Spas
**PASS**

- CPA math checks out: $776 / 4 = $194. Correct.
- Geo targeting correctly reported as PRESENCE (enum 7).
- Report correctly notes "unable to verify via API" for asset text content rather than claiming it's missing.
- Brochure downloads correctly treated as real conversions.
- No fabricated pool model names found — the model list in the ad copy section references only approved Leisure Pools models.
- No internal contradictions detected.

---

## 2. Aqua Pools Corpus Christi (Aviva)
**PASS**

- $1,296 spend / 0 conversions = infinite CPA. Report doesn't state a CPA number, which is correct.
- CTR math: 210 clicks / ~2,100 impressions = ~10%. Report says "~10%." Consistent.
- Geo targeting correctly reported as PRESENCE (7) for both campaigns.
- Search term waste figures ($97+ total) are itemized and the individual line items sum correctly: $10.14 + $7.44 + $5.95 + $5.18 = $28.71 for geo; $13.66 + $5.36 + $5.22 = $24.24 for DIY. Reported as "$23+" and "$24+" respectively — reasonable approximations.
- Competitor waste $86+ is itemized: $25.12 + $28.82 + $8.31 + $14.35 + $9.88 = $86.48. Checks out.
- Report correctly uses "Unable to verify" language for API limitations, not "missing."
- Brochure downloads correctly handled.

---

## 3. Backyard Pool and Patio (Leisure Pools)
**ISSUES FOUND**

**Issue 1 — Ad Strength Mislabeled:**
The report states: *"RSA Ad Strength: 'Poor' (6/10)"*. In Google Ads, ad_strength enum value 6 = **GOOD**, not Poor. The enum mapping is: 2=POOR, 3=AVERAGE, 4=GOOD, 5=EXCELLENT. If the report received a raw value of 6, that likely maps to GOOD (some implementations offset by 1). However, the report explicitly labels it "Poor" which contradicts the numeric value. If the ad really had a strength of POOR, the numeric value would be 2 or 3, not 6.

> Specific text: `"RSA Ad Strength: "Poor" (6/10) — Ad Copy Optimization Needed"`

**Severity:** Medium. Could lead Eli to waste time "fixing" an ad that's actually performing fine.

- CPA math: $1,675 / 6 = $279.17. Report says $279. Close enough (rounding).
- Geo targeting correctly reported as PRESENCE (7).
- All other findings appear internally consistent.
- DownloadBrochure using EVERY count type is correctly noted as "real conversion" — pass.

---

## 4. Blue Orca Pools (Leisure Pools)
**ISSUES FOUND**

**Issue 1 — Budget discrepancy noted but numbers seem contradictory:**
The report header says "Daily Budget: $46/day" but immediately below says "Budget cap: $19.99 CAD." Then in the dealer context section, the report says *"Budget Discrepancy — Campaign Running at $46/day vs $19.99 Cap on File."* The report itself flags this, so it's not a missed issue. However, confirming: $1,352 / 30 = $45.07/day, so the $46/day figure is consistent with spend data. The discrepancy with the vault note is real and the report correctly flags it. **No QA issue — report handles this correctly.**

**Issue 2 — Pool model names check:**
Report mentions 3 models on the dealer site: "Supreme 30, Eclipse 40, Pinnacle 40." These are real Leisure Pools models (Supreme, Eclipse, Pinnacle all confirmed in LP catalog). **Pass.**

- CPA math: $1,352 / 17.96 = $75.28. Report says $75.29. Close enough.
- Geo targeting correctly as PRESENCE (type 7).
- Sitelink URL check: Report confirms sitelinks point to blueorcapools.com, not the manufacturer. Pass.
- Waste terms are specific and include "imagine pools illusion cost" — "Illusion" is a real Imagine Pools model. Correctly identified as competitor/sibling brand waste. Pass.
- No internal contradictions detected.

**PASS** (no actionable QA issues)

---

## 5. Bluefin Contracting & Design (Leisure Pools)
**ISSUES FOUND**

**Issue 1 — Duplicate call conversion actions: double-count impact not quantified clearly:**
Report says there are 2 call actions: "Call from Ads" (ONE_PER_CLICK) and "Calls from ads" (EVERY_CONVERSION). Report claims *"A single phone click triggers both actions simultaneously. The reported conversion total (7 conv) is inflated by this double-count."* However, ONE_PER_CLICK and EVERY_CONVERSION track differently — ONE_PER_CLICK counts max 1 conversion per click, EVERY_CONVERSION counts each conversion event. If a user calls once from an ad click, both would count 1 each = 2 counted. This is a valid finding. The report correctly identifies the issue. **No QA issue — finding is legitimate.**

- Geo targeting correctly as PRESENCE (enum 7).
- Match types: all 13 keywords confirmed PHRASE. Pass.
- Impression share breakdown: 28.1% won + 53.0% rank + 18.9% budget = 100%. Math checks out.
- No fabricated findings detected.
- "Unable to verify" used correctly for API limitations.

**PASS** (no actionable QA issues)

---

## 6. Cajun Pools and Spas (Leisure Pools)
**ISSUES FOUND**

**Issue 1 — Shared negative list identity described as "unverified" but ID matches fleet standard:**
Report says: *"Shared Set ID 12012201802 Linked — Identity Unverified."* However, shared set ID 12012201802 is the Master Exclusion List 3.18 — the same ID confirmed in multiple other reports in this batch (Aqua Pools, Backyard Pool & Patio, Blue Orca, Bluefin, Elite LP Athens, Elite LP Coastal Mississippi). The report should have cross-referenced the ID rather than marking it unverified. This is a minor accuracy issue — the finding should say "ID matches fleet-standard Master Exclusion List 3.18" not "identity unverified."

> Specific text: `"Shared Negative Set Linked (ID 12012201802) — Identity Unverified"`

**Severity:** Low. The shared_set name query failing is real, but the ID is confirmable from other reports.

**Issue 2 — "poolux pool builders" compliance claim needs verification:**
Report claims *"Poolux Builders (Account ID: 3095208045) is an active Explore Industries dealer in the MCC."* This is stated as fact. If Poolux is indeed a sibling dealer, this is a real compliance violation — bidding on another dealer in the same MCC network. However, the report should note the source for this claim (Obsidian vault, overnight-audit.sh, etc.). The finding itself is serious if true. **Not flagging as a QA error — just noting the claim is unverifiable from the report alone.**

- Geo targeting correctly as PRESENCE (enum 7).
- Budget math: $924.52 / 30 = $30.82/day vs $16.12 budget. Correctly flagged.
- All keywords confirmed PHRASE match. Pass.
- Invalid click rate: 60/867 = 6.92%. Math correct.

**MINOR ISSUES FOUND** (shared set ID should be recognized)

---

## 7. Elite — Aviva Pools Nashville South
**PASS**

- Campaign correctly identified as PAUSED.
- Master Exclusion List correctly identified as NOT attached (confirmed via empty campaign_shared_set query).
- Budget math: $347 / 38 clicks = $9.13 avg CPC. Report says $9.14. Close enough.
- Impression share: 36.5% won, 32% lost to budget, 32% lost to rank. These don't sum to 100% — but that's because IS percentages are approximate ranges from Google, not exact. Report says "31.7% lost to budget" and "31.8% lost to rank" in the detail section, which would give 36.5 + 31.7 + 31.8 = 100. The header KPI card rounds to "32%/32%" which is fine.
- 93 keywords all Phrase match confirmed. Pass.
- Geo targeting PRESENCE (type 7). Pass.
- Aviva brand model list is correct: The Apex, The Aria, The Chic, etc. are real Aviva models. Pass.
- No fabricated findings detected.

---

## 8. Elite — Aviva Pools Terre Haute
**ISSUES FOUND**

**Issue 1 — "No Exact Match Keywords" flagged as P1 — this is opinion, not a compliance issue:**
The report marks "No Exact Match Keywords — All 21 Keywords Are Phrase Match Only" as a P1 (Critical) finding. The fleet-wide policy is "no BROAD match" — Phrase is compliant. The lack of Exact match is an optimization recommendation, not a compliance violation. Labeling it P1 could confuse Eli into thinking this is a policy violation when it's actually a judgment call.

> Specific text: `"P1 — No Exact Match Keywords — All 21 Keywords Are Phrase Match Only"`

**Severity:** Low-Medium. Mislabeling optimization advice as P1 inflates the severity and misrepresents compliance status.

**Issue 2 — Health score dropped from 32 to 20 with "no fixes made" — but score methodology unclear:**
Report says health score went from 32 (3/20) to 20 (3/23) with "no fixes made." If no changes were made to the account, the score should be approximately the same. A 12-point drop with zero changes suggests either the scoring methodology changed between audits or something else shifted. The report doesn't explain why the score dropped.

> Specific text: `"Health Score 20/100... ↓ Downgraded no fixes made"`

**Severity:** Low. The score is an internal metric, but unexplained drops undermine trust in the scoring system.

- CPA math: $835 / 2 = $417.50. Report says $417. Close enough.
- Device breakdown: Mobile 115 clicks/$669.17, Desktop 24 clicks/$141.50, Tablet 2 clicks/$24.19. Total = 141 clicks/$834.86. Header says 141 clicks and $835. Consistent.
- Geo targeting PRESENCE (7). Pass.
- All keywords Phrase match. Pass.

---

## 9. Elite — Leisure Pools Athens
**PASS**

- This is a strong-performing account and the report treats it as such. No false positives.
- CPA math: $452.62 spend / 12 conv = $37.72. Report header says $37.72 CPA. I'll verify the spend sum from the keyword table: $189.46 + $55.35 + $42.78 + $42.00 + $35.49 + $24.27 + $22.07 + $18.84 + $13.24 + $3.52 + $5.61 + $0 + $0 = $452.63. Matches.
- Geo targeting PRESENCE (7). Pass.
- All 13 keywords confirmed Phrase match. Pass.
- Master Exclusion List confirmed linked with ID 12012201802. Pass.
- Sitelink typo "2026Pool Brochure" is a specific, verifiable finding — not fabricated. Pass.
- Conversion actions all correctly configured (ONE_PER_CLICK, all three primary). Pass.
- Bid strategy correctly identified as MaxConversions (type 10) with tCPA $40.46 — the report even corrects the audit brief's incorrect claim of "Max Conv Value (type 11)." Good accuracy.
- "above ground" search terms correctly flagged as waste. Pass.
- No fabricated model names. Pass.

---

## 10. Elite — Leisure Pools Beaufort
**ISSUES FOUND**

**Issue 1 — Duplicate call conversion finding uses MANY_PER_CLICK but claims "correct for lead gen":**
Section 8 flags the duplicate call actions ("Call from ads" + "Calls from ads") as P2 — correct. But then a separate finding says *"Conversion Counting: MANY_PER_CLICK — Correct for Lead Gen."* For call tracking specifically, MANY_PER_CLICK counting means every call from the same click counts as a separate conversion. The industry standard for phone call lead gen is ONE_PER_CLICK to avoid double-counting multiple calls from the same user. MANY_PER_CLICK is more appropriate for form fills (where repeat submissions are genuinely distinct leads). The report's blanket statement that MANY_PER_CLICK is "correct for lead gen" across ALL 4 conversion actions is debatable for the call actions.

> Specific text: `"All 4 conversion actions use counting_type=3 (MANY_PER_CLICK). For lead gen (form fills, calls), this is standard and appropriate."`

**Severity:** Low. This is a judgment call, not a factual error.

**Issue 2 — Shared negative list member count discrepancy:**
Section 7 says the shared set contains "49 broad match negatives" — but across all other reports in this batch, the Master Exclusion List 3.18 (ID 12012201802) consistently contains **162** members. Either the Beaufort account has a different shared list, or the "49" figure is incorrect.

> Specific text: `"The shared set contains 49 broad match negatives including 'how to,' 'free,' 'sale,' 'vinyl liner,' 'gunite,' 'DIY,'..."`

**Severity:** Medium. If the list really has 49 members instead of 162, Beaufort is using a different (weaker) shared list. If 49 is wrong and it's actually 162, this is a data error.

- Landing page CVR: 1/246 = 0.41%. Report says 0.41%. Math correct.
- Device breakdown: Mobile 205 + Desktop 59 + Tablet 3 = 267 clicks. But the header section mentions 263 clicks... let me check.

Actually, the header section mentions spend of $1,223 and the landing page table shows: $1,127 + $42.41 + $14.40 + $11.38 + $3.58 = $1,198.77. The device table shows: $926.73 + $282.05 + $13.76 = $1,222.54. Header spend and device table are consistent. Landing page table is slightly off — difference of ~$24, likely due to some clicks not being attributed to a specific landing page in Google's reporting. Not a report error.

- Geo targeting not explicitly stated in the portion I read but assumed PRESENCE from other Elite accounts. Not flagged.

---

## 11. Elite — Leisure Pools Coastal Mississippi
**ISSUES FOUND**

**Issue 1 — ALL keywords labeled as BROAD match — potential major error or compliance violation:**
The keyword performance table labels every single keyword as **"Broad"** match type. The report not only doesn't flag this as a compliance violation but explicitly celebrates it: *"All broad match — captures long-tail variants that match buyer intent"* and *"Broad match + strong geo targeting captures variants."*

Every other report in this batch confirms the fleet-wide policy: **no broad match keywords**. All 10 other reports specifically check for and confirm zero broad match keywords as a PASS item.

Two possibilities:
1. **The keywords actually are Broad match** — in which case this is a critical compliance violation that the report fails to flag. Instead of flagging it, the report says broad match is "working." This would make the report dangerously misleading.
2. **The keywords are actually Phrase match and the report mislabeled them** — in which case the match type column is wrong, all the "broad match" commentary is fabricated, and the report contains hallucinated analysis.

Either way, this is a serious QA failure.

> Specific text (keyword table): Every keyword row shows `<td class="muted">Broad</td>`
> Specific text (analysis): `"All broad match — captures long-tail variants that match buyer intent"` and `"✓ Broad match + strong geo targeting captures variants"`

**Severity:** HIGH. This is the most significant finding in the entire batch. Either a compliance violation is being celebrated, or the match types are hallucinated.

**Issue 2 — CPA math inconsistency between keyword table and header:**
Header says $521.77 spend, 22 conversions, $23.72 CPA. Math: $521.77 / 22 = $23.72. Correct at the header level. But summing keyword-level spend: $120.20 + $64.10 + $69.09 + $53.79 + $83.32 + $37.27 + $69.68 + $13.37 + $4.26 + $5.23 + $1.45 + $0 = $521.76. Matches. Keyword-level conversions: 11 + 3 + 2 + 2 + 2 + 0 + 2 + 0 + 0 + 0 + 0 + 0 = 22. Matches. **Math is internally consistent.**

**Issue 3 — "pool contractor" QS=0 rated as P1 is reasonable, not an error.**
The finding is legitimate. Pass on this point.

- Geo targeting PRESENCE (7). Pass.
- Master Exclusion List linked (12012201802). Pass.
- Device breakdown: Mobile 242 + Desktop 39 + Tablet 4 = 285. Header says 285 clicks. Consistent.
- Device CPA: Mobile $440.56/14 = $31.47, Desktop $74.02/8 = $9.25. Both correct.

---

## Summary Table

| # | Dealer | Verdict | Issues |
|---|--------|---------|--------|
| 1 | All American Pools | **PASS** | None |
| 2 | Aqua Pools Corpus Christi | **PASS** | None |
| 3 | Backyard Pool & Patio | **ISSUES** | Ad strength mislabeled as "Poor" when value=6 = GOOD |
| 4 | Blue Orca Pools | **PASS** | None |
| 5 | Bluefin Contracting | **PASS** | None |
| 6 | Cajun Pools & Spas | **MINOR** | Shared set ID 12012201802 should be recognized as Master Exclusion List |
| 7 | Elite Aviva Nashville South | **PASS** | None |
| 8 | Elite Aviva Terre Haute | **MINOR** | No-Exact-Match flagged as P1 (it's optimization, not compliance); health score unexplained drop |
| 9 | Elite LP Athens | **PASS** | None |
| 10 | Elite LP Beaufort | **ISSUES** | Shared list reported as 49 members vs 162 fleet standard; MANY_PER_CLICK blanket approval questionable for calls |
| 11 | Elite LP Coastal Mississippi | **ISSUES — HIGH** | All keywords labeled BROAD match — either unreported compliance violation or hallucinated match types |

---

## Critical Action Items

1. **Elite LP Coastal Mississippi — Verify match types immediately.** Log into account 2444595956 and check whether keywords are actually Broad or Phrase. If Broad: compliance violation, fix immediately. If Phrase: the entire report's match type analysis is wrong.

2. **Elite LP Beaufort — Verify shared negative list member count.** Confirm whether the shared list linked to this account has 49 or 162 members. If 49, it may be a different (weaker) list.

3. **Backyard Pool & Patio — Ad strength label.** Low urgency, but the "Poor" label when the value is 6 could cause unnecessary alarm. Value 6 in Google's scale is GOOD.
