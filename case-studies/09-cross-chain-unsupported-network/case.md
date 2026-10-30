# Case Study: Cross-Chain Withdrawal Incident and Network Compatibility Risk

> **Note:** This is a real yet composite case based on recurring patterns in non-custodial fintech operations. It contains no real customer data, volumes, dates, or provider and partner names. Details have been generalized for portfolio purposes.

- **Domain:** GRC | Operational Risk | Incident Management | Third-Party Risk
- **Industry:** Fintech / Digital Assets
- **Case type:** Anonymized operational incident
- **Framework reference:** ISO/IEC 27001:2022
- **Status:** Closed from our side; destination recovery outcome not confirmed by the receiving provider

## 1. Executive Summary

A customer initiated a USDC withdrawal through a cross-chain transfer interface, with the intended destination being a third-party financial service. The source transaction was confirmed on the Stellar blockchain, but the application continued to display a *Pending User Transfer* status.

The investigation indicated that the destination service's published list of supported USDC deposit networks did not include Base, the network selected for the transfer. The interface already displayed the selected destination network and instructed the user to verify the recipient's network, and the receiving service publishes its supported networks in its documentation. The incident therefore did not stem from a missing control, but from a control that was present and did not prevent the outcome.

This case illustrates three things: the limits of warning-based preventive controls, the gap between on-chain status and application-level status, and the dependence on third parties for recovery. The final recovery outcome was not confirmed at the time of documentation.

## 2. Incident Overview

The investigation established the following facts:

- The source transaction was recorded as successful on Stellar.
- The transaction moved USDC from the originating account to a destination account associated with the cross-chain transfer process.
- The transfer interface continued to display *Pending User Transfer*.
- The intended recipient was a third-party service whose published deposit documentation did not list Base as a supported USDC deposit network.
- The customer was advised to contact the destination service and was given the relevant transaction information.

**Important distinction:** a successful source-chain transaction does not, by itself, establish that the cross-chain transfer has settled or that the destination service has credited the recipient.

## 3. Existing Controls and Effectiveness

| Control | Type | Status | Assessment |
|---|---|---|---|
| Destination network displayed in the withdrawal interface | Preventive | Present | Partially effective. It informs the user but does not check the choice against the destination's capabilities. |
| Instruction to verify the recipient's network before sending | Preventive (directive) | Present | Limited. The warning is generic, not specific to the chosen destination, and relies entirely on user diligence. |
| Receiving service's published list of supported deposit networks | Third-party reference | Available | Effective as a reference, but outside the company's control and not integrated into the flow. |
| Validation of the selected network against the destination's supported networks | Preventive | **Not in place** | Gap. |
| Reconciliation of source-confirmed but still-pending transfers | Detective | **Not in place** | Gap. |

**Key observation:** a control that exists is not necessarily a control that is effective. Generic warnings depend on the user acting on them, so the residual risk remains meaningful even though the control was operating as designed.

## 4. Risk Assessment

Ratings are a qualitative assessment based on this single incident and should be recalibrated with incident volume data.

| Risk | Likelihood | Impact | Rating |
|---|---|---|---|
| R1. Network compatibility | Medium | High | **High** |
| R2. Transaction status inconsistency | Medium | Medium | **Medium** |
| R3. Third-party dependency | Medium | Medium | **Medium** |

**R1. Network compatibility risk.** Sending a digital asset over a network the receiving service does not support may prevent automatic crediting and complicate recovery. Existing controls reduce the likelihood but depend on user attention. Potential impact: temporary or permanent loss of access to funds, manual recovery costs and delays, customer dissatisfaction.

**R2. Transaction status inconsistency.** The source transaction was confirmed on-chain while the application continued to show a pending status. Potential impact: uncertainty about whether the transfer was submitted, duplicate withdrawal attempts or unnecessary support requests, and delayed incident detection.

**R3. Third-party dependency.** Completion and any recovery depend on external providers and on the receiving service's ability to access the assets on the destination network. Potential impact: limited control over recovery timelines, unclear responsibility between providers, and added support workload.

## 5. Incident Response

The response followed a fact-based troubleshooting approach:

