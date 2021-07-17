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
> inside of Python program? Will they help me be a better Python programmer?

</div>

<br>

<div v-click>

## Intended Audience

> What are the **benefits** and **challenges** associated with using type annotations
> inside of Python program? Will they help me be a better Python programmer?

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

<div class="-ml-9">

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
What is action of <code>return urls</code> ?
</p>

</v-clicks>

---

# Python Program with Annotations

<style>
</style>

<div class="-ml-9">

```python {all|1|3|4-5|6-7|8|all}
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

---

<v-clicks>

<div class="flex row">

<uim-exclamation-triangle class="text-8xl ml-9 mt-8 text-orange-600" />

<div class="text-6xl text-true-gray-600 font-bold mt-8 ml-4">
Wait, isn't this <em>more</em> complicated?
</div>

</div>

<div class="flex row">

<uim-repeat class="text-8xl ml-9 mt-8 text-orange-600" />

<div class="text-6xl text-true-gray-600 font-bold mt-8 ml-4">
Do type annotations have <em>any</em> benefits?
</div>

</div>

<div class="flex row">

<uim-layers-alt class="text-8xl ml-9 mt-8 text-orange-600" />

<div class="text-6xl text-true-gray-600 font-bold mt-8 ml-4">
What are the trade-offs of type annotations?
</div>

</div>

</v-clicks>

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
