# Case Study: Request for Recipient Data After Incorrect Transfer

> **Note:** This is a real yet composite case based on recurring patterns in non-custodial fintech operations. It contains no real customer data, wallet addresses, transaction hashes, volumes, dates, or partner names. Details have been generalized for portfolio purposes.

---

## 1. Context

In a non-custodial payments application, users occasionally send funds to the wrong recipient (incorrect wallet address or account identifier). After realizing the error, some users contact support and request the personal or contact details of the recipient so they can ask for the funds to be returned directly.

Because the application is non-custodial, it has no technical ability to reverse the transaction or freeze the recipient’s funds. The only possible action is limited coordination.

---

## 2. Risk Identified

| Risk | Description |
|------|-------------|
| Unauthorized disclosure of personal data | Providing the recipient’s contact or identity information would constitute a serious privacy and security violation. |
| Social engineering / secondary fraud | The requesting user could misuse the information, or the situation itself could be part of a social-engineering attempt. |
| Residual risk due to architecture | Once the transaction is confirmed on the network, the application cannot force recovery of the funds. |
| Reputational and regulatory exposure | Sharing user data outside approved channels would breach confidentiality obligations and data-protection principles. |

---

## 3. Actions Taken

- Clearly refused the request for the recipient’s personal or contact details.
- Explained that disclosing such information would constitute a serious security and privacy violation.
- Offered the only available action: the support team can attempt to contact the recipient on the user’s behalf (within policy limits) to relay the recovery request.
- Documented the case and the decision not to share data.
- Communicated the structural limitation: the application cannot reverse or compel the return of funds.

---

## 4. Environmental Constraints

- The application is **non-custodial** and has no authority or technical capability to reverse transactions or control the recipient’s account.
- User data (including contact information) is protected and cannot be shared with other users.
- Any contact with the recipient must be performed by the application’s support team under controlled conditions, not by handing over personal data to the sender.

---

## 5. GRC Analysis

| Aspect | Observation | GRC Domain |
|--------|-------------|------------|
| Data protection & confidentiality | Refusing to share recipient details is a direct application of the principle of data minimization and purpose limitation. | Information Security / Privacy |
| Access control | Personal data of one user is not accessible to another user, even in error scenarios. | Identity & Access Management |
| Residual risk | The inability to force fund recovery is an inherent limitation of the non-custodial model and must be acknowledged. | Risk Assessment / Risk Treatment |
| Decision quality | The refusal is based on clear security principles rather than convenience or customer pressure. | Governance / Risk Appetite |
| Incident / request handling | Treating the request as a potential data-disclosure risk rather than a routine support ticket. | Security Operations / Incident Response |

---

## 6. Control Demonstrated

**Primary control:** Absolute prohibition on sharing one user’s personal or contact information with another user.

This is a preventive and directive control. It is non-negotiable because the harm of unauthorized disclosure outweighs the customer’s desire to recover funds directly.

**Compensating action:** Controlled, one-way outreach by the support team (when policy allows), without revealing contact details to the requesting user.

---

## 7. Key Risk Indicators (KRIs)

- Number of requests for recipient personal data per period.
- Percentage of such requests that are correctly refused.
- Number of cases in which support successfully contacts the recipient on the sender’s behalf.
- Number of complaints or escalations arising from the refusal to share data.

---

## 8. Alignment with Recognized Standards (Retrospective)

- **ISO/IEC 27001:** A.5.15 (Access Control), A.5.34 (Privacy and protection of PII), A.8.2 (Information classification and handling).
- **NIST CSF:** PR.AC (Identity Management and Access Control), PR.DS (Data Security), ID.RA (Risk Assessment).
- **Data protection principles:** Purpose limitation, data minimization, and confidentiality.
- **Security culture:** Demonstrates that security and privacy decisions are not subordinated to customer convenience.

This mapping is illustrative and does not constitute a formal compliance assessment.

---

## 9. Lessons Learned

- Customer pressure to “just share the contact details” is common and must be met with a consistent, principled refusal.
- The non-custodial architecture creates residual risk that cannot be fully eliminated; it must be clearly communicated and accepted at the governance level.
- Documenting both the request and the refusal creates an auditable record of correct security decision-making.
- Training support staff to recognize and correctly handle these requests is a practical control that protects both users and the organization.

---

## 10. Conclusion

This case illustrates a clear conflict between a user’s immediate goal (recovering funds) and fundamental security and privacy obligations. The correct response — refusing to disclose recipient data while offering limited controlled assistance — demonstrates the application of data-protection principles and residual-risk awareness in a non-custodial environment. From a GRC perspective, it highlights access control, confidentiality, decision quality under pressure, and the limits imposed by system architecture.
