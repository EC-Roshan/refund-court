# Refund Court — 2-3 Minute Hackathon Demo Video Script

**Track 01:** Best Business Workflow (Flip the Switch Hackathon)  
**App:** Mattermost (via Switch Bridge)  
**Provider:** OpenCode (with Gemini model) on Windows  
**Total Target Duration:** 2:45 minutes  

---

## Pre-Recording Checklist (30 seconds before recording)
1. Ensure Switch server is running and OpenCode provider is healthy.
2. Ensure Mattermost is open to `#refund-court`.
3. Ensure `verdicts.md` has its initial header and empty `## Log` section.
4. Have this script open on a second monitor or side-by-side to copy-paste.

---

## Scene 0: Introduction (0:00 – 0:25)
**Voiceover / On-camera:**
> "Hi everyone, this is **Refund Court**. In quick commerce, customer refund disputes cost millions: support agents either blindly issue refunds bleeding margins, or reject legitimate customers creating churn.
> With **Switch**, we turn a Mattermost chat room into an AI courtroom. Four specialized agents deliberate disputes using real order logs, warehouse packing scans, customer history, and business policy. But the human Support Lead—me—always delivers the final verdict. Let's see it in action."

---

## Scene 1: Case #1043 — Missing Items with Packing Scan Mismatch (0:25 – 1:10)
*Demonstrating: Neutral clerk investigation, policy citing advocates, human-in-the-loop decision, and precedent logging.*

### 1. Human Action (Type in Mattermost):
```text
@case-clerk Dispute on Order #1043: Customer Ananya reports Amul Milk and Bread were missing from delivery.
```

### 2. Expected Room Flow:
- **`case-clerk`**:
  > Order #1043 (Blinkit Koramangala). Customer: CUST-204 (Ananya Iyer, 240 days old, 48 orders, 0 refunds in last 30 days).  
  > Items billed: Milk 1L, Bread 400g, Eggs 6pc, Maggi 4-Pack (INR 194).  
  > Packing scan log: Eggs 6pc, Maggi 4-Pack only. Milk and Bread were NOT scanned into bag.  
  > Delivered in 15 min (promised 12 min).  
  > @customer-advocate
- **`customer-advocate`**:
  > The warehouse packing scan proves the customer never received the Milk (INR 54) and Bread (INR 36).  
  > Under **Rule 3.1**, the customer is entitled to a full refund of INR 90 for unfulfilled items.  
  > Ananya is a loyal customer with 48 orders and zero prior refund abuse.  
  > @company-advocate
- **`company-advocate`**:
  > The packing scan discrepancy corroborates the missing items; we agree to refund INR 90 per **Rule 3.1**.  
  > However, under **Rule 3.2**, the delivery fee of INR 20 is strictly non-refundable since the order arrived in 15 minutes (delay <= 30 min).  
  > Total payout must remain capped at INR 90.  
  > @precedent-keeper
- **`precedent-keeper`**:
  > Searched `verdicts.md`: No prior precedent on record for Order #1043.  
  > Case deliberation concluded under Rules 3.1 & 3.2.  
  > Awaiting binding verdict from Human Support Lead.

### 3. Human Verdict (Type in Mattermost):
```text
Verdict #1043: APPROVED_REFUND INR 90 for missing Milk and Bread. Warehouse packing scan confirms omission. Delivery fee retained per Rule 3.2. @precedent-keeper log verdict.
```

### 4. Agent Confirmation:
- **`precedent-keeper`**:
  > Verdict for Order #1043 recorded in `verdicts.md`. Precedent logged for future missing scan cases.

---

## Scene 2: Case #1058 — Fraud Signal & Packing Scan Match (1:10 – 1:55)
*Demonstrating: Fraud detection, Rule 3.4 & 3.5 policy enforcement, protecting business margin.*

### 1. Human Action (Type in Mattermost):
```text
@case-clerk Dispute on Order #1058: Customer Rahul claims Ferrero Rocher box was missing from his bag.
```

### 2. Expected Room Flow:
- **`case-clerk`**:
  > Order #1058 (Instamart HSR). Customer: CUST-215 (Rahul Kapoor, account age 18 days, 6 total orders, 5 refunds in last 30 days).  
  > Items billed: Ferrero Rocher 16pc Box, Epigamia Greek Yogurt 2pc (INR 890).  
  > Packing scan log: Both Ferrero Rocher and Greek Yogurt were scanned into bag.  
  > Delivered in 16 min (promised 15 min).  
  > @customer-advocate
