# Fraud Coordination in a Non-Custodial Environment (Stellar)

> **Note:** This is a real yet composite case based on recurring patterns in non-custodial fintech operations. It contains no real customer data, wallet addresses, transaction hashes, volumes, dates, or partner names. Details have been generalized for portfolio purposes.

### 1. Background

While managing operations and customer support for a non-custodial financial application built on the Stellar network, the Argentine anchor contacted the internal team after receiving a complaint from a user who had been affected by suspected fraud involving a romance scam or social engineering.

According to the information received, a third party had impersonated a European national associated with professional sports to deceive the user. Following the complaint, an analysis and coordination process was initiated among the parties involved to identify wallets associated with the case and communicate relevant information to the corresponding anchors.

### 2. Actions Taken

- **Complaint analysis and documentation:** Reviewed the information received through the Argentine anchor to understand the case and facilitate its assessment by the internal team.
- **Internal coordination:** Helped coordinate the efforts of the parties involved to follow up on the case and facilitate information sharing.
- **Wallet identification and reporting:** Coordinated efforts that led to the identification of wallets associated with the alleged fraudster and their reporting to the relevant African anchor, enabling it to assess possible actions within the scope of its policies and procedures.
- **Third-party escalation:** Communicated relevant information to the parties responsible for assessing potential measures concerning the accounts and transactions involved.

### 3. Environmental Constraints

Despite the identification and reporting of the wallets, the system architecture and distribution of responsibilities imposed limitations on the available response options:

- Because the application operated under a **non-custodial model**, it had no direct technical or contractual authority to freeze funds, reverse transactions, or block the wallets involved.
- KYC processes and the contractual relationships with end users were handled by the anchors, which operated as independent third parties.
- The application's ability to intervene directly was limited. Its response depended on the available information, internal coordination, and cooperation from the anchors, as well as the measures those parties could take within their respective policies and authority.

### 4. GRC Analysis

| Aspect | Observation | GRC Domain |
|---|---|---|
| Third-party risk | Dependence on anchors for KYC, complaint handling, and the assessment of potential measures affecting accounts and funds. | Third-Party Risk |
| Response capabilities | Direct intervention was limited by the non-custodial architecture and the distribution of responsibilities among the parties involved. | Risk Response |
| Interorganizational coordination | Cooperation among the Argentine anchor, the internal team, and the African anchor facilitated case analysis and reporting. | Governance / Incident Response |
| Fraud detection and investigation | Analysis of the available information and identification of associated wallets supported the investigation and communication of findings to third parties. | Fraud Detection and Investigation |
| Residual risk | Limitations on intervening in funds and accounts persist due to the non-custodial architecture and reliance on third parties. Formal assessment and acceptance of this risk require an explicit governance decision. | Risk Assessment / Risk Treatment |

### 5. Lessons Learned and Recommendations

The case highlighted opportunities to strengthen coordination, traceability, and risk management:

- **Formalize escalation channels:** Establish service-level agreements (SLAs) with anchors for handling suspected or confirmed fraud, including defined response times and prioritization criteria.
- **Standardize documentation:** Establish procedures for recording complaints, preserving relevant information, documenting the identification of wallets associated with potentially illicit activity, and reporting findings to anchors or competent authorities, as appropriate.
- **Evaluate additional detective controls:** Assess the feasibility of implementing alerts based on activity patterns, wallet clustering, and high-risk destinations, taking into account the technical capabilities and limitations of the non-custodial model.
- **Clarify responsibilities:** Develop a RACI matrix specifying who is responsible, accountable, consulted, and informed at each stage of fraud case management.
- **Define residual risk treatment:** Document the structural limitations of the non-custodial model, assess their impact, and establish a formal mechanism through which the appropriate governance body can decide whether to accept the residual risk or require additional mitigation measures.

These measures are recommendations derived from the case analysis and do not imply that the proposed controls or procedures have been implemented.

### 6. Conclusion

This case illustrates the challenges of managing suspected social engineering fraud in a non-custodial financial environment, where direct intervention capabilities are limited and the response depends partly on third parties.

From a GRC perspective, the case provides a practical basis for examining third-party risk management, interorganizational coordination, fraud investigation, and response limitations associated with the system architecture. It also highlights the importance of documenting responsibilities, establishing escalation mechanisms, and distinguishing between identifying residual risk and formally accepting it on behalf of the organization.
