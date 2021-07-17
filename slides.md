---
theme: ./simple
class: text-center
highlighter: prism
colorSchema: 'light'
download: true
preload: false
fonts:
  # basically the text
  sans: 'IBM Plex Sans'
  # use with `font-serif` css class from windicss
  serif: 'IBM Plex'
  # for code blocks, inline code, etc.
  mono: 'Fira Code'
info: |
  ## Simple-slidev-sample
  Simple Slidev Sample
---

# Type Annotations in Python

<style>
  code {
    font-size: 36px;
  }
</style>

## Terribly Intimidating or Tremendously Informative?

<div class="container my-1">
 &nbsp;
</div>

### Gregory M. Kapfhammer

### PyOhio 2021

<div class="container my-5">
 &nbsp;
</div>

<v-click>

```python {all|1|2|all|2}
def start(t: Talk) -> Union[Fun, Info]:
def start(t: Talk) -> List[Fun, Info]:
```

</v-click>

---

# <em>Okay</em>, what will I learn?

<style>
  h2 {
    font-size: 36px;
    @apply text-orange-600 mb-4;
  }
</style>

<br>

<div v-click>

## Key Questions

> What are the **benefits** and **challenges** associated with using type annotations
> inside of Python program? Will types make me be a better programmer?

</div>

<br>

<div v-click>

## Intended Audience

> An **adventuresome** Python programmer who wants to explore how a both new
> **paradigm** and software **tools** can improve their development skills!

</div>

<div v-click>

<div class="flex row">

<uim-rocket class="text-6xl ml-8 mt-5 text-blue-600" />

<div class="text-3xl font-bold mt-8 ml-4">
Let's explore type annotations in Python programs!
</div>

</div>

</div>

---

# Python Program without Annotations

<style>
</style>

<div class="-ml-0">

```python {all|1|3|4-5|6-7|8|all}
def extract_urls(df):
    """Extract a list of urls."""
    urls = []
    if "Url" in df.columns:
        urlc = df["Url"]
        if urlc is not None:
            urls = urlc.tolist()
    return urls
```

</div>

<br>

<v-clicks>

<p class = "bold">
What is the type of <code>df</code> ? The terrible docstring does not say!
</p>

<p class = "bold">
What is behavior of <code>return urls</code> in this function?
</p>

</v-clicks>

---

# Python Program without Annotations

<style>
</style>

<div class="-ml-0">

```python
def extract_urls(df):
    """Extract a list of urls."""
    urls = []
    if "Url" in df.columns:
        urlc = df["Url"]
        if urlc is not None:
            urls = urlc.tolist()
    return urls
```

</div>

<br>

<div v-click>

<div class="flex row">

<uim-refresh class="text-6xl ml-2 mt-4 text-orange-600" />

<div class="text-3xl font-bold mt-8 ml-4">
What happens if the program becomes more complex?
</div>

</div>

</div>


---

# Python Program with Annotations

<style>
</style>

<div class="-ml-9">

```python {all|1}
def extract_urls(df: pandas.DataFrame) -> List[str]:
    """Extract a list of urls."""
    urls = []
    if "Url" in df.columns:
        urlc = df["Url"]
        if urlc is not None:
            urls = urlc.tolist()
    return urls
```

</div>

<br>

<v-clicks>

<p class = "bold">
What is the purpose of <code>df: pandas.DataFrame</code> ?
</p>

<p class = "bold">
How does <code>List[str]</code> describe output of <code>extract_urls</code> ?
</p>

</v-clicks>

[comment]: <> ( {{{ )

---


<div class="flex row">

<uim-exclamation-triangle class="text-8xl ml-9 mt-8 text-orange-600" />

<div class="text-6xl text-true-gray-600 font-bold mt-8 ml-4">
Wait, isn't this more complicated?
</div>

</div>

<v-clicks>

<div class="flex row">

<uim-repeat class="text-8xl ml-9 mt-8 text-orange-600" />

<div class="text-6xl text-true-gray-600 font-bold mt-8 ml-4">
Do type annotations have any benefits?
</div>

</div>

<div class="flex row">

<uim-layers-alt class="text-8xl ml-9 mt-8 text-orange-600" />

<div class="text-6xl text-true-gray-600 font-bold mt-8 ml-4">
What are the trade-offs of type annotations?
</div>

</div>

</v-clicks>

[comment]: <> ( }}} )

---

<div class="ml-8 grid grid-cols-2 gap-19">
<div>

<v-click>

# Challenges

<style>
  li {
  font-size: 22px;
  margin-bottom: 10px;
  }
</style>

- *Readability* : function signatures are more difficult to read
- *Productivity* : programmer often must add type annotations
- *Complexity* : programs use many new classes and types

</v-click>

</div>

<div>

<v-click>

# Benefits

- *Fail-fast* : quickly catch errors before running Python programs
- *Tooling* : text editors signal problems to programmers
- *Understanding* : developers understand the structure of data

