[TOC]

# Packages

## babel

Multilingual support for Plain TeX or LaTeX.

This package manages culturallydetermined typographical (and other)
rules for a wide range of languages. A document may select a single
language to be supported, or it may select several, in which case the
document may switch from one language to another in a variety of ways.

Babel uses contributed configuration files that provide the detail of
what has to be done for each language. Included is also a set of ini
files for about 200 languages.

Many language styles work with pdfLATEX, as well as with XELATEX and
LuaLATEX, out of the box. A few even work with plain formats.

```
\usepackage[english]{babel}
```

## csquotes

Context sensitive quotation facilities.

This package provides advanced facilities for inline and display
quotations. It is designed for a wide range of tasks ranging from the
most simple applications to the more complex demands of formal
quotations. The facilities include commands, environments, and
userdefinable ‘smart quotes’ which dynamically adjust to their
context. Quotation marks are switched automatically if quotations are
nested and they can be adjusted to the current language if the babel
package is available. There are additional facilities designed to cope
with the more specific demands of academic writing, especially in the
humanities and the social sciences. All quote styles as well as the
optional active quotes are freely configurable.

```
\usepackage[autostyle, english = american]{csquotes}
```

## [nag](http://www.ctan.org/pkg/nag)

Warns when you accidentally use deprecated LaTeX constructs from
**l2tabu**. Place below line before the `\documentclass`:

`\RequirePackage[l2tabu, orthodox]{nag}`

## [microtype](http://www.ctan.org/pkg/microtype)

It plays with eversoslightly shrinking and stretching of the fonts and
with the extent to which text protrudes into the margins in a way that
yields results that look better, that have fewer instances of
hyphenation, and fewer overfull *hboxes*.

`\usepackage[stretch=10]{microtype}`

## [hyperref](http://tug.org/applications/hyperref/)

Extensive support for hypertext in LATEX.

The hyperref package is used to handle crossreferencing commands in
LATEX to produce hypertext links in the document. The package provides
backends for the \special set defined for HyperTEX DVI processors; for
embedded pdfmark commands for processing by Acrobat Distiller (dvips and
Y&Y’s dvipsone); for Y&Y’s dviwindo; for PDF control within pdfTEX and
dvipdfm; for TEX4ht; and for VTEX’s pdf and HTML backends.

The package is distributed with the backref and nameref packages,
which make use of the facilities of hyperref.

## [geometry](http://www.ctan.org/pkg/geometry)

Flexible and complete interface to document dimensions.

## [amsmath](http://ctan.org/pkg/amsmath)

AMS mathematical facilities for LATEX.

The principal package in the AMSLATEX distribution. It adapts for use in
LATEX most of the mathematical features found in AMSTEX; it is highly
recommended as an adjunct to serious mathematical typesetting in LATEX.

When amsmath is loaded, AMSLATEX packages amsbsy (for bold symbols),
amsopn (for operator names) and amstext (for text embedded in
mathematics) are also loaded.

amsmath is part of the LATEX required distribution; however, several
contributed packages add still further to its appeal; examples are
empheq, which provides functions for decorating and highlighting
mathematics, and ntheorem, for specifying theorem (and similar)
definitions.

## amsthm

Typesetting theorems (AMS style).

The package facilitates the kind of theorem setup typically needed in
American Mathematical Society publications. The package offers the
theorem setup of the AMS document classes (amsart, amsbook, etc.)
encapsulated in LATEX package form so that it can be used with other
document classes.

Amsthm is part of the (required) AMSLATEX distribution, so should be
present in any LATEX distribution.

## amsfonts

TEX fonts from the American Mathematical Society.

An extended set of fonts for use in mathematics, including: extra
mathematical symbols; blackboard bold letters (uppercase only); fraktur
letters; subscript sizes of bold math italic and bold Greek letters;
subscript sizes of large symbols such as sum and product; added sizes of
the Computer Modern small caps font; cyrillic fonts (from the University
of Washington); Euler mathematical fonts.  All fonts are provided as
Adobe Type 1 files, and all except the Euler fonts are provided as
METAFONT source.

The distribution also includes the canonical Type 1 versions of the
Computer Modern family of fonts.

Basic LATEX support for the symbol fonts is provided by amsfonts.sty,
with names of individual symbols defined in amssymb.sty. The Euler fonts
are supported by separate packages; details can be found in the
documentation.

