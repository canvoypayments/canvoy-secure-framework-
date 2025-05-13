# Threat Models - Canvoy Payments MVP Features

## Core Bill Payment Functionality

**Description**: Allows users to initiate and complete bill payments to connected service providers.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | Fake users impersonating real accounts | Strong authentication (MFA), rate limiting, session management |
| Tampering | Modification of payment amount or recipient data | Input validation, integrity checks, HMAC on API requests |
| Repudiation | Users deny making payments | Secure logging with non-repudiation measures (e.g., digital signs) |
| Information Disclosure | Leakage of payment or PII data | TLS 1.3, encryption at rest, strict access control policies |
| Denial of Service | Bot traffic or repeated failed transactions causing outages | CAPTCHA, WAF, rate-limiting |
| Elevation of Privilege | Low-privilege users accessing admin billing tools | RBAC enforcement, least privilege access control |


## Secure Authentication

**Description**: Authentication mechanism used to verify user identity.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | Password brute-force, session hijacking | MFA, account lockouts, session timeout, secure cookie flags |
| Tampering | Manipulation of login payloads or session tokens | JWT signature verification, input sanitization |
| Repudiation | Denial of login or logout actions | Audit trail logs |
| Information Disclosure | Exposure of credentials or tokens in transit | HTTPS only, avoid token in URL, secure headers |
| Denial of Service | Account lockout abuse or authentication API overload | Rate-limiting, progressive delays, monitoring |
| Elevation of Privilege | Access token misuse to impersonate higher-level roles | Token scope control, RBAC |


## Automated Reminders

**Description**: Push/email notifications to remind users about due payments.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | Fake reminders crafted to phish users | Message signing, verified domains |
| Tampering | Reminder data manipulated to send wrong info | Input validation, signed payloads |
| Repudiation | Claims of not receiving or receiving incorrect reminders | Logged delivery confirmations |
| Information Disclosure | Email or phone info exposed in reminders | Use masked PII, minimal info sharing |
| Denial of Service | Abusing reminder API to flood users | Throttling, abuse detection |
| Elevation of Privilege | Unauthorized users sending reminders | Auth checks before sending reminders |


## Payment History

**Description**: Display of a user’s past transactions.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | Viewing another user’s transaction history | Strict session/token validation |
| Tampering | Modifying past transaction records | Write-once transaction logs, digital signatures |
| Repudiation | Users deny making certain transactions | Time-stamped, signed logs |
| Information Disclosure | Access to other users' payment records | Access control by session, encryption of stored records |
| Denial of Service | Repeated access causing history system lag | Pagination, API rate limits |
| Elevation of Privilege | Standard users accessing admin views of history | Role-based access enforcement |


## Multiple Payment Methods

**Description**: Support for cards, wallets, bank transfers, etc.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | Impersonation to register unauthorized payment method | Verify ownership via OTP or token |
| Tampering | Payment method data altered | Field-level validation, signed sessions |
| Repudiation | Claims of not adding/removing a method | Logging of each payment method change |
| Information Disclosure | Exposure of stored card/bank info | Tokenization, vault-based storage, PCI compliance |
| Denial of Service | Flooding system with method additions/removals | Input throttling, backend validation |
| Elevation of Privilege | Unauthorized access to sensitive payment setup | Auth scopes, ownership checks |


## In-App Customer Support

**Description**: Real-time or asynchronous support via chat or form.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | Fake users impersonating others in chat | Session validation, user identity display |
| Tampering | Altering of chat logs or support messages | Immutable logs, message signing |
| Repudiation | Denial of having requested support or specific responses | Full audit trail with timestamps |
| Information Disclosure | Leakage of sensitive conversation content | TLS, data minimization, redaction automation |
| Denial of Service | Spam support messages | Captcha, message rate limits |
| Elevation of Privilege | Gaining access to other users' support sessions | Session/user context checks |


## Microservices Backend Setup

**Description**: Microservices architecture handling different responsibilities.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | One service impersonating another | mTLS between services, service identity |
| Tampering | Malicious service altering payloads | JWT/HMAC, signed inter-service messages |
| Repudiation | Denial of internal service calls | Logging all service-to-service requests |
| Information Disclosure | Leaking data between services due to improper boundary control | Strict API definitions, zero-trust between services |
| Denial of Service | Service overload by other services or external threats | Circuit breakers, quotas, service mesh policies |
| Elevation of Privilege | One service gaining access to unauthorized resources | Principle of least privilege, scoped service permissions |


## Compliance & UAT

**Description**: Regulatory testing and compliance review environment.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | Fake users simulating test activity | Secure test user management |
| Tampering | Altering test results to bypass compliance | Signed test logs, immutable result storage |
| Repudiation | Disputes over who ran/approved tests | Auditable logs with sign-offs |
| Information Disclosure | Real data used in UAT | Anonymize data, strict access control |
| Denial of Service | Overuse of test environment | Resource throttling |
| Elevation of Privilege | Testers accessing prod or sensitive configuration | Environment isolation, RBAC |


## Utility Partnerships

**Description**: Integration with third-party utility service providers.


| Threat Category | Potential Threats | Mitigations |
|----------------|-------------------|-------------|
| Spoofing | Fake utility providers injecting payment requests | Whitelisting, provider verification |
| Tampering | Altering API payloads between partners | Signed requests, endpoint authentication |
| Repudiation | Disputes over partner transactions | Partner-side logging, transaction tracing |
| Information Disclosure | Shared data leaked to unverified endpoints | Encrypt sensitive fields, minimum necessary sharing |
| Denial of Service | Malfunction or abuse from partner systems | Timeouts, circuit breakers, redundancy |
| Elevation of Privilege | Partner accessing broader user data than allowed | Access scoping per partner |


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


## Advanced Analytics

**Description**: Feature that provides insights into user behavior and data usage, which may pose privacy risks.

| Threat Category        | Potential Threats                                              | Mitigations                                |
|------------------------|----------------------------------------------------------------|---------------------------------------------|
| Information Disclosure | Unauthorized access to user behavioral data                   | Data anonymization and strict access control |


## AI Recommendation Engine

**Description**: Intelligent system for personalizing user experience, vulnerable to manipulation and integrity threats.

| Threat Category | Potential Threats                                      | Mitigations                             |
|-----------------|--------------------------------------------------------|------------------------------------------|
| Tampering       | Malicious manipulation of AI-generated recommendations | Input validations and integrity checks   |


## Interface in Nigerian Languages

**Description**: Multilingual support for users in Nigeria, with risks related to communication accuracy and legal clarity.

| Threat Category | Potential Threats                                                   | Mitigations                                          |
|-----------------|---------------------------------------------------------------------|------------------------------------------------------|
| Repudiation     | Users denying actions due to mistranslation or misunderstanding     | Legal wording and UX testing in native languages     |
