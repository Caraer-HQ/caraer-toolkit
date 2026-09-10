# Objects Schema

Caraer organises information in a consistent way. This makes it easier to find information, connect related work, and use the same process across your team.

## Objects

An **Object** describes a kind of thing Caraer can manage, such as a Company, Contact, Contract, Plan, or Task.

An Object defines:

- what kind of information it represents;
- which Properties are available;
- how Records are displayed;
- which capabilities or Traits can be used;
- who can view or change the information.

Common customer-facing Objects include:

- Company
- Contact
- Employee
- Lead
- Customer
- Contract
- Plan
- Meter
- Onboarding
- Project
- Task
- Deal
- Activity

## Canonical object families

The local schema uses two primary objects for the commercial and contact
model:

```text
Primary Object: Contact
├── Lead
├── Qualified Lead
├── Customer
└── Alumni

Primary Object: Company
├── Target
└── Account
```

`Lead`, `Qualified Lead`, `Customer`, and `Alumni` are Contact extensions.
They retain the underlying Contact identity and inherit shared Contact
properties. `Target` and `Account` are Company extensions and retain the
underlying Company identity. These are extensions, not Relations and not
duplicate records.

Some additional Objects are used internally by Caraer for administration, integrations, websites, or system behaviour. They may not be visible in your workspace.

## Records

A **Record** is one individual example of an Object. For example, “Top Match Recruitment B.V.” is a Company Record.

```text
Object: Company
└── Record: Top Match Recruitment B.V.
```

Records contain the actual information your team works with. A Record can be displayed in a table, opened as a detail page, included in a View, connected to other Records, or used by an Automation.

## Properties

**Properties** are the pieces of information stored on a Record, such as a name, email address, status, date, or amount.

Properties belong to the Object and are available on its Records. The value can be different for every Record.

```text
Object: Company

Properties
├── Company name
├── Website
├── Customer status
└── Renewal date
```

## Property types

Caraer supports the following property types and formats:

#### Text

Short written information, such as a name or reference.

#### Email

An email address.

#### Website

A website address or URL.

#### Phone number

A telephone or mobile number.

#### Long text

Notes, descriptions, or other longer written information.

#### Single choice

One option selected from a predefined list, such as a customer status.

#### Multiple choice

More than one option selected from a predefined list.

#### Date

A calendar date, such as a start date or renewal date.

#### Number

A numeric value.

#### Currency

A monetary amount with a currency, such as an invoice amount.

#### Duration

An amount of time.

#### Checkbox

A yes/no or on/off value.

#### Tags

One or more labels used to group or find Records.

#### File

A file attached to a Record.

#### Number range

A minimum and maximum numeric value.

#### Currency range

A minimum and maximum monetary value.

#### Structured information

Information with multiple related values stored together, such as an address or configuration.

#### System-managed linked information

Some information is created and maintained by Caraer itself. Users should not enter these values manually.

## Properties versus Relations

Use a **Property** for information about one Record. Use a **Relation** when you connect that Record to another Record.

```text
Property:
Company status = Active

Relation:
Company → Contract
```

For example, a Plan should normally be its own Record when it has its own limits, prices, or description. The Company can then be connected to that Plan with a Relation.

See [Relations](Relations.md) for more information about connections between Records.

## Traits and capabilities

Objects can receive reusable capabilities such as Table, Page, User, Task, or Analytics. These capabilities affect how people work with the Object but do not change what the Object represents.

See [Traits](Traits.md) for the complete list of nine Traits.

## A complete example

```text
Object: Company
└── Record: Top Match Recruitment B.V.
    ├── Website: example.com
    ├── Customer status: Active customer
    ├── Relation → Plan: Scale
    └── Relation → Contract: Top Match Recruitment B.V. - Contract
```

Use an Object when you need a new kind of thing. Use a Property when you need another piece of information about an existing thing. Use a Relation when you need to connect it to another Record.

## Caraer Main support model

The support model uses a Ticket as the work record. A Ticket can carry both
company and person context:

```text
Ticket ──> Account   (the company)
Ticket ──> Customer  (the contact person at that company)
```

Customer is a Contact extension, not a company. When both are known, both
relations should be stored on the Ticket. The direct Customer relation is
`customer_tickets`; Account also provides the Open tickets and Closed tickets
relation tabs.

## Who can change the data model?

Creating or editing an Object or Property may require administrator access. If you cannot create or edit something, contact your Caraer administrator or representative.