## mathtools

Mathematical tools to use with amsmath.

It will load amsmath if it's not loaded.

Mathtools provides a series of packages designed to enhance the
appearance of documents containing a lot of mathematics. The main
backbone is amsmath, so those unfamiliar with this required part of the
LATEX system will probably not find the packages very useful.

Mathtools provides many useful tools for mathematical typesetting. It is
based on amsmath and fixes various deficiencies of amsmath and standard
LATEX. It provides:

Extensible symbols, such as brackets, arrows, harpoons, etc.; Various
symbols such as \coloneqq (:=); Easy creation of new tag forms; Showing
equation numbers only for referenced equations; Extensible arrows,
harpoons and hookarrows; Starred versions of the amsmath matrix
environments for specifying the column alignment; More building blocks:
multlined, caseslike environments, new gathered environments; Maths
versions of \makebox, \llap, \rlap etc.; Cramped math styles; and
more...

## cancel

Place lines through maths formulae.

A package to draw diagonal lines (“cancelling” a term) and arrows with
limits (cancelling a term “to a value”) through parts of maths formulae.

## [urlbst](http://nxg.me.uk/dist/urlbst/)

Web support for BibTEX.

## [booktabs](http://www.ctan.org/pkg/booktabs)

Publication quality tables in LATEX.

## [array](http://www.ctan.org/pkg/array)

Extending the array and tabular environments.

## [memoir](http://www.ctan.org/pkg/memoir)

Typeset fiction, nonfiction and mathematical books

## [komascript](http://www.ctan.org/pkg/komascript)

A bundle of versatile classes and packages.


## [pgfTikZ](http://sourceforge.net/projects/pgf/)

Create PostScript and PDF graphics in TEX.

TikZ and PGF are TeX packages for creating graphics programmatically.
TikZ is build on top of PGF and allows you to create sophisticated
graphics in a rather intuitive and easy manner.

PGF is a macro package for creating graphics. It is platform and
formatindependent and works together with the most important TEX backend
drivers, including pdfTEX and dvips. It comes with a userfriendly syntax
layer called TikZ.

Its usage is similar to pstricks and the standard picture
environment. PGF works with plain (pdf)TEX, (pdf)LATEX, and
ConTEXt. Unlike pstricks, it can produce either PostScript or PDF
output.

## graphicx

Enhanced support for graphics.

The package builds upon the graphics package, providing a keyvalue
interface for optional arguments to the \includegraphics command. This
interface provides facilities that go far beyond what the graphics
package offers on its own.

For extended documentation, see epslatex.

The package is part of the latexgraphics bundle, which is one of the
collections in the LATEX ‘required’ set of packages.


## enumitem

Control layout of itemize, enumerate, description.

This package provides user control over the layout of the three basic
list environments: enumerate, itemize and description. It supersedes
both enumerate and mdwlist (providing wellstructured replacements for
all their funtionality), and in addition provides functions to compute
the layout of labels, and to ‘clone’ the standard environments, to
create new environments with counters of their own.

- conflict with paralist package

## fancyhdr

Extensive control of page headers and footers in LATEX2ε.

The package provides extensive facilities, both for constructing headers
and footers, and for controlling their use (for example, at times when
LATEX would automatically change the heading style in use).

## mdframed

Framed environments that can split at page boundaries.

The package develops the facilities of framed in providing breakable
framed and coloured boxes.

The user may instruct the package to perform its operations using
default LATEX commands, PStricks or TikZ.

## longtable

## [listing](http://www.ctan.org/texarchive/macros/latex/contrib/listings/)

## [verbatim]()

# Bibliography

## Backend bibliography processor

### [BibTeX](https://en.wikipedia.org/wiki/BibTeX)

BibTeX is reference management software for formatting lists of
references. BibTeX was created by Oren Patashnik and Leslie Lamport in
1985. It is written in WEB/Pascal.

#### Basic structure

Input:

An `.aux` file produced by LaTeX on an earlier run.  A `.bst` file (the
style file), which specifies the general referencelist style and
specifies how to format individual entries, and which is written by a
style designer [..] in a specialpurpose language [..].  A `.bib` file(s)
create a database of all referencelist entries the user might ever hope
to use.

