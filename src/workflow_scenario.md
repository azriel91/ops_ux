# Workflow Scenario

Consider the deployment steps for a standalone web application backed by a database.

The following steps represents this workflow:

```dot process Takeaway Sequential Process
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    a -> b -> c -> d -> e -> f -> g -> h
}
```
