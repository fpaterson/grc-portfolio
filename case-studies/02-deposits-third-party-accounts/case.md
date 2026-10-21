# Case Study: Deposits from Third-Party Accounts

> **Note:** This is a real yet composite case based on recurring patterns in non-custodial fintech operations. It contains no real customer data, wallet addresses, transaction hashes, volumes, dates, or partner names. Details have been generalized for portfolio purposes.

---

## 1. Context

In a non-custodial payments application built on the Stellar network, users fund their accounts through regulated third-party partners (anchors). A recurring operational pattern involves users depositing funds from bank accounts that do not belong to them (third-party accounts).

When this occurs, the support team requests proof of the deposit (receipt or transaction confirmation) and escalates the case to the corresponding anchor. The anchor then decides how to resolve the situation according to its own policies and regulatory obligations.

Typical resolution options available to the anchor include:
- Returning the deposit to the originating account, minus processing fees.
- Requesting that the original sender open an account with the application so the funds can be credited there.

---

## 2. Risk Identified

| Risk | Description |
|------|-------------|
| Source-of-funds uncertainty | Funds originate from an account that does not match the registered user, creating potential compliance and fraud exposure. |
| Third-party dependency | Resolution depends entirely on the anchor’s policies, timing, and willingness to act. |
| Customer friction and residual risk | Users may experience delays or partial recovery of funds; the application cannot force a specific outcome. |
| Regulatory exposure | Incomplete visibility into the true origin of funds may conflict with customer due diligence expectations. |

---

## 3. Actions Taken

- Requested deposit confirmation (receipt or bank statement excerpt) from the user.
- Documented the case in the internal ticketing system.
- Escalated the information to the relevant anchor with the available evidence.
- Communicated to the user that the final decision rests with the anchor and that the application has no authority to reverse or reassign the funds unilaterally.
- Followed up with the anchor until a resolution was communicated.

---

## 4. Environmental Constraints

- The application operates under a **non-custodial model** and has no technical or contractual ability to freeze, reverse, or reassign funds.
- KYC/KYB relationships and regulatory responsibility for the fiat side sit with the anchors.
- The application’s role is limited to coordination, documentation, and information sharing.

---

## 5. GRC Analysis

| Aspect | Observation | GRC Domain |
|--------|-------------|------------|
| Third-party risk | Heavy reliance on anchors for both detection outcome and final disposition of funds. | Third-Party Risk Management |
| Customer due diligence | Deposits from unmatched accounts raise source-of-funds questions that the application cannot fully resolve alone. | Customer Due Diligence / CDD |
| Residual risk | Even after escalation, the application retains residual risk related to delayed resolution, partial refunds, or incomplete visibility. | Risk Assessment / Risk Treatment |
| Process reliability | Lack of standardized SLAs with anchors can produce inconsistent handling times and outcomes. | Governance / Operational Risk |
| Documentation | Proper record-keeping of requests, evidence, and escalations is essential for auditability and dispute handling. | Governance / Accountability |

---

## 6. Recommended Controls

**Preventive**
- Clear in-app messaging stating that deposits should come from an account matching the registered user.
- Optional declaration at deposit time regarding the source of funds.

**Detective**
- Automated or manual flagging of name mismatches between the originating account and the registered customer.
- Tracking of repeated third-party deposit patterns per user.

**Corrective / Responsive**
- Standardized escalation template and evidence checklist for support agents.
- Defined follow-up cadence with anchors.
- Clear user communication scripts explaining limitations and expected timelines.

---

## 7. Key Risk Indicators (KRIs)

- Percentage of deposits flagged as originating from third-party accounts.
- Average time from detection to anchor resolution.
- Percentage of cases resolved by refund vs. account creation vs. other outcomes.
- Number of repeated third-party deposit incidents per user.

---

## 8. Alignment with Recognized Standards (Retrospective)

- **FATF Recommendation 10 (Customer Due Diligence):** Relevance of verifying the source of funds and the relationship between the payer and the account holder.
- **NIST CSF:** ID.RA (Risk Assessment), PR.AC (Access Control – limited by architecture), RS.CO (Communications during response).
- **ISO/IEC 27001:** Supplier relationships and information security in supplier agreements (A.5.19 / A.5.21 concepts).

This mapping is illustrative and does not constitute a formal compliance assessment.

---

## 9. Lessons Learned

- Third-party deposits are a predictable residual risk in non-custodial architectures that rely on external anchors for fiat rails.
- The quality of documentation and escalation discipline directly affects the speed and defensibility of the response.
- Clear communication of the application’s limitations reduces user frustration and sets realistic expectations.
- Measuring resolution times and outcomes turns an ad-hoc support process into a manageable risk.

---

## 10. Conclusion

This case illustrates the operational and compliance challenges created when funds arrive from accounts that do not match the registered user in a non-custodial environment. While the application can detect, document, and escalate, final control rests with the regulated third party. From a GRC perspective, the case highlights third-party risk, source-of-funds uncertainty, residual risk acceptance, and the importance of structured coordination and measurement.