BibTeX chooses from the `.bib` file(s) only those entries specified by
the `.aux` file (that is, those given by LaTeX's `\cite` or `\nocite`
commands), and creates as **output** a `.bbl` file containing these
entries together with the formatting commands specified by the `.bst`
file [..]. LaTeX will use the `.bbl` file, perhaps edited by the user,
to produce the reference list.

`aux + bib > bbl + bib > ref list`

#### [Style examples](http://www.cs.stir.ac.uk/~kjt/software/latex/showbst.html)

#### [bib file](https://en.wikipedia.org/wiki/BibTeX#Bibliographic_information_file)

Crossreferencing.
Using more than one bib file.
Nonreference section
        + @COMMENT{...}


### [Biber](http://biblatexbiber.sourceforge.net/)

[manual](http://mirrors.ctan.org/biblio/biber/documentation/biber.pdf)

## Packages

`\cite{cite_key}`
`\cite[p.~215]{citation01}`
`\cite{citation01,citation02,citation03}`
`\nocite{citation01}` : ref appear in bibliography but not where it is ref in the main text.

### [natbib](http://ctan.org/pkg/natbib)

[ref sheet](http://merkel.zoneo.net/Latex/natbib.php)

`\usepackage[options]{natbib}`
<figure>
<figcaption style="textalign:center;">Natbib Options</figcaption>
<hr style="width:70%;marginleft:auto;marginright:auto;" />
<img src="latexFigures/natbiboptions.png" alt="Natbib Options" title="Natbib Options">
</figure>
`\bibliographystyle{plainnat}`
<figure>
<figcaption style="textalign:center;">Styles compatible with Natbib</figcaption>
<hr style="width:70%;marginleft:auto;marginright:auto;" />
<img src="latexFigures/stylesnatbib.png" alt="Styles compatible with Natbib" title="Styles compatible with Natbib">
</figure>

### [biblatex](http://www.ctan.org/pkg/biblatex)


# Basic Tutorial

## Structure of a LaTeX file

```latex
%Preamble part
\documentclass{article}

%Document content part
\begin{document}
....
\end{document}
```

Using the symbol `%` to comment some texts.

## The preamble of a document

Everything before the line `\begin{document}`
You define
    + type of document
        * `\documentclas[12pt, letterpaper]{article}`
    + language
    + the packages that you want to use
        * `\usepackage[utf8]{inputenc}`
    + Adding a title, author, and date
        * `\title{First document}`
        * `\author{Son Tran}`
        * `\thanks{funded by ...}`
        * `\date{February 2019}`
        * You can print this information by using `\maketitle`command
        between `\begin{document}` and `\end{document}`

## Bold, italics, and underlining

`\textbf{...}`
`\textit{...}`
`\underline{...}`

## Adding images

```
\documentclass{article}
\usepackage{graphicx}
\graphicspath{ {images/} }

\begin{document}
The universe is immense and it seems to be homogeneous,
in a large scale, everywhere we look at.

% Here universe is the name of the file containing the image without the
% extension. The file name of the image should not contain white spaces
% nor multiple dots
\includegraphics{universe}

There's a picture of a galaxy above
\end{document}
```

## Captions, labels, and references

```
\begin{figure}[h]
\centering
\includegraphics[width=0.25\textwidth]{mesh}
\caption{a nice plot}
\label{fig:mesh1}
\end{figure}

As you can see in the figure \ref{fig:mesh1}, the
function grows near 0. Also, in the page \pageref{fig:mesh1}
is the same example.
```

There are three important commands in the example:
    + `\caption{a nice plot}`: As you may expect this command sets the
    caption for the figure. If you create a list of figures this
    caption will be used there. You can place it above or below the
    figure.
    + `\label{fig:mesh1}`: If you need to refer the image within your
    document, set a label with this command. The label will number the
    image, and combined with the next command will allow you to
    reference it.
    + `\ref{fig:mesh1}`: This code will be substituted by the number
    corresponding to the referenced figure.
    When placing images in a LATEX document, we should always put them
    inside a figure environment or similar so that LATEX will position the
    image in a way that fits in with the rest of your text.

## Creating lists

### Unordered lists

```
\begin{itemize}
\item The individual entries are indicated with a black dot, a socalled bullet.
\item The text in the entries may be of any length.
\end{itemize}
```

### Ordered lists

```
\begin{enumerate}
\item This is the first entry in our list
\item The list numbers increase with each entry we add
\end{enumerate}
```

## Adding math

Two modes to write mathematical expressions:
    + The inline mode
        * use one of these delimiters: \( ... \), $ ... $ or
        \begin{math} ... \end{math}
    + The display mode
        * numbered
        * unnumbered
        * To print your equations in display mode use one of these
        delimiters: \[ ... \], \begin{displaymath} ...
        \end{displaymath} or \begin{equation} ... \end{equation}. $$
        ... $$ is discouraged as it can give inconsistent spacing, and
        may not work well with some math packages.

        ```
        % Inline
        In physics, the massenergy equivalence is stated
        by the equation $E=mc^2$, discovered in 1905 by Albert Einstein.

        % Display
        The massenergy equivalence is described by the famous equation

        \[E=mc^2\]

        discovered in 1905 by Albert Einstein.
        In natural units ($c = 1$), the formula expresses the identity

        \begin{equation}
        E=m
        \end{equation}
        ```

        Using `amsmath` package for more flexibility.

## Basic Formatting

### Lengths in LaTeX

#### Units

| Abbreviation | Value                                                                                                                                                                           |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| pt           | a point is approximately 1/72.27 inch, that means about 0.0138 inch or 0.3515 mm (exactly point is defined as 1/864 of American printer’s foot that is 249/250 of English foot) |
| mm           | a millimeter                                                                                                                                                                    |
| cm           | a centimeter                                                                                                                                                                    |
| in           | inch                                                                                                                                                                            |
| ex           | roughly the height of an 'x' (lowercase) in the current font (it depends on the font used)                                                                                      |
| em           | roughly the width of an 'M' (uppercase) in the current font (it depends on the font used)                                                                                       |
| mu           | math unit equal to 1/18 em, where em is taken from the math symbols family                                                                                                      |

#### Lengths

Lengths are units of distance relative to some document elements.
Lengths can be changed by the command:

`\setlength{\lengthname}{value_in_specified_unit}`

For example, in a twocolumn document the column separation can be set
to 1 inch by:

`\setlength{\columnsep}{1in}`


| Length          | Description                                                             |
|-----------------|-------------------------------------------------------------------------|
| \baselineskip   | Vertical distance between lines in a paragraph                          |
| \columnsep      | Distance between columns                                                |
| \columnwidth    | The width of a column                                                   |
| \evensidemargin | Margin of even pages, commonly used in twosided documents such as books |
| \linewidth      | Width of the line in the current environment.                           |
| \oddsidemargin  | Margin of odd pages, commonly used in twosided documents such as books  |
| \paperwidth     | Width of the page                                                       |
| \paperheight    | Height of the page                                                      |
| \parindent      | Paragraph indentation                                                   |
| \parskip        | Vertical space between paragraphs                                       |
| \tabcolsep      | Separation between columns in a table (tabular environment)             |
| \textheight     | Height of the text area in the page                                     |
| \textwidth      | Width of the text area in the page                                      |
| \topmargin      | Length of the top margin                                                |

Default lengths can not only be set to any desired value, they can
also be used as units to set the dimensions of other LATEX elements.
For instance, you can set an image to have a width of one quarter the
total text width.

```
\includegraphics[width=0.25\textwidth]{lionlogo}
[...]
```

### Abstract

```
\begin{document}

\begin{abstract}
This is a simple paragraph at the beginning of the
document. A brief introduction about the main subject.
\end{abstract}
\end{document}
```

### Paragraphs and newlines

A new line without starting a new paragraph: add a break line
    + `\\`
    + `\newline`
    A new paragraph:
    + "Enter" twice (double blank line)
    + `\par` command

### Paragraphs indentation

By default, LATEX does not indent the first paragraph of a section or a
chapter. The size of the subsequent paragraph indents is determined by
\parindent

```
\setlength{\parindent}{4em}

\begin{document}
This is the text in first paragraph. This is the text in first
paragraph. This is the text in first paragraph. \par
This is the text in second paragraph. This is the text in second
paragraph. This is the text in second paragraph.

This is another paragraph, contains some text to test the paragraph
interlining, paragraph indentation and some other features. Also,
is easy to see how new paragraphs are defined by simply entering a
double blank space.
...
\end{document}
```

The default length of this parameter is set by the document class used.
It is possible to change the indent size. In the example, the first
lines of each paragraph are indented 4em (an "em" equals the length of
the "m" in the current font), this is accomplished by the command
\setlength{\parindent}{4em}. It's recommended to put this command in the
preamble of the document, but it can be set anywhere else.

If you want to create a nonindented paragraph, like the second one in
the example, put the command \noindent at the beginning of it. If you
want the whole document not to be indented, set the indentation length
to zero with \setlength{\parindent}{0pt}.

On the other side, if you want to indent a paragraph that is not
indented you can use \indent right above it. It should be noted that
this command will only have an effect when \parindent is set to zero.

### Paragraph spacing

The length parameter that characterises the paragraph spacing is
\parskip, this determines the space between a paragraph and the
preceding text.

```
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage[english]{babel}

\setlength{\parindent}{4em}
\setlength{\parskip}{1em}

\begin{document}
This is the text in first paragraph. This is the text in first
paragraph. This is the text in first paragraph. \par
This is the text in second paragraph...

\end{document}
```

### Line spacing

There are three commands that control the line spacing, below an example
redefining the length of \baselinestretch

```
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage[english]{babel}

\setlength{\parindent}{4em}
\setlength{\parskip}{1em}
\renewcommand{\baselinestretch}{1.5}

\begin{document}
This is the text in first paragraph. This is the text in first
paragraph. This is the text in first paragraph. \par
This is the text in second paragraph...
\end{document}
```

In the example above, \renewcommand{\baselinestretch}{1.5} scales the
default interline space to 1.5 its default value. Of course that number
can be set to any value.

As mentioned before, there are other two LATEX lengths that may change
the line spacing:

\baselineskip
    + Is a length determining the minimum space between the bottom of
    two successive lines in a paragraph; it may be changed (in the
    preamble) by \setlength{\baselineskip}{value}. Where value is set
    using any of the LaTeX units.
    \linespread{value}
    + where value determine line spacing. This value is somewhat
    confusing, because:

    Value   Line spacing
    1.0 single spacing
    1.3 oneandahalf spacing
    1.6 double spacing

### Text alignment

Text alignment can be manually controlled by several commands.


| Alignment       | Environment | Switch command | ragged2e environment | ragged2e switch command |
|-----------------|-------------|----------------|----------------------|-------------------------|
| Left            | flushleft   | \raggedright   | FlushLeft            | \RaggedRight            |
| Right           | flushright  | \raggedleft    | FlushRight           | \RaggedLeft             |
| Centre          | center      | \centering     | Center               | \Centering              |
| Fully justified |             |                | justify              | \justify                |

## Chapters and Sections

Commands to organize a document vary depending on the document type, the
simplest form of organization is the sectioning, available in all
formats.

```
\chapter{First Chapter}

\section{Introduction}

This is the first section.

Lorem  ipsum  dolor  sit  amet,  consectetuer  adipiscing
elit.   Etiam  lobortisfacilisis sem.  Nullam nec mi et
neque pharetra sollicitudin.  Praesent imperdietmi nec ante.
Donec ullamcorper, felis non sodales...

\section{Second Section}

Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Etiam lobortis facilisissem.  Nullam nec mi et neque pharetra
sollicitudin.  Praesent imperdiet mi necante...

\subsection{First Subsection}
Praesent imperdietmi nec ante. Donec ullamcorper, felis non sodales...

\section*{Unnumbered Section}
Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Etiam lobortis facilisissem
```

The command \section{} marks the beginning of a new section, inside the
braces is set the title. Section numbering is automatic and can be
disabled by including a * in the section command as \section*{}. We can
also have \subsection{}s, and indeed \subsubsection{}s. The basic levels
of depth are listed below:

1  \part{part}
0   \chapter{chapter}
1   \section{section}
2   \subsection{subsection}
3   \subsubsection{subsubsection}
4   \paragraph{paragraph}
5   \subparagraph{subparagraph}

Note that \part and \chapter are only available in report and book
document classes.

## Creating Tables

Using tool: `https://www.tablesgenerator.com/`

Simple Tables without border

```
\begin{center}
\begin{tabular}{ c c c }
cell1 & cell2 & cell3 \\
cell4 & cell5 & cell6 \\
cell7 & cell8 & cell9
\end{tabular}
\end{center}
```

Tables with borders

```
\begin{center}
\begin{tabular}{ |c|c|c| }
\hline
cell1 & cell2 & cell3 \\
cell4 & cell5 & cell6 \\
cell7 & cell8 & cell9 \\
\hline
\end{tabular}
\end{center}
```

## Adding a Table of Contents

`\tableofcontents`

```
\documentclass{article}
\usepackage[utf8]{inputenc}

\title{Sections and Chapters}
\author{Gubert Farnsworth}
\date{ }

\begin{document}

\maketitle

\tableofcontents

\section{Introduction}

This is the first section.

Lorem  ipsum  dolor  sit  amet,  consectetuer  adipiscing
elit.   Etiam  lobortisfacilisis sem.  Nullam nec mi et
neque pharetra sollicitudin.  Praesent imperdietmi nec ante.
Donec ullamcorper, felis non sodales...

\addcontentsline{toc}{section}{Unnumbered Section}
\section*{Unnumbered Section}

Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Etiam lobortis facilisissem.  Nullam nec mi et neque pharetra
sollicitudin.  Praesent imperdiet mi necante...

\section{Second Section}

Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Etiam lobortis facilisissem.  Nullam nec mi et neque pharetra
sollicitudin.  Praesent imperdiet mi necante...

\end{document}
```

# Mac OS  MacTeX

http://www.tug.org/mactex/

## Installing packages

For packages found on CTAN: use the TeX Live Utility found in your
/Applications/TeX folder. This application can keep all of your TeX
packages up to date.
Place the relevant files in `~/Library/texmf/tex/latex`. TeX will find
them.
Enter `tlmgr install *packagename*` in the terminal


# Writing mathematical document with amsmath

Usage guide: http://texdoc.net/texmfdist/doc/latex/amsmath/amsldoc.pdf

# Drawing electrical circuits

- https://www.overleaf.com/learn/latex/LaTeX_Graphics_using_TikZ:_A_Tutorial_for_Beginners_(Part_4)%E2%80%94Circuit_Diagrams_Using_Circuitikz
- https://www.latextutorial.com/tutorials/circuitikz/
    + https://github.com/circuitikz/circuitikz/issues/101

# LaTeX and Vim

## Introduction

- https://castel.dev/post/lecture-notes-1/
- https://castel.dev/post/lecture-notes-2/
- Tools
    + Vim + vimtex + ultisnips + vim-snippets + Inkscape + TikZ
    + vimtex
        * compiling and preview
        * forward and backward search
    + ultisnips + vim-snippets
        * increase typing speed
    + Inkscape: drawing and export to pdf+LaTeX
    + TikZ
- vimtex Usage: through mappings
    + https://github.com/lervag/vimtex/wiki/Usage
    + https://github.com/lervag/vimtex#features
    + forward search:
        * Put the cursor at the place you want to see it in the pdf file
        * Using mapping forward search: `<localleader>lv` (`\lv`)
    + backward search:
        * Skim:
            - `Shift + Command + Click` on the pdf file to jump to the
            corresponding text.
- vimtex's workflow:
    + Open a .tex file
    + Checking that the vimtex is running or not: `\lg`
    + Toggling the continuous compiling if it isn't running: `\ll`
    + Edit the file using vimtex features
        * Motions:
            - Section boundaries: `[[`, `]]`, `[]`, `][`
            - Environment boundaries: `[m`, `[M`, `]m`, `]M`
            - Comment boundaries: `[*`, `]*`
            - Matching delimiters: `%`
        * Text objects
            - Commands: `ic`, `ac`
            - Delimiters: `id`, `ad`
            - LaTeX environments: `ie`, `ae`
            - Inline Math blocks: `i$`, `a$`
            - Sections: `iP`, `aP`
        * Delete the surrounding command, environment, delimiter
            - `dsc`, `dse`, `dsd`, `ds$`
        * Change the surrounding command, environment, delimiter
            - `csc`, `cse`, `csd`, `cs$`
        * Toggle starred command or environment: `tsc`, `tse`
        * Close the current environment/delimiter in insert mode by ]]
        * Insert a new command: `<F7>`
        * Show all insert mode mapping in math mode: `\lm`
            - In math type the leader "backtick" and the mapping
            - `q` to quit the list
        * Toggle table of contents: `\lT`
    + After writing the file is compiled automatically
        * If errors occur, it will show the list of errors
        * Reading the errors to know what's wrong
        * Usually the first error caused by the line right above the
        error
    + Typing `\lv` to do the forward search
    + Typing `\lk` to stop the continuous compiling for the current file
        * `\lK` stop for all files
    + `\lc`: clean, `\lC` full clean


