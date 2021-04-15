# Naive

The simple model &ndash; I do as you ask.

```dot process Naive Workflow
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    a -> b -> c -> d -> e -> f -> g -> h
}
```


## Usage And Outcomes

<details>
<summary>✅ All goes well.</summary>
<div style="margin-left: 18px;">

🍛 We get to eat

</div>
</details>

<details>
<summary>⚠️ You send me two messages.</summary>
<div style="margin-left: 18px;">

* **A:** Prepare two dinners.
* **B:** Panic and do nothing.

</div>
</details>

<details>
<summary>❌ I burn the rice.</summary>
<div style="margin-left: 18px;">

* **A:** Serve you the burnt rice.
* **B:** Panic and do nothing.

    You only realize there is no dinner when I take too long.

</div>
</details>

## Model Attributes

* Fast to implement / test how things should work.
* Maintenance cost scales quickly with usage.
* Difficult (costly) to diagnose process failure.
