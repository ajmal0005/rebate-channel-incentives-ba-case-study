# Discovery Notes — Coastal Building Supplies: Rebate Program Kickoff

## Meeting Metadata

| Field | Detail |
|---|---|
| **Date** | 12 July 2026 |
| **Meeting type** | Discovery / Requirements Kickoff (Call 1 of 1, mock) |
| **Attendees** | Rajesh Menon (Sales Manager), Priya Nair (Finance Controller), BA (self) |
| **Duration** | 45 minutes (simulated) |
| **Purpose** | Understand the current rebate process and gather initial requirements for automating it |

---

## Part A — Mock Call Transcript

> This is a simulated conversation written to reflect a realistic first discovery call. It is used as the source material for the structured notes and BRD that follow.

**BA:** Thanks for making time today. To start — can you walk me through how rebates work for your distributors right now?

**Rajesh (Sales):** Sure. We have four regional distributors — ABC Traders, BuildMart, Prime Hardware, and Metro Distributors. Every quarter, based on how much they buy from us, they get a rebate — basically a percentage refund on their purchases. It's meant to reward the bigger buyers and keep them loyal to us instead of switching to competitors.

**BA:** And how is that percentage decided today?

**Priya (Finance):** We have three tiers. Under ₹5 lakh a quarter is 1%, ₹5 lakh to ₹10 lakh is 2%, and above ₹10 lakh is 3%. It's all tracked in an Excel sheet right now.

**BA:** Got it. What's going wrong with the Excel process that's making you want to change it?

**Priya:** Honestly, human error. Last quarter one of our finance executives misread the tier boundary and paid a distributor ₹45,000 instead of ₹36,000. That's a ₹9,000 overpayment on one distributor alone. With four distributors and growing, these mistakes add up.

**BA:** That's helpful context. Does the rebate apply to everything a distributor buys, or are there exclusions?

**Rajesh:** Good question — actually, that's something we've never written down formally. My instinct is no, returns shouldn't count. If they bought something and sent it back, they shouldn't get a rebate on it.

**Priya:** Agreed from Finance's side. Same for cancelled orders and anything that arrived damaged and was written off. We shouldn't be paying a rebate on revenue we never actually kept.

**BA:** Understood — I'll write that up as a formal exclusion rule and confirm it back to you. Is there anything beyond the volume tiers? I noticed you mentioned "loyalty" earlier.

**Rajesh:** Yes — we've talked informally about rewarding distributors who are growing, not just ones who are already big. Someone like Metro Distributors is smaller but growing fast, and right now they get less reward than a big distributor who's actually flat or shrinking. That doesn't feel right.

**BA:** So a growth-based bonus on top of the volume tier?

**Rajesh:** Exactly. If a distributor grows their purchases by, say, 15% or more compared to the same quarter last year, they should get a little extra — maybe half a percent on top of their normal tier.

**Priya:** I'd want that to be simple to calculate and audit, though. Nothing overly complex in year one.

**BA:** Understood. Last question for today — who ultimately approves a rebate before it's paid out?

**Priya:** Finance does. Sales can flag if something looks wrong, but Finance signs off before any payment goes out.

**BA:** Perfect, that answers my structural questions for today. I'll turn this into a documented set of requirements and circulate it before we move to formalizing the rules.

---

## Part B — Structured Meeting Notes

**Attendees:** Rajesh Menon (Sales Manager), Priya Nair (Finance Controller), BA

**Date:** 12 July 2026

### Key Decisions Made
- Rebate program will continue to use a 3-tier quarterly volume structure (1% / 2% / 3%).
- Returned, cancelled, and damaged/written-off goods are **excluded** from rebate-eligible purchase value.
- A new **Growth Bonus** (+0.5%) will be introduced for distributors growing >15% YoY on top of their tier rebate.
- Finance retains final sign-off authority on all rebate payouts; Sales can flag discrepancies but cannot approve.

### Open Questions (Unresolved — carried into BRD as "Open Issues")
1. Should taxes (GST) be included or excluded when calculating the purchase value used for tier lookup?
2. Is the growth comparison based on the *same quarter last year* or *trailing 12 months*? (Rajesh said "same quarter" verbally, but this needs written confirmation.)
3. What happens if a distributor is *new* this year and has no prior-year purchase data to compare growth against?
4. Is there a cap on the maximum rebate % a distributor can earn in total (tier + growth bonus)?

### Action Items

| Action Item | Owner | Due |
|---|---|---|
| Share current Excel rebate-tracking sheet with BA for reference | Priya Nair (Finance) | 15 July 2026 |
| Confirm GST treatment for purchase value calculation | Priya Nair (Finance) | 17 July 2026 |
| Confirm growth comparison period (quarter vs. trailing 12 months) | Rajesh Menon (Sales) | 17 July 2026 |
| Draft first version of Business Requirements Document | BA | 19 July 2026 |
| Circulate draft BRD for stakeholder review | BA | 20 July 2026 |

### Requirement Changes Raised Mid-Call
- Growth Bonus concept was **not** part of the original ask (which was just "digitize the existing tiers") — it emerged organically during the call. Flagged as a **scope addition** to confirm formally in the BRD rather than assumed as in-scope by default.
