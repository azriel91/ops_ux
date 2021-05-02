# Path Handling

> How exhaustive code path coverage is, and how each path is handled.

```dot process Workflow With Errors
digraph {
    rankdir = "LR";

    {{#include workflow_nodes_with_outcomes.dot}}
}
```

## Maturity Levels

```dot process Download App
digraph {
    {{#include graphviz/graph_settings.dot}}
    {{#include graphviz/node_c.dot}}

    c -> c_text [style = "invis"];
}
```

<details>
<summary><b>Happy Path only</b></summary>
<div style="margin-left: 18px;">

```dot process Download app happy path only
digraph {
    rankdir = "LR"

    {{#include graphviz/graph_settings.dot}}
    {{#include graphviz/node_c.dot}}

    {
        node [{{#include graphviz/node_label_shape.dot}}]
        c_success [label = <<b>✅ Downloaded</b>>, {{#include graphviz/node_style_green.dot}}];
        c_unknown [label = <<b>⁉️ Unknown</b>>, {{#include graphviz/node_style_red.dot}}];
    }

    c -> c_text [style = "invis"];
    c -> c_success;
    c -> c_unknown;
}
```

1. If it works, it works.
2. If it fails, it might crash, it might carry on with a bad value.

<details>
<summary>code snippets</summary>
<div style="margin-left: 18px;">

Bash:

```bash
#! /bin/bash
curl http://somewhere.com/app.zip -o app.zip

# Much better with:
# set -euo pipefail
```

C#:

```c#
void AppDownload()
{
    var webClient = new WebClient();
    webClient.DownloadFile("https://somewhere.com/app.zip", "app.zip");
}
```

In Rust:

```rust,ignore
fn app_download() {
    let bytes = reqwest::blocking::get("https://somewhere.com/app.zip")
        .unwrap()
        .bytes()
        .unwrap();

    let mut file = File::create("app.zip").unwrap();
    file.write_all(bytes).unwrap();
}
```

</div>
</details>

### Model Attributes

* Fast to implement / test how things should work.
* Maintenance cost scales quickly with usage.
* Difficult (costly) to diagnose failure (no logic to reply with failure information).

</div>
</details>

<details>
<summary><b>It worked vs it didn't</b></summary>
<div style="margin-left: 18px;">

Similar to "happy path only", but treat all errors the same.

To the user, this is similar to happy path only, but in code, there is effort to capture whether something worked vs it did not work.

```dot process Download app success vs error
digraph {
    rankdir = "LR"

    {{#include graphviz/graph_settings.dot}}
    {{#include graphviz/node_c.dot}}

    {
        node [{{#include graphviz/node_label_shape.dot}}]
        c_success [label = <<b>✅ Downloaded</b>>, {{#include graphviz/node_style_green.dot}}];
        c_error [
            label = <
                <table cellspacing="0" cellpadding="4" border="0">
                    <tr><td colspan="3"><b>❌ Error</b></td></tr>
                    <tr>
                        <td>ArgumentNull</td>
                        <td>WebException</td>
                        <td>NotSupported</td>
                    </tr>
                </table>
            >,
            {{#include graphviz/node_style_red.dot}}
        ];
    }

    c -> c_text [style = "invis"];
    c -> c_success;
    c -> c_error;
}
```

<details>
<summary>code snippets</summary>
<div style="margin-left: 18px;">

C#:

```c#
void AppDownload()
{
    var webClient = new WebClient();

    try { webClient.DownloadFile("https://somewhere.com/app.zip", "app.zip"); }
    catch (Exception e)
    {
        throw new System.InvalidOperationException("Failed to download app.zip", e);
    }
}
```

Rust:

```rust,ignore
fn app_download() -> Result<(), Box<dyn std::error::Error>> {
    let bytes = reqwest::blocking::get("https://somewhere.com/app.zip")?.bytes()?;

    let mut file = File::create("app.zip")?;
    file.write_all(bytes)?;
}
```

</div>
</details>

### Model Attributes

* Medium effort to implement / test how things should work.
* Maintenance cost still scales quickly with usage.
* May be difficul to diagnose failure (failure information is not suitable to pass across systems &ndash; not strongly typed).

</div>
</details>

<details>
<summary><b>99% complete<sup>1</sup> handling</b></summary>
<div style="margin-left: 18px;">

Every code path is handled; same treatment of two code paths is intentional.

```dot process Download app separate code path handling
digraph {
    rankdir = "LR"

    {{#include graphviz/graph_settings.dot}}
    {{#include graphviz/node_c.dot}}
    {{#include graphviz/node_c_outcomes.dot}}

    c -> c_text [style = "invis"];
    c -> c_error_0;
    c -> c_error_1;
    c -> c_error_2;
    c -> c_error_3;
    c -> c_error_4;
    c -> c_error_5;
    c -> c_warn_0;
    c -> c_success_0;
}
```

Every error has its own type, so at compile time you know exactly what case you are handling.

Rust supports you by having **sum types** and **exhaustive pattern matching**.

<details>
<summary>code snippets</summary>
<div style="margin-left: 18px;">

C#:

```c#
void AppDownload()
{
    var webClient = new WebClient();
    var download_failed = new System.InvalidOperationException("Failed to download app.zip", e);

    // https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadfile?view=net-5.0
    try { webClient.DownloadFile("https://somewhere.com/app.zip", "app.zip"); }
    catch (ArgumentNullException e) { throw download_failed; }
    catch (WebException e)          { throw download_failed; }
    catch (NotSupportedException e) { throw download_failed; }
}
```

Rust:

```rust,ignore
enum Error {
    Connect(reqwest::Error),
    Download(reqwest::Error),
    AppCreateFile(std::io::Error),
    AppWriteToDisk(std::io::Error),
}

fn app_download() -> Result<(), Error> {
    let bytes = reqwest::blocking::get("https://somewhere.com/app.zip")
        .map_err(Error::Connect)?
        .bytes()
        .map_err(Error::Download)?;

    let mut file = File::create("app.zip").map_err(Error::AppCreateFile)?;
    file.write_all(bytes).map_err(Error::AppWriteToDisk)?;
}
```

</div>
</details>

### Model Attributes

* Highest effort to implement.
* Maintenance cost scales slowly with usage.
* Easier to diagnose failure as the error should indicate the exact point in the sequence of events where the failure occurs.

<sup>1</sup> <sub>99% because we aren't handling running out of memory, or the power went out</sub>

</div>
</details>

## API Implications

* Any possible failing functions must return `Result`.
* So, the return type of consumer-implemented functions must be type parameterized.
* **Handle interrupts and stop gracefully.**
* `choochoo` constrains users to provide [`srcerr:SourceError<E>`](https://github.com/azriel91/srcerr), which forces consumers to have:
    - Strongly typed error codes.
    - Provide the error information that [`codespan`](https://github.com/brendanzab/codespan) can consume.

## Importance

Arguably the most important dimension for robustness &ndash; ensuring that a system is not left in an unrecoverable state.
