# Intent Document: Web3 Participation Bottleneck Selection

**Author:** Christopher Tiku  
**Role:** Web3 Product Owner / Crypto Business Ops Manager Candidate  
**Quest Objective:** Select and validate a Web3 participation loop bottleneck connecting user action to business conversion.  

---

## 1. Executive Summary & Problem Context
Many Web3 platforms suffer from vanity-metric inflation—tracking raw wallet connects or top-of-funnel waitlist signups that yield zero long-term business value. For an asset-information platform, true business conversion occurs when a high-intent user evaluates a public project disclosure and submits a meaningful review or inquiry.

---

## 2. Bottleneck Comparison & Prioritization Matrix

To select the most impactful operational bottleneck, four distinct participation stages were evaluated across four weighted criteria (Scored 1–5, where 5 is highest):

* **User Value (Weight: 25%):** Value provided to the participant or platform ecosystem.
* **Business Conversion (Weight: 35%):** Direct contribution to qualified pipeline vs. vanity noise.
* **Confidence (Weight: 20%):** Certainty in measurement and execution.
* **Effort Required (Weight: 20%):** Operational/Engineering complexity (5 = Lowest effort / easiest).

### Comparison Matrix

| Bottleneck Stage | User Value (25%) | Business Conversion (35%) | Confidence (20%) | Effort Score (20%) | Weighted Total | Rank |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **1. Waitlist Onboarding** | 2 | 1 | 4 | 5 | **2.65** | 4th |
| **2. Disclosure Reading** | 3 | 2 | 3 | 4 | **2.85** | 3rd |
| **3. Reviewer Activation (SELECTED)** | **5** | **5** | **4** | **3** | **4.40** | **1st** |
| **4. Qualified Follow-Up** | 4 | 4 | 3 | 2 | **3.40** | 2nd |

### Justification: Why Reviewer Activation Ranked First
* **High Impact on Business Conversion:** Converting a passive reader into an active reviewer directly creates proprietary platform data and qualified project leads.
* **Focus Over Vanity Metrics:** Waitlist signups and raw disclosure views are easily gameable and do not reflect intent. Reviewer activation forces proof-of-work/intent from the user.
* **Feasible Operational Boundary:** It sits right at the intersection of off-chain participation (reviews) and optional on-chain credentials (testnet badges).

---

## 3. Targeted Users & Evidence

* **Primary Users:** Web3 researchers, protocol analysts, and prospective project backers seeking verified asset information.
* **Observed Friction:** Web3 users are hesitant to connect wallets upfront due to security concerns; conversely, non-wallet incentive loops are frequently spammed by automated sybil bots.
* **Operational Evidence:** Standard Web3 quests report >60% drop-off when wallet connection is forced at entry, while un-gated forms experience >40% low-quality or duplicate spam.

---

## 4. Intended Value & Non-Goals

### Intended Value
* Establish a high-conversion participation loop accessible without mandatory wallet connection.
* Implement anti-bot validation logic to filter non-meaningful reviews.
* Measure true business metrics (`review_qualified`) separately from vanity metrics (`wallet_connected`).

### Non-Goals
* **No Mainnet / Financial Transactions:** Mainnet smart contracts, token rewards, or financial yields are strictly out of scope.
* **No Asset Guarantees:** On-chain acknowledgements do not represent proof of asset ownership, verified reserves, or financial backing.
* **No Manual Moderation Dependency:** Automated validation rules must filter >80% of bot activity before human review.
