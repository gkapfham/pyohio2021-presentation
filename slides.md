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

```python {all}
def start(t: Talk) -> List[Fun, Learn]:
```

<!--

Hello, my name is Gregory Kapfhammer. I'm a computer science professor and a
software engineer and I have a question: "are you a Python programmer who wants
to write high quality software? " If you are, then I hope that you will stay
tuned to this talk! It will reveal how the use of type annotations can make it
easier to add features to your program. It will also show how types help to find
bugs in your Python code.

Type annotations tell both tools and developers about the kind of data stored in
a variable. If you are like me, then you might have found that these annotations
are terribly intimidating. However, I kept us¡ng type annotations in several of
my recent Python projects and now I find them to be tremendously informative!

I don't always add type annotations to my programs and, of course, I still get
confused and make mistakes some times. However, my current view is that
when linting and testing are combined with types and type checkers, I write
better Python programs with fewer defects.

Do you want to learn more about type annotations in Python? Are you interested
in learning to use cool new tools that improve programmer productivity? Let's
dive into the presentation!

The title of this talk is "Type Annotations in Python: Terribly Intimidating or
Tremendously Informative?" and it was originally given at PyOhio 2021.

In it I share my experiences with using type annotations in a Python
project that I created recently to download information about the run of GitHub
Action workflows from GitHub's REST API.

**CUT IN SHORT VERSION**

But first, check out the start function at the bottom of this slide.

**Explain**:

- The talk parameter
- That Union[Fun, Info] means that the talk could either be fun or informative
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
> inside of Python program? Will types make me a better programmer?

</div>

<br>

<div v-click>

## Intended Audience

> An **adventuresome** Python programmer who wants to explore how both a new
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
What is the behavior of <code>return urls</code> in this function?
</p>

</v-clicks>

<!--

Here is an example of a Python function that does not have any type annotations.
You have probably seen many functions like this when you are reading online
tutorials. This one is called extract_urls and it extracts all of the URLs from
a column of a variable called df.

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

<div class="flex row">

<uim-refresh class="text-6xl ml-2 mt-4 text-orange-600" />

<div class="text-3xl font-bold mt-8 ml-4">
What happens if the program becomes more complex?
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
discovering that it is a list would not reveal the type of data that the list
stores!

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

# Challenges

<style>
  li {
  font-size: 22px;
  margin-bottom: 10px;
  }
</style>

- *Readability* : function signatures are more difficult to read
- *Productivity* : programmers often must add type annotations
- *Complexity* : programs use many new classes and types

</div>

<div v-click>

<div>

# Benefits

- *Fail-fast* : quickly catch errors before running Python programs
- *Tooling* : text editors signal problems to programmers
- *Understanding* : developers understand the structure of data

</div>

</div>

</div>

<div v-click>

<div class="flex row">

<uim-visual-studio class="text-6xl ml-8 mt-5 text-blue-600" />

<div class="text-3xl font-bold mt-8 ml-4">
Pyright language server in VS Code and Neovim
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

Let's first address the challenges associated with regularly applying type
annotations to the functions in a Python program:

**[[Read the list of challenges]]**

Let me also tell you about some of the benefits that accrue from adding type
annotations to your Python program.

**[[Read the list of benefits]]**

Some of these benefits will only be evident if you use the right tools.
Let's investigate the landscape of tool support before moving on!

- **Using text editors that integrate with language servers**
- **Using the mypy type checker in your terminal window of text editor**

In my experience, Pyright and mypy are exceptional tools that have detected many
defects in my code before I ran either the test suite or the program itself.

**CUT IN SHORT VERSION**

For my recent Python projects, I setup Pyright to run asynchronously in Neovim
and to highlight problems as soon as they are detected. I also run mypy in my
terminal window and in GitHub actions whenever I push a commit to a branch.

**Full screen video -- CUT IN SHORT VERSION**

Okay, let's recap where we're at in this talk!

I acknowledge that it has taken time for me to understand better how to
interpret the output of these tools -- and to know when to ignore their output!
However, I've seen evidence that they help me write better Python programs.

In the remainder of the talk I want to highlight some of my experiences in
building a Python program with type annotations. Specifically, I want to show
you how using type annotations can give you features "nearly for free" and help
you to find bugs very quickly. If you check the notes for this video on YouTube
you will see references to the project I built. Check out the source code that I
wrote and share your feedback on either YouTube or GitHub!

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

<!--

In the remainder of this talk I'm going to use source code and type checker
output to tell you two stories!

- **Read the command-line interface comment**
- **Read the defect finding comments**

The experiences that I share in this talk took place in the context of building
an open-source program, called WorkKnow, that keeps you "in the know" about the
history of workflow builds on GitHub Actions. WorkKnow uses GitHub's REST API to
download the history of workflow executions. It then extracts, parses, and
summarizes the data and stores the most important results in CSV files.

**CUT IN SHORT VERSION**

I'm building and using WorkKnow because it helps me to gain insights into the
trends evident in both my GitHub action workflows and the workflows of popular
projects that leverage GitHub Actions.

If you would like to try out WorkKnow you can find it in the AnalyzeActions
organization on GitHub. Even though the tool is in a very early stage of
development, I hope that you will try it out, raise issues, and add new
features.

Okay, let's dive into my experience with using type annotations to build this
tool!

-->

---

# Command-Line Interface with Typer

<div class="ml-2 my-2">

