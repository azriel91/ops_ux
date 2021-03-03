# Workflow Example

Imagine I'm your friend, and you ask me to get takeout for dinner.

Let's consider the workflow of ordering takeout.

```dot process Takeaway Sequential Process
digraph {
    node [
        fontname  = "Monospace"
        fontsize  = 10
        fixedsize = shape
        width     = 0.2
        shape     = circle
        style     = "rounded, filled"
    ]

    a [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Place Order&nbsp;</b></td></tr>
            </table>
        >]
    b [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pay&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</b></td></tr>
            </table>
        >]
    c [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fry fish&nbsp;&nbsp;&nbsp;&nbsp;</b></td></tr>
            </table>
        >]
    d [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fry chips&nbsp;&nbsp;&nbsp;</b></td></tr>
            </table>
        >]
    e [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get drink&nbsp;&nbsp;&nbsp;</b></td></tr>
            </table>
        >]
    f [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pack meal&nbsp;&nbsp;&nbsp;</b></td></tr>
            </table>
        >]
    g [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pick up food</b></td></tr>
            </table>
        >]
    h [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Deliver food</b></td></tr>
            </table>
        >]
    i [
        label = <
            <table border="0" cellborder="0" cellspacing="0">
            <tr><td align="left"><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Eat&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</b></td></tr>
            </table>
        >]

    a -> b -> c -> d -> e -> f -> g -> h -> i
}
```
