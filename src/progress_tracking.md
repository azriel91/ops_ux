# Progress Tracking

You roughly know where things are up to.

<details open>
<summary>You can see the completed steps, but not necessarily remaining steps.</summary>
<div style="margin-left: 18px;">

```dot process Progress Tracking
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    a [{{#include graphviz/node_style_green.dot}}]
    b [{{#include graphviz/node_style_green.dot}}]
    c [{{#include graphviz/node_style_green.dot}}]
    d [color = "#6688ee", fillcolor = "#99ddff"]
    e_text [label = ".."]
    e [label = <<b>?</b>>, color = "#333355", fillcolor = "#aaaacc"]
    f [style = "invis"]
    f_text [style = "invis"]
    g [style = "invis"]
    g_text [style = "invis"]
    h [style = "invis"]
    h_text [style = "invis"]

    a -> b -> c -> d -> e;

    chef [
        label = <<table border="0" cellpadding="1" cellspacing="0">
                <tr>
                    <td rowspan = "3"><font point-size = "30">🧑‍🍳</font></td>
                    <td color="#333333" border="1" valign="middle" style="rounded"><i> <font point-size = "13">H</font><font point-size = "11">EAT THE MEAT&nbsp;</font></i></td>
                </tr>
                <tr><td>&nbsp;</td></tr>
                <tr><td>&nbsp;</td></tr>
            </table>>
        fontname = "Helvetica"
        labelloc = "t"
    ]
    {rank = same; d; d_text; chef;}
}
```

</div>
</details>

<details open>
<summary>If it fails, you will be able to see how far it got.</summary>
<div style="margin-left: 18px;">

```dot process Naive Workflow Failure
digraph {
    {{#include workflow_nodes_with_labels.dot}}

    a [{{#include graphviz/node_style_green.dot}}]
    b [{{#include graphviz/node_style_green.dot}}]
    c [{{#include graphviz/node_style_green.dot}}]
    d [color = "#dd7755", fillcolor = "#ff9977"]
    e [style = "invis"]
    e_text [style = "invis"]
    f [style = "invis"]
    f_text [style = "invis"]
    g [style = "invis"]
    g_text [style = "invis"]
    h [style = "invis"]
    h_text [style = "invis"]

    a -> b -> c -> d;

    chef [
        label = <<table border="0" cellpadding="1" cellspacing="0">
                <tr>
                    <td rowspan = "3"><font point-size = "30">🧑‍🍳</font></td>
                    <td color="#333333" border="1" valign="middle" style="rounded"><i> <font point-size = "13">O</font><font point-size = "11">OPS </font></i></td>
                </tr>
                <tr><td>&nbsp;</td></tr>
                <tr><td>&nbsp;</td></tr>
            </table>>
        fontname = "Helvetica"
        labelloc = "t"
    ]
    {rank = same; d; d_text; chef;}
}
```

</div>
</details>

## Model Attributes

* TODO
