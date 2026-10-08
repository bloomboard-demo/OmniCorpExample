# OmniCorpExample
AI for business internship sample project using OmniCorp case study
**OmniCorp Return Assist AI** is an intelligent customer service agent and support workbench designed to automate and standardize product return requests for OmniCorp Retail. It parses inbound customer emails, validates company return policies, generates RMA codes, produces structured records for Google Sheets, and drafts policy-compliant email responses for human review.

---

## 🚀 What the Agent Does

The agent executes a multi-step verification and response pipeline for every inbound return request:

```
[Customer Email / Webhook] 
       │
       ▼
1. Extract Order #, SKU, Condition & Photo Analysis 
       │
       ▼
2. Cross-reference OmniCorp Master Order Database
       │
       ▼
3. Evaluate 30-Day Window & Company Return Rules
       │
       ▼
4. Generate Official RMA Code (RMA-YYYY-XXXX)
       │
       ▼
5. Draft Policy-Compliant Response (Addressed to [Customer Name])
       │
       ▼
6. Human Worker Review Workbench (Create email Draft)
```

---

## 📋 Core Policy Rules Enforced

The agent evaluates every inquiry against OmniCorp Retail's standard policies:

1. **Entity Extraction (Rule 1)**: Identifies the order number (`ORD-YYYY-XXXX`), product SKU (`SKU-OMNI-XXXX`), and reason for return (e.g., unopened, shipping damage, sizing, or changed mind).
2. **30-Day Purchase Window (Rule 2)**: Computes elapsed days since purchase date.
3. **Status Determination (Rule 3)**:
   - **Full Refund Eligible**: Unopened merchandise or items damaged during shipping within 30 days.
   - **Restocking Fee Required (15%)**: Opened, non-defective items returned within 30 days.
   - **Manager Review Needed**: Inquiries past 30 days, final sale items, or requests missing purchase verification.
   - **Not Eligible for Return**: Items explicitly outside policy (e.g., clearance / hygiene restrictions).
4. **RMA Tracking Code (Rule 4)**: Generates a tracking identifier formatted as `RMA-YYYY-XXXX` (e.g., `RMA-2026-9481`).
5. **Customer Email Drafting (Rule 5)**: Produces a tailored, professional response explaining return instructions, required packing slips, and next steps.
6. **Strict Guardrail (Rule 6)**: The agent **never** promises unauthorized refunds or waives restocking fees outside official rules.
7. **Clean Structured Record (Rule 7)**: Exports a normalized data object with all policy and order attributes.

---

## 🛡️ Privacy & PII Guidelines Enforced

The application adheres strictly to data protection guidelines across all drafts, inputs, and UI cards:

- **Customer Names**: Automatically replaced with role placeholders like `[Customer Name]`.
- **Street Addresses & Phones**: Replaced with general descriptors (e.g., `[Customer Street Address]`, `[Customer Phone Number]`).
- **Credit Cards & Banking Codes**: Masked with secure blocks (e.g., `[████-████-████-4192]`, `[SECURE-BANKING-BLOCK]`).

---

## 🔒 Operational Boundaries (Section 2.4)

The agent operates with strict safeguards to ensure safe, human-supervised execution:

- **Draft-Maker Only**: Operates strictly as a draft generator. All messages must be approved and dispatched by a human customer service worker. Direct autonomous emailing to customers is blocked.
- **Financial Isolation**: The agent has zero API access to payment gateways, merchant banks, or credit card processors. It cannot issue money.
- **Read-Only Inventory Ledger**: Master order databases and inventory ledgers are query-only; records cannot be modified or deleted.
- **Immutable Audit Trail**: Inquiries and customer interaction records cannot be deleted or purged by the agent.