</v-click>

</div>
</div>

<div v-click-hide="6">

<div v-click>

<div class="flex row">

<uim-stethoscope class="text-6xl ml-8 mt-5 text-blue-600" />

<div class="text-3xl font-bold mt-8 ml-4">
Software tools for static or dynamic analysis
</div>

</div>

</div>

<div v-click>

<div class="flex row">

<uim-microscope class="text-6xl ml-8 mt-5 text-blue-600" />

<div class="text-3xl font-bold mt-8 ml-4">
Difference between linting and type checking
</div>

</div>

</div>

</div>

---

<div class="ml-8 grid grid-cols-2 gap-19">
<div>

# Challenges

<style>
  li {
  font-size: 22px;
  margin-bottom: 10px;
  }
</style>

- *Readability* : function signatures are more difficult to read
- *Productivity* : programmer often must add type annotations
- *Complexity* : programs use many new classes and types

</div>

<div>

# Benefits

- *Fail-fast* : quickly catch errors before running Python programs
- *Tooling* : text editors signal problems to programmers
- *Understanding* : developers understand the structure of data

</div>
</div>

<div v-click>

<div class="flex row">

<uim-visual-studio class="text-6xl ml-8 mt-5 text-blue-600" />

<div class="text-3xl font-bold mt-8 ml-4">
Pyright language server in VS Code or Neovim
</div>

</div>

</div>

<div v-click>

<div class="flex row">

<uim-grid class="text-6xl ml-8 mt-5 text-blue-600" />

<div class="text-3xl font-bold mt-8 ml-4">
Mypy static type checker in terminal or editor
</div>

</div>

</div>

[comment]: <> ( {{{ )

---

<v-clicks>

<div class="flex row">

<uim-layer-group class="text-8xl ml-9 mt-8 text-orange-600" />

<div class="text-6xl text-true-gray-600 font-bold mt-8 ml-4">
Easy command-line interface with Typer
</div>

</div>

<div class="flex row">

<uim-line class="text-8xl ml-9 mt-8 text-orange-600" />

<div class="text-6xl text-true-gray-600 font-bold mt-8 ml-4">
Quickly find a defect that crashes a program
</div>

</div>

<div class="flex row">

<uim-github class="text-8xl ml-9 mt-8 text-blue-600" />

<div class="text-5xl text-true-gray-600 font-bold mt-15 ml-4">
AnalyzeActions/WorkKnow
</div>

</div>

</v-clicks>

[comment]: <> ( }}} )

---

[comment]: <> ( {{{ )

# Command-Line Interface with Typer

<style>
</style>

<div class="-ml-0 my-2">

```python {all|1|2|3-4|5|6-8|9|10-11|all}
import python
cli = typer.Typer()
@cli.command()
def download(
    repo_urls: List[str],
    repos_csv_file: Path = typer.Option(None),
    results_dir: Path = typer.Option(None),
    env_file: Path = typer.Option(None),
    save: bool = typer.Option(False),
    debug_level: debug.DebugLevel =
         debug.DebugLevel.ERROR,
):
```

</div>

[comment]: <> ( }}} )

---

[comment]: <> ( {{{ )

# Defining the <code>DebugLevel</code> Enumeration

<br>

```python {all|0}
from enum import Enum
```

```python {0|all|0}
from workknow import constants
```

```python {all|1-2|4-9|all}

class DebugLevel(str, Enum):
    """The predefined levels for debugging."""

    DEBUG = constants.logging.Debug
    INFO = constants.logging.Info
    WARNING = constants.logging.Warning
    ERROR = constants.logging.Error
    CRITICAL = constants.logging.Critical
```

---

## Command-Line Interface

<style>
  h2 {
    font-size: 42px;
    @apply text-orange-600 mb-4;
  }
  li {
  font-size: 28px;
  margin-bottom: 9px;
  }
</style>

<div class="border rounded-2xl border-gray-600 bg-true-gray-300 p-5">

<pre>
Usage: workknow download [OPTIONS] REPO_URLS...
  Download the GitHub Action workflow history of repositories.
Arguments:
  REPO_URLS...  [required]
Options:
  --repos-csv-file PATH
  --results-dir PATH
  --env-file PATH
  --peek / --no-peek              [default: False]
  --save / --no-save              [default: False]
  --debug-level [DEBUG|INFO|WARNING|ERROR|CRITICAL]
                                  [default: ERROR]
  --help                          Show this message and exit.
</pre>

</div>

<div v-click>

<div class="flex row">

<uim-rocket class="text-9xl ml-5 mt-5 text-blue-600" />

<div class="text-3xl font-bold mt-8 ml-4">

- With type annotations, Typer can:
  - automatically generates all menus
  - performs error checking on all arguments
  - converts all arguments to the correct type

</div>

</div>

</div>

[comment]: <> ( }}} )
