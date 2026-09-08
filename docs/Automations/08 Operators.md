# Operators

**Operators** help a Scenario inspect, compare, transform, and work with data as it moves between Nodes.

## Common uses

Operators can help you:

- compare a value with a limit;
- check whether text contains a word;
- format a date or time;
- work with numbers and mathematical values;
- count or inspect items in a list;
- use a variable in a route or Node field.

## Operators and routes

Operators are often used in conditions on routes between Nodes.

```text
Amount is greater than 1,000
→ Send the request to a manager
```

If the condition is not met, the Scenario can use another route or a fallback route.

## Choose the right operation

Before adding an Operator, identify:

1. the value you are working with;
2. whether it is text, a number, a date, or a list;
3. the result you need;
4. what should happen if the value is empty or unexpected.

Test Operators with representative data. A date, number, or text value may not behave as expected if it arrives in a different format.

See the official Latenode [Operators documentation](https://documentation.latenode.com/visual-builder/operators/operators-basics).
