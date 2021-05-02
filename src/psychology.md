# Psychology

> Did the user request what they intended?

Does the software understand the *intent* of the user?

a.k.a. Can the developer predict intent ahead of time?

## Maturity Levels

```bash
# User: "create 100 servers"
choochoo deploy --server-count 100
```

<details>
<summary><b>Do as they say. Every time.</b></summary>
<div style="margin-left: 18px;">

Want 100 servers? Sure.

</div>
</details>

<details>
<summary><b>Guess desired state.</b></summary>
<div style="margin-left: 18px;">

There's already 10 servers, so I'll just add 90 more.

</div>
</details>

<details>
<summary><b>Protect from extreme values.</b></summary>
<div style="margin-left: 18px;">

<div style="background-color: #111111; color: #ffffff; padding: 0px 5px 2px 5px; border-radius: 4px;;">
<pre class="terminal">
<span class="shell"><span style="color: #4f4;">❯</span> </span><span class="cmd">choochoo deploy</span> <span class="flag">--server-count 100</span>
<b><span style='color:#ff0'>warning[W02]</span>: High server count.</b>
  <span style='color:#05f'>┌─</span> command:1:16
  <span style='color:#05f'>│</span>
<span style='color:#05f'>1</span> <span style='color:#05f'>│</span> choochoo deploy <span style='color:#ff0'>--server-count 100</span>
  <span style='color:#05f'>│</span>                 <span style='color:#ff0'>^^^^^^^^^^^^^^^^^^</span> <span style='color:#ff0'>specified here</span>
  <span style='color:#05f'>│</span>
  <span style='color:#05f'>=</span> This can incur high costs.
  <span style='color:#05f'>=</span> Specify the `--allow-high-server-count` flag to bypass this check.<br />
  🚂 Please type `<span style='color:#ff0;'>pancakes</span>` to proceed:
  <span class="shell"><span style="color: #ff0;">❯</span> pancakes_</span>
</pre>
</div>

</div>
</details>

## API Implications

* Provide types with value limit checking.
* Detect long elapsed time, and support graceful interrupt handling.
* Design for dry run &ndash; show what the software *would* do.

`choochoo` doesn't do this yet.