## Ultisnips

```basic-snippet
snippet "b(egin)?" "begin{} / end{}" br
snippet abs "abstract environment" b
snippet tab "tabular / array environment" b
snippet "gentbl(\d+)x(\d+)" "Generate table of *width* by *height*" r
snippet "tr(\d+)" "Add table row of dimension ..." r
snippet table "Table environment" b
snippet fig "Figure environment" b
snippet enum "Enumerate" b
snippet item "Itemize" b
snippet desc "Description" b
snippet it "Individual item" b
snippet part "Part" b
snippet cha "Chapter" b
snippet sec "Section"
snippet sec* "Section*"
snippet sub "Subsection"
snippet sub* "Subsection*"
snippet ssub "Subsubsection"
snippet ssub* "Subsubsection*"
snippet par "Paragraph"
snippet subp "Subparagraph"
snippet ac "Acroynm normal" b
snippet acl "Acroynm expanded" b
snippet ni "Non-indented paragraph" b
snippet pac "Package" b
snippet lp "Long parenthesis"
snippet "mint(ed)?( (\S+))?" "Minted code typeset" br
```

```custom-snippets
snippet mk "Inline Math" wA
snippet dm "Display Math" wA

# Expand when type a character followed by a digit
snippet '([A-Za-z])(\d)' "Auto Subscript" wrA

# Expand when type a character followed by `_` and two digits
snippet '([A-Za-z])_(\d\d)' "Auto Subscript2" wrA

snippet '([A-Za-z])\^(\d+)\s' "Auto Superscript" wrA

# Expand a character followed by `_` and other characters by tab
snippet '([A-Za-z])_([A-Za-z]+)' "Subscript" r

# Expand vector by typing "vec_name., or vec_name,."
snippet "(\\?\w+)(,\.|\.,)" "Vector postfix" riA

# The bar on top by typing tab
snippet "bar" "bar" ri
snippet "([a-zA-Z])bar" "bar" ri

snippet compl "Complement" i
```



