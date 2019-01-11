# Pandoctools

Pandoctools is a combination of tools that help write reproducible markdown reports. They rely on Pandoc and Jupyter kernels.

**Introduction articles**:

* [**Best Python/Jupyter/PyCharm experience + report generation with Pandoc filters**](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/best_python_jupyter_pycharm_experience.md).
* [**Convenient and easily tweakable Atom+Markdown+Pandoc+Jupyter experience (can export to ipynb)**](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/atom_jupyter_pandoc_markdown.md).  


“Glueing” part of pandoctools is a profile manager of text processing pipelines. It stores short crossplatform bash scripts that define chain operations over text. They are mostly Pandoc filters but any CLI text filter is OK.


## Update instructions

(*Update instructions to v.1.3.0*)

* Switch to bash profiles as batch profiles are no longer supported (and install bash if needed),
* `results=pandoc` was a misunderstanding. The right way to output Markdown is to use  
  `from IPython.display import Markdown; Markdown('hello')`.
* Import matplotlib and feather helpers from separate modules: [matplotlibhelper](https://github.com/kiwi0fruit/matplotlibhelper), [featherhelper](https://github.com/kiwi0fruit/featherhelper),
* **v1.3.0** is not backward compatible but profiles can be easily fixed. Uninstall Pandoctools before updating. Update your custom bash scripts as names and logic changed. References: [**Default_args**](https://github.com/kiwi0fruit/pandoctools/blob/master/pandoctools/sh/Default_args), [**Kiwi**](https://github.com/kiwi0fruit/pandoctools/blob/master/pandoctools/sh/Kiwi) (profile), [**Default_pipe**](https://github.com/kiwi0fruit/pandoctools/blob/master/pandoctools/sh/Default_pipe).


# Contents

* [Pandoctools](#pandoctools)
  * [Update instructions](#update-instructions)
* [Contents](#contents)
* [Notable parts of Pandoctools](#notable-parts-of-pandoctools)
* [Examples](#examples)
* [Install](#install)
* [Useful tips (reload imported modules in Hydrogen, R kernel, LyX)](#useful-tips-reload-imported-modules-in-hydrogen-r-kernel-lyx)
* [Alternatives to R Markdown (Markdown-based Literate Programming)](#alternatives-to-r-markdown-markdown-based-literate-programming)


# Notable parts of Pandoctools

* [**Pandoc**](https://pandoc.org/), [**Jupyter**](http://jupyter.org/), [**pandoc-crossref**](https://github.com/lierdakil/pandoc-crossref) (dependence) - classical tools.
* [**Pandoctools CLI app**](https://github.com/kiwi0fruit/pandoctools/tree/master/pandoctools/cli): profile manager of text processing pipelines. It stores short bash scripts - called profiles - that define chain operations over text. They are mostly Pandoc filters but any CLI text filter is OK. Profiles can be used to convert any document of choise in the specified manner.
* [**Knitty**](https://github.com/kiwi0fruit/knitty) (dependence): Knitty is a Pandoc filter and another CLI for Stitch/Knotr: reproducible report generation tool via Jupyter, Pandoc and Markdown. Insert python code (or other Jupyter kernel code) to the Markdown document and have code's results in the output document. Can even export to Jupyter ipynb notebooks. You can use [vscode-ipynb-py-converter](https://github.com/nojvek/vscode-ipynb-py-converter) to convert .ipynb to .py to use with Knitty.
* [**SugarTeX**](https://github.com/kiwi0fruit/sugartex) (dependence): SugarTeX is a more readable LaTeX language extension and transcompiler to LaTeX.
* [**Pandas Helper**](https://github.com/kiwi0fruit/pandoctools/blob/master/pandoctools/pandas_helper) helps print dataframes to Markdown.
* (*optional*) [**Matplotlib Helper**](https://github.com/kiwi0fruit/matplotlibhelper): custom helper to tune Matplotlib experience in Atom/Hydrogen and Pandoctools/Knitty.
* (*optional*) [**Feather Helper**](https://github.com/kiwi0fruit/featherhelper): concise interface to cache 2D numpy arrays and pandas dataframes.

Pandoctools is a tool for converting markdown document. But we also need tools for writing markdown and deploying python/Jupyter code blocks.  
And the best one for it is:

* [**Atom editor with plugins**](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/atom.md). It helps easily type Unicode, interactively run highlighed python/Jupyter code blocks and instantly see results (+ completions from the running Jupyter kernel), can convert basic pandoc markdown to html with live preview.
* Must have plugins: [**SugarTeX Completions**](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/atom.md#sugartex-completions), [**Unix Filter**](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/atom.md#unix-filter), [**Hydrogen**](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/atom.md#hydrogen), [**Markdown Preview Plus**](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/atom.md#markdown-preview-plus)


# Examples

Here are [**examples**](https://github.com/kiwi0fruit/pandoctools/blob/master/examples) that demonstrate converting documents:

* from markdown `.md` with Jupyter python code blocks, SugarTeX math and cross-references to `ipynb` notebook.
* from Hydrogen/python notebook `.py` with Atom/Hydrogen code cells, Knitty markdown incerts (again with SugarTeX math and cross-references) to `.ipynb` notebook.

**Examples are given for to .ipynb conversion but Pandoctools surely capable of conversion to .html, .pdf, .md.md or any Pandoc output format.**

Extras:

* If you need to capture Matplotlib plots please see [matplotlibhelper](https://github.com/kiwi0fruit/matplotlibhelper) (the approach showed in examples there can be used with other plot libraries).


# Install

## Windows:

**_Via conda_**:

* Install [Miniconda](https://conda.io/miniconda.html),
* Install [Git together with Bash](https://git-scm.com/downloads).  
  Git is needed for writing text conversion profiles in cross-platform bash language,
* Fresh install preparations (incl. creating "myenv" conda environment):
  ```bat
  call activate root
  conda update conda
  conda create -n myenv python=3 pip setuptools

  call activate myenv
  conda update python pip setuptools
  ```
* Pandoctools installation:
  ```bat
  conda install -c defaults -c conda-forge "pip>=10.0.1" "pandoc>=2.3.1" ^
  click pyyaml pandas notebook jupyter future shutilwhich ^
  jupyter_core traitlets ipython jupyter_client nbconvert pandocfilters ^
  pypandoc psutil nbformat pandoc-attributes pywin32

  pip install pandoctools pandoctools-ready
  ```
* Install latest stable [pandoc-crossref](https://github.com/lierdakil/pandoc-crossref/releases) (compatible with pandoc version) to `<miniconda-path>/envs/myenv/Library/bin`,
* Tips:
  - if pip install fails try to change codepage: `chcp 1252`,
  - If Pandoc errors try downgrade to `"pandoc>=2.0,<2.1"` and pandoc-crossref v0.3.0.1,
  - Should be `"conda>=4.5.4"` (`conda update conda` should be enough).


**_Via pip_**:

* Install [Git together with Bash](https://git-scm.com/downloads).  
  Git is needed for writing text conversion profiles in cross-platform bash language,
* :
  ```
  pip install pandoctools pandoctools-ready
  ```
* Install latest stable [pandoc-crossref](https://github.com/lierdakil/pandoc-crossref/releases) (compatible with pandoc version) to virtual environment's `.\Scripts` folder.


## Unix:

Via conda:

* Install [Miniconda](https://conda.io/miniconda.html),
* Fresh install preparations (incl. creating "myenv" conda environment):
  ```bash
  source activate root
  conda update conda
  conda create -n myenv python=3 pip setuptools

  source activate myenv
  conda update python pip setuptools
  ```

* Pandoctools installation:
  ```bash
  conda install -c defaults -c conda-forge "pip>=10.0.1" "pandoc>=2.3.1" \
  click pyyaml pandas notebook jupyter future shutilwhich \
  jupyter_core traitlets ipython jupyter_client nbconvert pandocfilters \
  pypandoc psutil nbformat pandoc-attributes

  pip install pandoctools pandoctools-ready
  ```
* Install latest stable [pandoc-crossref](https://github.com/lierdakil/pandoc-crossref/releases) (compatible with pandoc version) to `<miniconda-path>/envs/myenv/bin`,
* Tips:
  - If Pandoc errors try downgrade to `"pandoc>=2.0,<2.1"` and pandoc-crossref v0.3.0.1,
  - Should be `"conda>=4.5.4"` (`conda update conda` should be enough).


Via pip:

* :
  ```
  pip install pandoctools pandoctools-ready
  ```
* Install latest stable [pandoc-crossref](https://github.com/lierdakil/pandoc-crossref/releases) (compatible with pandoc version) to virtual environment's `./bin` folder.


# Useful tips (reload imported modules in Hydrogen, R kernel, LyX)

[Useful tips](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/tips.md)


# Alternatives to R Markdown (Markdown-based Literate Programming)

[Alternatives to R Markdown](https://github.com/kiwi0fruit/pandoctools/blob/master/docs/alternatives_to_r_markdown.md)
