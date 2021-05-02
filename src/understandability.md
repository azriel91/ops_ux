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

*"The ultimate complexity is simplicity."*

* Show useful information.
* Hide unnecessary information.
* *Could:* Show progress detail for current step, hide detail when it's done.
* Highlight important information, dim contextual information.

Example progress:

<div style="background-color: #111111; color: #ffffff; padding: 0px 5px 2px 5px; border-radius: 4px; width: 900px;">
<pre class="terminal">
<span class="shell"><span style="color: #4f4;">❯</span> </span><span class="cmd">./target/release/examples/demo</span> <span class="flag">--concurrent</span>
✅ <span style='color:#05f'><b>a</b></span> <b>Upload App</b>         [<span style='color:#0a0'>████████████████████████████████████████</span>] 26.01KiB/26.01KiB (<span style='color:#f90'>0s</span> Ok!)
<span style='color:#0a0;width:25px;display:inline-block;'>⠦⠦</span><span style='color:#05f'><b>b</b></span> <b>Create DB</b>          [<span style='color:#0aa'>███████████████████████████░<span style='color:#05f'>░░░░░░░░░░░░</span></span>] 68B/100B (<span style='color:#f90'>0s</span> 1s)
✅ <span style='color:#05f'><b>c</b></span> <b>Download App</b>       [<span style='color:#0a0'>████████████████████████████████████████</span>] 26.01KiB/26.01KiB (<span style='color:#f90'>0s</span> Ok!)
⏳ <span style='color:#05f'><b>d</b></span> <b>Link App to DB</b>     [<span style='color:#05f'><span style='opacity:0.67'>                                        </span></span>] 0/100 (queued)
⏳ <span style='color:#05f'><b>e</b></span> <b>Run App</b>            [<span style='color:#05f'><span style='opacity:0.67'>                                        </span></span>] 0/100 (queued)
<span style='color:#0a0;width:25px;display:inline-block;'>⠤⠤</span><span style='color:#05f'><b>f</b></span> <b>Allocate Domain</b>    [<span style='color:#0aa'>██████████████████████████░<span style='color:#05f'>░░░░░░░░░░░░░</span></span>] 67B/100B (<span style='color:#f90'>0s</span> 1s)
⏳ <span style='color:#05f'><b>g</b></span> <b>Attach Domain</b>      [<span style='color:#05f'><span style='opacity:0.67'>                                        </span></span>] 0/100 (queued)
⏳ <span style='color:#05f'><b>h</b></span> <b>Notify Completion</b>  [<span style='color:#05f'><span style='opacity:0.67'>                                        </span></span>] 0/100 (queued)
</pre>
</div>

Example error:


<div style="background-color: #111111; color: #ffffff; padding: 0px 5px 2px 5px; border-radius: 4px; width: 900px;">
<pre class="terminal">
<span class="shell"><span style="color: #4f4;">❯</span> </span><span class="cmd">./target/release/examples/demo</span> <span class="flag">--concurrent</span>
❌ <span style='color:#05f'><b>a</b></span> <b>Upload App</b>         [<span style='color:#555'><span style='color:#f00'>░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░</span></span>] 0B/772.42KiB (<span style='color:#f90'>0s</span>)
☠️ <span style='color:#05f'><b>b</b></span> <b>Create DB</b>          [<span style='color:#f00'><span style='opacity:0.67'>░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░</span></span>] 0/100 (parent failed)
☠️ <span style='color:#05f'><b>c</b></span> <b>Download App</b>       [<span style='color:#f00'><span style='opacity:0.67'>░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░</span></span>] 0/100 (parent failed)
☠️ <span style='color:#05f'><b>d</b></span> <b>Link App to DB</b>     [<span style='color:#f00'><span style='opacity:0.67'>░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░</span></span>] 0/100 (parent failed)
☠️ <span style='color:#05f'><b>e</b></span> <b>Run App</b>            [<span style='color:#f00'><span style='opacity:0.67'>░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░</span></span>] 0/100 (parent failed)
✅ <span style='color:#05f'><b>f</b></span> <b>Allocate Domain</b>    [<span style='color:#0a0'><span style='opacity:0.67'>████████████████████████████████████████</span></span>] 100B/100B (<span style='color:#f90'>0s</span> Unchanged)
☠️ <span style='color:#05f'><b>g</b></span> <b>Attach Domain</b>      [<span style='color:#f00'><span style='opacity:0.67'>░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░</span></span>] 0/100 (parent failed)
☠️ <span style='color:#05f'><b>h</b></span> <b>Notify Completion</b>  [<span style='color:#f00'><span style='opacity:0.67'>░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░</span></span>] 0/100 (parent failed)
<b><span style='color:#f55'>error[E06]</span>: Failed to connect to artifact server.</b>
  <span style='color:#05f'>┌─</span> artifact_server_address:1:8
  <span style='color:#05f'>│</span>
<span style='color:#05f'>1</span> <span style='color:#05f'>│</span> http://<span style='color:#f00'>127.0.0.1:8000</span>
  <span style='color:#05f'>│</span>        <span style='color:#f00'>^^^^^^^^^^^^^^</span> <span style='color:#f00'>failed to connect to server</span>
  <span style='color:#05f'>│</span>
  <span style='color:#05f'>=</span> Try running `simple-http-server --nocache -u --ip 127.0.0.1 --port 8000`.
</pre>
</div>

</div>
</details>

## API Implications

* Provide mechanism to specify end limit and progress.
* Collect information, present it in a useful way:

    - Real time interactive CLI presentation.
    - Useful errors.

`choochoo` currently uses [`indicatif`](https://github.com/mitsuhiko/indicatif/) to display progress, and [`codespan-reporting`](https://github.com/brendanzab/codespan) to display errors.

`indicatif` provides:

* Progress rendering
* Elapsed time
* Estimated time remaining
* Styling
