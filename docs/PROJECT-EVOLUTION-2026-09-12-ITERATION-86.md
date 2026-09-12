# Project Evolution — 2026-09-12 — Iteration 86

## Input

User-provided comparison of 10 Minute Mail, Firefox Relay and Apple Hide My Email, followed by verification against current official product documentation.

## Portfolio decision

**Primary project: P115 — OmniPrivacy Identity Relay & Disposable Communications Fabric MAX**

**Classification:** existing-project extension.

**New standalone project:** no.

The source set describes three variants of the same broader communication-privacy domain already owned by P115: disposable mailbox, persistent forwarding mask and platform-integrated email alias.

## Evidence synthesis

### 10 Minute Mail
Official documentation describes a temporary mailbox that expires after approximately ten minutes, with an option to extend the active period. No signup is required. The address and messages are deleted after expiration.

### Firefox Relay
Official documentation describes masked email addresses forwarding to the user's real mailbox, dashboard management, blocking, and additional capabilities such as tracker removal and anonymous replies depending on plan. Relay explicitly distinguishes masks from channels appropriate for critical identity verification.

### Apple Hide My Email
Apple documents random email addresses that forward to the user's personal mailbox, integrated across Safari, Mail, supported apps, Settings and iCloud.com, with deactivation/deletion controls.

## New architectural distinction

P115 must distinguish:

`DISPOSABLE ENDPOINT ≠ PERSISTENT FORWARDING MASK ≠ PLATFORM-INTEGRATED ALIAS`

## New capability dimensions
- mailbox TTL;
- forwarding target;
- send/reply capability;
- account dependency;
- revocation mode;
- retention policy;
- platform binding;
- attachment policy;
- tracker handling;
- promotional filtering.

## New provider-neutral model

`identity_id → channel → provider → endpoint → mode → owner → purpose → TTL → forwarding_target → send_policy → retention → revocation → provenance → audit`

## Product consequence
P115 should expose user intent as a semantic choice: one-time/disappearing, long-term mask, or platform-bound alias. Provider adapters then match actual live capabilities rather than treating every privacy-email provider as equivalent.

## Security / epistemic invariants

`ALIAS ≠ ANONYMITY`

`TEMPORARY ≠ UNTRACEABLE`

`FORWARDING ≠ END-TO-END CONFIDENTIALITY`

`PROVIDER PRIVACY CLAIM ≠ INDEPENDENT AUDIT`

`DISPOSABLE MAILBOX ≠ ACCOUNT RECOVERY CHANNEL`

`MASK ≠ IDENTITY VERIFICATION BYPASS`

`RECEIVED MESSAGE ≠ TRUSTED CONTENT`

## Repository writes

- `docs/knowledge-base/2026-09-12-corpus-disposable-email-masks-10-minute-mail-firefox-relay-apple-hide-my-email.md`
- `projekty/115-omniprivacy-disposable-email-mask-capability-extension-2026-09-12.md`

## Outcome

P115 is materially strengthened as a provider-neutral privacy identity fabric. No new standalone project is justified by this source set.
