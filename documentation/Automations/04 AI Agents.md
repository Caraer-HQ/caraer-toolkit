# AI Agents

AI Agents can choose which connected tools to use and in what order. They are useful when the next step depends on the meaning of a request instead of a fixed sequence of rules.

## When to use an AI Agent

Use an AI Agent when:

- the input is free text or otherwise unstructured;
- several tools may be needed;
- the order of actions can change from one request to another;
- a person would normally decide what to do next.

Use a regular Scenario when the process is predictable. A fixed flow is usually easier to test, explain, and control.

## Keep an Agent focused

- give the Agent a clear responsibility;
- connect only the tools it needs;
- describe the expected result and limits;
- protect actions that send messages, change data, or create costs;
- test normal, incomplete, and unexpected requests.

See the official Latenode guidance on [Agent Design Foundations](https://documentation.latenode.com/ai-agents/agent-design-foundations), the [AI Agent Node](https://documentation.latenode.com/ai-agents/ai-agent-node), and [Guardrails for AI Agents](https://documentation.latenode.com/ai-agents/guides-and-examples/guardrails-for-ai-agents).
