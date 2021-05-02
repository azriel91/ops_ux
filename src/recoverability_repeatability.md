# Recoverability / Repeatability

> Can execution resume from halfway.

<details open>
<summary>Workflow Steps</summary>

```dot process Recoverability
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    a [{{#include graphviz/node_style_green.dot}}]
    b [{{#include graphviz/node_style_green.dot}}]
    c [{{#include graphviz/node_style_green.dot}}]
    d [{{#include graphviz/node_style_green.dot}}]
    e [{{#include graphviz/node_style_green.dot}}]
    f [{{#include graphviz/node_style_green.dot}}]
    g [{{#include graphviz/node_style_red.dot}}]

    a -> b -> c -> d -> e -> f -> g -> h;

    person [
        label = <<table border="0" cellpadding="1" cellspacing="0">
                <tr>
                    <td rowspan = "3"><font point-size = "30">🧑</font></td>
                    <td color="#333333" border="1" valign="middle" style="rounded"><i> <font point-size = "13">O</font><font point-size = "11">OPS </font></i></td>
                </tr>
                <tr><td>&nbsp;</td></tr>
                <tr><td>&nbsp;</td></tr>
            </table>>
        fontname = "Helvetica"
        labelloc = "t"
    ]
    { rank = same; g; g_text; person; }
}
```

</details>

## Maturity Levels

<details>
<summary><b>🧹 Need manual clean up, <i>then</i> restart from scratch.</b></summary>
<div style="margin-left: 18px;">

Usually takes effort to:

* Find out what needs cleaning up.
* Figure out how to clean up, and do it.

This will happen again.

</div>
</details>

<details>
<summary><b>🔁 Restart from scratch.</b></summary>
<div style="margin-left: 18px;">

Tooling can automatically clean up for you.

Maybe you want to keep the failing environment around for investigation.

</div>
</details>

<details>
<summary><b>♻️ Reuse and recycle</b></summary>
<div style="margin-left: 18px;">

```dot process Recoverability
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    g [{{#include graphviz/node_style_green.dot}}]

    a -> b -> c -> d -> e -> f -> g -> h;

    person [
        label = <<table border="0" cellpadding="1" cellspacing="0">
                <tr>
                    <td rowspan = "3"><font point-size = "30">🧑</font></td>
                    <td color="#333333" border="1" valign="middle" style="rounded"><i> <font point-size = "13">Y</font><font point-size = "11">AY </font></i></td>
                </tr>
                <tr><td>&nbsp;</td></tr>
                <tr><td>&nbsp;</td></tr>
            </table>>
        fontname = "Helvetica"
        labelloc = "t"
    ]
    { rank = same; g; g_text; person; }
}
```

* If it's already done, we won't do it again.
* Replace / update existing resources.
* Dependency updates must be propagated.

    - Re-download file if it changed.
    - Restart the web application if configuration changed.

This means if we fail at 90% / 2 hours into the process, we can restart at that point without waiting another 2 hours.

</div>
</details>

## API Implications

* Implementors should provide a "check" function, and a "do it" function.
* The check function checks if the task is in the desired state.
* If not, the do it function is called.

`choochoo`:

* Requires a `visit_fn` ("do it" function).
* `check_fn` is run if present, otherwise it always runs the `visit_fn`.
* **Bonus:** The check function is run after the visit function to detect if the logic is correct.
