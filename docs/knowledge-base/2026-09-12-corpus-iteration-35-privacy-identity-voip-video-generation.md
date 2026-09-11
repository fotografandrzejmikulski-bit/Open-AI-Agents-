# Knowledge Corpus — Iteration 35

Date: 2026-09-12
Repository: mojealterego/Knowledge-projects

## Source clusters

### A. Privacy-preserving alternate communications identity
Sources supplied by the user include 2nr, GetCode, Google Voice, MoreMins, Surfshark Alternative Number/ID material, TextNow/TextMe, Firefox Relay, Hide My Email, DuckDuckGo Email Protection, YOPmail, 10 Minute Mail, Zadarma, Ringostat, Bitrix24/Actio references and related VoIP material.

Observed capability classes:
- temporary or secondary phone numbers without a physical SIM;
- inbound/outbound calling and SMS depending on provider;
- multiple identities on one device;
- time-window activation and user-controlled deletion in 2nr;
- business virtual numbers and cloud PBX;
- email aliases/masks and forwarding;
- temporary disposable mailboxes;
- separation of private and public/business contact identities;
- privacy-oriented forwarding and tracker removal;
- call routing, IVR, recording, analytics and CRM integration in business VoIP platforms.

2nr explicitly describes up to three additional numbers on one smartphone, configurable names/colors and activation schedules, and use for classifieds, work and online privacy. It also states that it is not a substitute for a primary telecom number and does not provide emergency calling. Source: https://drugi-numer.pl/.

GetCode describes virtual numbers from 60+ countries and SMS verification workflows for popular platforms. This material is retained as a market/capability witness; operational account-verification automation is not promoted into the public engineering substrate. Source: Apple App Store listing supplied by the user.

MoreMins describes SIM-free virtual numbers, multiple simultaneous numbers, calling/SMS and country selection. Source: https://www.moremins.com/.

Firefox Relay provides email masks forwarding to a real mailbox and explicitly warns against using masks where identity verification or critical correspondence is required. Premium material also describes phone masking availability by region. Source: https://relay.firefox.com/.

DuckDuckGo Email Protection provides unique private email addresses and tracker stripping while forwarding to an existing inbox. Source: https://duckduckgo.com/duckduckgo-help-pages/email-protection/.

YOPmail and 10 Minute Mail represent disposable mailbox models with intentionally short-lived or low-identity email access. These are useful as privacy-pattern witnesses, not as identity-verification bypass mechanisms.

Ringostat represents the business/cloud-PBX branch: virtual numbers, SIP/VoIP, IVR, routing, recording, analytics, SMS and CRM integrations. Source: https://ringostat.com/.

### B. VoIP engineering and defensive security
The supplied GitHub VoIP topic points to open-source softphones, RTP abstractions, PBX/call-center systems and defensive VoIP fraud detection. Recent examples include a PHP/Swoole web softphone, SentryPeer fraud detection, and other SIP/VoIP projects. The topic also contains offensive caller-ID spoofing/scam-bot research; that content is retained only as threat-model context and not as an operational capability.

### C. Current image-to-video/video-generation ecosystem
The supplied GitHub topics were inspected for current repositories. Relevant current signals include:
- HunyuanCustom for multimodal/customized video generation;
- HunyuanPortraitLCM for portrait/talking-avatar generation;
- OpenS2V-Nexus as a subject-to-video benchmark/dataset;
- gflow-cli for scripted/batched Google Flow control with an MCP server (unofficial/alpha);
- ViMax for agentic video generation with director/screenwriter/producer/generator roles;
- Duix-Avatar for offline digital-human/video generation;
- video-shotcraft for agent skills, cinematic shot recipes and Remotion workflows;
- vllm-omni for omni-modal inference.

These are evolution inputs to P97/P113, not a separate project boundary in this iteration.

## Epistemic / safety handling
- Provider marketing claims are source claims until independently benchmarked.
- Temporary-number and disposable-email capabilities are classified as privacy/identity-separation patterns.
- Account-verification automation, bulk activation and anti-abuse bypasses are not converted into operational recipes.
- Caller-ID spoofing/scam automation is defensive threat-model input only.
- GitHub topic freshness is a discovery signal, not proof of software quality or production readiness.
