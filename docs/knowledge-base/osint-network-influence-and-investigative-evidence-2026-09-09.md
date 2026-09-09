# OSINT Network Influence & Investigative Evidence — 2026-09-09

## Status

`SOURCE_DERIVED → ENGINEERING_SYNTHESIS → PROPOSED`

This artifact consolidates the newly supplied Deep OSINT, Deepsearch and investigative-report materials into a reusable evidence methodology. It does not treat allegations, inferred relationships or search absence as established facts.

## 1. Investigation as a typed graph

A person, organization, company, public institution, event or document is represented as a node. Relationships are typed rather than flattened into an undifferentiated "connection".

```text
PERSON
 ├── PERSON: mentor / ally / rival / associate
 ├── ORG: employee / officer / owner / contractor
 ├── COMPANY: shareholder / director / beneficial-interest candidate
 ├── PUBLIC BODY: office / appointment / procurement / program
 ├── FAMILY: documented family relation
 └── DOCUMENT: source / allegation / record / observation
```

The supplied Deepsearch prompt explicitly proposes mapping key people, business structures, political/public functions and family relationships. The engineering interpretation is an evidence graph in which each edge requires its own provenance and confidence rather than inheriting certainty from adjacent nodes.

## 2. Influence-map dimensions

A network investigation should separately model:

1. **Key people** — mentors, sponsors, allies, rivals and recurring associates.
2. **Business structures** — direct and indirect capital relationships, common boards and shared officers.
3. **Political/public sphere** — public functions, party roles, publicly documented political financing and institutional positions.
4. **Family/business/public overlap** — documented family relationships and roles held by relatives.
5. **Temporal dimension** — when the relationship existed and whether it is current, historical or disputed.

A graph edge is therefore closer to:

```yaml
Edge:
  subject:
  predicate:
  object:
  valid_from:
  valid_to:
  source:
  source_type:
  evidence:
  confidence:
  counterevidence:
  status: observed|reported|inferred|verified|disputed
```

## 3. Negative findings are evidence objects, not conclusions

The supplied investigative report repeatedly demonstrates a useful pattern: a search can produce a documented negative finding. For example, the report describes searches across public/commercial databases, staff lists and historical/current registry records and reports no formal connection for the investigated person.

The reusable rule is:

`NO_RESULT ≠ PROOF_OF_NONEXISTENCE`

Instead:

`SEARCH_SCOPE + SOURCES + TIME + QUERY_SPACE + RESULT = DOCUMENTED_NEGATIVE_FINDING`

This distinction prevents an OSINT system from converting incomplete visibility into categorical claims.

## 4. Chronology as an evidence structure

Narrative reports often contain a sequence of events, observations, allegations, third-party statements and attached evidence. The system should decompose them into atomic timeline records:

```yaml
Event:
  event_id:
  date_or_interval:
  actor:
  action:
  location:
  claim_type: direct_observation|third_party_report|documented_record|allegation
  source:
  corroboration:
  contradiction:
  confidence:
```

This prevents a long narrative from silently upgrading hearsay or interpretation into observed fact.

## 5. Source hierarchy

For identity, corporate and institutional relationships, prioritize:

```text
PRIMARY REGISTRY / OFFICIAL RECORD
        ↓
OFFICIAL ORGANIZATION DOCUMENT
        ↓
COURT / PUBLIC INSTITUTION RECORD
        ↓
CONTEMPORANEOUS REPUTABLE REPORTING
        ↓
ARCHIVE / SECONDARY DATABASE
        ↓
SOCIAL MEDIA / USER-GENERATED CONTENT
        ↓
UNVERIFIED CLAIM
```

The hierarchy is not absolute: a lower-level source may be valuable for discovering a lead, while a primary record may verify only one narrow fact. Discovery value and evidentiary value must remain separate.

## 6. Deep OSINT collector layer

The supplied `DeepOSINT` implementation provides four collector classes:

- search-query generation / Google dork construction;
- website crawling and extraction of e-mail, telephone and social links;
- image EXIF analysis including camera/software/time/GPS fields;
- TCP checks against a small set of common ports.

These remain **collector primitives**, not conclusions. A collector result requires normalization, provenance, scope validation and confidence assessment before entering the evidence graph.

## 7. Active vs passive investigation

Passive collection is the default. Active network operations, including port checks, require explicit authorization and target scope. Search patterns for administration panels, configuration files or leaked credentials are treated as high-risk discovery patterns and are not an implicit authorization to access or obtain protected data.

```text
PASSIVE DISCOVERY
 → EVIDENCE VALIDATION
 → PIVOT DECISION
 → AUTHORIZATION CHECK
 → ACTIVE COLLECTION ONLY IF ALLOWED
```

## 8. Counterevidence and conflict handling

A mature investigation does not only collect confirming edges. Every material claim should trigger a bounded counterevidence search:

```text
CLAIM
 ↓
SUPPORTING SOURCES
 ↓
CONTRADICTING SOURCES
 ↓
IDENTITY / ENTITY RESOLUTION
 ↓
TEMPORAL RECONCILIATION
 ↓
CONFIDENCE UPDATE
```

Conflicting sources remain visible. The system must not average incompatible evidence into a misleading single fact.

## 9. Identity resolution

Names alone are insufficient for network attribution. Candidate identity matching should use independent attributes such as organization, role, geography, dates and publicly documented identifiers. Ambiguous matches remain separate nodes until resolved.

A graph should prefer:

`PERSON_A?` → `candidate_identity` → `identity_verified`

over prematurely merging two people with the same name.

## 10. Investigative safety and privacy

The architecture is intended for lawful, authorized and proportionate research. It must minimize unnecessary personal-data collection, separate public-interest evidence from sensitive personal material and avoid publishing unsupported accusations. The system should store the minimum data necessary to establish a claim and retain source provenance.

## 11. Integration with Project 32

This artifact strengthens Project 32 by adding:

- typed influence edges;
- network roles and relationship classes;
- negative-finding records;
- event chronology objects;
- source hierarchy;
- identity-resolution states;
- explicit counterevidence handling.

The resulting principle is:

`OSINT = collection + entity resolution + temporal graph + evidence validation + counterevidence + governed action`.
