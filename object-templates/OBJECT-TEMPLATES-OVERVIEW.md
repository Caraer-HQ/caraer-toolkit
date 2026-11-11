# Object Templates Overview

Central inventory of shared references and reusable object templates. Update
this file whenever a template or shared trait/system reference changes.

## Status legend

| Field | Meaning |
| --- | --- |
| **Formal status** | The status declared in the template itself. |
| **Structure** | `Normalised` uses the shared property-table structure and references inherited/shared fields; `Legacy` still needs that structural review; `Reference` is a shared, non-object document. |
| **Next action** | The next audit or decision needed; `-` means no current structural action. |

## Shared references

| Reference | Formal status | Structure | Next action |
| --- | --- | --- | --- |
| [System properties](system-properties.md) | Shared reference | Reference | - |
| [Page trait](traits/page.md) | Shared reference | Reference | - |
| [Action trait](traits/action.md) | Shared reference | Reference | Confirm native provisioned property keys against a live portal before adding any. |
| [Message trait](traits/message.md) | Shared reference | Reference | Confirm native provisioned property keys against a live portal before adding any. |
| [Event trait](traits/event.md) | Shared reference | Reference | Confirm native provisioned property keys against a live portal before adding any. |
| [Task trait](traits/task.md) | Shared reference | Reference | Confirm native provisioned property keys against a live portal before adding any. |

## Activities

| Template | Formal status | Structure | Next action |
| --- | --- | --- | --- |
| [Activity](activities/activities.md) | Draft base object | Normalised | Confirm base schema against a live portal before adoption. |
| [Action](activities/action.md) | Draft Activity extension | Normalised | Confirm core schema against a live portal before adoption. |
| [Event](activities/event.md) | Draft Activity extension | Normalised | Confirm core schema against a live portal before adoption. |
| [Message](activities/message.md) | Draft Activity extension | Normalised | Confirm core schema against a live portal before adoption. |
| [Task](activities/task.md) | Draft Activity extension | Normalised | Confirm core schema against a live portal before adoption. |
| [Milestone](activities/milestone.md) | Draft | Legacy | Align with Activity inheritance and the shared property table. |
| [Meeting](activities/event/meeting.md) | Draft | Legacy | Reference Activity/Event and retain only Meeting-specific properties. |
| [Subtask](activities/task/subtask.md) | Draft | Legacy | Reference Activity/Task and retain only Subtask-specific properties. |
| [Action — Automation](activities/action/automation.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — Call to action](activities/action/call-to-action.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — Call](activities/action/call.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — Comment](activities/action/comment.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — Data enrichment](activities/action/data-enrichment.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — First login](activities/action/first-login.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — Form submission](activities/action/formsubmission.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — Marketing email](activities/action/marketing-email.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — Profile completion](activities/action/profile-completion.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — User creation](activities/action/user-creation.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Action — Website sessions](activities/action/website-sessions.md) | Draft | Legacy | Reference Activity/Action and retain only child-specific properties. |
| [Message — Email](activities/message/email.md) | Draft | Legacy | Reference Activity/Message and retain only child-specific properties. |
| [Message — LinkedIn](activities/message/linkedin.md) | Draft | Legacy | Reference Activity/Message and retain only child-specific properties. |
| [Message — WhatsApp](activities/message/whatsapp.md) | Live Caraer Main schema reference, updated 2026-11-03; integration verification pending | Normalised | Verify identifier writes, person relations, bidirectional storage and send deduplication before transport testing. |

## Recruitment

