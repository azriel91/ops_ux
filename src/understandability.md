# Understandability

> Presentation / verbosity.

Show information when it's relevant, hide information when it's not.

## Maturity Levels

<details>
<summary><b>📃 Text, text everywhere..</b></summary>
<div style="margin-left: 18px;">

Show the user 200 MB of uncoloured logs per minute.

```text
2021-02-21T15:13:01.123 | Debug | my::krate::module | Starting application.
2021-02-21T15:13:01.325 | Info | another::krate::module | Connecting to server.
2021-02-21T15:13:01.500 | Debug | third::krate::module | Resolving DNS for `some.domain.com`.
2021-02-21T15:13:01.531 | Debug | someones::krate::module | Looking up name server for `some.domain.com`
2021-02-21T15:13:01.570 | Debug | third::krate::module | DNS Resolved to 1.2.3.4
..
```

</div>
</details>

<details>
<summary><b>🎨 Beautiful</b></summary>
<div style="margin-left: 18px;">

The ultimate complexity is simplicity.

* Show progress detail for current step, hide detail when it's done.
* Highlight important information, dim contextual information.

</div>
</details>

## API Implications

* Collect typed data, present it differently:
    - Real time interactive CLI presentation.
    - Renderable report.
* `choochoo` just deals with progress strings for now.
