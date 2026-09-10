# Views and Filters

A **View** is a way of displaying Records. A **Filter** limits the Records shown in that View. Together, they help you focus on the information that matters for a particular task.

Views and Filters do not duplicate, delete, or change the underlying Records. They change which Records you see and how they are organised.

## Common views

Depending on your workspace, you may use:

- **Table views** for reviewing many Records in rows and columns;
- **Detail views** for focusing on one Record;
- **Board views** for work moving through stages;
- **Calendar views** for date-based work.

The available View types depend on the Object and the capabilities enabled in your workspace.

## Create a View

1. Choose the Object you want to work with, such as Company, Contact, Contract, or Task.
2. Choose the way you want to display the Records.
3. Select the information you want to see, such as name, status, owner, or due date.
4. Add Filters if you only want to see part of the Records.
5. Arrange the results using sorting or grouping where available.
6. Save the View if you want to use it again.

For example, you could create a Company View showing company name, customer status, Plan, and contract status.

## Add Filters

A Filter usually has three parts:

```text
Information   →   Condition   →   Value
Status        →   is           →   Active
```

To add a Filter:

1. Open the View settings.
2. Choose **Add Filter**.
3. Select the Property or related information to filter on.
4. Choose the condition, such as is, is not, contains, or is empty.
5. Enter or select the value.
6. Apply the Filter.

Some workspaces also allow Filters based on Relations. For example, you may be able to show Companies that have an Active Contract or Tasks related to a particular Project.

## Combine Filters

Multiple Filters can be combined to narrow the results.

```text
Customer Status = Active
AND
Contract Status = Active
```

This shows Records that meet both conditions. Where supported, an **OR** condition can show Records that meet at least one of several conditions:

```text
Status = Active
OR
Status = Opportunity
```

The available combination options depend on the View configuration.

## Useful examples

### Active customers

```text
Object: Company
Filter: Customer Status is Active customer
```

### Contracts renewing soon

```text
Object: Contract
Filter: End Date is within the chosen period
```

### Tasks assigned to you

```text
Object: Task
Filter: Assignee is me
Filter: Status is not completed
```

### Companies without a Plan

```text
Object: Company
Filter: Plan is empty
```

## Save and share Views

You may be able to save a View for personal use or share it with your team. A shared View should have a clear name and Filters that make sense to everyone who uses it.

Good names describe the purpose, for example:

- Active Customers;
- Contracts Renewing This Month;
- My Open Tasks;
- Companies Without a Plan.

## Views versus Records

A View is a lens on your data. Editing a Record from a View changes the Record itself, while changing the View only changes the way the Records are displayed.

## Good practice

- keep Views focused on one task;
- use clear names;
- show only the Properties people need;
- check Filters before sharing a View;
- review saved Views when the workflow changes;
- avoid creating many Views that show the same information.

## Who can create or change Views?

Creating, sharing, or changing Views may require administrator access. If an option is missing or a View cannot be changed, contact your Caraer administrator or representative.
