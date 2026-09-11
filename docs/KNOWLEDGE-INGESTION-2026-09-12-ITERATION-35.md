# Knowledge Ingestion — Iteration 35

## Status
COMPLETE

## Source batch
User supplied a mixed source set covering virtual/temporary phone numbers, email masking/disposable mail, VoIP/cloud telephony, a public GitHub profile/topic set, and current image-to-video/video-generation repositories.

## Deduplication
- MoreMins links are one provider family; multiple URLs are consolidated as one capability witness.
- Zadarma, FCN and repeated GitHub topic URLs are consolidated as VoIP ecosystem witnesses.
- 10 Minute Mail is represented once despite repeated naming/linking.
- Firefox Relay and Mozilla Relay naming are one lineage.
- GitHub image-to-video/video-generation topic pages overlap heavily and are treated as discovery indexes rather than separate sources.
- romantut1988 repositories are treated as a corpus/market-research signal, not as one project per repository.

## Decisions
1. Create P115 for the privacy-preserving alternate-identity communications boundary.
2. Evolve P95 with communication-identity separation and privacy-resilient contact surfaces, without turning P95 into a telecom provider.
3. Evolve P112 with optional user-controlled communication aliases as a companion privacy capability, while keeping P112's core companion boundary intact.
4. Evolve P111/P100 with a provider-neutral communications connector contract, subject to authorization and policy gates.
5. Evolve P108 with defensive tests for identity-provider abuse, disposable-channel risk, caller-ID spoofing and unsafe verification automation patterns.
6. Evolve P97/P113 with the current image-to-video/video-generation ecosystem signals; no new visual-generation project is justified because P97/P113 already own production and compilation boundaries.
7. Treat GitHub topic freshness as discovery evidence only; repository quality requires independent inspection and reproducible benchmarks.

## Safety classification
The repository corpus contains material that can be used for legitimate privacy and communication separation, but some services and repositories also describe account verification, spoofing or automation. Public KB retains architectural/privacy patterns and defensive threat models only. It does not operationalize bulk account activation, bypasses, fraud, caller-ID spoofing or credential/session extraction.
