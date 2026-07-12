# Process Flow — Distributor Rebate Lifecycle
### Coastal Building Supplies Pvt. Ltd.

This diagram traces one distributor's purchase through the full rebate lifecycle — from the original transaction to the payout — reflecting the rules defined in `02-Business-Requirements-Document.md`.

It renders automatically as a diagram on GitHub (Mermaid is natively supported). If viewing outside GitHub, paste the code block into [mermaid.live](https://mermaid.live) or draw.io's Mermaid import.

```mermaid
flowchart TD
    A["Distributor places purchase order"] --> B["Invoice generated"]
    B --> C["Purchase recorded in sales ledger"]
    C --> D{"Quarter ends"}
    D --> E["Gross purchase value aggregated per distributor"]
    E --> F["Exclude returns, cancellations, damaged/written-off goods\n(BR-02)"]
    F --> G["Net Eligible Purchase Value calculated"]
    G --> H["Tier % determined from Net Eligible Purchase Value\n(BR-01, FR-05)"]
    G --> I["YoY growth calculated vs. same quarter, prior year\n(FR-06)"]
    I --> J{"Growth > 15%?"}
    J -- "Yes" --> K["+0.5% Growth Bonus applied\n(BR-03, BR-04)"]
    J -- "No" --> L["No Growth Bonus"]
    H --> M["Total Rebate % = Tier % + Growth Bonus %"]
    K --> M
    L --> M
    M --> N["Rebate Amount calculated\n(Net Eligible Value x Total Rebate %)"]
    N --> O["Finance reviews calculation breakdown\n(FR-09, NFR-03)"]
    O --> P{"Finance approves?"}
    P -- "Approved" --> Q["Rebate marked Approved for Payout\n(FR-10, NFR-02)"]
    P -- "Disputed / Rejected" --> R["Returned to BA/Sales for clarification"]
    Q --> S["Payout issued to distributor"]
    R --> E
```

## Reading the Flow

1. **Steps A–C** happen continuously throughout the quarter as normal sales activity.
2. **Steps D–G** are the exclusion logic — this is the step that directly fixes the manual-error problem raised in discovery (a human no longer manually subtracts returns).
3. **Steps H–M** run the tier lookup and growth bonus calculation in parallel, then combine them — matching FR-09's requirement that each component stay separately visible for audit.
4. **Steps O–Q** are the human control point: Finance must review and approve before anything is paid, per NFR-02. Nothing is auto-paid.
5. **Step R** is the exception path — if Finance disputes a number, it loops back to re-aggregate rather than being manually overridden, which protects NFR-01 (reproducibility).
