# State Visibility

> What state is it in now, progress tracking.

Is enough information captured and presented.

## Maturity Levels

<details>
<summary><b>Zero Visibility:</b> It's running vs it's not.</summary>
<div style="margin-left: 18px;">

```dot process Progress Tracking
digraph {
    {{#include graphviz/graph_settings.dot}}
    {{#include graphviz/node_a.dot}}

    a [label = <<b>?</b>>, color = "#333355", fillcolor = "#aaaacc"]
    a_text [label = ".."]

    a -> a_text [style = "invis"]

    person [
        label = <<table border="0" cellpadding="1" cellspacing="0">
                <tr>
                    <td rowspan = "3"><font point-size = "30">🧑</font></td>
                    <td color="#333333" border="1" valign="middle" style="rounded"><i> <font point-size = "13">M</font><font point-size = "11">AYBE IT'S FROZEN&nbsp;</font></i></td>
                </tr>
                <tr><td>&nbsp;</td></tr>
                <tr><td>&nbsp;</td></tr>
            </table>>
        fontname = "Helvetica"
        labelloc = "t"
    ]
    {rank = same; a; a_text; person;}
}
```

</div>
</details>

<details>
<summary><b>Imperative:</b> You can see the completed steps, but not necessarily remaining steps.</summary>
<div style="margin-left: 18px;">

```dot process Progress Tracking
digraph {
    {{#include graphviz/graph_settings.dot}}
    {{#include graphviz/node_a.dot}}
    {{#include graphviz/node_b.dot}}
    {{#include graphviz/node_c.dot}}
    {{#include graphviz/node_d.dot}}

    a [{{#include graphviz/node_style_green.dot}}]
    b [{{#include graphviz/node_style_green.dot}}]
    c [color = "#6688ee", fillcolor = "#99ddff"]
    d_text [label = ".."]
    d [label = <<b>?</b>>, color = "#333355", fillcolor = "#aaaacc"]

    a -> a_text [style = "invis"];
    a -> b -> c -> d;

    person [
        label = <<table border="0" cellpadding="1" cellspacing="0">
                <tr>
                    <td rowspan = "3"><font point-size = "30">🧑</font></td>
                    <td color="#333333" border="1" valign="middle" style="rounded"><i> <font point-size = "13">N</font><font point-size = "11">EXT NEXT&nbsp;</font></i></td>
                </tr>
                <tr><td>&nbsp;</td></tr>
                <tr><td>&nbsp;</td></tr>
            </table>>
        fontname = "Helvetica"
        labelloc = "t"
    ]
    {rank = same; c; c_text; person;}
}
```

<details>
<summary>If it fails, you will be able to see how far it got.</summary>
<div style="margin-left: 18px;">

```dot process Naive Workflow Failure
digraph {
    {{#include graphviz/graph_settings.dot}}
    {{#include graphviz/node_a.dot}}
    {{#include graphviz/node_b.dot}}
    {{#include graphviz/node_c.dot}}
    {{#include graphviz/node_d.dot}}

    a [{{#include graphviz/node_style_green.dot}}]
    b [{{#include graphviz/node_style_green.dot}}]
    c [{{#include graphviz/node_style_green.dot}}]
    d [color = "#dd7755", fillcolor = "#ff9977"]

    a -> a_text [style = "invis"];
    a -> b -> c -> d;

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
    {rank = same; d; d_text; person;}
}
```

</div>
</details>
<br/>
</div>
</details>

<details>
<summary><b>Planner:</b> The steps to completion are known, and progress is shown.</summary>
<div style="margin-left: 18px;">

```dot process Progress Tracking
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    a [{{#include graphviz/node_style_yellow.dot}}]
    b [{{#include graphviz/node_style_green.dot}}]
    c [{{#include graphviz/node_style_green.dot}}]
    d [color = "#dd7755", fillcolor = "#ff9977"]

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
    {rank = same; d; d_text; person;}
}
```

</div>
</details>

## API Implications

* Need overall execution plan steps.
* Additional steps discovered at runtime are "sub-steps".
* Elapsed duration is essential.
* Accurate estimated duration remaining is nice, but can be difficult to provide.