| Template | Formal status | Structure | Next action |
| --- | --- | --- | --- |
| [Candidate](recruitment/candidate.md) | Canonical primary object; recruitment lifecycle anchor | Legacy | Normalise property table and extract verified shared trait references. |
| [New Candidate](recruitment/new-candidate.md) | Canonical Candidate extension; first lifecycle state | Legacy | Reference Candidate and retain only lifecycle-specific properties. |
| [Qualified Candidate](recruitment/qualified-candidate.md) | Canonical Candidate extension; qualified lifecycle state | Legacy | Reference Candidate and retain only lifecycle-specific properties. |
| [Employee](recruitment/employee.md) | Canonical Candidate extension; exclusive recruitment lifecycle | Legacy | Reference Candidate and retain only lifecycle-specific properties. |
| [Alumni](recruitment/alumni.md) | Canonical Candidate extension; exclusive recruitment lifecycle | Legacy | Reference Candidate and retain only lifecycle-specific properties. |
| [Vacancy](recruitment/vacancy.md) | Canonical primary object; recruitment record | Normalised | - |

## Sales

| Template | Formal status | Structure | Next action |
| --- | --- | --- | --- |
| [Company](sales/company.md) | Canonical primary object | Legacy | Normalise property table and confirm shared references. |
| [Contact](sales/contact.md) | Canonical primary object | Legacy | Normalise property table and confirm shared references. |
| [Target](sales/target.md) | Canonical Company extension | Legacy | Reference Company and retain only extension-specific properties. |
| [Account](sales/account.md) | Canonical Company extension | Legacy | Reference Company and retain only extension-specific properties. |
| [Lead](sales/lead.md) | Canonical Contact extension | Legacy | Reference Contact and retain only extension-specific properties. |
| [Qualified Lead](sales/qualified-lead.md) | Canonical Contact extension | Legacy | Reference Contact and retain only extension-specific properties. |
| [Customer](sales/customer.md) | Canonical Contact extension | Legacy | Reference Contact and retain only extension-specific properties. |
| [Deal](sales/deal.md) | Central draft; independent sales transaction | Legacy | Confirm live model before normalising. |
| [Partner](sales/partner.md) | Central draft; confirm against the live portal before schema changes | Legacy | Resolve ownership/model before normalising. |
| [Reseller](sales/reseller.md) | Central draft; model discrepancy under review | Legacy | Resolve the model discrepancy before normalising. |

## Organisation

| Template | Formal status | Structure | Next action |
| --- | --- | --- | --- |
| [Location](organisation/location.md) | Central primary object | Legacy | Normalise property table and confirm hierarchy/relations. |
| [Department](organisation/department.md) | Central primary object | Legacy | Normalise property table and confirm hierarchy/relations. |
| [Business Unit](organisation/business-unit.md) | Central primary object | Legacy | Normalise property table and confirm hierarchy/relations. |

## Campaigns

| Template | Formal status | Structure | Next action |
| --- | --- | --- | --- |
| [Meta Campaign](campaigns/meta-campaign.md) | Central primary object | Legacy | Normalise table; preserve provider field mappings. |
| [Meta Ad Set](campaigns/meta-ad-set.md) | Central primary object | Legacy | Normalise table; preserve provider field mappings. |
| [Meta Ad](campaigns/meta-ad.md) | Central primary object | Legacy | Normalise table; preserve provider field mappings. |

## Integrations

| Template | Formal status | Structure | Next action |
| --- | --- | --- | --- |
| [Order](integrations/tickettailor/order.md) | Draft Action extension; internal name `purchase_order` | Normalised | Validate optional/null field shapes and provider money units before live adoption. |
| [Ticket](integrations/tickettailor/ticket.md) | Draft Action extension; internal name `event_ticket` | Normalised | Validate cancellation source, additional webhook examples, optional field shapes, and fulfilment cardinality before live adoption. |

## Support and onboarding

| Template | Formal status | Structure | Next action |
| --- | --- | --- | --- |
| [Ticket](support/ticket.md) | Live Caraer Main schema reference, updated 2026-08-13 | Legacy | Preserve live evidence while mapping to the shared table structure. |
| [Onboarding](onboarding/onboarding.md) | Central draft; independent operational record | Legacy | Confirm the live model before normalising. |

## Update rules

1. Keep every object template and every shared system/trait reference listed.
2. Update the relevant row in the same change that modifies the template.
3. Do not mark a template `Normalised` until it references inherited/shared
   fields and uses the standard property table.
4. Validate live schema facts before changing a formal status or claiming trait
   provisioning.
