---
theme: ./simple
class: text-center
highlighter: prism
colorSchema: light
download: true
preload: true
fonts:
  sans: IBM Plex Sans
  serif: IBM Plex
  mono: Fira Code
  italic: true
info: |
  ## Simple-slidev-sample
  Simple Slidev Sample
title: Type Annotations in Python
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

<!--
Hello, my name is Gregory Kapfhammer. I'm a computer science professor and a
software engineer and I have a question: "are you a Python programmer who wants
to write high quality software? " If you are, then I hope that you will stay
tuned to this talk! It will reveal how the use of type annotations can make it easier to
add features to and find bugs in your program.

Type annotations tell both tools and developers about the kind of data stored in
a variable. If you are like me, then you might have found that these annotations
are terribly intimidating. However, I kept using type annotations in several of
my recent Python projects and now I find them tremendously informative!

I don't always add type annotations to my programs and, of course, I still get
confused and make mistakes some times. However, my current view is that
when linting and testing are combined with types and type checkers, I write
better Python programs with fewer defects.

Do you want to learn more about type annotations in Python? Are you interested
in learning to use cool new tools that improve programmer productivity? You
are? Great! Let's dive into the presentation!

The title of this talk is "Type Annotations in Python: Terribly Intimidating or
Tremendously Informative?" and it was originally given at PyOhio 2021.

In it I will share my experiences with using type annotations in a Python
project that I created recently to download information about the run of GitHub
Action workflows from GitHub's REST API.

But first, check out the `start` function at the bottom of this slide.

**Explain**:

- The talk parameter
- That Union[Fun, Info] means that the talk could either be fun or
informative
- That List[Fun, Into] suggests that the talk could be both fun and informative

Let's pick the second option in hopes that this talk is both fun and informative
for you!

-->

---

# <em>Okay</em>, what is this about?

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

<!--

Example

-->

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

<div class="ml-2 my-2">

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

[comment]: <> ( }}} )

---

[comment]: <> ( {{{ )

## Command-Line Interface

<style>
  h2 {
    font-size: 42px;
    @apply text-orange-600 mb-4;
  }
  li {
    font-size: 28px;
    margin-top: 4px;
    margin-bottom: 9px;
  }
</style>

<div class="border-2 rounded-2xl border-gray-700 bg-true-gray-300 p-5">

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

<div class="text-3xl font-bold mt-7 ml-4">

- Using type annotations, Typer can:
  - automatically generate all menus
  - perform error checking on all arguments
  - convertall arguments to the correct type

</div>

</div>

</div>

[comment]: <> ( }}} )

---

[comment]: <> ( {{{ )

# Defect Detection with Pyright

```python {all|1-3|5-8|9-10|all}
def create_results_zip_file(
    results_dir: Path, results_files: List[str]
 ) -> None:
    """Make a .zip file of all results."""
    with zipfile.ZipFile(
        "results/All-WorkKnow-Results.zip",
        "w",
    ) as results_zip_file:
        for results_file in results_files:
            results_zip_file.write(results_files)
```

<v-click>

<mdi-message-question-outline class="text-8xl absolute top-108 left-8 text-orange-600" />
<mdi-bug class="text-8xl absolute top-105 left-34 text-orange-600" />

</v-click>

[comment]: <> ( }}} )

---

[comment]: <> ( {{{ )

<v-click>

## Pyright Feedback in VS Code

<style>
  h2 {
    font-size: 42px;
    @apply text-orange-600 mb-4;
  }
  li {
    font-size: 28px;
    margin-top: 4px;
    margin-bottom: 9px;
    }
  pre {
    @apply text-3xl
  }
</style>

<div class="border-3 rounded-2xl border-gray-700 bg-true-gray-300 p-5 mb-6">

<pre>
Argument of type "List[str]" cannot be
assigned to parameter "filename" of
type "StrPath" in function "write"
</pre>

</div>

</v-click>

<v-click>

```python
with zipfile.ZipFile(
    "results/All-WorkKnow-Results.zip",
    "w",
) as results_zip_file:
    for results_file in results_files:
        results_zip_file.write(results_files)
```

</v-click>

<v-click>

<mdi-bug class="text-8xl absolute top-99 left-215 text-orange-600" />

</v-click>

<v-click>

<mdi-arrow-up class="text-6xl absolute top-118 left-175 text-orange-600" />

</v-click>

<v-click >

<div class="text-8xl ml-100 mt-5">

<code>results_file</code>

</div>

</v-click>

[comment]: <> ( }}} )

---

# Type Annotations in Python

<style>
  h1 {
    @apply text-6xl -my-2 leading-20 font-bold text-dark-100 text-orange-600;
  }
  h2 {
    @apply text-4xl leading-20 font-bold text-dark-100;
  }
  code {
    font-size: 36px;
  }
</style>

## Terribly Intimidating or Tremendously Informative?

<v-clicks>

<div class="flex row">

<uim-exclamation-triangle class="text-7xl ml-0 mt-0 text-blue-600" />

<div class="text-4xl font-medium mt-6 ml-4">
Programmers define types
</div>

</div>

<div class="flex row">

<uim-layer-group class="text-7xl ml-0 mt-8 text-blue-600" />

<div class="text-4xl font-medium mt-12 ml-4">
Automatically create command-line
</div>

</div>

<div class="flex row">

<uim-layers-alt class="text-7xl ml-0 mt-8 text-blue-600" />

<div class="text-4xl font-medium mt-12 ml-4">
Type checkers automatically find bugs
</div>

</div>

</v-clicks>

<!--

This is a note

-->
