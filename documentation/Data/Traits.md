# Traits

A **Trait** gives an Object an additional capability. Traits affect how people work with Records; they do not change what the Object represents.

For example, the Table Trait lets people manage Records in a table. It does not turn the Object into a different kind of thing.

## The nine Caraer Traits

Caraer recognises these nine Traits:

1. Table
2. Flow
3. Page
4. User
5. Action
6. Message
7. Event
8. Task
9. Analytics

An Object can have more than one Trait. The available Traits and configuration depend on your workspace and access.

## Table

The **Table** Trait lets people view and manage Records in rows and columns.

It can support:

- columns;
- sorting;
- filtering;
- saved views;
- selecting multiple Records;
- bulk actions where permitted.

Table is the most commonly used Trait in the current Caraer portal.

## Flow

The **Flow** Trait lets Records move through stages in a process.

For example, a sales process may use stages such as New, In progress, Won, and Lost.

The meaning of each stage is configured for the Object and the team using it.

## Page

The **Page** Trait lets Records be used as pages or other published content.

It can support:

- page content;
- previewing;
- publishing;
- website addresses;
- publication status.

## User

The **User** Trait lets Records represent people who can sign in or receive access to Caraer.

It can support:

- user identity;
- invitations;
- activation and deactivation;
- roles and permissions.

Employee and Partner User are examples of Objects using User behaviour in the current portal.

## Analytics

The **Analytics** Trait lets Records contribute to reporting and analysis.

It may support:

- counts and totals;
- trends over time;
- dashboards;
- calculated measures;
- reporting by status, date, or other information.

Analytics behaviour may need to be enabled or configured for your workspace.

## Combining Traits

Traits can be combined when they support the same way of working.

```text
Object: Onboarding
├── Table
├── Flow
├── Task
└── Analytics
```

For example, a team may use Table to manage onboarding items, Flow to show their stage, Task to track work, and Analytics to measure completion.

Traits add capabilities; they do not replace Properties, Extended Objects, or Relations.

## Who can change Traits?

Adding, removing, or configuring Traits may require administrator access. If a Trait is missing or cannot be changed, contact your Caraer administrator or representative.
