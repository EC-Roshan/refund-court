# ⚖️ Refund Court

> **Flip the Switch Hackathon — Track 01: Best Business Workflow**  
> AI-powered courtroom in your team chat for e-commerce and quick-commerce refund disputes.  
> Powered by [Switch](https://github.com/sandbox-quantum/switch) + [OpenCode](https://github.com/opencode-ai) + Mattermost on Windows.

---

## 📽️ Demo Video
- **Video Link:** *[Insert Demo Video Link Here]*
- **Team:** *[Insert Team Names / Contact Here]*

---

## 1. The Problem: Inconsistent Refund Decisions Cost Millions

In rapid-fulfillment e-commerce and quick-commerce (Blinkit, Zepto, Instamart), customer support receives thousands of refund tickets every hour:
- **Margin Bleed:** First-line support agents often blindly grant refunds to close tickets quickly, paying out on fraudulent or unverified claims.
- **Customer Churn:** Frustrated agents unfairly reject genuine buyers whose items were legitimately missed at the warehouse packing station.
- **Siloed Context:** Customer support reps don't cross-reference warehouse packing barcode scans, customer refund frequency, or company policy in real time.
- **Zero Precedent Consistency:** Two customers with identical missing item claims get opposite outcomes depending on which agent handles the ticket.

---

## 2. How It Works

Refund Court turns a Mattermost chat channel into an adversarial AI courtroom:
- **`case-clerk`**: Gathers objective evidence from `data/orders.csv` and `data/customers.csv` (billed vs packing scan, delivery times, refund history).
- **`customer-advocate`**: Argues for consumer rights, citing specific rules from `policy.md` and highlighting customer loyalty.
- **`company-advocate`**: Defends business margins, flags fraud signals (>3 refunds in 30 days), and protects delivery fee retention.
- **`precedent-keeper`**: Searches historical rulings in `verdicts.md` to identify matching case law, then asks the Human Support Lead to decide.
- **Human Support Lead (YOU)**: The human is the sole judge. **Agents never decide.**
- **Verdict Archival**: The Human Lead delivers the verdict; `precedent-keeper` automatically records it to `verdicts.md` to establish binding precedent for future disputes.

### Text Flow Diagram

```text
[Human Support Lead]
        │
        ▼ (Pastes dispute ticket: "@case-clerk Dispute on Order #1043...")
┌─────────────────┐
│   case-clerk    │ ──> Reads data/orders.csv & customers.csv (neutral facts)
└────────┬────────┘
         │ @customer-advocate
         ▼
┌─────────────────┐
│customer-advocate│ ──> Cites policy.md (Rule 3.1, 3.3; argues for customer)
└────────┬────────┘
         │ @company-advocate
         ▼
┌─────────────────┐
│company-advocate │ ──> Cites policy.md (Rule 3.2, 3.4, 3.5; guards margins/fraud)
└────────┬────────┘
         │ @precedent-keeper
         ▼
┌─────────────────┐
│precedent-keeper │ ──> Searches verdicts.md; cites past cases
└────────┬────────┘
         │
         ▼ (Yields to human judge)
[Human Support Lead]
        │
        ▼ (Delivers binding verdict: "Verdict #1043: APPROVED_REFUND...")
┌─────────────────┐
│precedent-keeper │ ──> Appends ruling to verdicts.md & confirms
└─────────────────┘
```

---

## 3. How Switch is Used

Switch provides the multi-agent operating framework that makes Refund Court possible:

1. **Team Chat Rooms (`room:`):**
   Switch provisions a shared `#refund-court` channel mirrored directly into the team chat application (bundled Mattermost). The human lead and all agents reside in the exact same workspace.
2. **Multiple Collaborative Agents (`agents:`):**
   Instead of a single monolithic prompt, Switch orchestrates 4 lean, specialized agents with isolated roles (`case-clerk`, `customer-advocate`, `company-advocate`, `precedent-keeper`), all running under the `opencode` provider.
3. **Directed Multi-Agent Handoffs:**
   Agents maintain strict turn-taking discipline without runaway loops. Each agent speaks only when addressed, processes data via tool calls, and hands off execution to the next peer using `@mention` triggers.
4. **Human-in-the-Loop Governance:**
   Switch enables autonomous agent collaboration while ensuring the human remains the definitive decision-maker. Critical financial disbursements never occur without explicit human sign-off.
5. **Shared Room Memory & Persistent Precedents:**
   Every agent in the room has visibility into previous turns and can read/write to the local workspace filesystem (`verdicts.md`), creating compounding institutional memory.

---

## 4. Setup Steps

### Prerequisites
- **OS:** Windows 10/11
- **Docker Desktop:** Installed and running (for Switch and bundled Mattermost)
- **OpenCode Provider:** Installed and configured with your Gemini API key:
  ```powershell
  $env:GEMINI_API_KEY="your-gemini-api-key-here"
  ```

### Step 1: Clone & Navigate to Repository
```powershell
git clone <your-repo-url> refund-court
cd refund-court
```

Verify the files are present:
- `data/orders.csv` (order logs with hidden dispute cases)
- `data/customers.csv` (customer profiles and refund histories)
- `policy.md` (6 codified dispute policies)
- `verdicts.md` (clean precedent log)
- `agents/*.md` (agent instructions)
- `refund-court.template.yaml` (Switch provisioning template)

### Step 2: Start Switch and OpenCode
Start Switch according to the [Switch documentation](https://github.com/sandbox-quantum/switch). Ensure the `opencode` provider is running and registered with Switch.

### Step 3: Import Template in Switch Console
1. Open the **Switch Console** in your browser.
2. Navigate to **Templates** -> **Import Template**.
3. Select or paste `refund-court.template.yaml`.
4. Ensure the working directory points to your project folder (e.g., `E:\refund-court` or `.`).
5. Click **Create** / **Run Template**. Switch will:
   - Create the 4 agents: `case-clerk`, `customer-advocate`, `company-advocate`, `precedent-keeper`.
   - Create the `#refund-court` room on Mattermost.
   - Post the initial kickoff announcement.

### Step 4: Open Mattermost & Run Demo
1. Open Mattermost in your browser or desktop app and enter `#refund-court`.
2. Follow the step-by-step walkthrough in [`demo/script.md`](file:///E:/refund-court/demo/script.md) to test:
   - **Case #1043:** Missing items with packing scan discrepancy.
   - **Case #1058:** Fraud attempt blocked (5 refunds in 30 days + full packing scan).
   - **Case #1062:** Instant verdict enabled by Case #1043 precedent!

---

## 5. Repository Structure

```text
refund-court/
├── .gitignore                    # Ignores keys, environment files, and local logs
├── README.md                     # Project documentation & setup instructions
├── policy.md                     # 6 numbered refund rules (Rules 3.1 - 3.6)
├── verdicts.md                   # Log of precedents rendered by Human Support Lead
├── refund-court.template.yaml    # Switch template (version: 1)
├── agents/                       # Agent prompt instructions
│   ├── case-clerk.md
│   ├── customer-advocate.md
│   ├── company-advocate.md
│   └── precedent-keeper.md
├── data/                         # Dispute & customer dataset
│   ├── orders.csv                # 30 quick-commerce orders with 4 dispute test cases
│   └── customers.csv             # Customer age, lifetime orders, and refund frequency
└── demo/
    └── script.md                 # 2-3 minute copy-paste video recording script
```