1. **Transaction verification:** confirmed that the source transaction succeeded on Stellar.
2. **Transaction identification:** reviewed the transaction details and memo to support investigation by the relevant providers.
3. **Destination assessment:** compared the selected network against the receiving service's published deposit-network documentation.
4. **Evidence package:** gave the customer the transaction details and memo needed for a recovery request.
5. **Customer communication:** advised the customer to contact the receiving service.
6. **Recovery escalation:** left the final recovery determination to the service controlling, or potentially controlling, the destination address.

**Decision on provider contact.** The company did not contact the receiving service directly. Only the account holder can prove ownership of the destination account to that service, and the company has no contractual relationship with it, so a request from the company would likely carry no standing. The company's role was to supply the evidence package. The trade-off is that the company cannot accelerate recovery.

The investigation did not establish that the funds were permanently lost, nor did it confirm recovery.

## 6. Recommended Control Improvements

These build on the existing controls rather than replacing them.

| Improvement | Type | Builds on | ISO/IEC 27001:2022 |
|---|---|---|---|
| Explicit acknowledgment before confirming (checkbox or typed confirmation) | Preventive | Existing network warning | A.8.26 |
| Hard validation or blocking where the destination's supported networks are known | Preventive | Network display | A.8.26 |
| Source and destination status tracking | Detective | Pending status display | A.8.16, A.8.15 |
| Automated reconciliation of source-confirmed but pending transfers | Detective | Gap | A.8.16 |
| Defined escalation procedure with required evidence | Corrective | Existing response steps | A.5.24, A.5.26, A.5.28 |
| Customer communication and recovery-expectation procedure | Corrective | Existing customer advice | A.6.8, A.5.26 |
| Periodic review of supported-network information for common destinations | Preventive | Third-party reference | A.5.19, A.5.22 |

Where automated validation is not feasible, an explicit acknowledgment is a proportionate fallback.

## 7. ISO/IEC 27001:2022 Mapping

| Case element | Clause / Annex A control |
|---|---|
| Risk identification and rating (R1-R3) | Cl. 6.1.2, 8.2 |
| Selection of improvements | Cl. 6.1.3, 8.3 |
| Effectiveness assessment of existing controls | Cl. 9.1 |
| Network display, warning and validation | A.8.26 Application security requirements |
| Status tracking and reconciliation | A.8.15 Logging, A.8.16 Monitoring activities |
| Receiving service and external providers | A.5.19 Supplier relationships, A.5.21 ICT supply chain, A.5.22 Monitoring of supplier services |
| Triage of the event | A.5.25 Assessment and decision on events |
| Incident handling and escalation | A.5.24, A.5.26 |
| Evidence given to the customer and providers | A.5.28 Collection of evidence |
| Customer reporting and communication | A.6.8 Event reporting |
| Lessons learned and corrective action | A.5.27, Cl. 10.1, 10.2 |

*Scope note:* ISO/IEC 27001 centers on information security, so the fit here is strongest for availability and integrity of transactions. The A.8.26 mapping is the loosest and is applied by analogy to transaction integrity.

## 8. Lessons Learned

- Source-chain confirmation and end-to-end payment completion must be treated as separate operational states.
- A warning is not the same as an effective control. Controls should be assessed on whether they change user behavior, not only on whether they exist.
- Visibility into each stage of a cross-chain transfer and defined escalation paths for transfers confirmed at the source but not credited at the destination reduce both detection time and customer uncertainty.
- Verified facts must be kept separate from assumptions. An unsupported destination network is a plausible explanation for the failed credit, but the final cause and recoverability must be confirmed by the relevant providers.

## 9. GRC Relevance

This case demonstrates practical application of:

- Operational risk identification, rating and treatment.
- Evaluation of existing controls, including the difference between control presence and control effectiveness.
- Incident investigation and evidence-based documentation.
- Third-party dependency and service-provider risk analysis.
- Preventive, detective and corrective control design.
- Mapping of findings to ISO/IEC 27001:2022.

The objective is not to assign blame to an individual customer or provider, but to identify control improvements that reduce the likelihood and impact of similar incidents.

---

*Confidentiality note: this case study is anonymized. Customer identifiers, wallet addresses, transaction hashes, internal reference numbers and provider-specific operational details have been excluded. It should be published only if permitted by applicable workplace confidentiality requirements.*
