
**NEW:** For html, equation numbers are now written into a span and justified right.  Also: Equation numbers by section in LaTeX/pdf and html.


pandoc-eqnos 0.16
=================

*pandoc-eqnos* is a [pandoc] filter for numbering equations and equation references in processed markdown documents.  A cross-referencing syntax is added to markdown for this purpose.

Demonstration: Processing [demo3.md] with `pandoc --filter pandoc-eqnos` gives numbered equations and references in [pdf][pdf3], [tex][tex3], [html][html3], [epub][epub3], [md][md3] and other formats.

This version of pandoc-eqnos was tested using pandoc 1.15.2 - 1.19.1.  It works under linux, Mac OS X and Windows.  Older versions and other platforms can be supported on request.  I am pleased to receive bug reports and feature requests on the project's [Issues tracker].

If you find pandoc-eqnos useful, then please encourage further development by giving it a star [on GitHub].

See also: [pandoc-fignos], [pandoc-tablenos]

[pandoc]: http://pandoc.org/
[Issues tracker]: https://github.com/tomduck/pandoc-eqnos/issues
[on GitHub]:  https://github.com/tomduck/pandoc-eqnos
[pandoc-fignos]: https://github.com/tomduck/pandoc-fignos
[pandoc-tablenos]: https://github.com/tomduck/pandoc-tablenos


