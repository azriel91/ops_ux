# Parallelism and Concurrency

```dot process Parallelism and Concurrency
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    a -> b
    a -> c

    b -> d [style = "invis"]
    c -> d

    b -> e
    d -> e

    e -> g
    f -> g
    g -> h
}
```
