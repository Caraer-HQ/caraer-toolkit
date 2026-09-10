# Nodes

A **Node** is one step in a Latenode Scenario. It is a visual block with clear fields that performs an action or receives an event from a connected service.

## Trigger Nodes

A **Trigger Node** starts a Scenario. It defines when the Scenario should run.

Examples include:

- a new email;
- a new message;
- a scheduled time;
- a new form or spreadsheet row;
- an incoming webhook;
- a manual run.

Every Scenario that should start automatically needs a Trigger Node.

## Action Nodes

An **Action Node** performs a step after the Trigger or another Node.

Examples include:

- send a message or email;
- add or update a spreadsheet row;
- create a task in another service;
- call an AI model or Agent;
- run JavaScript;
- query a database;
- send an HTTP request.

## Add and connect Nodes

1. Add the first Node to the canvas.
2. Add the next Node from the connector or Node picker.
3. Connect the Nodes in the order the data should flow.
4. Add a route condition when a branch should only run in certain cases.
5. Save the Scenario regularly.

## Data from earlier Nodes

Nodes pass their output to later Nodes. When configuring a field, choose the value from the data produced by an earlier Node.

If the value you need is not available, run the earlier Node once first. A Node that has not run may not yet have an example output for the next Node to use.

Run Nodes in order while building:

```text
Run Trigger → inspect output → configure Action → inspect output → continue
```

## Run a Node once

Running a Node once is useful for testing. After a Node runs, review its input, output, log, and any error information before configuring the next step.

## Required fields

Fields marked as required must be completed before a Node can run. When mapping data, choose the value that matches the field you are filling, such as a chat ID, email address, record ID, or message text.

## Routes instead of separate filter Nodes

In Latenode, filtering and routing are commonly configured on the connections between Nodes. A route can have a condition, and a Node can have multiple outgoing routes.

If no condition is added, the route runs whenever data reaches it. A fallback route can handle cases where no conditions match.

## Custom and AI Nodes

When a ready-made Node is not available, Latenode may support an HTTP Request or JavaScript Node. These options are more advanced and should be tested carefully.

AI Nodes and Agents can process information or choose tools, but they may consume more credits than a simple action. Use a clear instruction and connect only the tools that are needed.

## Further reading

See the official [How Latenode works](https://documentation.latenode.com/get-started/quickstarts/how-it-works) and [How to Build a Scenario](https://documentation.latenode.com/get-started/quickstarts/how-to-build-scenario) documentation for current interface details.