```python {all|1-4|5|6-8|all}
import typer
cli = typer.Typer()
@cli.command()
def download(
    repo_urls: List[str],
    repos_csv_file: Path = typer.Option(None),
    results_dir: Path = typer.Option(None),
    env_file: Path = typer.Option(None),
):
```

</div>

<v-click>

<div class="flex row">

<uim-github class="text-7xl ml-0 mt-0 text-blue-600" />

<div class="text-4xl font-medium mt-6 ml-4">
See <code>AnalyzeActions/WorkKnow</code> for details!
</div>

</div>

</v-click>

<!--

Let's create a command-line interface for WorkKnow.

If you have not yet tried the Typer package for the construction of command-line
interfaces in Python then you should right away! It is awesome!

Now we can review this source code segment to better understand how Typer works
and how it uses type annotations.

<br>

**Review each highlighted line of source code.**

- The first four lines of the function import typer and designate that the
download will be one of the program's main commands

- Download's first parameter is a list of GitHub repository URLs with builds to
analyze

- The next three parameters are pathlib Path objects to files and directories
that WorkKnow needs to collect inputs and save output

WorkKnow's command-line interface also accepts other arguments. Checkout its
GitHub repository for more details!

-->

---

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
  - convert all arguments to the correct type

</div>

</div>

</div>

<!--

This is what would appear in your terminal window if you typed "workknow
download --help". It is important to stress that:

<br>

**Transition to and explain the bottom list on the slide.**

- Using type annotations, Typer can automatically generate all of the menus,
like the one you see here.

- Since Typer know the type of each command-line argument it can perform error
checking to make sure that a person definitely uses the right arguments.

- Amazingly, Typer can also convert all of the strings that a person passes into
the program on the command-line into the correct type for the program! For
instance, if the program accepts a string that points to the directory in which
WorkKnow should store the data, then Typer will convert that string to a pathlib
Path without any effort on the part of the programmer! Fantastic!

**CUT IN SHORT VERSION**

, for instance, a string or a boolean in the right order and for the right
parameter. If you have ever built a command-line interface using argparse then
you probably remember how long it took you to write the error-prone code that
verifies the arguments. Now, as long as you add the type of each variable, Typer
can do all of this work for you!

- Finally, did you notice how Typer will only allow a person to specify specific
values for the debugging level command-line argument. Again, this feature is due
to the fact that source code stipulated that it was of the type DebugLevel.

-->

---

# Defect Detection with Pyright

```python {all}
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

<!--

One of WorkKnow's features is that it can create a ZIP file of all the results
that it saves about the history of GitHub Action workflows for different
projects. This feature has come in handy when the data that it downloads is too
large to send to someone on a per-file basis.

When I first wrote this function, I did so in the way that you see right now.
That leads me to my next question:

- Can you find the bug in this program?

Thankfully, Pyright can find it for us!

**CUT IN SHORT VERSION**

After walking through the source code for this function, I have a story to tell
you about how type annotations helped me to implement it correctly!

**Explain each line of source code in the function.**

Although I acknowledge that the defect is a small one and that, in fact, I would
have been able to find it without using type annotations and type checkers, I'm
delighted to report that pyright found it for me immediately! I appreciate
pyright because it works asynchronously in the background, pointing out likely problems
while I focus on the next feature or test that I want to write.

-->

---

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

<!--

Let's take a look at the error message that Pyright shared with me!

**Read the error message.**

As soon as I read this message I realized that I need to focus on the call to
the write function and the parameter that I passed to it. After contemplating
Pyright's error again, I realized that I had made a mistake by passing
results_files, a list containing strings, instead of results_file, the specific
file, to the write function.

Yep, one extra s would have caused a major problem when I either ran the test
suite or the program itself! Of course, it is reasonable to ask whether or not I
would have found this bug by other means. Yes, I think that I would have! But,
it was nice to find it so quickly through the use of type annotations and the
Pyright type checker.

-->

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

So, what have I introduced in this talk?

First, I showed you how a programmer can define type annotations in their Python
program. Although these annotations take time to add and can make a program
appear more complex, they have a myriad of benefits!

For instance, when you use the Typer package it will automatically create a
robust and well-documented command line interface! Make sure that you search
for Typer and read its the exceptional documentation.

The talk also showed how typer checkers can automatically find bugs.

-->

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

## Yes, they are Tremendously Informative! Try them!

<v-clicks>

<div class="flex row">

<uim-github class="text-7xl ml-0 mt-0 text-blue-600" />

<div class="text-4xl font-medium mt-6 ml-4">
AnalyzeActions/WorkKnow
</div>

</div>

<div class="flex row">

<uim-comment-dots class="text-7xl ml-0 mt-8 text-blue-600" />

<div class="text-4xl font-medium mt-12 ml-4">
https://www.gregorykapfhammer.com/
</div>

</div>

<div class="flex row">

<uim-github class="text-7xl ml-0 mt-8 text-blue-600" />

<div class="text-4xl font-medium mt-12 ml-4">
gkapfham/pyohio2021-presentation
</div>

</div>

</v-clicks>

<!--

I'm hoping that you are now saying to yourself that, yes, type annotations in
Python are tremendously informative!

Whether or not you are now convinced of this fact, I hope that you will try them
soon. If you want see a Python program that is using type annotations, check out
WorkKnow's GitHub repository.

Once you have formed your own opinion about type annotations, I hope that you
will get in touch with me through my web site and leave a comment on YouTube.

Oh, one last thing! Are you interested in seeing the source code for my slides?
If so, please check the GitHub repository for their source code!

Okay, thanks for your attention! Now, get out there and write some Python code
with type annotations!

-->
