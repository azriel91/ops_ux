# Workflow Scenario

Imagine I'm your friend, and you ask me to prepare dinner.

The following steps represents this workflow:

```dot process Takeaway Sequential Process
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    a -> b -> c -> d -> e -> f -> g -> h
}
```
