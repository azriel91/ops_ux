# Performance / Efficiency

> How well is execution scheduled, time spent, and resources used.

```dot process Performance / Efficiency
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

## Maturity Levels

<details>
<summary><b>Sequential:</b> One thing at a time.</summary>
<div style="margin-left: 18px;">

* Very simple for troubleshooting.
* Usually already good enough.

No (extra) threads, no threading problems.

</div>
</details>

<details>
<summary><b>Coarse parallelism:</b> Make a thread per task.</summary>
<div style="margin-left: 18px;">

*"More threads means more speed right?"*

Only if you design for it.

This is like having one person allocated to each task. If your task breakdown is not good, then a person will be idling.

</div>
</details>

<details>
<summary><b>Granular concurrency:</b> Task hopping.</summary>
<div style="margin-left: 18px;">

When a threads needs to wait for something to be done for a given task, it can switch to another task &ndash; assuming the task switched to can be worked on by different threads.

</div>
</details>

## API Implications

* Use `async` to operate concurrently.
* Use multiple threads for parallelism.
* Shared data must be behind appropriate `RwLock`s.
* Can hurt API ergonomics.
* Potential for deadlock if not designed well.

`choochoo`:

* Uses `Pin<Box<dyn Future .. >>` for the function return types &ndash; tasks cannot be worked on by different threads.
* Uses `tokio` as the async executor.

## Live Demo

```bash
rm -rf /tmp/choochoo/demo/station_{b,c,d,e,f,g,h} /tmp/server/app.zip
```

```bash
time ./target/release/examples/demo
```

```bash
time ./target/release/examples/demo --concurrent
```