# Tips and Tricks

## Block/Multiline comments

Using verbartim package
    + `\userpackage{verbatim}`
    + `\begin{comment`
    + `<comment here>`
    + `\end{comment}`

## Add text in math mode

\text{}
https://tex.stackexchange.com/questions/3415/whatisthecorrectwayofembeddingtextintomathmode#3418

## Align multiline equation with indent equal signs

```
\documentclass{article}

\usepackage{amsmath}


\begin{document}

\begin{align*}
\mathcal{L}^{1}\left\{f(d)\right\} &= \mathcal{L}^{1}\left\{f_1(\delta).f_2(\delta)\right\} \\
&= \exp(mt) \star \left\{\frac{l}{2\sqrt{\pi t^3}} \exp(l^2/{4t})\right\} \\
&= F_1 * F_2
\end{align*}

\end{document}
```

## Create posters using LaTeX

https://tex.stackexchange.com/questions/341/howtocreatepostersusinglatex
    + beamerposter
    + fancytikzposter
    + baposter
    templates
    + https://www.latextemplates.com/cat/conferenceposters
    + https://www.overleaf.com/gallery/tagged/poster

## [Latex templates](https://github.com/bamos/latextemplates)

## [Popular packages in latex](https://tex.stackexchange.com/questions/553/whatpackagesdopeopleloadbydefaultinlatex)


## [Problems with Vietnamese](http://vntex.sourceforge.net/vntexse4.html)

## Set up for includegraphic

Use variable environment **TEXINPUTS** to set up path to directory
contain figures. Eg. **TEXINPUTS=E:/Software/Report/Figures**
Use package graphicx to include figures.

## [Integrating Local Additions](http://docs.miktex.org/manual/localadditions.html)

Use to install offline, manual package at local.

## Miktex packages

Use package manager to install packages, change repositories to have
best speed.

# Alternatives

https://tex.stackexchange.com/questions/120271/alternativestolatex

# References
