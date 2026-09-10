# Data Flow

**Data Flow** describes how information moves through a Latenode Scenario. A Trigger or Node produces output, and later Nodes use that output as input.

```text
Trigger output → next Node input → next Node output
```

## Passing data between Nodes

When configuring a field in a Node:

1. open the data available from earlier Nodes;
2. choose the value you need;
3. place it in the target field;
4. run the Node and check the result.

The data panel can include values from multiple earlier Nodes, not only the immediately previous Node.

## Run Nodes in order

Run the Node that provides the data before configuring the Node that consumes it. If an earlier Node has not run, its output may be unavailable or appear as an empty value.

```text
Run Trigger → inspect output → configure next Node → run next Node
```

## Branches

Data can follow different routes. Each route may have a condition, allowing the Scenario to branch based on the information received.

```text
New request
├── Status is urgent → Notify the team
└── Otherwise        → Add to the normal queue
```

## Check the data

After a Node runs, review its input, output, log, and errors. Check that:

- the expected fields are present;
- values have the expected format;
- the next Node receives the correct information;
- empty or unexpected values are handled safely.

See the official Latenode documentation for [Passing Data](https://documentation.latenode.com/visual-builder/data-flow/passing-data), [Iterating](https://documentation.latenode.com/visual-builder/data-flow/iterating), and [Handling Files](https://documentation.latenode.com/visual-builder/data-flow/handling-files).
