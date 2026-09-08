# Caraer Central Object Setup

This folder is the central, customer-independent object setup for Caraer. It
defines the reusable object hierarchy, inheritance rules, Traits, and object
templates used as the basis for each customer portal.

Billing objects such as Plan, Contract, and Meter are intentionally excluded;
they are Caraer Main Portal-specific and documented under `/billing/`.

It is **not customer documentation** and must not contain customer-specific
records, properties, branding, or configuration.

## Canonical object hierarchy

```text
Contact                         Company                         Candidate (primary)
├── Lead                        ├── Target                    ├── New Candidate
├── Qualified Lead              ├── Account                    ├── Qualified Candidate
└── Customer                    └── Partner (draft)             ├── Employee
                                                               └── Alumni

Contact partner role: Reseller (draft; model discrepancy)

Independent operational objects
├── Activity
│   ├── Action
│   ├── Event
│   ├── Message
│   ├── Task
│   └── Milestone
├── Ticket
├── Deal (draft)
├── Onboarding (draft)
└── Vacancy
```

`Lead`, `Qualified Lead`, and `Customer` are Contact extensions. `Target` and
`Account` are Company extensions. `Candidate` is an independent primary
object; `New Candidate`, `Qualified Candidate`, `Employee`, and `Alumni` are
Candidate extensions. Extensions preserve the
identity of the primary record and inherit shared properties; they are not
duplicate records and not Relations.

## Property ownership

Primary Objects are deliberately small and stable. Contact contains only
personal identity and personal communication details. Role- or company-
specific information belongs on the relevant Extended Object or Relation.
Company is retained as a relationship anchor, but this central setup does not
define a customer-specific Company property set.

The shared `works_at` relation connects `Contact`, `Customer`, `Lead`, and
`Qualified Lead` to the relevant `Company`, `Target`, or `Account` context.
Company-context associations belong in this relation rather than duplicated
company fields on person or extension records.

### Contact — base person record

Contact owns only properties intrinsic to the person:

- identity: `first_name`, `last_name`
- contact details: `email`, `phone`, `mobile_phone`, `linkedin_url`
- communication context: `platforms`
- employment context that belongs to the person: `job_title`, employment status/details

Contact must not own company, marketing, sales, contractual, support, or
generic catch-all properties. A person's job title and employment details may
be stored on Contact; the company or Account they work for must be represented
by a Relation. If employment details vary by company, relation metadata or a
dedicated employment extension is required rather than duplicating fields on
Contact.

### Contact extensions

| Extension | Owns role-specific properties such as |
| --- | --- |
| **Lead** | marketing source/campaign, consent, audience, engagement, and lead status |
| **Qualified Lead** | sales stage, qualification outcome/date, owner, opportunity context, next step, and sales notes |
| **Customer** | customer status, customer since, onboarding context, support status, and service notes |
| **Alumni** | alumni date, former relationship context, and alumni notes |

Marketing properties belong on `Lead`. Sales properties belong on
`Qualified Lead`. Contractual and support properties belong on `Customer`.
None of these should be added to the base Contact or Company objects.

### Company extensions

| Extension | Owns role-specific properties such as |
| --- | --- |
| **Target** | Extension anchor only; no central property set is defined here |
| **Account** | Extension anchor for customer and operational relations; no billing property set is defined here |

The live Caraer Main portal is the reference for naming and behaviour. This
folder is the generic template source that can be applied to customer
portals.

## Folder structure

## Tree

- `activities` — reusable activity object family and templates
  - `access.md`
  - `activities.md`
  - `action.md`
  - `task.md`
  - `message.md`
  - `event.md`
  - `milestone.md`
  - `action/`
    - `call.md`
    - `comment.md`
    - `formsubmission.md`
    - `website-sessions.md`
    - `marketing-email.md`
    - `call-to-action.md`
    - `data-enrichment.md`
    - `profile-completion.md`
    - `user-creation.md`
    - `first-login.md`
    - `automation.md`
  - `task/`
    - `subtask.md`
  - `message/`
    - `email.md`
    - `whatsapp.md`
    - `linkedin.md`
  - `event/`
    - `meeting.md`
- `support` — reusable support object templates
  - `access.md`
  - `ticket.md`
- `sales` — sales and customer relationship objects
  - `access.md`
  - `contact.md`
  - `lead.md`
  - `qualified-lead.md`
  - `customer.md`
  - `deal.md`
  - `reseller.md` (draft; model discrepancy)
  - `company.md`
  - `target.md`
  - `account.md`
  - `partner.md`
- `recruitment` — recruitment primary and lifecycle objects
  - `access.md`
  - `candidate.md`
  - `new-candidate.md`
  - `qualified-candidate.md`
  - `employee.md`
  - `alumni.md`
  - `vacancy.md`
- `organisation` — organisation structure and organisation extensions
  - `access.md`
  - `location.md`
  - `department.md`
  - `business-unit.md`
- `onboarding` — independent implementation records
  - `access.md`
  - `onboarding.md`
- `analytics` — cross-suite reporting and analytics
  - `README.md`
  - `access.md`
- `campaigns` — campaign structures and advertising performance
  - `README.md`
  - `access.md`
  - `meta-campaign.md`
  - `meta-ad-set.md`
  - `meta-ad.md`

## Notes

- Extended Objects only define fields that are unique to them.
- Shared fields live on the base Object and inherit downward automatically in Caraer.
- Traits belong to Object definitions, not individual Records.
- Relations connect independent Records; they must not be used to model extension ownership.
- Customer-specific overrides belong in the relevant customer workspace, never here.
- `Partner`, `Deal`, and `Onboarding` are explicitly marked draft until their
  live Caraer model is confirmed. Do not apply these templates to the portal
  automatically.

## Trait requirement

Every object template in this folder must include a `## Traits` section that
documents enabled-by-default, optional, and excluded Traits. The activity and
support templates have been audited against this requirement.
