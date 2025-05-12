# Risk Register - Canvoy Payments

## Referral programs

| Risk | Description | Mitigation |
|------|-------------|------------|
| Abuse of referral codes | Users create fake accounts to earn referral rewards. | Implement device fingerprinting, fraud detection logic. |
| Information disclosure | Exposure of personal referral links or data | Limit data shared in referral links, use tokens. |
| Spoofing | Impersonating users to misuse referral benefits | Verify user identity during referral credit application. |

## Premium subscription plans

| Risk | Description | Mitigation |
|------|-------------|------------|
| Privilege escalation | Regular users gaining premium access via API manipulation | RBAC checks on backend and subscription status validation. |
| Tampering | Manipulating plan data or pricing | Signed pricing configs, backend validation. |
| Repudiation | Denial of plan upgrades or billing | Detailed transaction logging and user confirmations. |

## Cashback and rewards

| Risk | Description | Mitigation |
|------|-------------|------------|
| Fraud | Users exploiting reward calculations | Cap limits, behavior monitoring, rate limiting. |
| Tampering | Modification of reward points or cashbacks | Secure backend-side reward computation, input validation. |
| Information disclosure | Reward balances leaked between users | Strict access controls and data isolation. |

## Polite/customizable push notifications

| Risk | Description | Mitigation |
|------|-------------|------------|
| Spoofing | Fake notifications mimicking app alerts | Message authenticity via signing and source validation. |
| Denial of Service | Abuse of notification service | Rate-limiting, per-user quota. |
| Information Disclosure | Sensitive data exposed in notifications | Avoid PII in messages, use tokenized language. |
