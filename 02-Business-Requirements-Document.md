# Business Requirements Document (BRD)
## Distributor Volume Incentive Rebate (VIR) Program
### Coastal Building Supplies Pvt. Ltd.

| | |
|---|---|
| **Document version** | 1.0 (Draft) |
| **Prepared by** | Business Analyst |
| **Date** | 19 July 2026 |
| **Status** | Draft — pending stakeholder review |
| **Source** | Discovery call, 12 July 2026 (see `01-Discovery-Notes.md`) |

---

## 1. Introduction

This document defines the business requirements for automating Coastal Building Supplies' distributor rebate program. It translates the needs expressed by Sales and Finance stakeholders during discovery into a structured, testable set of requirements that a development or configuration team can build against.

## 2. Purpose

Coastal Building Supplies currently calculates distributor rebates manually in Excel each quarter. This process is error-prone — a recent tier-boundary misread resulted in a ₹9,000 overpayment to a single distributor — and does not scale as the distributor network grows. This document specifies the requirements to replace the manual process with a rules-based, auditable rebate calculation.

## 3. Current Process (As-Is)

1. Finance exports quarterly purchase totals per distributor from the sales ledger.
2. A Finance executive manually looks up the applicable tier percentage in a reference sheet.
3. The rebate amount is manually calculated and entered into a payout sheet.
4. No systematic exclusion is applied for returns, cancellations, or damaged goods.
5. No growth-based incentive currently exists.

**Key pain point:** manual tier lookup is the direct cause of the most recent calculation error.

## 4. Proposed Solution (To-Be)

Introduce a rules-based rebate calculation that:
- Automatically determines the correct tier from net eligible purchase value.
- Automatically excludes returns, cancellations, and damaged/written-off goods.
- Automatically applies a Growth Bonus where eligible.
- Produces an auditable, formula-driven output that Finance can review before approval (see `03-Business-Rules-and-Calculator.xlsx`).

## 5. Stakeholders

| Stakeholder | Role | Primary Concern |
|---|---|---|
| Rajesh Menon | Sales Manager | Distributor motivation and fairness of rewards, especially for growing distributors |
| Priya Nair | Finance Controller | Calculation accuracy, auditability, and control over final payout approval |
| Distributor (ABC Traders, BuildMart, Prime Hardware, Metro Distributors) | External partner | Timely, accurate, and transparent rebate payout |
| IT/Development Team | Implementation | Clear, unambiguous rules to configure — no verbal-only logic |

## 6. Scope

**In Scope:**
- Quarterly Volume Incentive Rebate (VIR) calculation for all four current distributors.
- Growth Bonus calculation (+0.5% for >15% YoY growth).
- Exclusion logic for returns, cancellations, and damaged goods.
- Finance approval step before payout.

**Out of Scope (this phase):**
- Consumer-facing / retail rebates.
- SPIFFs (sales rep-level incentives).
- Integration with an external ERP or accounting system (manual export/import assumed for v1).
- Multi-currency support (INR only).

## 7. Functional Requirements

| ID | Requirement |
|---|---|
| FR-01 | System shall calculate a distributor's quarterly rebate tier based on **net eligible purchase value**. |
| FR-02 | System shall exclude returned goods from the net eligible purchase value. |
| FR-03 | System shall exclude cancelled orders from the net eligible purchase value. |
| FR-04 | System shall exclude damaged/written-off goods from the net eligible purchase value. |
| FR-05 | System shall apply the following tier structure: 1% for ₹0–₹500,000; 2% for ₹500,001–₹1,000,000; 3% for above ₹1,000,000. |
| FR-06 | System shall calculate year-over-year (YoY) purchase growth by comparing the current quarter's net eligible purchase value to the same quarter of the prior year. |
| FR-07 | System shall apply an additional +0.5% Growth Bonus when YoY growth exceeds 15%. |
| FR-08 | System shall flag (not calculate a growth bonus for) any distributor with no prior-year data, rather than defaulting to 0% or error. |
| FR-09 | System shall display the calculated tier %, growth bonus %, and total rebate % separately before combining them into a final rebate amount, so each component is auditable. |
| FR-10 | System shall require Finance sign-off before a calculated rebate is marked as approved for payout. |
| FR-11 | System shall log which purchases were excluded (and why) for any distributor whose net eligible value differs from their gross purchase value, to support audit and dispute resolution. |

