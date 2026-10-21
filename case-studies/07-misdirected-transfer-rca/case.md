# Case Study: Misdirected Transfer Complaint and Root Cause Analysis

> **Note:** This is a real yet composite case based on recurring patterns in non-custodial fintech operations. It contains no real customer data, wallet addresses, transaction hashes, volumes, dates, or partner names. Details have been generalized for portfolio purposes.

## 1. Context

In a non-custodial remittance application built on the Stellar network, a customer reported that he had tried to send crypto to a specific external address, but the application had sent it to a different one. He supplied a screenshot of the address he intended to use and pointed to a blockchain explorer entry showing another address as the recipient.

The initial reading was ambiguous: it could have been an application defect, a compromised account, a user error, or a manipulated screenshot. This required a structured investigation to determine the root cause, rule out fraud, and manage customer communication.

## 2. Initial Claim and Red Flags

- The customer's own wallet screen labeled the operation as a *send by link*, not as a withdrawal to an external address.
- The explorer showed a transfer to an address that matched neither the address in the screenshot nor the address in the customer's wallet history.
- The customer's account was receiving unsolicited micro-transactions carrying phishing-style messages (fake "airdrop" and "staking" links). This is consistent with **address-poisoning / dusting attacks** and made a fraud hypothesis worth ruling out.

## 3. Investigation and Hypotheses Testing

| Hypothesis | Evidence Needed | Result |
|---|---|---|
| The app altered the destination | Compare the signed transaction with the customer's inputs | Not supported. A transaction on this network has a single destination, and nothing was altered after signing. |
| The customer sent the link to the wrong person | Check whether anyone had opened or claimed the link | Not supported. The link was unclaimed and the funds were untouched. |
| The screenshot was edited | Compare the screenshot with the on-chain data | Not supported. Amount, time, and operation matched the on-chain record. |
| Compromised account or leaked link | Review claim logs and account activity | Not supported. No claim, no unusual movement. The dust transactions looked like opportunistic spam. |
| The customer used a different feature than intended | Inspect the transaction structure and the memo field | **Supported.** See section 4. |

## 4. Root Cause

The transaction was created through the **"send by link" feature**, which moves the funds into a temporary account controlled by the platform's recovery process. They stay there until the recipient opens the link or the sender cancels it. The destination on the blockchain was therefore the temporary account, not an address chosen by the customer.

The address the customer believed he had sent to was not a destination at all. It appeared in the **memo field** of the transaction. The customer wanted to withdraw to his own external wallet, selected the link feature instead of the standard send option, and pasted his wallet address into the description (memo) field. Engineering identified this pattern from the transaction data, and it matched the customer's own screenshots.

**Classification:** User error. A mitigating control (an explanatory text on the send screen) was already live, having been implemented following a recommendation from the Product Owner (the author of this case study), but it did not prevent the error. Not a defect in transaction handling, and not fraud.

## 5. GRC Analysis

| Aspect | Observation | GRC Domain |
|---|---|---|
| Incident Triage | The ability to distinguish between an app defect, a fraud attempt (address poisoning), and user error based on evidence rather than assumptions. | Incident Response / Fraud Detection |
| Control Effectiveness | A preventive UX control (informational text) existed but was insufficient. It describes the feature but does not explain that funds leave the balance immediately and are held until claimed. | Security Controls / Risk Treatment |
| Communication & Customer Trust | Handling a complaint without admitting fault or blaming the customer, focusing on education and resolution. | Governance / Customer Compliance |
| Documentation & Evidence | Preserving logs and reviewing on-chain data to avoid misclassification of the incident and to support the final decision. | Auditability / Record Keeping |

## 6. Control Gaps

| Gap | Type | Observation |
|---|---|---|
| Explanatory text on the send screen | Preventive (UX) | Existing but limited. It does not state that funds leave the sender's balance immediately and are held until claimed or cancelled. |
| No confirmation step summarizing the outcome | Preventive (UX) | The customer's mental model did not match the feature. A confirmation screen stating "Funds leave your balance now" was missing. |
| Help content was outdated | Detective / Documentation | It happened to still match the app, but the match was not verified until this case. |
| Diagnosis depended on blockchain-level knowledge | Detective (Process) | A first-line agent could easily misclassify this as an app defect or a security breach. |
| Premature customer communication | Process Risk | Replied to the customer based on inference before engineering confirmed the diagnosis. While correct in this instance, premature communication in incident response can lead to reputational damage if the initial diagnosis is wrong. |

## 7. Recommendations

- **Strengthen the existing control:** Extend the explanatory text to clarify that funds leave the balance immediately and are held until claimed or cancelled. Label the memo field explicitly as *not* a destination.
- **Add a confirmation screen:** Show a clear prompt when creating a link: *"Funds leave your balance now and are held until the link is claimed or you cancel."*
- **Surface the alternative:** Offer a prompt in the link flow such as *"Want to send to an external wallet? Use Withdraw."*
- **Build a triage checklist:** Create a standard operating procedure for "wrong address" complaints: identify the feature used, the transaction type, whether the link was claimed, and what the memo contains before concluding anything.
- **Review help articles on a schedule:** Test the documented flows to ensure accuracy.
- **Verify before replying:** When a customer response depends on a technical assumption, wait for engineering confirmation or label the response as provisional.
- **Track the pattern:** Count similar complaints to decide whether the UX change is a priority.

## 8. Alignment with Recognized Standards (Retrospective)

The controls and triage process in this case come from operational experience, not from a formal framework. Reviewed afterwards, they are consistent with:

- **NIST CSF:** RS.MA (Incident Management), RS.AN (Incident Analysis), RS.CO (Incident Response Reporting and Communication).
- **ISO/IEC 27001:** A.5.24 (Information security incident management planning and preparation), A.5.26 (Response to information security incidents), A.8.11 (Data masking - relevant to avoiding exposure of PII in support interactions).

*This mapping is illustrative and is not a compliance assessment.*

## 9. Lessons Learned

- A customer's claim and his evidence can both be honest and still describe different things. The wallet screen, the explorer, and the memo field each showed a different "address".
- A control that exists is not necessarily effective. Informational text is easy to skip, so measure whether it reduces incidents and consider stronger controls (like a confirmation step or added friction) where the cost of an error is high.
- Customers rarely acknowledge a mistake once it is explained. Define closure by what the company controls (correct diagnosis, instructions delivered, evidence kept), not by an admission.
- Separate what is **proven** from what is **inferred**. Key permissions on an account show what is technically possible, not what the customer can actually do.
- Rule out fraud and defects with evidence before classifying a complaint as user error, and avoid blame in the reply even when user error is likely.
- Small interface ambiguities in financial flows create disproportionate support, trust, and compliance costs.

## 10. Conclusion

This case illustrates the challenges of incident triage and root cause analysis in a non-custodial environment, where claims of technical failure or fraud must be separated from user error through on-chain evidence and structured investigation.

From a GRC perspective, the case highlights the importance of testing control effectiveness, the risk of premature customer communication, the need to rule out address-poisoning attacks, and how UI/UX ambiguities can create real operational and compliance overhead. It also demonstrates a disciplined approach to complaint handling: proportionate escalation, evidence-based diagnosis, and closure defined by company-controlled outcomes rather than customer admission.
