# ⚖️ Refund Court

> **AI agents argue refund disputes. A human decides. Every verdict becomes precedent.**

---

## Problem

Customer support teams make inconsistent refund decisions:
- **Same case, different outcome:** Support agents handle disputes subjectively. Two customers with identical missing item claims often receive opposite verdicts depending on which agent reviews the ticket.
- **Costs money:** Overwhelmed agents grant refunds indiscriminately to close tickets quickly, paying out on fraudulent or unverified claims and bleeding company margins.
- **Costs trust:** Frustrated agents unjustly reject genuine buyers whose items were missed at the packing station, eroding customer trust and driving churn.

---

## How It Works

Refund Court turns dispute resolution into an adversarial deliberation among 4 specialized AI agents, with a human lead making the binding call.

### Text Flow Diagram

```text
Support Lead
     │
     ▼ (posts dispute on Order #)
┌─────────────────┐
│   case-clerk    │ ──> Pulls neutral facts from CSV (orders.csv & customers.csv)
└────────┬────────┘
         │ @customer-advocate
         ▼
┌─────────────────┐
│customer-advocate│ ──> Cites policy.md (argues for customer rights & remedies)
└────────┬────────┘
         │ @company-advocate
         ▼
┌─────────────────┐
│company-advocate │ ──> Cites policy.md (protects margins & flags fraud signals)
└────────┬────────┘
         │ @precedent-keeper
         ▼
┌─────────────────┐
│precedent-keeper │ ──> Searches verdicts.md for matching precedent
└────────┬────────┘
         │
         ▼ (yields to Human judge)
[  Human Verdict  ]
         │
         ▼ (posts final ruling: "Verdict #... logged.")
┌─────────────────┐
│precedent-keeper │ ──> Logged to verdicts.md & posts confirmation
└─────────────────┘
```

1. **Support Lead** initiates a hearing by tagging `@case-clerk` with an Order # and dispute summary.
2. **`case-clerk`** gathers objective facts from `data/orders.csv` and `data/customers.csv` (billed vs scanned items, delivery times, customer refund history).
3. **`customer-advocate`** reviews `policy.md` and argues for the consumer.
4. **`company-advocate`** reviews `policy.md` and protects business margins, fraud rules, and fee retention.
5. **`precedent-keeper`** searches historical rulings in `verdicts.md` and summarizes relevant precedents.
6. **Human Support Lead** evaluates the arguments and issues the final verdict. **Agents never decide.**
7. **`precedent-keeper`** appends the ruling to `verdicts.md`, establishing binding precedent for future disputes.

---

## Example from Our Real Test

In our testing across live scenarios:

- **Order #1043:** Customer Ananya reported missing Amul Milk and Bread. `case-clerk` discovered that while billed, the items were never scanned at the warehouse packing station. `customer-advocate` argued for an item refund under Rule 3.1. `company-advocate` agreed to refund the missing items (INR 90) but insisted on retaining the delivery fee (INR 20) under Rule 3.2 since delivery was on time. The Human Support Lead approved the partial refund, and `precedent-keeper` logged the verdict under Rule 3.1 & 3.2.
- **Order #1062:** Later, customer Tanvi filed a dispute with the exact same pattern (missing Milk and Bread at the same Blinkit Koramangala store):
  - `precedent-keeper` automatically cited Order #1043 as precedent.
  - `company-advocate` noticed it was the **second milk+bread scan miss at the same store** — identifying a warehouse packing issue, not a customer issue.
  - The Human Support Lead issued a verdict in seconds based on established precedent!

---

## How Switch is Used

Switch provides the multi-agent operating environment:
- **One Switch Room on Mattermost:** The Human Support Lead and all 4 agents operate within a single shared `#refund-court` channel mirrored directly to Mattermost.
- **4 Agents with Separate Roles:** Tasks are decoupled across 4 focused agents (`case-clerk`, `customer-advocate`, `company-advocate`, `precedent-keeper`) rather than one monolithic prompt.
- **Handoffs via @Mentions:** Agents hand off turns seamlessly by ending their messages with targeted `@mention` tags, keeping turn-taking orderly without infinite loops.
- **Human-in-the-Loop Final Decision:** Switch facilitates autonomous agent deliberation while keeping final decision authority with the human judge.
- **Shared Files as Room Memory:** Agents read and write shared project files (`data/orders.csv`, `data/customers.csv`, `policy.md`, `verdicts.md`) as persistent room memory that deepens with every verdict.

---

## Setup (Windows)

1. **Install Prerequisites:**
   - Install and start **Docker Desktop**.
   - Install **Node.js** (LTS).
   - Install the OpenCode CLI:
     ```powershell
     npm install -g opencode-ai
     ```
   - Authenticate with OpenCode:
     ```powershell
     opencode auth login
     ```

2. **Start Switch Console:**
   - Open the Switch application and choose **Run a server on this computer**.
   - Ensure the Switch local server and Mattermost container are up.

3. **Create the 4 Agents Manually:**
   > [!NOTE]
   > `refund-court.template.yaml` is included in this repository. However, on our Windows setup, the template form did not detect the provider, so we created agents manually.

   In **Switch Console** -> **Your Agents** -> **Add agent**, create each of the 4 agents:
   - **Provider:** Select `OpenCode`.
   - **Instructions:** Copy and paste the text from:
     - [`agents/case-clerk.md`](file:///E:/refund-court/agents/case-clerk.md)
     - [`agents/customer-advocate.md`](file:///E:/refund-court/agents/customer-advocate.md)
     - [`agents/company-advocate.md`](file:///E:/refund-court/agents/company-advocate.md)
     - [`agents/precedent-keeper.md`](file:///E:/refund-court/agents/precedent-keeper.md)
   - **Model:** Under **Advanced configuration**, set **Model** to a working model (e.g. free OpenCode models).

4. **Create Room & Add Agents:**
   - Create room `refund-court` on Mattermost.
   - Add all 4 agents (`case-clerk`, `customer-advocate`, `company-advocate`, `precedent-keeper`) to the room.

5. **Post First Dispute:**
   - Open `#refund-court` on Mattermost and post the first dispute from [`demo/script.md`](file:///E:/refund-court/demo/script.md):
     ```text
     @case-clerk Dispute on Order #1043: Customer Ananya reports Amul Milk and Bread were missing from delivery.
     ```

---

## Challenges We Faced

- **Windows username with spaces confused provider detection:** Having a space in the Windows user profile path interfered with automatic provider discovery in the template form.
- **Local Switch server stopping and needing restart:** The local Switch server occasionally halted during multi-turn testing and needed to be restarted.
- **Gemini free tier 20 requests/day ran out, moved to free OpenCode models:** Hit the daily Gemini rate limits rapidly during debugging, switching to free OpenCode models to continue development.
- **Agents stopping the handoff chain until instructions forced it:** Agents occasionally dropped the trailing `@mention`, halting the chain until strict handoff instructions were enforced in each prompt.

---

## Demo Video
- [link coming soon]

---

## Team
- Roshan Maddeshiya
- [teammate name]

---

## Track
- **Flip the Switch Hackathon, Track 01: Best Business Workflow**