## 8. Non-Functional Requirements

| ID | Requirement |
|---|---|
| NFR-01 | Rebate calculations must be reproducible — the same input data must always produce the same output (no manual override without a logged reason). |
| NFR-02 | Only Finance-role users may mark a rebate as "Approved for Payout." |
| NFR-03 | All exclusion and calculation logic must be visible/reviewable by Finance, not hidden in an unauditable black box. |
| NFR-04 | The calculation model should support adding a 5th, 6th, etc. distributor without redesign. |

## 9. User Stories

- **As a Finance Controller**, I want the system to automatically exclude returns and cancellations from rebate calculations, so that I don't have to manually cross-check each distributor's return log every quarter.
- **As a Sales Manager**, I want growing distributors to receive a visible bonus, so that the incentive structure rewards momentum, not just current size.
- **As a Finance Controller**, I want to see the tier %, growth bonus %, and final rebate amount as separate, traceable numbers, so that I can approve payouts with confidence and defend them in an audit.
- **As a Distributor**, I want a clear, consistent explanation of how my rebate was calculated, so that I trust the program and don't need to dispute it.
- **As a BA/Implementation team member**, I want every business rule written down and confirmed by stakeholders before build, so that no rule exists only in someone's memory.

## 10. Business Rules

| Rule ID | Rule |
|---|---|
| BR-01 | Rebate tiers apply to **net eligible purchase value**, not gross purchase value. |
| BR-02 | Returns, cancellations, and damaged/written-off goods are excluded from net eligible purchase value. |
| BR-03 | Growth Bonus requires >15% YoY growth in net eligible purchase value, compared quarter-over-same-quarter-prior-year. |
| BR-04 | Growth Bonus adds +0.5% on top of the applicable tier %; it does not replace it. |
| BR-05 | A distributor with no prior-year purchase history is not eligible for the Growth Bonus in their first year (flagged, not defaulted). |

*(Full tier table and a working formula-based calculator are in `03-Business-Rules-and-Calculator.xlsx`.)*

## 11. Assumptions

- All amounts are in INR (₹); no multi-currency requirement exists today.
- "Quarterly" aligns to Coastal's existing fiscal quarter definitions (not independently defined in this phase).
- Distributor purchase data is available as a clean quarterly export; no real-time transaction feed is assumed for v1.

## 12. Constraints

- No integration with an external ERP/accounting system in this phase — data import/export is manual.
- Only four distributors exist today; the model must not hardcode logic to exactly four (see NFR-04).

## 13. Risks

| Risk | Impact | Mitigation |
|---|---|---|
| GST treatment of purchase value is unresolved (see Open Issues) | Could change every tier boundary and rebate amount | Confirm with Finance before final sign-off; do not build against an assumption |
| Growth comparison period (quarter vs. trailing 12 months) is unconfirmed | Growth Bonus eligibility could be calculated incorrectly | Confirm with Sales in writing before implementation |
| New distributors with no prior-year data could be mishandled | Risk of incorrect Growth Bonus payout or system error | FR-08 explicitly requires a flag, not a silent default |

## 14. Open Issues Log

| # | Issue | Raised By | Status |
|---|---|---|---|
| 1 | Should GST be included or excluded from the purchase value used for tier lookup? | BA (during discovery) | Open — awaiting Finance confirmation |
| 2 | Is Growth Bonus based on same-quarter-last-year, or trailing 12 months? | BA (during discovery) | Open — awaiting Sales confirmation |
| 3 | How should first-year distributors with no prior-year data be handled? | BA (during discovery) | Addressed in FR-08 (flag, don't default) — pending stakeholder sign-off |
| 4 | Is there a maximum cap on combined tier % + growth bonus %? | BA (during discovery) | Open — not raised by stakeholders yet, needs follow-up |

---

*Next document in this case study: `03-Business-Rules-and-Calculator.xlsx` — the tier table and rebate calculator implementing these rules as live formulas.*
