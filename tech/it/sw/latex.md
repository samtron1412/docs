[TOC]

# TeX

TeX is a [typesetting system](http://en.wikipedia.org/wiki/Typesetting_system) designed and mostly written by [Donald Knuth](http://en.wikipedia.org/wiki/Donald_Knuth) and released in 1978.

Together with the [Metafont](http://en.wikipedia.org/wiki/Metafont) language for font description and the [Computer Modern](http://en.wikipedia.org/wiki/Computer_Modern) family of [typefaces](http://en.wikipedia.org/wiki/Typeface), TeX was designed with two main goals in mind:

- Allow anybody to produce high-quality books using a reasonably minimal
  amount of effort.
- Provide a system that would give exactly the same results on all
  computers, now and in the future.

Written in originally [WEB](http://en.wikipedia.org/wiki/WEB) an [literate programming](http://en.wikipedia.org/wiki/Literate_programming).


## Why TeX?

Eight reason in four areas: output quality (1), superior engineering (2-5), freedom (6-7) and popularity (8).

1. Best output
2. Fast
3. Stable
4. Input is plain text
5. Output can be anything
6. Free
7. Run anywhere
8. TeX is the standard

## Typesetting system

Typesetting is the composition of text by means of arranging physical
[types](http://en.wikipedia.org/wiki/Sort_(typesetting)) or the digital
equivalents. Stored letters and other symbols (called
[sorts](http://en.wikipedia.org/wiki/Sort_(typesetting)) in mechanical
systems and [glyphs](http://en.wikipedia.org/wiki/Glyphs) in digital
systems) are retrieved and ordered according to a language's orthography
for visual display. Typesetting requires the prior process of designing
a [font](http://en.wikipedia.org/wiki/Font).

## WEB

WEB is a computer programming system created by Donald E. Knuth as the
first implementation of what he called "[literate
programming](https://en.wikipedia.org/wiki/Literate_programming)": the
idea that one could create software as works of literature, by embedding
source code inside descriptive text, rather than the reverse (as is
common practice in most programming languages), in an order that is
convenient for exposition to human readers, rather than in the order
demanded by the compiler.

WEB consists of two secondary programs: `TANGLE`, which produces
compilable Pascal code from the source texts, and `WEAVE`, which
produces nicely-formatted, printable documentation using TeX.

## Literate programming

Literate programming is an approach to programming introduced by Donald
Knuth in which a program is given as an explanation of the program logic
in a natural language, such as English, interspersed with snippets of
macros and traditional source code, from which a compilable source code
can be generated.

Literate programming is very often misunderstood to refer only to
formatted documentation produced from a common file with both source
code and comments – which is properly called `documentation generation`
– or to voluminous commentaries included with code. This is backwards:
well-documented code or documentation extracted from code follows the
structure of the code, with documentation embedded in the code; in
literate programming code is embedded in documentation, with the code
following the structure of the documentation.

## TeX engines (binaries/executables)

### TeX (binary: *inittex*)

Originally TeX, current version is TeX version 3 'TeX90'

### e-TeX (binary: *etex*)

Released in the late 1990. Add number of additional primitives to TeX.
Use by packages developer not end users.

### pdfTeX (binary: *pdftex*)

Write by Hàn Thế Thành in 1996. Include e-TeX and add number of PDF-
related primitives. Can produce DVI and PDF.

### XeTeX (binary: *xetex*)

Include e-TeX, works with native UTF-8 input and can access system
fonts.

### LuaTeX (binary: *luatex*)

Include e-TeX, works with native UTF-8 input and includes the Lua
scripting engine, access system font by Lua.

## TeX macro packages (a.k.a TeX formats)

### Plain TeX (binary: *tex*)

Low-level than LaTeX

### [LaTeX](http://www.latex-project.org/) (binary: *latex*)

This tool provides several predefined document classes (book, article,
report) with extensive sectioning and cross-referencing capabilities,
and auxiliary tools for such processes as bibliography and index
creation.

### [AMSTeX](http://www.ams.org/publications/authors/tex/tex)

AMS-TeX and AMS-LaTeX are macro collections developed at the American
Mathematical Society for preparing publications containing extensive
mathematical content. AMS-TeX works directly with TeX, and AMS-LaTeX
works on top of LaTeX.

As LaTeX increased in popularity, authors sought to submit papers to the
AMS in LaTeX, so AMSLaTeX was developed. AMSLaTeX is a collection of
LaTeX packages and classes that offer authors most of the functionality
of AMSTeX. The AMS no longer recommends the use of AMSTeX, and urges its
authors to use AMSLaTeX instead.

### [ConTeXt](http://wiki.contextgarden.net/Main_Page) (binary: *texmfstart*)

ConTeXt is an independent macro package which has a basic document
structuring approach similar to LaTeX.  It also supports creating
interactive PDF files and has integrated MetaPost support, among many
other interesting features.

Whereas LaTeX insulates the writer from typographical details, ConTeXt
takes a complementary approach by providing structured interfaces for
handling typography, including extensive support for colors,
backgrounds, hyperlinks, presentations, figure-text integration, and
conditional compilation. It gives the user extensive control over
formatting while making it easy to create new layouts and styles without
learning the TeX macro language. ConTeXt’s unified design avoids the
package clashes that can happen with LaTeX.

ConTeXt is a special case, straddling levels. It contains a format at
the level of plain TeX and LaTeX, but unlike the other formats, it is
invoked via a separate utility (e.g., texmfstart) which then indirectly
runs a TeX engine. This makes it possible to support a wide array of
advanced features, such as integrated graphics and XML input, since the
startup utility can control the flow of processing.

### [TeXinfo](http://www.gnu.org/software/texinfo/) (binary: *makeinfo*)

Texinfo is the documentation format created by the GNU project. This
macro set is designed to generate both print and on-line output (an
"Info file", HTML, plain text, ...) from a single source file. Texinfo
is integrated with GNU Emacs, and emacs can be used (but is not
required) both to read Info files and create Texinfo source.

Texinfo is a macro language, somewhat similar to LaTeX, but with
slightly less expressive power. Its appearance is of course rather
similar to any TeX-based macro language, except that its macros start
with @ rather than the \ that’s more commonly used in TeX systems.

### [Eplain](http://tug.org/eplain/) (Extended Plain TeX - binary: *eplain*)

Eplain is not intended to provide typesetting capabilities, as does
LaTeX (originally written by Leslie Lamport) and Texinfo (Originally
written by Richard Stallman). Instead, it provides definitions that are
intended to be useful regardless of the high-level commands that you use
when you actually prepare your manuscript.

For example, Eplain does not have a command \section to format section
headings in an “appropriate” way, such as LaTeX’s \section. The
philosophy of Eplain is that some people will always need or want to go
beyond the macro designer’s idea of “appropriate”. Such canned macros
are fine—as long as you are willing to accept the resulting output. If
you don’t like the results, or if you are trying to match a different
format, you have to put in extra work to override the defaults.


## TeX distribution

A TeX distribution provides a structured collection of TeX-related
software. Generally, a TeX distribution includes a set of *“core”* TeX
executables such as *tex* and *latex*; various *fonts* optimized for use
with TeX; helper programs such as the *BibTeX* bibliographic-database
formatter, editors, *integrated development environments*, file-format-
conversion programs; numerous LaTeX *packages*; configuration tools; and
any other goodies the distributor chooses to include.

Commonly encountered TeX distributions include [TeX
Live](https://www.tug.org/texlive/), [MiKTeX](http://miktex.org/) and
[MacTeX](http://tug.org/mactex/); older ones include ozTeX, CMacTeX and
teTeX. MiKTeX is also available as the basis of the ProTeXt bundle,
distributed on the TeX Live DVD mailing, as well as being available
online.

## Front-ends (Editors)

These editors are what you use to create a document file. Some (e.g.,
TeXShop) are devoted specifically to TeX, others (e.g., Emacs) can be
used to edit any sort of file. TeX documents are independent of any
particular editor; the TeX typesetting program itself does not include
any sort of editor whatsoever.

## Packages

These are add-ons to the basic TeX system, developed independently,
providing additional typesetting features, fonts, documentation, etc. A
package might or might not work with any given format and/or engine; for
example, many are designed specifically for LaTeX, but there are plenty
of others, too. The [CTAN](http://www.ctan.org/) sites provide access to
the vast majority of packages in the TeX world; CTAN is generally the
source used by the distributions.

# Starting out with TeX, LaTeX and friends
## Get a TeX distribution (TeX implementation)

| Distribution | Description              |
| -            | -                        |
| TeX Live     | Unix and Windows         |
| MacTeX       | Mac OS                   |
| MikTeX       | Windows and Mac OS       |
| proTeXt      | MikTeX-based for Windows |
| ShareLaTeX   | Online                   |
| Papeeria     | Online                   |
| Overleaf     | Online                   |
| Datazar      | Online                   |

## Get a editor (front-ends)

Maybe TeX distribution have a editor default for you. If you don't like
it, you can replace with another editor. Search Google "TeX editor" and
choose your editor.

## Get documentation

### Online documentation

**LaTeX**:

- [LaTeX Documentation Pointers](http://www.ctan.org/pkg/latex-doc-ptr) has references to documentation for many common LaTeX tasks (by Jim Hefferon).
- [A First LaTeX Document](http://www.ctan.org/pkg/first-latex-doc) takes you through writing a small document with text and math for the first time (by Jim Hefferon).
 - [Getting Started with LaTeX](http://www.maths.tcd.ie/~dwilkins/LaTeXPrimer/), a primer for text, math, and basic formatting.
- [Online LaTeX tutorials](http://www.andy-roberts.net/misc/latex/), a graduated series (by Andy Roberts).
- [Spoken (video) tutorial on LaTeX](http://spoken-tutorial.org/Study_Plans_LaTeX) (from spoken-tutorial.org).
- [The Not So Short Introduction to LaTeX2e](http://www.ctan.org/pkg/lshort) is a more comprehensive manual on writing LaTeX (by Tobias Oetiker, translated into many languages).
- [LaTeX Cheat Sheet](http://www.stdout.org/~winston/latex/), a two-page quick reference (Winston Chang).

**Plain TeX**: [TeX by Topic, A TeXnician's Reference](http://www.eijkhout.net/tbt/), by Victor Eijkhout.

**Fonts**: a discussion of the [fonts available](http://tug.org/fonts/) for use with TeX is available separately.

**General help**: see [community](#community) below; first place to look is the [FAQ](http://www.tex.ac.uk/faq).

### Books

- [The TeXbook](http://tug.org/books/index.html#texbook): of Donald E. Knuth covering plain TeX.
- [A Guide to LaTeX2e](http://tug.org/books/index.html#guidelatex): covering LaTeX.

## Community

- [TUG](http://www.tug.org/): TeX User Group
- [TeX in StackExchange](http://tex.stackexchange.com/): Q&A site
- [CTAN](www.ctan.org): The Comprehensive TeX Archive Network

# LaTeX

## Packages should load in LaTeX

### [nag](http://www.ctan.org/pkg/nag)

Warns when you accidentally use deprecated LaTeX constructs from
**l2tabu**. Place below line before the `\documentclass`:

`\RequirePackage[l2tabu, orthodox]{nag}`

### [microtype](http://www.ctan.org/pkg/microtype)

It plays with ever-so-slightly shrinking and stretching of the fonts and
with the extent to which text protrudes into the margins in a way that
yields results that look better, that have fewer instances of
hyphenation, and fewer overfull *hboxes*.

`\usepackage[stretch=10]{microtype}`

### [hyperref](http://tug.org/applications/hyperref/)

Extensive support for hypertext in LATEX.

### [geometry](http://www.ctan.org/pkg/geometry)

Flexible and complete interface to document dimensions.

### [AMS math packages](http://ctan.org/pkg/amsmath)
### [urlbst](http://nxg.me.uk/dist/urlbst/)

Web support for BibTEX.

### [booktabs](http://www.ctan.org/pkg/booktabs)

Publication quality tables in LATEX.

### [array](http://www.ctan.org/pkg/array)

Extending the array and tabular environments.

### [memoir](http://www.ctan.org/pkg/memoir)

Typeset fiction, non-fiction and mathematical books

### [koma-script](http://www.ctan.org/pkg/koma-script)

A bundle of versatile classes and packages.


### [TikZ](http://sourceforge.net/projects/pgf/)

TikZ and PGF are TeX packages for creating graphics programmatically.
TikZ is build on top of PGF and allows you to create sophisticated
graphics in a rather intuitive and easy manner.

### [graphicx]()

### enumerate

enumerated environment

### fancyhdr

Create header

### longtable

### [listing](http://www.ctan.org/tex-archive/macros/latex/contrib/listings/)

### [verbatim]()

## Bibliography

### Back-end bibliography processor

#### [BibTeX](https://en.wikipedia.org/wiki/BibTeX)

BibTeX is reference management software for formatting lists of
references. BibTeX was created by Oren Patashnik and Leslie Lamport in
1985. It is written in WEB/Pascal.

##### Basic structure

Input:

- An `.aux` file produced by LaTeX on an earlier run.
- A `.bst` file (the style file), which specifies the general reference-list style and specifies how to format individual entries, and which is written by a style designer [..] in a special-purpose language [..].
- A `.bib` file(s) create a database of all reference-list entries the user might ever hope to use.

BibTeX chooses from the `.bib` file(s) only those entries specified by the `.aux` file (that is, those given by LaTeX's `\cite` or `\nocite` commands), and creates as **output** a `.bbl` file containing these entries together with the formatting commands specified by the `.bst` file [..]. LaTeX will use the `.bbl` file, perhaps edited by the user, to produce the reference list.

`aux + bib -> bbl + bib -> ref list`

##### [Style examples](http://www.cs.stir.ac.uk/~kjt/software/latex/showbst.html)

##### [bib file](https://en.wikipedia.org/wiki/BibTeX#Bibliographic_information_file)

- Cross-referencing.
- Using more than one bib file.
- Non-reference section
	+ @COMMENT{...}


#### [Biber](http://biblatex-biber.sourceforge.net/)

[manual](http://mirrors.ctan.org/biblio/biber/documentation/biber.pdf)

### Packages
- `\cite{cite_key}`
- `\cite[p.~215]{citation01}`
- `\cite{citation01,citation02,citation03}`
- `\nocite{citation01}` : ref appear in bibliography but not where it is ref in the main text.

#### [natbib](http://ctan.org/pkg/natbib)
[ref sheet](http://merkel.zoneo.net/Latex/natbib.php)

- `\usepackage[options]{natbib}`
		<figure>
		  <figcaption style="text-align:center;">Natbib Options</figcaption>
		  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
		  <img src="latexFigures/natbiboptions.png" alt="Natbib Options" title="Natbib Options">
		</figure>
- `\bibliographystyle{plainnat}`
		<figure>
		  <figcaption style="text-align:center;">Styles compatible with Natbib</figcaption>
		  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
		  <img src="latexFigures/stylesnatbib.png" alt="Styles compatible with Natbib" title="Styles compatible with Natbib">
		</figure>

#### [biblatex](http://www.ctan.org/pkg/biblatex)


# Tutorial

## [Popular packages in latex](https://tex.stackexchange.com/questions/553/what-packages-do-people-load-by-default-in-latex)


## [Problems with Vietnamese](http://vntex.sourceforge.net/vntexse4.html)

## Set up for includegraphic

- Use variable environment **TEXINPUTS** to set up path to directory
  contain figures. Eg. **TEXINPUTS=E:/Software/Report/Figures**
- Use package graphicx to include figures.

## [Integrating Local Additions](http://docs.miktex.org/manual/localadditions.html)

Use to install offline, manual package at local.

## Miktex packages

Use package manager to install packages, change repositories to have
best speed.

## Bibliography

Use biber package

# Tips and Tricks

## [Latex templates](https://github.com/bamos/latex-templates)


# References
