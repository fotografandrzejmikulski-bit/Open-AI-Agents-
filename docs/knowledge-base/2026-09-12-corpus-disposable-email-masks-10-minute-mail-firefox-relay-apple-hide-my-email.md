# Knowledge Corpus — Disposable Email, Email Masks & Privacy Relay

## Date
2026-09-12

## Classification
Source-derived market/product intelligence + architecture signal.

## Source set
1. User-supplied comparison of 10 Minute Mail, Firefox Relay and Apple Hide My Email.
2. Official 10 Minute Mail pages inspected 2026-09-12.
3. Official Firefox Relay pages inspected 2026-09-12.
4. Official Apple Support documentation inspected 2026-09-12.

## 1. 10 Minute Mail — disposable mailbox
The official 10 Minute Mail FAQ describes a private temporary mailbox whose address and mail self-destruct after 10 minutes. No signup or personal information is required. The service is designed for short-lived verification and registration flows. The FAQ states that the mailbox can receive mail, that verification links can be opened from the inbox, and that the timer can be reset with an additional 10 minutes. The about page describes automatic expiration and deletion and a privacy-oriented in-memory architecture.

Important distinction: this is a **temporary mailbox**, not a long-lived alias forwarding layer. The mailbox itself is the endpoint and disappears after its TTL.

Source: official 10 Minute Mail FAQ/about pages. Exact current implementation/privacy claims remain provider claims and should be treated as source-derived until independently audited.

## 2. Firefox Relay — persistent email mask / forwarding layer
Firefox Relay uses masked/private email addresses that forward messages to a user's real address. The official service describes random email masks, dashboard management, labeling, and the ability to block messages from a mask. Current Relay documentation also describes tracker removal, promotional-email blocking, and anonymous replies for eligible plans. Free accounts currently expose a limited number of masks; paid offerings provide more capabilities.

Relay is therefore a **persistent identity-separation layer** rather than a disposable inbox. A mask can remain active until the user blocks/deactivates it. Relay explicitly warns that masks are not appropriate where strong identity verification or critical correspondence is required, such as banking, medical or legal contexts.

The official FAQ states that forwarded emails may be temporarily stored during service outages, for no longer than three days, and that attachment forwarding has a 10 MB limit.

Source: official Firefox Relay site and FAQ, inspected 2026-09-12.

## 3. Apple Hide My Email — platform-integrated alias layer
Apple's Hide My Email, available with iCloud+, generates unique random email addresses that forward to a user's personal email account. Apple documents use from Safari, Mail, Apple Pay, supported third-party apps, Settings and iCloud.com. Addresses can be labeled/noted and deactivated or deleted.

The key architectural property is **platform-integrated identity masking**: the alias is generated inside the Apple ecosystem and remains associated with the user's Apple/iCloud account rather than acting as a ten-minute anonymous mailbox.

Apple's documentation also states that replies can preserve the privacy of the personal address by appearing to originate from the generated Hide My Email address.

Source: official Apple Support documentation, inspected 2026-09-12.

## Comparative model

| Class | Example | Primary endpoint | Lifetime | Forwarding | Account required | Best-fit use |
|---|---|---|---|---|---|---|
| Disposable mailbox | 10 Minute Mail | Temporary inbox | ~10 min by default | No | No | One-time verification / low-value signup |
| Email mask / relay | Firefox Relay | User's real inbox via mask | Persistent until revoked | Yes | Yes | Long-term exposure reduction / spam control |
| Platform alias | Apple Hide My Email | User's personal inbox via Apple alias | Persistent until deactivated | Yes | iCloud+ / Apple Account | Integrated privacy during forms, apps and email |

## Architecture insight
These are not interchangeable implementations. The market contains at least three distinct privacy primitives:

`DISPOSABLE ENDPOINT`
`PERSISTENT FORWARDING MASK`
`PLATFORM-INTEGRATED ALIAS`

A provider-neutral privacy fabric must model them as separate capability classes rather than one generic "temporary email" feature.

## P115 impact
This corpus strengthens **P115 — OmniPrivacy Identity Relay & Disposable Communications Fabric MAX**, which already owns provider-neutral email masks, disposable communication endpoints, lifecycle management, routing, provenance, consent and deletion controls. P115 therefore remains the correct project boundary; no new standalone project is warranted.

## New P115 capability dimensions
- `mailbox_ttl` — explicit expiration semantics.
- `forwarding_target` — whether mail is delivered to a persistent mailbox.
- `send_capability` — receive-only vs reply/send-through-mask.
- `account_dependency` — anonymous session vs authenticated identity.
- `revocation_mode` — automatic expiry vs user-controlled deactivation/blocking.
- `retention_policy` — ephemeral deletion vs provider-defined persistence.
- `platform_binding` — provider-neutral vs ecosystem-bound alias.
- `attachment_policy` — supported size/type constraints.
- `tracker_handling` — pass-through vs tracker removal.
- `promotional_filtering` — optional relay-level suppression.

## Security / epistemic controls
- `ALIAS ≠ ANONYMITY`
- `TEMPORARY ≠ UNTRACEABLE`
- `FORWARDING ≠ END-TO-END CONFIDENTIALITY`
- `PROVIDER PRIVACY CLAIM ≠ INDEPENDENT AUDIT`
- `DISPOSABLE MAILBOX ≠ SUITABLE ACCOUNT RECOVERY CHANNEL`
- `MASK ≠ IDENTITY VERIFICATION BYPASS`
- `RECEIVED MESSAGE ≠ TRUSTED CONTENT`

## Product opportunity signal
A stronger OmniPrivacy product should not compete merely on "temporary email." It should expose a unified **identity lifecycle abstraction** across disposable mailboxes, persistent email masks, platform aliases, secondary numbers and VoIP identities while preserving the semantics of each provider class.

## Recommended canonical data model
`identity_id → channel → provider → endpoint → mode → owner → purpose → TTL → forwarding_target → send_policy → retention → revocation → provenance → audit`

## Evidence status
- 10 Minute Mail product behavior: official-source-derived.
- Firefox Relay current features/limits: official-source-derived and time-sensitive.
- Apple Hide My Email current behavior: official-source-derived and time-sensitive.
- Comparative architecture: model synthesis from the sources.
- Market demand / profitability: not established by this corpus alone.
