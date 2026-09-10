# Relations

A **Relation** connects two Records that exist independently.

For example, a Candidate Record and a Company Record are separate Records. A Relation can show that the Candidate works at that Company.

## What a Relation does

A Relation makes it possible to:

- see which Records belong together;
- open one Record from another Record;
- show related information in a View;
- find Records based on their connections;
- keep information in the right place instead of duplicating it.

Creating or removing a Relation does not create or delete the connected Records.

## Relation parts

When creating a Relation, define:

1. **The source Record** — where the connection starts.
2. **The target Record** — what it connects to.
3. **The relation label** — what the connection means.
4. **The reverse label**, when useful — how the connection is described from the other side.
5. **Whether more than one connection is allowed** — for example, one Company with many Employees.

## How to create a Relation

1. Create or open the Records that need to be connected.
2. Decide whether the connection is a Property or a Relation.
3. Choose a clear label that describes the connection.
4. Select the source and target Objects.
5. Choose whether one or multiple Records can be connected.
6. Save the Relation definition.
7. Add the Relation between the relevant Records.
8. Check both Records to confirm the connection is visible and correctly labelled.

## Relation or Property?

Use a **Property** for information about one Record:

```text
Candidate status = Interviewing
```

Use a **Relation** when the other side is its own Record:

```text
Candidate → works at → Company
```

If the connected item has its own name, information, permissions, or lifecycle, it will usually be better represented as a separate Record connected by a Relation.

## Works-at relations

The Caraer Main portal uses the shared `works_at` relation to connect a
person-based record or company context to the organisation where the person
works or is engaged. It supports these object combinations:

- `contact`, `customer`, `lead`, and `qualified_lead` ↔ `company`
- `lead` and `qualified_lead` ↔ `target`
- `contact`, `customer`, `lead`, and `qualified_lead` ↔ `account`

The live relation definition includes all seven participating objects:
`contact`, `customer`, `lead`, `qualified_lead`, `company`, `target`, and
`account`. `target` and `account` extend `company`, preserving the specific
company context without duplicating company fields on person records.

## Account and Ticket relations

The Caraer Main portal defines two Account-to-Ticket relation definitions:

```text
Account ── Open tickets ──> Ticket
Account ── Closed tickets ──> Ticket
```

All Tickets is the automatic complete set of related Tickets. The Ticket
status remains the source of truth; the Open tickets and Closed tickets
relations are intended for the corresponding filtered relation tabs/views.

Customer is the contact person and has a direct Ticket relation as well:

```text
Customer ── Tickets (`customer_tickets`) ──> Ticket
```

When a Ticket concerns a known customer, link both the Customer and the
Customer's Account. This makes the person and company context explicit.

Tickets also have an ownership relation:

```text
Employee ── Ticket owner ──> Ticket
```

Internal name: `ticket_owner`.

`ticket_owner` is the accountable Employee. The existing `assignee` relation
is the working assignment and may point to an Employee, Partner User, Ticket,
Thread, or Task; the two relations should not be treated as interchangeable.

## Example: WhatsApp communication

Suppose a WhatsApp message is stored as a Message Record. It can be connected to the people involved using two Relations:

```text
WhatsApp Message ── sent to ──> Contact
Contact ── received from ──> WhatsApp Message
```

Depending on the chosen model, the same message could also use labels such as:

- Sent by
- Sent to
- Received from
- About
- Part of conversation

The labels should match the way your team talks about communication. This is an example, not a required Caraer setup.

## Example: Candidate, Employee, and Company

A person may have different Records or contexts during their relationship with an organisation:

```text
Candidate ── works at ──> Company
Employee ── works at ──> Company
Candidate ── related to ──> Employee
```

The exact Relations depend on the business process. A Candidate may become an Employee through **morphing** when both represent the same underlying person, or they may remain separate Records when the business needs separate identities.

## Good Relation labels

Use labels that are:

- clear when read from either side;
- based on a real business meaning;
- consistent across similar Objects;
- specific enough to avoid confusion.

Prefer:

```text
Employee → works at → Company
```

over:

```text
Employee → linked to → Company
```

## Flexible setup

Caraer does not require one fixed Relation model for every organisation. Relations should reflect the customer’s process, terminology, and information needs.

Some workspaces may use Relations for Companies and Contracts, while others may use Relations for Customers, Projects, Messages, Activities, or external systems.

## Who can configure Relations?

Creating or changing Relation definitions and links may require administrator access. If a Relation is missing or cannot be changed, contact your Caraer administrator or representative.
