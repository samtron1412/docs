[TOC]

# Overview

TeX is a [typesetting
system](http://en.wikipedia.org/wiki/Typesetting_system) designed and
mostly written by [Donald
Knuth](http://en.wikipedia.org/wiki/Donald_Knuth) and released in 1978.

Together with the [Metafont](http://en.wikipedia.org/wiki/Metafont)
language for font description and the [Computer
Modern](http://en.wikipedia.org/wiki/Computer_Modern) family of
[typefaces](http://en.wikipedia.org/wiki/Typeface), TeX was designed
with two main goals in mind:

- Allow anybody to produce high-quality books using a reasonably minimal
  amount of effort.
- Provide a system that would give exactly the same results on all
  computers, now and in the future.

Written in originally [WEB](http://en.wikipedia.org/wiki/WEB) an
[literate
programming](http://en.wikipedia.org/wiki/Literate_programming).


## Why TeX?

Eight reason in four areas: output quality (1), superior engineering
(2-5), freedom (6-7) and popularity (8).

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

## Levels of TeX

- http://www.tug.org/levels.html
- Distributions: TeX Live, MiKTeX, ...
- Front ends and editors: Emacs, vim, TeXworks, TeXnicCenter, ...
- Engines: TeX, pdfTeX, pdfLaTeX, LuaTeX, XeTeX, ...
- Formats: LaTeX, plain TeX, ConTeXt, ...
- Packages: geometry, lm, ...

# TeX engines (binaries/executables)

## TeX (binary: *inittex*)

Originally TeX, current version is TeX version 3 'TeX90'

## e-TeX (binary: *etex*)

Released in the late 1990. Add number of additional primitives to TeX.
Use by packages developer not end users.

## pdfTeX (binary: *pdftex*)

Write by Hàn Thế Thành in 1996. Include e-TeX and add number of PDF-
related primitives. Can produce DVI and PDF.

## XeTeX (binary: *xetex*)

Include e-TeX, works with native UTF-8 input and can access system
fonts.

## LuaTeX (binary: *luatex*)

Include e-TeX, works with native UTF-8 input and includes the Lua
scripting engine, access system font by Lua.

# TeX macro packages (a.k.a TeX formats)

## Plain TeX (binary: *tex*)

Low-level than LaTeX

## [LaTeX](http://www.latex-project.org/) (binary: *latex*)

This tool provides several predefined document classes (book, article,
report) with extensive sectioning and cross-referencing capabilities,
and auxiliary tools for such processes as bibliography and index
creation.

## [AMSTeX](http://www.ams.org/publications/authors/tex/tex)

AMS-TeX and AMS-LaTeX are macro collections developed at the American
Mathematical Society for preparing publications containing extensive
mathematical content. AMS-TeX works directly with TeX, and AMS-LaTeX
works on top of LaTeX.

As LaTeX increased in popularity, authors sought to submit papers to the
AMS in LaTeX, so AMSLaTeX was developed. AMSLaTeX is a collection of
LaTeX packages and classes that offer authors most of the functionality
of AMSTeX. The AMS no longer recommends the use of AMSTeX, and urges its
authors to use AMSLaTeX instead.

## [ConTeXt](http://wiki.contextgarden.net/Main_Page) (binary: *texmfstart*)

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

- [stackoverflow](https://tex.stackexchange.com/questions/223177/what-is-the-mindset-to-take-when-using-context-vs-latex)
    + LaTeX: separating the content making from formatting, so the
    writer only uses LaTeX to create content, and use built-in support
    or packages to finish the formatting.
    + ConTeXt: it supports both content making and formatting so the
    writer doesn't need to install plugins to format the document.

## [TeXinfo](http://www.gnu.org/software/texinfo/) (binary: *makeinfo*)

Texinfo is the documentation format created by the GNU project. This
macro set is designed to generate both print and on-line output (an
"Info file", HTML, plain text, ...) from a single source file. Texinfo
is integrated with GNU Emacs, and emacs can be used (but is not
required) both to read Info files and create Texinfo source.

Texinfo is a macro language, somewhat similar to LaTeX, but with
slightly less expressive power. Its appearance is of course rather
similar to any TeX-based macro language, except that its macros start
with @ rather than the \ that’s more commonly used in TeX systems.

## [Eplain](http://tug.org/eplain/) (Extended Plain TeX - binary: *eplain*)

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


# TeX distribution

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

# Front-ends (Editors)

These editors are what you use to create a document file. Some (e.g.,
TeXShop) are devoted specifically to TeX, others (e.g., Emacs) can be
used to edit any sort of file. TeX documents are independent of any
particular editor; the TeX typesetting program itself does not include
any sort of editor whatsoever.

## Tex directives

- Editors use these directives to figure out what engine, encoding, root
  file, and spellcheck options of the source file.

```text
% !TEX encoding = UTF-8 Unicode
% !TEX program = xelatex
% !TEX root = mythesis.tex
% !TEX spellcheck = fr-FR
```


```text
              E P R S
TeXShop       x x x x
TeXStudio     x x x x
TextMate      ? x x ?
TeXworks      x x x x
SublimeText   o x x x
Atom          o x x o
Vim (vimtex)  o x x o
Overleaf      ? x ? ?
              | | | |
x = yes       | | | Spellcheck
o = no        | | Root
? = ?         | Program
              Encoding
```


# Packages

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
|--------------|--------------------------|
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

- [LaTeX Documentation Pointers](http://www.ctan.org/pkg/latex-doc-ptr)
  has references to documentation for many common LaTeX tasks (by Jim
  Hefferon).
- [A First LaTeX Document](http://www.ctan.org/pkg/first-latex-doc)
  takes you through writing a small document with text and math for the
  first time (by Jim Hefferon).  - [Getting Started with
  LaTeX](http://www.maths.tcd.ie/~dwilkins/LaTeXPrimer/), a primer for
  text, math, and basic formatting.
- [Online LaTeX tutorials](http://www.andy-roberts.net/misc/latex/), a
  graduated series (by Andy Roberts).
- [Spoken (video) tutorial on
  LaTeX](http://spoken-tutorial.org/Study_Plans_LaTeX) (from
  spoken-tutorial.org).
- [The Not So Short Introduction to
  LaTeX2e](http://www.ctan.org/pkg/lshort) is a more comprehensive
  manual on writing LaTeX (by Tobias Oetiker, translated into many
  languages).
- [LaTeX Cheat Sheet](http://www.stdout.org/~winston/latex/), a two-page
  quick reference (Winston Chang).

**Plain TeX**: [TeX by Topic, A TeXnician's
Reference](http://www.eijkhout.net/tbt/), by Victor Eijkhout.

**Fonts**: a discussion of the [fonts available](http://tug.org/fonts/)
for use with TeX is available separately.

**General help**: see [community](#community) below; first place to look
is the [FAQ](http://www.tex.ac.uk/faq).

### Books

- [The TeXbook](http://tug.org/books/index.html#texbook): of Donald
  E. Knuth covering plain TeX.
- [A Guide to LaTeX2e](http://tug.org/books/index.html#guidelatex):
  covering LaTeX.

## Community

- [TUG](http://www.tug.org/): TeX User Group
- [TeX in StackExchange](http://tex.stackexchange.com/): Q&A site
- [CTAN](www.ctan.org): The Comprehensive TeX Archive Network
