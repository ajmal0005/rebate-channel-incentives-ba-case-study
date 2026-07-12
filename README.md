# Mock Rebate & Channel Incentives Program — BA Case Study

**Coastal Building Supplies Pvt. Ltd. — Distributor Volume Incentive Rebate (VIR) Program**

A complete, self-contained Business Analyst case study built to mirror how a real rebate/channel-incentive implementation (in the style of Vistex, Enable, or Vendavo) is scoped, documented, and validated — from first client conversation to UAT sign-off.

This repository showcases an end-to-end Business Analyst case study based on a realistic rebate and channel incentive management implementation. It includes stakeholder discovery, business requirements documentation, process modeling, business rules, and User Acceptance Testing (UAT) artifacts to demonstrate industry-standard BA practices.

---

## The Business Problem (in plain terms)

Coastal Building Supplies manufactures hardware (bolts, nuts, steel pipes, door hinges) and sells through regional distributors, not directly to end customers. Distributors earn a **rebate** — a back-end percentage payout — based on how much they purchase each quarter. Today this is calculated manually in Excel, and manual tier lookups have already caused at least one real overpayment. Management wants the rules formalized and the calculation automated. That's the problem this case study solves, end to end.

```
Factory  →  Distributor  →  Hardware Shop  →  Customer
```

---

## Project Structure

```
Mock-Rebate-Project/
│
├── README.md                              ← you are here
├── 01-Discovery-Notes.md                  ← mock client kickoff call + structured meeting notes
├── 02-Business-Requirements-Document.md   ← full BRD (scope, FRs, NFRs, user stories, business rules)
├── 03-Business-Rules-and-Calculator.xlsx  ← rebate tier rules + a live, formula-driven calculator
├── 04-Process-Flow.md                     ← end-to-end rebate lifecycle diagram (Mermaid, renders on GitHub)
├── 05-UAT-Test-Cases.xlsx                 ← 13 UAT scenarios incl. edge cases, formula-validated Pass/Fail
└── scripts/                               ← Python (openpyxl) source used to generate the two workbooks
    ├── build_rules_workbook.py
    └── build_uat_workbook.py
```

Read them in order — each one builds on the last, using the same fictional company, the same four distributors, and the same rebate rules throughout, so it reads as one coherent engagement rather than four disconnected exercises.

---

## The Fictional Company

| | |
|---|---|
| **Client** | Coastal Building Supplies Pvt. Ltd. |
| **Products** | Bolts, Nuts, Steel Pipes, Door Hinges |
| **Distributors** | ABC Traders, BuildMart, Prime Hardware, Metro Distributors |
| **Program type** | Quarterly Volume Incentive Rebate (VIR) + Growth Bonus |
| **Currency** | ₹ (INR) |

---

## The Rebate Rules (Business Logic Modeled)

| Tier | Quarterly Net Purchase | Rebate % |
|---|---|---|
| 1 | ₹0 – ₹500,000 | 1% |
| 2 | ₹500,001 – ₹1,000,000 | 2% |
| 3 | Above ₹1,000,000 | 3% |

Plus a **Growth Bonus**: +0.5% additional rebate if a distributor's purchases grew more than 15% year-over-year.

**Exclusions from rebate-eligible purchase value:** returned goods, cancelled orders, damaged goods.

---

## What Each File Demonstrates

| File | BA Skill Demonstrated |
|---|---|
| Discovery Notes | Structured note-taking during stakeholder calls; tracking open items and action items |
| BRD | Translating stakeholder needs into functional requirements, user stories, and business rules |
| Business Rules & Calculator (Excel) | Modeling business logic as testable, auditable formulas — not just static tables |
| Process Flow | Visualizing an end-to-end operational workflow across teams (Sales, Finance, Distributor) |
| UAT Test Cases | Validating that a built system matches documented requirements, including edge cases |

---

## Notes on Method

This is a **mock/fictional case study** — no real client, company, or data is involved. It was built to practice and demonstrate Business Analyst deliverables in the rebate/channel-incentive domain ahead of a Business Analyst Internship application.