- **`customer-advocate`**:
  > The customer claims the high-value item was absent upon opening.  
  > While Rule 3.1 covers missing items, the packing scan shows all items were packed.  
  > Under **Rule 3.4**, photo evidence of the delivered bag and tamper seal is required to proceed.  
  > @company-advocate
- **`company-advocate`**:
  > Disallow immediately. The warehouse scan proves all items packed; zero photo evidence was provided (**Rule 3.4**).  
  > Furthermore, this account has 5 refunds in 30 days on just 6 lifetime orders, triggering **Rule 3.5** fraud threshold.  
  > This is an 890 INR margin leak attempt. Immediate rejection recommended.  
  > @precedent-keeper
- **`precedent-keeper`**:
  > Searched `verdicts.md`: Zero precedents approving refunds with complete packing scans and >3 prior refunds.  
  > Advocates cite Rules 3.4 and 3.5.  
  > Awaiting binding verdict from Human Support Lead.

### 3. Human Verdict (Type in Mattermost):
```text
Verdict #1058: REJECTED. Packing scan confirms all items packed. Account flagged for excessive refunds (5 in 30 days) under Rule 3.4 and Rule 3.5. Photo proof required. @precedent-keeper log verdict.
```

### 4. Agent Confirmation:
- **`precedent-keeper`**:
  > Verdict for Order #1058 recorded in `verdicts.md`. Rejection precedent logged for fraud prevention.

---

## Scene 3: Case #1062 — Precedent Acceleration (1:55 – 2:25)
*Demonstrating: Institutional memory in action. Precedent-keeper cites Case #1043, enabling human to decide in 5 seconds.*

### 1. Human Action (Type in Mattermost):
```text
@case-clerk Dispute on Order #1062: Customer Tanvi reports missing Milk and Bread.
```

### 2. Expected Room Flow:
- **`case-clerk`**:
  > Order #1062 (Blinkit Koramangala). Customer: CUST-220 (Tanvi Saxena, 195 days old, 39 orders, 0 refunds in last 30 days).  
  > Items billed: Milk 1L, Bread 400g, Butter 100g (INR 149).  
  > Packing scan log: Butter 100g only. Milk and Bread were NOT scanned.  
  > Delivered in 14 min (promised 12 min).  
  > @customer-advocate
- **`customer-advocate`**:
  > Clear packing omission of Milk and Bread under **Rule 3.1**. Same darkstore pattern as seen earlier.  
  > Customer has zero refund history in 30 days.  
  > @company-advocate
- **`company-advocate`**:
  > Concur on missing item value refund (INR 90) under **Rule 3.1** due to scan mismatch.  
  > Delivery fee non-refundable under **Rule 3.2**.  
  > @precedent-keeper
- **`precedent-keeper`**:
  > **Direct Precedent Found:** Order #1043 (Blinkit Koramangala) established refund of INR 90 for missing Milk and Bread with warehouse scan omission, retaining delivery fee under Rule 3.2.  
  > Facts and customer clean record match Order #1043 exactly.  
  > Recommending identical ruling to Human Support Lead.

### 3. Human Verdict (Type in Mattermost — decided in seconds!):
```text
Verdict #1062: APPROVED_REFUND INR 90 per Precedent #1043 and Rule 3.1. Delivery fee retained per Rule 3.2. @precedent-keeper log verdict.
```

### 4. Agent Confirmation:
- **`precedent-keeper`**:
  > Verdict for Order #1062 appended to `verdicts.md`. Case closed via Precedent #1043.

---

## Scene 4: Conclusion & Wrap-Up (2:25 – 2:45)
**Voiceover / On-camera:**
> "In under three minutes, we resolved three tricky disputes:
> 1. Approved a legitimate claim with clear data evidence.
> 2. Blocked an ₹890 fraud attempt by catching a serial refunder.
> 3. Used instant precedent to decide the third case in seconds.
> 
> Because **Switch** brings multiple AI agents and human leads into one shared Mattermost room with persistent memory, we get faster decisions, zero fraud blindspots, and a 100% human-governed audit trail. That's Refund Court."
