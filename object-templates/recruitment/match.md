# Match Object Template

Status: Draft; independent operational recruitment object. Not yet canonical or applied to a portal.

## Purpose

`match` represents one Candidate's application to one Vacancy. It combines
current Candidate and Vacancy information through linked properties and stores
only application-specific answers, status, and marketing attribution.

Candidate identity, qualifications, and general preferences remain on Candidate.
Role information remains on Vacancy. These values must not be duplicated as
editable properties on Match. Linked properties display current source values.
[Form Submission](../activities/action/formsubmission.md) preserves the answers
as submitted and links to the relevant Match; Match does not store snapshots.

Match does not extend Candidate or Vacancy and does not replace `new_candidate`,
`qualified_candidate`, `employee`, or `alumni`. Match outcomes do not automatically
transition the Candidate lifecycle.

## Traits

### Enabled by default

- **Table** — application list; default trait.
- **Flow** — application pipeline grouped by `status_match`; verify the actual Flow configuration before use.

### Optional by workspace configuration

- **Analytics** — application funnel reporting, subject to access controls.
- **Task** — application follow-up, where supported and explicitly configured.

### Not enabled by default

- **Page** — Match is an internal recruitment record, not a public webpage.
- Candidate lifecycle extensions — these extend Candidate, not Match.
- Other operational traits require an explicit workspace decision.

## Core Properties

Proposed labels: Match / Matches. Suite: Recruitment. Object icon:
`solidCalendarCheck`. Description: Een sollicitatie of match tussen een kandidaat
en een vacature. Number ID is not enabled by default.

Groups: `Details`, `System`, `Candidate`, `Vacature`, `Kwalificatie`, `Marketing`.
These are schema keys; interfaces may localize their labels.

The proposed business schema contains **32 properties: 25 linked properties and
7 stored properties**. Source bindings below describe ownership, not verified
property identifiers. Resolve each source against the destination schema.

### Candidate

| Property | Type | Notes |
| --- | --- | --- |
| `first_name` | linked-property | Voornaam. Candidate → first name. |
| `last_name` | linked-property | Achternaam. Candidate → last name. |
| `phone` | linked-property | Mobiel telefoonnummer. Candidate → designated phone/mobile property. |
| `mail` | linked-property | E-mailadres. Candidate → email; canonical source name is `email`. |
| `candidate_status` | linked-property | Kandidaatstatus. Candidate → explicitly selected candidate-wide status/lifecycle source. No universal `status_candidate` property is assumed. |
| `candidate_notes` | linked-property | Kandidaatnotities. Candidate → shared notes; display in Details. Not application-specific notes. |

### Kwalificatie — linked Candidate information

These eleven fields belong to Candidate and are read-only projections on Match.
Their source properties must exist before binding them. Candidate qualification
source additions are proposed dependencies, not existing canonical schema facts.

| Property | Type | Notes |
| --- | --- | --- |
| `candidate_qualification_education_level` | linked-property | Hoogst afgerond opleidingsniveau. Candidate → education level; proposed source option family: `education_level`. |
| `candidate_qualification_education_status` | linked-property | Opleidingsstatus. Candidate → education status; proposed source option family: `education_status`. |
| `candidate_qualification_experience_areas` | linked-property | Relevante werkgebieden. Candidate → experience areas; workspace-specific controlled multi-select catalog. |
| `candidate_qualification_driver_licenses` | linked-property | Rijbewijzen. Candidate → driving licences held; proposed source option family: `driver_licenses`. |
| `candidate_qualification_certificates` | linked-property | Certificaten. Candidate → certificates held; workspace-specific controlled multi-select catalog. |
| `candidate_qualification_systems` | linked-property | Ervaring met systemen. Candidate → systems experience; workspace-specific controlled multi-select catalog. |
| `candidate_qualification_work_schedule` | linked-property | Voorkeur werktijden. Candidate → general preference; proposed source option family: `work_schedule`. |
| `candidate_qualification_irregular_shifts` | linked-property | Bereid tot onregelmatige diensten. Candidate → general willingness; proposed source option family: `yes_no`. |
| `candidate_qualification_available_hours` | linked-property | Beschikbare uren per week. Candidate → general weekly availability as an exact number. |
| `candidate_qualification_available_from` | linked-property | Beschikbaar vanaf. Candidate → general availability date. |
| `candidate_qualification_zzp` | linked-property | Zelfstandig ondernemer (zzp). Candidate → self-employed status; proposed source option family: `yes_no`. |