Contents
--------

 1. [Usage](#usage)
 2. [Markdown Syntax](#markdown-syntax)
 3. [Customization](#customization)
 4. [Technical Details](#technical-details)
 5. [Installation](#installation)
 6. [Getting Help](#getting-help)


Usage
-----

To apply the filter during document processing, use the following option with pandoc:

    --filter pandoc-eqnos

Note that any use of `--filter pandoc-citeproc` or `--bibliography=FILE` options should come *after* the pandoc-eqnos filter call.


Markdown Syntax
---------------

The markdown syntax extension used by pandoc-eqnos was developed in [pandoc Issue #813] -- see [this post] by [@scaramouche1].

To mark an equation for numbering, add the label `eq:id` to its attributes:

    $$ y = mx + b $$ {#eq:id}

The prefix `#eq:` is required. `id` should be replaced with a unique identifier composed of letters, numbers, dashes, slashes and underscores.  If `id` is omitted then the equation will be numbered but unreferenceable.

To reference the equation, use

    @eq:id

or

    {@eq:id}

Curly braces around a reference are stripped from the output.

Demonstration: Processing [demo.md] with `pandoc --filter pandoc-eqnos` gives numbered equations and references in [pdf], [tex], [html], [epub], [md] and other formats.

[pandoc Issue #813]: https://github.com/jgm/pandoc/issues/813
[this post]: https://github.com/jgm/pandoc/issues/813#issuecomment-70423503
[@scaramouche1]: https://github.com/scaramouche1
[demo.md]: https://raw.githubusercontent.com/tomduck/pandoc-eqnos/master/demos/demo.md
[pdf]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo.pdf
[tex]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo.tex
[html]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo.html
[epub]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo.epub
[md]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo.md


#### Clever References ####

Writing markdown like

    See eq. @eq:id.

seems a bit redundant.  Pandoc-eqnos supports "clever referencing" via single-character modifiers in front of a reference.  You can write

     See +@eq:id.

to have the reference name (i.e., "eq.") automatically generated.  The above form is used mid-sentence.  At the beginning of a sentence, use

     *@eq:id

instead.  If clever referencing is enabled by default (see [Customization](#customization), below), you can disable it for a given reference using<sup>[1](#footnote1)</sup>

    !@eq:id

Demonstration: Processing [demo2.md] with `pandoc --filter pandoc-eqnos` gives numbered equations and references in [pdf][pdf2], [tex][tex2], [html][html2], [epub][epub2], [md][md2] and other formats.

Note: If you use `*eq:id` and emphasis (e.g., `*italics*`) in the same sentence, then you must backslash escape the `*` in the clever reference; e.g., `\*eq:id`.

[demo2.md]: https://raw.githubusercontent.com/tomduck/pandoc-eqnos/master/demos/demo2.md
[pdf2]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo2.pdf
[tex2]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo2.tex
[html2]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo2.html
[epub2]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo2.epub
[md2]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo2.md


#### Tagged Equations ####

You may optionally override the equation number by placing a tag in an equation's attributes block as follows:

    $$ y = mx + b $$ {#eq:id tag="B.1"}

The tag may be arbitrary text, or an inline equation such as `$\mathrm{B.1'}$`.  Mixtures of the two are not currently supported.


Customization
-------------

Pandoc-eqnos may be customized by setting variables in the [metadata block] or on the command line (using `-M KEY=VAL`).  The following variables are supported:

  * `eqnos-cleveref` or just `cleveref` - Set to `On` to assume "+"
    clever references by default;

  * `eqnos-plus-name` - Sets the name of a "+" reference 
    (e.g., change it from "eq." to "equation"); and

  * `eqnos-star-name` - Sets the name of a "*" reference 
    (e.g., change it from "Equation" to "Eq.").

[metadata block]: http://pandoc.org/README.html#extension-yaml_metadata_block

Demonstration: Processing [demo3.md] with `pandoc --filter pandoc-eqnos` gives numbered equations and references in [pdf][pdf3], [tex][tex3], [html][html3], [epub][epub3], [md][md3] and other formats.

[demo3.md]: https://raw.githubusercontent.com/tomduck/pandoc-eqnos/master/demos/demo3.md
[pdf3]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo3.pdf
[tex3]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo3.tex
[html3]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo3.html
[epub3]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo3.epub
[md3]: https://rawgit.com/tomduck/pandoc-eqnos/master/demos/out/demo3.md


#### Equation Numbers by Section ####

The `--number-sections` option enables section numbers in pandoc.  Equation numbers by section (e.g., "Eq. 2.1") can be obtained as follows:

 1) **html:** Add `xnos-section-numbers: On` to your YAML metadata or
    use the `-M xnos-section-numbers=On` option with pandoc.  This
    variable is ignored for other output formats.

 2) **LaTeX/pdf:** Add 
    `header-includes: \numberwithin{equation}{section}` to your YAML
    metadata.  If you need multiple header includes, then add
    something like this:

    ~~~
    header-includes:
      - \numberwithin{figure}{section}
      - \numberwithin{equation}{section}
      - \numberwithin{table}{section}
    ~~~

    Alternatively, write your header includes into FILE,
    and use the `--include-in-header=FILE` option with pandoc.

    If you set either `--top-level-division=part` or
    `--top-level-division=chapter` then these header includes can be
    dropped.

    LaTeX header-includes are ignored for html output.


Technical Details
-----------------

TeX/pdf:

  * The `equation` environment is used;
  * Tagged equations make use of the `\tag` macro;
  * The `\label` and `\ref` macros are used for equation labels and
    references; and
  * The clever referencing macros `\cref` and `\Cref` are used
    if they are available (i.e. included in your LaTeX template via
    `\usepackage{cleveref}`), otherwise they are faked.  Set the 
    meta variable `xnos-cleveref-fake` to `Off` to disable cleveref
    faking.

Html:

  * The `math` element and a hard-coded equation number/tag are
    wrapped in an "outer" `span` element;
  * The equation number/tag is wrapped in its own "inner" `span` and
    justified right; and
  * (Clever) references are hard-coded and linked to their target.

Other formats:

  * Numbers/tags are hard-coded into the equation; and
  * (Clever) references are hard-coded into the output.


Installation
------------

Pandoc-eqnos requires [python], a programming language that comes pre-installed on linux and Mac OS X, and which is easily installed on Windows.  Either python 2.7 or 3.x will do.

[python]: https://www.python.org/


#### Standard installation ####

Install pandoc-eqnos (as root) using the shell command

    pip install pandoc-eqnos

To upgrade to the most recent release, use

    pip install --upgrade pandoc-eqnos 

Pip is a program that downloads and installs modules from the Python Package Index, [PyPI].  It should come installed with your python distribution.

[PyPI]: https://pypi.python.org/pypi


#### Troubleshooting ####

If you are prompted to upgrade `pip`, then do so.  Installation errors may occur with older versions.   The command you need to execute (as root) is

    python -m pip install --upgrade pip

You may test the installation as a regular user using the shell command

    which pandoc-eqnos

This will tell you where pandoc-eqnos is installed.  If it is not found, then please submit a report to our [Issues tracker].


#### Installing on linux ####

If you are running linux, pip may be packaged separately from python.  On Debian-based systems (including Ubuntu), you can install pip as root using

    apt-get update
    apt-get install python-pip

During the install you may be asked to run

    easy_install -U setuptools

owing to the ancient version of setuptools that Debian provides.  The command should be executed as root.  You may now follow the [standard installation] procedure given above.

[standard installation]: #standard-installation


#### Installing on Mac OS X ####

To install as root on Mac OS X, you will need to use the `sudo` command.  For example:

    sudo pip install pandoc-eqnos

Troubleshooting with `which` should be done as a regular user (i.e., without using `sudo`).


#### Installing on Windows ####

It is easy to install python on Windows.  First, [download] the latest release.  Run the installer and complete the following steps:

 1. Install Python pane: Check "Add Python 3.5 to path" then
    click "Customize installation".

 2. Optional Features pane: Click "Next".

 3. Advanced Options pane: Optionally check "Install for all
    users" and customize the install location, then click "Install".

Once python is installed, start the "Command Prompt" program.  Depending on where you installed python, you may need elevate your privileges by right-clicking the "Command Prompt" program and selecting "Run as administrator".  You may now follow the [standard installation] procedure given above.  Be sure to close the Command Prompt program when you have finished.

[download]: https://www.python.org/downloads/windows/


Getting Help
------------

If you have any difficulties with pandoc-eqnos, or would like to see a new feature, please submit a report to our [Issues tracker].


----

**Footnotes**

<a name="footnote1">1</a>: The disabling modifier "!" is used instead of "-" because [pandoc unnecessarily drops minus signs] in front of references.

[pandoc unnecessarily drops minus signs]: https://github.com/jgm/pandoc/issues/2901
