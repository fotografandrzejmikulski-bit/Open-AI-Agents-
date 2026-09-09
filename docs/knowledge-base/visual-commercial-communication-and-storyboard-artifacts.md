# Visual Commercial Communication & Storyboard Artifacts

## Evidence classification

`SOURCE_DERIVED → INFERRED`

This artifact records reusable structure extracted from the supplied CMYK outdoor-advertising offer and the supplied multipanel comic/storyboard. It preserves factual inventory separately from design inferences.

## 1. Outdoor advertising inventory pattern

The supplied CMYK offer documents billboard inventory in the Cieszyn area and nearby Goleszów route. The material identifies at least 18 numbered advertising positions and repeatedly presents the operator contact point as Cieszyn, ul. Bielska 61A.

Observed locations include:

- positions 1–5 — Cieszyn, ul. Bobrecka / PKS;
- position 6 — Cieszyn, ul. Bielska / MDM;
- positions 7–8 — Cieszyn, ul. Bielska at the Bielska–Stawowa intersection and its second location;
- positions 9–10 — Cieszyn, ul. Katowicka, near the market and toward the cemetery;
- positions 11–12 — Goleszów, route Ustroń–Cieszyn;
- positions 13 — Goleszów, route Cieszyn–Ustroń;
- positions 14–15 — Cieszyn, ul. Wyższa Brama I and II;
- positions 16–17 — Cieszyn, ul. Katowicka / cemetery area;
- position 18 — Cieszyn, ul. Bielska.

The supplied visual pages use photographs of the actual roadside environments with the advertising surfaces overlaid or highlighted. This is useful evidence for a future inventory system because each advertising asset can be modeled as a location-bound commercial capability rather than merely an image.

## 2. Billboard inventory data model

A reusable representation is:

```text
AdvertisingPosition
 ├─ position_id
 ├─ locality
 ├─ street_or_route
 ├─ landmark_context
 ├─ direction_of_travel
 ├─ physical_dimensions
 ├─ visibility_notes
 ├─ source_image
 ├─ availability_status
 ├─ campaign_id
 ├─ price
 └─ evidence_timestamp
```

The supplied offer does not provide all of these fields. Missing values must remain unknown rather than inferred from photographs.

## 3. Commercial decision layer

A future advertising-management system can separate:

`INVENTORY → AUDIENCE / TRAFFIC ASSUMPTION → CAMPAIGN → CREATIVE → PLACEMENT → MEASUREMENT → OUTCOME`.

A billboard photograph proves the existence or appearance of a position at the time represented by the source. It does not, by itself, prove current availability, traffic volume, price, conversion rate or campaign performance.

## 4. Visual communication principles extracted from the material

The offer demonstrates a useful sales pattern:

1. identify the medium immediately;
2. expose the geographic context visually;
3. number each asset for unambiguous reference;
4. associate the physical asset with a direct contact path;
5. keep the location description adjacent to the image.

For an AI-assisted commercial catalog, the numbered identifier should remain canonical and should not be replaced by an LLM-generated descriptive name.

## 5. Multipanel storyboard structure

The supplied comic is a multipanel narrative artifact using repeated visual motifs, short Polish captions and recurring characters. Its pages alternate between environment establishing shots, character-focused frames and short narrative statements.

The extracted panels establish a reusable sequence architecture:

```text
WORLD / ATMOSPHERE
      ↓
MYSTERY / HOOK
      ↓
ENVIRONMENT REVEAL
      ↓
CHARACTER INTRODUCTION
      ↓
ANOMALY / CONFLICT
      ↓
DISCOVERY
      ↓
ESCALATION
      ↓
COLLABORATION / CHOICE
      ↓
TRANSFORMATION / RESOLUTION HOOK
```

The supplied visual pages repeatedly use city-scale establishing imagery before narrowing to character and object detail. This creates a cinematic rhythm suitable for digital comics, promotional storyboards and interactive narrative interfaces.

## 6. Panel schema

A machine-readable storyboard representation can use:

```text
Panel
 ├─ panel_id
 ├─ page_id
 ├─ image_asset
 ├─ characters
 ├─ location
 ├─ action
 ├─ dialogue
 ├─ narration
 ├─ emotional_state
 ├─ visual_focus
 ├─ continuity_refs
 └─ next_state
```

The important engineering invariant is separation between visual evidence and generated interpretation. Character state, narrative causality and continuity should be explicit rather than reconstructed from filenames.

## 7. Narrative continuity

A storyboard system should maintain a continuity graph:

```text
CHARACTER
   ↕
LOCATION
   ↕
OBJECT / ARTIFACT
   ↕
EVENT
   ↕
EMOTIONAL / NARRATIVE STATE
```

This prevents a later generated panel from silently changing established character properties, locations or causal relationships.

## 8. Portfolio integration

The commercial-advertising component is relevant to Projects 45, 46 and 56. The storyboard component is relevant to Projects 40, 45, 46, 53 and 57.

The combined opportunity is a governed **Visual Commercial Artifact Pipeline** that can ingest real-world advertising inventory and creative narrative assets, preserve provenance, generate campaign variants and measure outcomes without confusing generated imagery with evidence of physical placement.

## 9. Evidence invariants

1. A photographed advertising position is evidence of the represented scene, not proof of current availability.
2. Location, price, dimensions and traffic must remain separate fields.
3. Generated creative must be marked as generated.
4. Canonical asset identifiers must remain stable.
5. Storyboard continuity is stateful and should be validated across pages.
6. Narrative interpretation must remain distinct from visual observation.
7. Commercial performance claims require measured campaign evidence.
