# Refund Court — Verdicts Log

Official precedent log for dispute decisions rendered by the Human Support Lead.
Agents must search this file for precedents before hearings and append signed verdicts here.

## Verdict Entry Format
Each recorded verdict must be appended as a single line under `## Log` using this pipe-delimited structure:
`YYYY-MM-DD | Order #{order_id} | Customer: {customer_id} | Dispute: {dispute_type} | Verdict: {APPROVED_REFUND|REJECTED|PARTIAL_REFUND} | Amount: INR {amount} | Policy Cited: {rules} | Rationale: {one_line_summary} | Decided By: Human Support Lead`

## Log
2026-11-04 | Order #1043 | Customer: CUST-204 | Dispute: missing_items | Verdict: PARTIAL_REFUND | Amount: INR 65-70 | Policy Cited: Rule 3.1, Rule 3.2 | Rationale: Two unscanned items refunded under Rule 3.1; delivery fee retained (3-min delay within 30-min tolerance) and no goodwill credit | Decided By: Human Support Lead
2026-11-06 | Order #1062 | Customer: CUST-220 | Dispute: missing_items | Verdict: PARTIAL_REFUND | Amount: INR 70-75 | Policy Cited: Rule 3.1, Rule 3.2 | Rationale: Two unscanned items refunded under Rule 3.1 same as #1043; delivery fee retained (2-min delay within 30-min tolerance); Blinkit Koramangala packing station flagged for review | Decided By: Human Support Lead
