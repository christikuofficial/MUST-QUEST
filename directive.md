# Directive Document: Web3 Reviewer Activation Operating Loop

**Author:** Christopher Tiku  
**Status:** Complete & Verified  

---

## 1. Objective & Scope

### Objective
Deploy an operating loop that converts waitlist users into active reviewers on an asset-information platform, driving qualified project inquiries while maintaining anti-sybil protections and optional wallet paths.

### Scope
* **In-Scope:** Off-chain review submission, automated qualification filtering, optional EVM testnet acknowledgement, synthetic metric tracking, channel experiment brief.
* **Out-of-Scope:** Mainnet contracts, token sales, guaranteed investment disclosures.

---

## 2. Participation Journey & Rule Set

### User Journey Map
1. **Registration:** User enters via waitlist using Email/Username.
2. **Disclosure Access:** User reads public disclosure report.
3. **Core Action (Off-Chain):** User submits structured review/inquiry.
4. **Qualification Engine:** System checks length (>=150 chars) and IP/duplicate flags.
5. **Optional On-Chain Action:** Qualified user may optionally connect wallet and mint testnet acknowledgement badge.

### Rules & Exclusions
* **Non-Wallet Access:** Wallet connection is strictly **optional**. Non-wallet users retain 100% eligibility for review qualification.
* **Anti-Bot / Exclusion Logic:**
  * Submissions < 150 characters marked `EXCLUDED_BOT`.
  * Duplicate IP / Fingerprint within 24h marked `EXCLUDED_DUPLICATE_IP`.
* **Acknowledgement Rules:** Testnet minting is available **only after** review qualification. Acknowledgements grant no financial rights or proof of reserves.

---

## 3. Product Requirement Document (PRD) & Backlog

### Core Requirements
* **FR-1:** Dual-path submission form (Email-only vs. Wallet-connected).
* **FR-2:** Qualification engine validating character count and duplicate IP flags.
* **FR-3:** Post-qualification optional testnet badge trigger.

### Prioritized 5-Item Backlog

#### Task 1: Review Submission API (P0)
* **Description:** REST endpoint for review submission handling both guest and wallet users.
* **Acceptance Criteria:** Accepts `user_id`, `email`, `disclosure_id`, `review_text`, optional `wallet_address`. Returns `201 Created` with `PENDING_QUALIFICATION` status.

#### Task 2: Automated Anti-Spam & Qualification Service (P0)
* **Description:** Service evaluating submission rules prior to database commit.
* **Acceptance Criteria:** Rejects or flags entries <150 chars as `EXCLUDED_BOT`. Flags matching IP/Fingerprint within 24h as `EXCLUDED_DUPLICATE_IP`. Sets valid items to `QUALIFIED`.

#### Task 3: Dual-Metric Conversion Analytics Pipeline (P1)
* **Description:** Metric logging separating vanity metrics from true conversion.
* **Acceptance Criteria:** Tracks `raw_wallet_connects` separately from `qualified_reviews`. Computes conversion denominator as `Qualified Reviews / Total Registered Users`.

#### Task 4: Optional Testnet Acknowledgement Issuer (P1)
* **Description:** Optional Web3 prompt for testnet proof-of-review minting.
* **Acceptance Criteria:** Displays "Mint Badge" prompt only when `Qualification_Status == QUALIFIED`. Provides clear "Skip Wallet" button that completes flow without error.

#### Task 5: Status Dashboard & Feedback UI (P2)
* **Description:** User-facing status component.
* **Acceptance Criteria:** Displays qualification status to user within 5 seconds. Displays actionable error message if flagged (e.g., "Review must exceed 150 characters").
  
