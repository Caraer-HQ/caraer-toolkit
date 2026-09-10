# Scenarios

In Latenode, an automation is called a **Scenario**. A Scenario is a chain of Nodes connected on a visual canvas. Each Node performs one step and passes its result to the next Node.

```text
Trigger → Action → Action → Result
```

The exact steps depend on the service and process you are automating.

## Scenario types

Latenode documentation describes five common types of Scenario:

### Linear scenarios

The same Nodes run in the same order every time.

```text
New form submission → Save to a spreadsheet → Notify the team
```

### Conditional scenarios

The Scenario chooses a route based on structured information such as status, amount, country, or score.

```text
New request → Check amount → Notify manager or send an automatic reply
```

### AI-based routing

The Scenario uses AI when the decision depends on meaning, tone, intent, or other unstructured information.

```text
Incoming message → AI classifies the message → Route to the right action
```

### Agent scenarios

An AI Agent chooses which connected tools to use and in what order. This is useful for flexible requests that cannot be described as one fixed sequence.

### Multi-agent scenarios

Several specialised agents work together on a larger task. This is intended for complex work that naturally separates into roles such as research, writing, review, or publishing.

## Build a Scenario

1. Describe the result you want.
2. Decide what starts the Scenario: an event, a schedule, a webhook, or a manual run.
3. Choose the Nodes needed for each step.
4. Connect the Nodes from left to right.
5. Run the first Node once and inspect its output.
6. Map the required information into the next Node.
7. Test each step in order.
8. Save and activate the Scenario when the result is understood.

## Copy a Scenario

To copy an existing Scenario:

1. Go to the **Scenarios** page.
2. Open the menu (**⋯**) for the Scenario you want to copy.
3. Select **Copy**.
4. Create or open the Scenario where you want to place the copy.
5. Right-click an empty area of the canvas and select **Paste**.
6. Rename the copied Scenario, review its settings, and test it before activation.

The copied Nodes retain their routes and settings. Keep these points in mind:

- A copied **Trigger on Webhook** retains its webhook address. Change the address manually so it is unique before saving or activating the copied Scenario.
- Authorisations are retained when copying within the same account.
- Authorisations are not transferred between accounts and must be configured again in the destination account.

You can also copy selected Nodes by right-clicking a Node and choosing **Copy**, or by holding **Shift** and dragging across multiple Nodes. Paste them by right-clicking an empty area of the destination canvas and choosing **Paste**.

## Routes and conditions

A Node can have more than one outgoing route. A route can have a condition so that it only runs when the condition is met. A fallback route can handle cases where none of the other conditions match.

```text
New lead
├── Budget is high → Notify sales manager
└── Otherwise      → Send information email
```

## Development and production

Test a Scenario before activating it for real events. Depending on the trigger, Latenode may provide separate development and production behaviour. Confirm which branch, URL, schedule, or external event is being used before activation.

## Scenario types and complexity

Start with the simplest type that fits the process:

| Need | Suitable type |
|---|---|
| Always the same sequence | Linear |
| Clear field-based decisions | Conditional |
| Decisions based on meaning or tone | AI-based routing |
| AI chooses the tools and order | Agent |
| Several specialised AI roles | Multi-agent |

## Further reading

This page is based on the official [Latenode documentation](https://documentation.latenode.com/), especially [How Latenode works](https://documentation.latenode.com/get-started/quickstarts/how-it-works), [How to Build a Scenario](https://documentation.latenode.com/get-started/quickstarts/how-to-build-scenario), [Scenario Types](https://documentation.latenode.com/get-started/quickstarts/scenario-types), and [Copy Scenarios & Nodes](https://documentation.latenode.com/visual-builder/nodes/copy-nodes).