Options and validation belong to the Candidate source properties; do not create
independent option catalogs or editable copies on Match. The proposed families
below guide source setup where a matching property does not already exist.

| Option family | Proposed source values |
| --- | --- |
| `yes_no` | `ja`, `nee` |
| `education_level` | `geen_opleiding`, `lbo`, `vmbo_basis`, `vmbo_kader`, `vmbo_tl`, `mbo`, `mbo_3`, `mbo_4`, `hbo`, `wo`, `anders` |
| `education_status` | `afgerond`, `in_opleiding`, `niet_afgerond`, `niet_van_toepassing` |
| `driver_licenses` | `am`, `a1`, `a2`, `a`, `b`, `b_plus_code_96`, `be`, `c1`, `c1e`, `c`, `ce`, `d1`, `d1e`, `d`, `de`, `t`, `geen` |
| `work_schedule` | `overdag`, `in_de_nacht`, `beide` |

### Vacature

| Property | Type | Notes |
| --- | --- | --- |
| `vacature` | linked-property | Vacature. Vacancy → title; canonical source `vacancy_name`, sometimes `job_title` in existing portals. |
| `vacancy_status` | linked-property | Vacaturestatus. Vacancy → status. |
| `description` | linked-property | Functieomschrijving. Vacancy → description. |
| `location` | linked-property | Werklocatie. Vacancy → location. |
| `employment_type` | linked-property | Dienstverband. Vacancy → employment type. |
| `published_at` | linked-property | Gepubliceerd op. Vacancy → publication date/time. |
| `closing_date` | linked-property | Sluitingsdatum. Vacancy → closing date. |
| `vacancy_notes` | linked-property | Vacaturenotities. Vacancy → shared notes, subject to source access. |

### Match-specific properties

Only these seven business properties store independent values on Match.
All qualification answers are optional in the base template; a vacancy-specific
form may require a relevant subset. No defaults are defined.

| Property | Type | Notes |
| --- | --- | --- |
| `status_match` | single-select | Matchstatus. Required; `match_status` options below. Group: Details. |
| `candidate_qualification_interest` | single-select | Interesse in deze vacature. `ja`, `nee`; interest in this Vacancy/workfield. Group: Kwalificatie. |
| `candidate_qualification_experience_range` | single-select | Jaren relevante werkervaring. `experience_range` options below; experience relevant to this Vacancy, not total career experience. Group: Kwalificatie. |
| `candidate_qualification_certificate_willingness` | single-select | Bereid benodigde certificaten te behalen. `ja`, `nee`; willingness concerning this Vacancy's requirements. Group: Kwalificatie. |
| `candidate_qualification_commute_range` | single-select | Reistijd tot werklocatie. `commute_range` options below; specific to this Vacancy's location. Group: Kwalificatie. |
| `match_latest_campaign_name` | string / single-line | Laatste campagnenaam. Optional, editable application-specific attribution; populated manually or by integration. Group: Marketing. |
| `match_meta_id` | string / single-line | Meta-ID. Optional application-specific identifier; preserve exact digits. Define whether it identifies a lead, campaign, ad set, or ad before integration. Group: Marketing. |

The `candidate_qualification_*` prefix is retained for compatibility. It does not
establish ownership: linked fields belong to Candidate; the four stored
qualification answers above belong to Match.

### Match status options

| Value | Label |
| --- | --- |
| `nieuw` | Nieuw |
| `gekwalificeerd` | Gekwalificeerd |
| `sollicitatie_gesprek` | Sollicitatiegesprek |
| `2e_gesprek` | 2e gesprek |
| `contract_voorstel` | Contractvoorstel |
| `gestart` | Contract gestart |
| `geen_match` | Geen match |

Preserve internal values when integrating; these are proposed normalized labels.

### Relevant experience options

| Value | Label |
| --- | --- |
| `geen_ervaring` | Geen ervaring |
| `minder_dan_1_jaar` | Minder dan 1 jaar |
| `1_tot_minder_dan_3_jaar` | 1 tot minder dan 3 jaar |
| `3_tot_minder_dan_5_jaar` | 3 tot minder dan 5 jaar |
| `5_tot_minder_dan_10_jaar` | 5 tot minder dan 10 jaar |
| `10_jaar_of_meer` | 10 jaar of meer |

### Commute options

| Value | Label |
| --- | --- |
| `tot_en_met_30_minuten` | Tot en met 30 minuten |
| `meer_dan_30_tot_en_met_45_minuten` | Meer dan 30 tot en met 45 minuten |
| `meer_dan_45_tot_en_met_60_minuten` | Meer dan 45 tot en met 60 minuten |
| `meer_dan_60_minuten` | Meer dan 60 minuten |

