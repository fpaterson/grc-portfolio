# Third-Party Fraud Escalation in a Non-Custodial Stellar Environment

## 1. Context

During day-to-day operations and user support for a non-custodial financial application built on the Stellar network, the Argentine anchor contacted the internal team after receiving a complaint from a user who had been the victim of a possible fraud (romance scam / social engineering).

The user had been deceived by a third party impersonating a European professional athlete. Based on the information received, the case was identified and joint coordination was initiated.

## 2. Actions Taken

- The complaint received through the Argentine anchor was analyzed.
- All wallets associated with the scammer were identified collaboratively.
- The identified wallets were reported to the corresponding Nigerian anchor so that it could take the measures available under its policies (monitoring, internal restrictions, or further reporting).

## 3. Limitations of the Environment

Despite the identification and reporting:

- As a non-custodial application, there was no technical or contractual ability to freeze funds, reverse transactions, or directly block wallets.
- KYC and the contractual relationship with the end user rested with the anchors (third parties).
- Action was limited to detection, documentation, on-chain identification, and reporting to the involved anchors.

## 4. GRC Perspective Analysis

| Aspect                        | Observation                                                                 | GRC Domain                        |
|-------------------------------|-----------------------------------------------------------------------------|-----------------------------------|
| Third-party risk              | Dependence on anchors for KYC, complaint handling, and possible measures over funds | Third-Party Risk                  |
| Response capability           | Limited to identification and reporting; no control over the assets         | Risk Response                     |
| Inter-organizational coordination | Effective collaboration between the Argentine anchor, internal team, and Nigerian anchor | Governance / Incident Response    |
| Detective controls            | Ability to identify patterns and associated wallets despite the non-custodial model | Fraud Detection & Investigation   |
| Residual risk                 | Elevated by design due to the non-custodial architecture and reliance on third parties. Formal evaluation and acceptance of this risk fall outside the operational scope of the team | Residual Risk                     |

## 5. Lessons Learned and Recommendations

- Formalize escalation channels and SLAs with anchors for confirmed or suspected fraud cases.
- Standardize documentation procedures for identifying wallets linked to illicit activity and reporting them to anchors / authorities.
- Evaluate the need for additional internal detective controls (pattern alerts, wallet clustering, high-risk destination monitoring, etc.).
- Clarify in the RACI matrix which actions the non-custodial application can and cannot take in response to fraud.
- Formally record the residual risk inherent to the non-custodial model and its treatment at the governance level.

## 6. Conclusion

This case illustrates both the real limitations of a non-custodial environment and the importance of effective coordination with third parties (anchors) to mitigate the impact of social-engineering fraud. It serves as a practical example of incident handling, third-party risk management, and control definition in non-custodial blockchain architectures.
