# Case Study: Payer–Account Holder Mismatch and KYB Refusal

**Note:** This is an illustrative, composite case based on a recurring pattern in non-custodial fintech operations. It contains no real customer data, volumes, dates, or partner names. Details have been generalized for portfolio purposes.

## 1. Context

A non-custodial payments application relies on a regulated third-party partner (the *anchor*) to handle fiat on/off-ramps and customer due diligence. Users complete onboarding with the anchor as **individuals** (KYC).

A recurring pattern emerges: some users fund their transactions from a **business bank account** (for example, an LLC or similar legal entity) while being registered only as individuals. The payer of record does not match the customer of record.

## 2. Red Flags Identified

- The name on the originating bank account differs from the registered customer.
- Funds appear to originate from a legal entity, but the profile has no business relationship on file.
- Business and personal funds are potentially commingled.
- Refusal to complete additional verification when asked.

These are **indicators that require due diligence**, not proof of wrongdoing. In many cases the cause is convenience, tax structuring, or unawareness of the difference between KYC and KYB.

## 3. Observed Behavior

When asked to open a separate business account and complete KYB with the anchor, a significant share of users decline and request an immediate refund instead. Declining to provide business verification, combined with the corporate origin of the funds, raises the case's risk profile. The anchor may then escalate under its own regulatory reporting obligations and decide whether to return or hold the funds according to its policy.

## 4. Risk Assessment

| **Risk** | **Likelihood** | **Impact** | **Rating** |
| :--- | :-: | :-: | :-: |
| Incomplete due diligence (KYC applied where KYB is required) | High | Medium | High |
| Commingling of personal and business funds / misuse of corporate structure | Medium | Medium | Medium |
| Circumvention of onboarding controls | Medium | High | High |
| Regulatory and reputational exposure for the app and the anchor | Medium | High | High |
| Money laundering (unconfirmed, indicator-based) | Low | High | Medium |

*Ratings are qualitative and illustrative.*

## 5. Control Gaps

1. **Detection happens after the deposit**, not at onboarding. The mismatch is found reactively.
2. **No upfront declaration** of expected source of funds or intended use (personal vs business).
3. **Limited automated name matching** between the originating account holder and the registered customer.
4. **Unclear ownership of the decision** between the app and the anchor when a user refuses KYB.

## 6. Recommended Controls

**Preventive**

- Ask at onboarding whether funds will come from a personal or business account, and route business users to KYB from the start.
- Show clear in-app messaging: the sender's name must match the registered account holder.

**Detective**

- Automated payer-name vs customer-name matching on incoming deposits.
- Alerts for repeated mismatches or business-looking payer names on personal profiles.

**Corrective**

- A documented playbook for mismatches: request, deadline, escalation, refund or hold.
- Clear criteria for when the case moves from support to compliance review.

## 7. Escalation Workflow

1. **Detect** a mismatch between the payer of record and the registered customer.
2. **Request** that the user open a business account and complete KYB, with a clear explanation and deadline.
3. **Assess** the response. If the user completes KYB, process normally.
4. **Escalate** to the anchor and compliance if the user refuses or the explanation is inconsistent.
5. **Resolve** according to the anchor's policy (refund, hold, or further review). The app does not inform the user of any regulatory reporting decision.

## 8. Key Risk Indicators (KRIs)

- Percentage of deposits with a payer/customer name mismatch.
- Percentage of mismatches resolved through KYB completion vs refusal.
- Average time from detection to resolution.
- Number of cases escalated to the anchor per period.

## 9. Alignment with Recognized Standards (Retrospective)

The controls in this case come from operational experience and practical risk management, not from a formal framework. Reviewed afterwards, they are consistent with widely used standards:

- **FATF Recommendation 10 (customer due diligence):** matching the payer to the customer of record, and verifying the business when funds come from an entity.
- **FATF Recommendation 20 (suspicious transaction reporting):** escalation to the regulated partner when a user refuses verification.
- **FATF Recommendation 24 (transparency of legal persons):** relevant to verifying the business behind the funds.
- **Anchor's internal policy:** governs refunds, holds, and reporting decisions.

This mapping is illustrative and is not a compliance assessment.

## 10. Lessons Learned

- Source-of-funds checks are most effective at onboarding, not after the first deposit.
- Treating a mismatch as a risk indicator, not an accusation, keeps the process fair and defensible.
- Clear ownership between the app and the regulated partner avoids delays and inconsistent decisions.
- Confidentiality of regulatory reporting must be built into support scripts to avoid disclosing it to the user.
