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

```python {all|1|2|}
def start(t: Talk) -> Union[Fun, Info]:
def start(t: Talk) -> List[Fun, Info]:
```

</v-click>

<!--

Hello, my name is Gregory Kapfhammer. I'm a computer science professor and a
software engineer and I have a question: "are you a Python programmer who wants
to write high quality software? " If you are, then I hope that you will stay
tuned to this talk! It will reveal how the use of type annotations can make it
easier to add features to your program. It will also show how types help to find
bugs in your Python code.

Type annotations tell both tools and developers about the kind of data stored in
a variable. If you are like me, then you might have found that these annotations
are terribly intimidating. However, I kept using type annotations in several of
my recent Python projects and now I find them to be tremendously informative!

I don't always add type annotations to my programs and, of course, I still get
confused and make mistakes some times. However, my current view is that
when linting and testing are combined with types and type checkers, I write
better Python programs with fewer defects.

Do you want to learn more about type annotations in Python? Are you interested
in learning to use cool new tools that improve programmer productivity? You
are? Great! Let's dive into the presentation!

The title of this talk is "Type Annotations in Python: Terribly Intimidating or
Tremendously Informative?" and it was originally given at PyOhio 2021.

In it I share my experiences with using type annotations in a Python
project that I created recently to download information about the run of GitHub
Action workflows from GitHub's REST API.

But first, check out the start function at the bottom of this slide.

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

At the start of this talk, let's ask and answer another question: what is this
presentation about?

First, the talk has two key questions:

- What are the benefits and challenges associated with using type annotations in
Python programs?
- Will types make me a better Python programmer?

I will answer both of those questions by highlighting how type annotations
helped me to recently write some Python functions.

I had you in mind when I was preparing this talk if you are an adventuresome
Python programmer who wants to explore how type annotations --- and their new
paradigm for thinking and their affiliated software tools --- can improve your
development workflow.

Don't be concerned if you have never used types before or if you found them
confusing the last time you tried to add them to your Python program. And, if
you are an programmer who frequently uses type annotations, I hope that your
adventuresome spirit will convince you to stick around since I'm hopeful that
you will learn something new in the next ten minutes.

Okay, let's explore some type annotations in Python programs!

-->

---

# Python Program without Annotations

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

<!--

Here is an example of a Python function that does not have any type annotations.
You have probably seen many functions like this when you are reading online
tutorials. This one is called extract_urls and it extracts all of the URLs from
a column of a Pandas DataFrame called df.

Let's walk through each line in this function:

**Explain each highlighted line of the function

Now that we understand the inputs, outputs, and behavior of this function, let's
ask and answer some questions about it.

- What is the type of the df parameter? Sadly, the terrible docstring for this
function does not say. If you have programmed with the Pandas package before
then you might guess that it is a data frame. However, you would have to study
other parts of the program to be sure!

The second question is:

- What is the behavior of the return urls statement in this function?
Specifically, what is the type of data that this function returns? In this
specific case, we can scan the rest of the function's source code to note that
urls is a variable of type list. However, this version of the function
does not reveal the type of the data stored in the list!

Moreover, it is important to note that if this function was a part of a more
complex Python program then it would become more difficult for a programmer to
have a full-featured understanding of the inputs, outputs, and behavior of
extract_urls.

-->

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

<!--

*Continued from previous slide*

<br>

With that said, it is important to note that if this function was a part of a
more complex Python program then it would become more difficult to have a
full-featured understanding of the inputs, outputs, and behavior of
extract_urls. For instance, if the function had more lines of code it would be
more difficult for a programmer to see that urls is a list. And, remember,
discovering that it is a list would not reveal the type of data the list stored!

-->

---

# Python Program with Annotations

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

<!--

This is a version of the extract_urls function that uses type annotations. You
will notice that the main difference between this function and the previous
version is that its signature is different. Let's take a look at it more closely
and answer some questions about its syntax and semantics.

The first question to ask and answer is:

- What is the purpose of df: pandas.DataFrame?

In response to this question, note that df is the variable and pandas.DataFrame
is the type annotation for the variable. This type annotation tells the
programmer --- and the tools used by the programmer --- that df contains tabular
data in the form of a DataFrame.

The second question is:

- How does List[str] describe the output of the extract_urls functions?

In this case, the type annotation clearly reveals that the list returned by this
function must contain string variables. The type annotation will help the
programmer to understand the function's output while also enabling tools like
type checkers to ensure that all functions calling this one store the return
value in a list designed for strings.

-->

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

<!--

When I first saw a Python function with type annotations several pressing
questions came to my mind.

First:

- Wait, isn't the function with type annotations syntactically more complicated
than the one that does not have them?

Second:

- Are there any real benefits to type annotations if they are going to take
extra time for me to write them?

And, finally:

- In the context of Python programming, what are the trade-offs of type
annotations? If they take extra time for programmers to write, can they realize
any benefits in terms of programmer productivity or software quality?

Let's investigate some of the challenges and benefits associated with adding
type annotations to our Python programs!

-->

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

<!--

Let's first address the challenges associated with regularly applying type
annotations to the functions in a Python program:

**Read the list of challenges**

In the context of program complexity it's worth noting that Python programmers
who use types will now need to become familiar with the typing package and the
types available from it, like List, Union, Dict, and others. When I first
starting adding types to my programs I spent a lot of time reading the
documentation for the typing package until I could comfortably create constructs
like type aliases and annotations for complex nested data structures.

Was it challenging? Yes, it really was! Was it worth it? Yes, I think so!

Let me tell you about some of the benefits that accrue from adding type
annotations to your Python program.

**Read the list of benefits**

One thing that I really appreciate about type annotations is that it made me
think very carefully about my data, especially when I was dealing with nested
structures like dictionaries that contains lists of dictionaries.

But some of these benefits will only be evident if you use the right tools.
Let's investigate the landscape of tool support before moving on!

- **Static versus dynamic analysis**
- **Linting versus type checking**

-->

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

<!--

*Continued from previous slide*

- **Using text editors that integrate with language servers**
- **Using the mypy type checker in your terminal window of text editor**

-->

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