### System properties

Platform-managed fields are separate from the 32 business properties. Do not
recreate, rename, or attach defaults/uniqueness rules without checking platform
ownership. Preserve the existing camel-case identifiers.

| Property | Type | Notes |
| --- | --- | --- |
| `uuid` | string / single-line | Unieke ID. Platform-owned unique record identity. |
| `createdAt` | date / date | Aangemaakt op. Platform-managed creation timestamp. |
| `updatedAt` | date / date | Laatst gewijzigd op. Platform-managed last-update timestamp. |
| `deletedAt` | date / date | Verwijderd op. Platform-managed deletion/archive context. |
| `primary_object` | single-select | Primair objecttype. Platform object selector. |
| `extended_objects` | multi-select | Aanvullende objecttypen. Platform extension/context selector. |

System selector options come from the destination portal, not a hard-coded list.
Types/formats throughout this draft require destination-schema verification;
this document is not an executable provisioning script.

## Relations

| From | To | Relation | Notes |
| --- | --- | --- | --- |
| Match | Candidate | `has_candidate` | Proposed name; exactly one Candidate per Match. Candidate may have many Matches. |
| Match | Vacancy | `for_vacancy` | Proposed name; exactly one Vacancy per Match. Vacancy may have many Matches. |
| Match | Employee | `owner` | Application owner; existing reference convention, to verify per destination. |
| Match | Business Unit | `allocated` | Allocated business unit; existing reference convention, to verify per destination. |
| Form Submission | Match | `submitted_for` | Proposed name; a Match may have multiple submissions preserving answers and submission time. |

Employee and Business Unit details remain on their source records. Introduce
linked display properties only when needed; do not copy names/contact details.
Application-specific tasks should relate to Match, not duplicate Task properties.

Candidate and Vacancy views should show related Matches with their individual
statuses and application context. A single linked Match status is ambiguous when
multiple Matches exist unless an explicit selection rule is defined.

Resolve relation/property identifiers per destination; never copy tenant UUIDs.
Cardinalities above are proposed application invariants, not verified database
constraints. The reference portal's shared `applied` relation is not assumed to
be an alias of these proposed relations or the toolkit's existing `applies_to`.

## Lifecycle

A Match progresses independently through `match_status`. An unsuccessful Match
must not prevent the Candidate from progressing with another Vacancy. No
application automation, Candidate lifecycle transition, default status, or
hiring handoff is defined here.

Linked properties show current source information. Form Submissions preserve
the submitted answers in `form_fields`; preserving those payloads is an
integration requirement, not a verified platform immutability guarantee.

## Access

Use the proposed Match column in [Recruitment access](access.md). Linked values
require authorization to their source data as well as Match. Marketing receives
only approved attribution fields, not implicit access to Candidate contact
details, qualifications, or notes. Hiring managers see assigned Matches and
approved fields only. Match is not publicly published; qualification fields
must not be made public merely to expose them through forms.

## Validation and Integration

- Preflight source availability, supported property types/formats, global name collisions, and linked traversal before provisioning. Do not silently reuse a same-name property of another type.
- Create groups and source properties before linked bindings; create required relations before configuring traversal. Enable traits using trait tools.
- Preserve linked-property bindings and formats; do not fall back to editable copies.
- Route Candidate answers to Candidate and application answers to Match. Preserve the full submitted answer set on the related Form Submission.
- Unanswered differs from `nee`, `geen`, and `geen_ervaring`.
- Enforce `geen` exclusivity in relevant multi-select forms/integrations.
- Validate Candidate available hours as non-negative; any upper bound requires a product decision.
- Do not infer mappings from legacy overlapping experience ranges.
- Verify linked values and Flow rendering with multiple applications before applying this draft to a portal.

## Open Questions

- Reconcile Candidate and Qualified Candidate `applies_to` links with Match as the application record. Do not maintain duplicate application tracking without a consistency contract.
- Resolve overlap between `qualified_candidate_status` and the Match pipeline before making Match canonical.
- Resolve Candidate status/lifecycle display and qualification source properties. Existing `availability` and `specialisms` are not automatically equivalent to the proposed sources.
- Decide whether repeated applications to the same Vacancy are allowed and define deduplication accordingly.
- Confirm proposed relation names, source bindings, access enforcement, and Flow support against the destination schema.
- Choose workspace-specific experience-area, certificate, and system catalogs outside this central template.