### Advanced Anti-Sybil Architecture (v2 Roadmap)
To prevent users from bypassing basic IP rate-limiting via VPNs or proxy networks:
1. **Persistent Device Fingerprinting:** Deploy client-side fingerprinting (Canvas/WebGL hash + LocalStorage tokens) to uniquely identify devices across changing IP addresses.
2. **Semantic Plagiarism & Entropy Scoring:** Run string-similarity checks (Levenshtein distance) against historical submissions to flag duplicate or AI-generated copy-paste review text (>85% similarity threshold).
3. **Behavioral Telemetry & Velocity:** Track `time_on_page` and paste events; forms submitted in <8 seconds or initiated via headless browser environments are tagged as `EXCLUDED_BOT_VELOCITY`.


---

## 4. Measurement Architecture & Synthetic Dataset

### Funnel Definitions & Event Schema
* `user_registered`: User enters waitlist.
* `review_submitted`: Raw submission event.
* `review_qualified`: Submission passes qualification filters.
* `wallet_connected`: (Optional) Wallet connection event.
* `testnet_ack_minted`: (Optional) On-chain testnet event.

### Baseline, Target, and Stop Rules
* **Baseline Qualified Conversion:** 10%
* **Target Qualified Conversion:** 25%
* **Kill / Stop Rule:** If `EXCLUDED_BOT` + `EXCLUDED_DUPLICATE` exceeds 35% of total submissions over 48h, pause campaign to update anti-spam rules.

---

## 5. Channel Experiment Brief & Decision Memo

### 1-Week Channel Experiment Brief
* **Hypothesis:** Web3 Research Discord/Telegram channels yield 2x higher Qualified Conversion Rates than general Twitter/X traffic.
* **Channel Split:** 50% Research Communities / 50% Public Social.

### Weekly Decision Memo
* **Simulated Finding:** Public social channels generated high volume but a 44% bot/duplicate flag rate. Research channels yielded an 80% qualification rate.
* **Next Action for Engineering:** Implement Cloudflare turnstile CAPTCHA on review endpoints.
* **Next Action for Operations:** Reallocate 80% of acquisition budget into dedicated Web3 research communities.

---

## 6. Results & Handoff Appendix

### Required Artifact Links
* **Operating Prototype (Google Sheets):** [Insert Your Public Google Sheets URL Here]
* **Loom Walkthrough Video (< 5 min):** [Insert Your Public Loom URL Here]

### Verification & Reproduction Steps
1. Open the Google Sheets prototype link.
2. Observe Rows 2–11 containing 10 synthetic participant records.
3. Verify edge cases:
   * **Row 3 (`USR_002`):** Non-wallet user who successfully converts to `QUALIFIED`.
   * **Row 5 (`USR_004`):** Duplicate IP flagged as `EXCLUDED_DUPLICATE_IP`.
   * **Row 10 (`USR_009`):** Qualified user experiencing a `FAILED` testnet minting edge case without invalidating their qualification status.
4. Verify summary formulas in cells `K2:K6` proving separation of `Raw Wallet Connections` (7) vs.  `Qualified Conversions⁠` (7) and a 70% Qualified Conversion Rate.

### AI Collaboration & Specification Audit Log
* **Initial AI Output:** AI initially generated KPI formulas using raw wallet connections (`C2:C11`) as the main conversion numerator.
* **Correction Applied:**
1. Corrected the conversion rate formula to `=COUNTIF(G2:G11, "QUALIFIED") / COUNTA(A2:A11)`. This ensures non-wallet qualified users are counted and vanity wallet connects are excluded.
2. Recognized that basic IP and character filters are easily bypassed by VPN hopping and script farms. Suggested and authored an advanced, multi-layer Anti-Sybil specification incorporating persistent client-side device fingerprinting (Canvas/LocalStorage tokens), semantic similarity/plagiarism checks, and interaction velocity telemetry.
* **Specification Refinement:** Refined task backlog acceptance criteria to handle testnet transaction drop-outs without degrading off-chain review metrics.

### Limitations
* Synthetic dataset size is limited to 10 records for prototype demonstration.
* Anti-bot filtering uses static character count and IP flags rather than live machine-learning NLP models.
