# Extended Objects

An **Extended Object** adds a specialised context to an existing Record without losing the original Record.

The original Object remains the primary identity, while the Extended Object provides information or behaviour for a specific situation.

## Primary Object

The **Primary Object** is the original kind of Record. It provides the identity that remains stable.

```text
Primary Object: Contact
└── Record: Sarah Johnson
```

Caraer keeps track of the primary Object and any additional contexts attached to the Record.

## Extended Object

An **Extended Object** adds specialised information to the same underlying Record.

```text
Primary Record: Sarah Johnson
└── Extended Object: Employee
    ├── Start date
    ├── Department
    └── Manager
```

The person remains the same Record. The Employee context adds information relevant to employment.

In the Caraer portal, the canonical contact contexts are Lead, Qualified
Lead, Customer, and Alumni. The canonical company contexts are Target,
Account, and Partner. Employee and other contexts may also exist where
configured by the workspace.

The canonical families are:

```text
Contact
├── Lead
├── Qualified Lead
├── Customer
└── Alumni

Company
├── Target
└── Account
└── Partner
```

Partner records may use the `Partner Type` multi-select, with `Reseller` and
`Whitelabel` as the supported values.

## When to use one

Use an Extended Object when:

- the original Record remains important;
- the specialised context needs its own information;
- the same Record may need more than one context;
- changing context should not create a duplicate Record.

## More than one context

A Record can have more than one valid context when those contexts describe different aspects of the same thing.

```text
Contact Record: Sarah Johnson
├── Customer context
└── Employee context
```

The contexts should only be added when both are genuinely relevant. They do not create duplicate Contact Records.

## Morphing

**Morphing** means moving a Record from one Extended Object to another Extended Object.

For example, a Record can morph from a Candidate Extended Object to an Employee Extended Object. Morphing changes the active context; it does not create a duplicate of the original Record.

## Changing context

Some contexts represent stages that should not be active at the same time. For example, a person may move from a candidate context to an employee context.

When a context changes:

- the original Record identity remains;
- the new context becomes the relevant one;
- previous information should remain available where history is important;
- a second copy of the original Record should not be created just because its context changed.

## Extended Objects versus Relations

An Extended Object describes an additional context for the same underlying Record.

A Relation connects two Records that have independent identities and information.

```text
Extended Object:
Contact Record → Employee context

Relation:
Company Record → Contract Record
```

Use [Relations](Relations.md) when the connected item should exist independently.

## Who can configure them?

Creating or changing Extended Objects and contexts may require administrator access. If a context is missing or cannot be changed, contact your Caraer administrator or representative.
