# Case Study: Account Takeover Mitigation via Recovery Email Validation

> **Note:** This is a real yet composite case based on recurring patterns in non-custodial fintech operations. It contains no real customer data, wallet addresses, transaction hashes, volumes, dates, or partner names. Details have been generalized for portfolio purposes.

---

## 1. Context

A non-custodial payments application relies on a regulated third-party partner (the anchor) to handle fiat on/off-ramps and customer due diligence, including KYC.

Users can request a change to their **primary email address** through the support team. The primary email is the main login identifier for the account. Because the application is non-custodial and does not perform identity verification itself, support agents have no way to physically verify the identity of the person making the request.

This creates an exposure: an attacker who has obtained leaked or purchased credentials could attempt to take over an account by changing the primary email to one they control, effectively displacing the legitimate user.

---

## 2. Risk Identified

| Risk | Description |
|---|---|
| **Account Takeover (ATO) via email takeover** | An attacker with partial access to the account changes the primary email to lock out the legitimate user. |
| **Identity impersonation** | The support workflow cannot independently verify the requester's identity. |
| **Credential reuse from external breaches** | Users who reuse passwords across services are exposed when those credentials appear in leaked databases. |

The primary email is not just a contact field — it is the account's identity anchor. Changing it without additional verification is a high-impact action.

---

## 3. Control Implemented

**Business rule:** To change the primary email, the user must send the same request **from the recovery email previously registered on the account**.

This acts as an **out-of-band verification** step: the support agent confirms that the person requesting the change also controls the recovery channel tied to the account.

The control is a **compensating control**, because:

- The application cannot verify identity in person.
- KYC and the contractual relationship with the end user rest with the anchor, not the application.
- Support operates remotely and cannot rely on physical presence or document inspection.

---

## 4. Limitations and False Positives

The control is effective at raising the cost of ATO, but it is **not a fraud detector**. A refusal to complete the recovery-email step is a **risk indicator**, not proof of fraud.

Legitimate users may decline or abandon the process for reasons unrelated to fraud:

- **Friction:** They do not want to take an extra step for what feels like a routine request.
- **Loss of access:** They no longer have access to the recovery email and cannot complete the verification.
- **Distrust:** They are uncomfortable sending a request from a second account, or they suspect phishing.
- **Confusion:** They do not understand why a second email is required.

Treating every refusal as confirmed fraud would generate false positives, unfair blocks, and potential customer-treatment issues. The correct posture is: **a refusal raises the risk profile and justifies escalation or additional review, but does not by itself confirm fraud.**

---

## 5. GRC Analysis

| Aspect | Observation | GRC Domain |
|---|---|---|
| Access control | The primary email is the account's identity anchor; changing it is a high-impact action that requires additional verification. | Identity & Access Management |
| Compensating control | Recovery-email validation substitutes for identity verification the application cannot perform directly. | Security Controls / Risk Treatment |
| Fraud risk | ATO via email takeover is a known pattern in credential-stuffing and leaked-credential scenarios. | Fraud Risk Management |
| UX vs. security trade-off | The control introduces friction for all users in order to reduce risk from a subset of malicious actors. | Governance / Risk Appetite |
| Escalation ownership | It is not always clear when a refusal should move from support to compliance or to the anchor. | Governance / Incident Response |
| Residual risk | Legitimate users who have lost access to their recovery email cannot complete the process; no alternative verification path is defined. | Risk Assessment / Risk Treatment |

---

## 6. Escalation Workflow

1. User requests a change to the primary email through support.
2. Support explains the requirement: the same request must be sent from the recovery email on file.
3. **If the user completes the step:** the change is processed according to the anchor's policy and internal procedures.
4. **If the user refuses or cannot complete the step:** the case is flagged as a risk indicator and escalated for additional review.
5. **If the pattern is repeated or inconsistent:** the case is escalated to the anchor and/or compliance, depending on the anchor's policy and applicable reporting obligations.
6. The application does not inform the user of any regulatory reporting decision.

---

## 7. Key Risk Indicators (KRIs)

- Percentage of primary-email change requests that require recovery-email validation.
- Percentage of requests completed vs. refused or abandoned.
- Average time from request to resolution.
- Number of cases escalated to the anchor or compliance per period.
- Number of legitimate users blocked due to loss of access to the recovery email (a measure of false-positive cost).

---

## 8. Alignment with Recognized Standards (Retrospective)

The control in this case came from operational experience and practical risk management, not from a formal framework. Reviewed afterwards, it is consistent with widely used standards:

- **NIST CSF:** PR.AA (Identity Management, Authentication, and Access Control), DE.CM (Continuous Monitoring).
- **ISO/IEC 27001:** A.5.15 (Access Control), A.5.16 (Identity Management), A.8.5 (Secure Authentication).
- **Applicable data protection rules:** Handling of the recovery email as personal data, including minimization and secure transmission.

This mapping is illustrative and is not a compliance assessment.

---

## 9. Lessons Learned

- The recovery-email requirement is a **risk indicator**, not a fraud conclusion. The distinction matters for fair and defensible decisions.
- A control that blocks malicious actors will also create friction for some legitimate users; that cost should be measured, not ignored.
- There is a structural gap for legitimate users who have lost access to their recovery email. An alternative verification path should be defined and documented.
- Clear escalation criteria reduce dependence on individual agent judgment and make outcomes more consistent.
- Measuring refusal rates, resolution times, and false-positive costs turns the control from a rule into a managed risk.

---

## 10. Conclusion

This case illustrates how a simple business rule — requiring confirmation from the recovery email — can act as a meaningful compensating control against account takeover in an environment where the application cannot verify identity directly.

From a GRC perspective, it highlights the tension between security and user experience, the difference between a risk indicator and proof of fraud, and the importance of measuring both the control's effectiveness and its cost to legitimate users.

---

*These measures are derived from case analysis. They do not imply that the proposed controls or procedures have been formally implemented or audited.*
