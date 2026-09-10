# Practical Examples

These examples show how Caraer concepts can work together. Your workspace may use different Objects, names, Relations, or workflows.

## Customer and billing information

```text
Company
├── Relation → Contract
├── Relation → Plan
└── Relation → Usage or Meter
```

The Company represents the customer. The Plan describes the package. The Contract describes the agreement. Usage or Meter Records can support reporting or billing calculations.

The exact labels and setup are configurable. For example, a workspace may use **Active** and **Cancelled** to describe different Contract connections, while another workspace may use different labels.

## Candidate, Employee, and Company

```text
Candidate ── works at ──> Company
Employee  ── works at ──> Company
```

A person can be represented in different contexts. If the same person moves from Candidate to Employee, the workspace may use **Morphing** to change the active Extended Object while retaining the same underlying Record identity.

## WhatsApp communication

```text
WhatsApp Message
├── sent to       → Candidate
├── received from → Employee
└── about         → Company
```

The Message remains a Message. Relations explain who sent or received it and what it concerns. This is usually clearer than storing every connection as plain text.

## Employee assignment

```text
Onboarding Activity ── assigned to ──> Employee
```

The Activity remains an Activity and is connected to the responsible Employee. A follow-up Task can be connected when a specific piece of work needs to be completed.

## Renewal follow-up

```text
Contract nearing renewal
→ Automation checks Contract status
→ Follow-up Task is created
→ Task appears in a View for the responsible team
```

This combines a Contract, an Automation, a Task, and a View without changing the meaning of any of those Records.

## Choosing the right concept

- Need another kind of thing? Use an **Object**.
- Need another piece of information? Use a **Property**.
- Need a specialised context for the same Record? Use an **Extended Object**.
- Need to connect separate Records? Use a **Relation**.
- Need reusable behaviour? Use a **Trait**.
- Need to record work or communication? Use an **Activity**.
- Need to find a useful subset of Records? Use a **View** and **Filter**.
- Need repeated work to happen automatically? Use an **Automation**.

When two options seem possible, start with the simplest model that accurately describes the work. Ask your Caraer administrator or representative when the setup affects multiple teams or important customer information.
