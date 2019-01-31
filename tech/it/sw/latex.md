[TOC]

# Packages

## babel

Multilingual support for Plain TeX or LaTeX.

This pack­age man­ages cul­tur­ally-de­ter­mined ty­po­graph­i­cal (and
other) rules for a wide range of lan­guages. A doc­u­ment may se­lect a
sin­gle lan­guage to be sup­ported, or it may se­lect sev­eral, in which
case the doc­u­ment may switch from one lan­guage to an­other in a
va­ri­ety of ways.

Ba­bel uses con­tributed con­fig­u­ra­tion files that pro­vide the
de­tail of what has to be done for each lan­guage. In­cluded is also a
set of ini files for about 200 lan­guages.

Many lan­guage styles work with pdfLATEX, as well as with XELATEX and
LuaLATEX, out of the box. A few even work with plain for­mats.

```
\usepackage[english]{babel}
```

## csquotes

Context sensitive quotation facilities.

This pack­age pro­vides ad­vanced fa­cil­i­ties for in­line and dis­play
quo­ta­tions. It is de­signed for a wide range of tasks rang­ing from
the most sim­ple ap­pli­ca­tions to the more com­plex de­mands of
for­mal quo­ta­tions. The fa­cil­i­ties in­clude com­mands,
en­vi­ron­ments, and user-de­fin­able ‘smart quotes’ which
dy­nam­i­cally ad­just to their con­text. Quo­ta­tion marks are switched
au­to­mat­i­cally if quo­ta­tions are nested and they can be ad­justed
to the cur­rent lan­guage if the ba­bel pack­age is avail­able. There
are ad­di­tional fa­cil­i­ties de­signed to cope with the more spe­cific
de­mands of aca­demic writ­ing, es­pe­cially in the hu­man­i­ties and
the so­cial sci­ences. All quote styles as well as the op­tional ac­tive
quotes are freely con­fig­urable.

```
\usepackage[autostyle, english = american]{csquotes}
```

## [nag](http://www.ctan.org/pkg/nag)

Warns when you accidentally use deprecated LaTeX constructs from
**l2tabu**. Place below line before the `\documentclass`:

`\RequirePackage[l2tabu, orthodox]{nag}`

## [microtype](http://www.ctan.org/pkg/microtype)

It plays with ever-so-slightly shrinking and stretching of the fonts and
with the extent to which text protrudes into the margins in a way that
yields results that look better, that have fewer instances of
hyphenation, and fewer overfull *hboxes*.

`\usepackage[stretch=10]{microtype}`

## [hyperref](http://tug.org/applications/hyperref/)

Extensive support for hypertext in LATEX.

The hy­per­ref pack­age is used to han­dle cross-ref­er­enc­ing
com­mands in LATEX to pro­duce hy­per­text links in the doc­u­ment. The
pack­age pro­vides back­ends for the \spe­cial set de­fined for HyperTEX
DVI pro­ces­sors; for em­bed­ded pdf­mark com­mands for pro­cess­ing by
Acro­bat Dis­tiller (dvips and Y&Y’s dvip­sone); for Y&Y’s dvi­windo;
for PDF con­trol within pdfTEX and dvipdfm; for TEX4ht; and for VTEX’s
pdf and HTML back­ends.

The pack­age is dis­tributed with the back­ref and nameref pack­ages,
which make use of the fa­cil­i­ties of hy­per­ref.

## [geometry](http://www.ctan.org/pkg/geometry)

Flexible and complete interface to document dimensions.

## [amsmath](http://ctan.org/pkg/amsmath)

AMS mathematical facilities for LATEX.

The prin­ci­pal pack­age in the AMS-LATEX dis­tri­bu­tion. It adapts for
use in LATEX most of the math­e­mat­i­cal fea­tures found in AMS-TEX; it
is highly rec­om­mended as an ad­junct to se­ri­ous math­e­mat­i­cal
type­set­ting in LATEX.

When ams­math is loaded, AMS-LATEX pack­ages ams­bsy (for bold
sym­bols), am­sopn (for op­er­a­tor names) and am­s­text (for text
em­bed­ded in math­e­mat­ics) are also loaded.

ams­math is part of the LATEX re­quired dis­tri­bu­tion; how­ever,
sev­eral con­tributed pack­ages add still fur­ther to its ap­peal;
ex­am­ples are em­pheq, which pro­vides func­tions for dec­o­rat­ing and
high­light­ing math­e­mat­ics, and nthe­o­rem, for spec­i­fy­ing
the­o­rem (and sim­i­lar) def­i­ni­tions.

## amsthm

Typesetting theorems (AMS style).

The pack­age fa­cil­i­tates the kind of the­o­rem setup typ­i­cally
needed in Amer­i­can Math­e­mat­i­cal So­ci­ety pub­li­ca­tions. The
pack­age of­fers the the­o­rem setup of the AMS doc­u­ment classes
(am­sart, ams­book, etc.) en­cap­su­lated in LATEX pack­age form so that
it can be used with other doc­u­ment classes.

Am­sthm is part of the (re­quired) AMS-LATEX dis­tri­bu­tion, so should
be present in any LATEX dis­tri­bu­tion.

## amsfonts

TEX fonts from the American Mathematical Society.

An ex­tended set of fonts for use in math­e­mat­ics, in­clud­ing: ex­tra
math­e­mat­i­cal sym­bols; black­board bold let­ters (up­per­case only);
frak­tur let­ters; sub­script sizes of bold math italic and bold Greek
let­ters; sub­script sizes of large sym­bols such as sum and prod­uct;
added sizes of the Com­puter Modern small caps font; cyril­lic fonts
(from the Univer­sity of Wash­ing­ton); Euler math­e­mat­i­cal fonts.
All fonts are pro­vided as Adobe Type 1 files, and all ex­cept the Euler
fonts are pro­vided as METAFONT source.

The dis­tri­bu­tion also in­cludes the canon­i­cal Type 1 ver­sions of
the Com­puter Modern fam­ily of fonts.

Ba­sic LATEX sup­port for the sym­bol fonts is pro­vided by
ams­fonts.sty, with names of in­di­vid­ual sym­bols de­fined in
amssymb.sty. The Euler fonts are sup­ported by sep­a­rate pack­ages;
de­tails can be found in the doc­u­men­ta­tion.

## mathtools

Mathematical tools to use with amsmath.

It will load amsmath if it's not loaded.

Math­tools pro­vides a se­ries of pack­ages de­signed to en­hance the
ap­pear­ance of doc­u­ments con­tain­ing a lot of math­e­mat­ics. The
main back­bone is ams­math, so those un­fa­mil­iar with this re­quired
part of the LATEX sys­tem will prob­a­bly not find the pack­ages very
use­ful.

Math­tools pro­vides many use­ful tools for math­e­mat­i­cal
type­set­ting. It is based on ams­math and fixes var­i­ous
de­fi­cien­cies of ams­math and stan­dard LATEX. It pro­vides:

Ex­ten­si­ble sym­bols, such as brack­ets, ar­rows, har­poons, etc.;
Var­i­ous sym­bols such as \coloneqq (:=); Easy cre­ation of new tag
forms; Show­ing equa­tion num­bers only for ref­er­enced equa­tions;
Ex­ten­si­ble ar­rows, har­poons and hookar­rows; Starred ver­sions of
the ams­math ma­trix en­vi­ron­ments for spec­i­fy­ing the col­umn
align­ment; More build­ing blocks: mult­lined, cases-like
en­vi­ron­ments, new gath­ered en­vi­ron­ments; Maths ver­sions of
\make­box, \llap, \rlap etc.; Cramped math styles; and more...

## cancel

Place lines through maths formulae.

A pack­age to draw di­ag­o­nal lines (“can­celling” a term) and ar­rows
with lim­its (can­celling a term “to a value”) through parts of maths
for­mu­lae.

## [urlbst](http://nxg.me.uk/dist/urlbst/)

Web support for BibTEX.

## [booktabs](http://www.ctan.org/pkg/booktabs)

Publication quality tables in LATEX.

## [array](http://www.ctan.org/pkg/array)

Extending the array and tabular environments.

## [memoir](http://www.ctan.org/pkg/memoir)

Typeset fiction, non-fiction and mathematical books

## [koma-script](http://www.ctan.org/pkg/koma-script)

A bundle of versatile classes and packages.


## [pgf-TikZ](http://sourceforge.net/projects/pgf/)

Create PostScript and PDF graphics in TEX.

TikZ and PGF are TeX packages for creating graphics programmatically.
TikZ is build on top of PGF and allows you to create sophisticated
graphics in a rather intuitive and easy manner.

PGF is a macro pack­age for cre­at­ing graph­ics. It is plat­form- and
for­mat-in­de­pen­dent and works to­gether with the most im­por­tant TEX
back­end drivers, in­clud­ing pdfTEX and dvips. It comes with a
user-friendly syn­tax layer called TikZ.

Its us­age is sim­i­lar to pstricks and the stan­dard pic­ture
en­vi­ron­ment. PGF works with plain (pdf-)TEX, (pdf-)LATEX, and
ConTEXt. Un­like pstricks, it can pro­duce ei­ther PostScript or PDF
out­put.

## graphicx

Enhanced support for graphics.

The pack­age builds upon the graph­ics pack­age, pro­vid­ing a key-value
in­ter­face for op­tional ar­gu­ments to the \in­clude­graph­ics
com­mand. This in­ter­face pro­vides fa­cil­i­ties that go far be­yond
what the graph­ics pack­age of­fers on its own.

For ex­tended doc­u­men­ta­tion, see ep­s­la­tex.

The pack­age is part of the la­tex-graph­ics bun­dle, which is one of
the col­lec­tions in the LATEX ‘re­quired’ set of pack­ages.


## enumitem

Control layout of itemize, enumerate, description.

This pack­age pro­vides user con­trol over the lay­out of the three
ba­sic list en­vi­ron­ments: enu­mer­ate, item­ize and de­scrip­tion. It
su­per­sedes both enu­mer­ate and md­wlist (pro­vid­ing well-struc­tured
re­place­ments for all their fun­tion­al­ity), and in ad­di­tion
pro­vides func­tions to com­pute the lay­out of la­bels, and to ‘clone’
the stan­dard en­vi­ron­ments, to cre­ate new en­vi­ron­ments with
coun­ters of their own.

## fancyhdr

Extensive control of page headers and footers in LATEX2ε.

The pack­age pro­vides ex­ten­sive fa­cil­i­ties, both for
con­struct­ing head­ers and foot­ers, and for con­trol­ling their use
(for ex­am­ple, at times when LATEX would au­to­mat­i­cally change the
head­ing style in use).

## mdframed

Framed environments that can split at page boundaries.

The pack­age de­vel­ops the fa­cil­i­ties of framed in pro­vid­ing
break­able framed and coloured boxes.

The user may in­struct the pack­age to per­form its op­er­a­tions us­ing
de­fault LATEX com­mands, PStricks or TikZ.

## longtable

## [listing](http://www.ctan.org/tex-archive/macros/latex/contrib/listings/)

## [verbatim]()

# Bibliography

## Back-end bibliography processor

### [BibTeX](https://en.wikipedia.org/wiki/BibTeX)

BibTeX is reference management software for formatting lists of
references. BibTeX was created by Oren Patashnik and Leslie Lamport in
1985. It is written in WEB/Pascal.

#### Basic structure

Input:

- An `.aux` file produced by LaTeX on an earlier run.
- A `.bst` file (the style file), which specifies the general reference-list style and specifies how to format individual entries, and which is written by a style designer [..] in a special-purpose language [..].
- A `.bib` file(s) create a database of all reference-list entries the user might ever hope to use.

BibTeX chooses from the `.bib` file(s) only those entries specified by the `.aux` file (that is, those given by LaTeX's `\cite` or `\nocite` commands), and creates as **output** a `.bbl` file containing these entries together with the formatting commands specified by the `.bst` file [..]. LaTeX will use the `.bbl` file, perhaps edited by the user, to produce the reference list.

`aux + bib -> bbl + bib -> ref list`

#### [Style examples](http://www.cs.stir.ac.uk/~kjt/software/latex/showbst.html)

#### [bib file](https://en.wikipedia.org/wiki/BibTeX#Bibliographic_information_file)

- Cross-referencing.
- Using more than one bib file.
- Non-reference section
	+ @COMMENT{...}


### [Biber](http://biblatex-biber.sourceforge.net/)

[manual](http://mirrors.ctan.org/biblio/biber/documentation/biber.pdf)

## Packages

- `\cite{cite_key}`
- `\cite[p.~215]{citation01}`
- `\cite{citation01,citation02,citation03}`
- `\nocite{citation01}` : ref appear in bibliography but not where it is ref in the main text.

### [natbib](http://ctan.org/pkg/natbib)

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

- Using the symbol `%` to comment some texts.

## The preamble of a document

- Everything before the line `\begin{document}`
- You define
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

- `\textbf{...}`
- `\textit{...}`
- `\underline{...}`

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

- There are three important commands in the example:
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
- When placing images in a LATEX document, we should always put them
  inside a figure environment or similar so that LATEX will position the
  image in a way that fits in with the rest of your text.

## Creating lists

### Unordered lists

```
\begin{itemize}
  \item The individual entries are indicated with a black dot, a so-called bullet.
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

- Two modes to write mathematical expressions:
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
In physics, the mass-energy equivalence is stated
by the equation $E=mc^2$, discovered in 1905 by Albert Einstein.

% Display
The mass-energy equivalence is described by the famous equation

\[E=mc^2\]

discovered in 1905 by Albert Einstein.
In natural units ($c = 1$), the formula expresses the identity

\begin{equation}
E=m
\end{equation}
```

- Using `amsmath` package for more flexibility.

## Basic Formatting

### Lengths in LaTeX

#### Units

| Abbreviation | Value                                                                                                                                                                           |
| -            | -                                                                                                                                                                               |
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

For example, in a two-column document the column separation can be set
to 1 inch by:

`\setlength{\columnsep}{1in}`


| Length          | Description                                                              |
| -               | -                                                                        |
| \baselineskip   | Vertical distance between lines in a paragraph                           |
| \columnsep      | Distance between columns                                                 |
| \columnwidth    | The width of a column                                                    |
| \evensidemargin | Margin of even pages, commonly used in two-sided documents such as books |
| \linewidth      | Width of the line in the current environment.                            |
| \oddsidemargin  | Margin of odd pages, commonly used in two-sided documents such as books  |
| \paperwidth     | Width of the page                                                        |
| \paperheight    | Height of the page                                                       |
| \parindent      | Paragraph indentation                                                    |
| \parskip        | Vertical space between paragraphs                                        |
| \tabcolsep      | Separation between columns in a table (tabular environment)              |
| \textheight     | Height of the text area in the page                                      |
| \textwidth      | Width of the text area in the page                                       |
| \topmargin      | Length of the top margin                                                 |

- Default lengths can not only be set to any desired value, they can
  also be used as units to set the dimensions of other LATEX elements.
  For instance, you can set an image to have a width of one quarter the
  total text width.

```
\includegraphics[width=0.25\textwidth]{lion-logo}
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

- A new line without starting a new paragraph: add a break line
    + `\\`
    + `\newline`
- A new paragraph:
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

If you want to create a non-indented paragraph, like the second one in
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

In the example above, \renewcommand{\baselinestretch}{1.5} scales the default interline space to 1.5 its default value. Of course that number can be set to any value.

As mentioned before, there are other two LATEX lengths that may change
the line spacing:

- \baselineskip
    + Is a length determining the minimum space between the bottom of
      two successive lines in a paragraph; it may be changed (in the
      preamble) by \setlength{\baselineskip}{value}. Where value is set
      using any of the LaTeX units.
- \linespread{value}
    + where value determine line spacing. This value is somewhat
      confusing, because:

Value   Line spacing
1.0 single spacing
1.3 one-and-a-half spacing
1.6 double spacing

### Text alignment

Text alignment can be manually controlled by several commands.


| Alignment       | Environment | Switch command | ragged2e environment | ragged2e switch command |
| -               | -           | -              | -                    | -                       |
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

-1  \part{part}
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

- `\tableofcontents`

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

# Mac OS - MacTeX

- http://www.tug.org/mactex/

## Installing packages

- For packages found on CTAN: use the TeX Live Utility found in your
  /Applications/TeX folder. This application can keep all of your TeX
  packages up to date.
- Place the relevant files in `~/Library/texmf/tex/latex`. TeX will find
  them.
- Enter `tlmgr install *packagename*` in the terminal


# Writing mathematical document with amsmath

- Usage guide: http://texdoc.net/texmf-dist/doc/latex/amsmath/amsldoc.pdf

# Drawing electrical circuits

- https://www.overleaf.com/learn/latex/LaTeX_Graphics_using_TikZ:_A_Tutorial_for_Beginners_(Part_4)%E2%80%94Circuit_Diagrams_Using_Circuitikz
- https://www.latex-tutorial.com/tutorials/circuitikz/

# Tips and Tricks

## Add text in math mode

- \text{}
- https://tex.stackexchange.com/questions/3415/what-is-the-correct-way-of-embedding-text-into-math-mode#3418

## Align multiline equation with indent equal signs

```
\documentclass{article}

\usepackage{amsmath}


\begin{document}

\begin{align*}
\mathcal{L}^{-1}\left\{f(d)\right\} &= \mathcal{L}^{-1}\left\{f_1(\delta).f_2(\delta)\right\} \\
                                    &= \exp(mt) \star \left\{\frac{l}{2\sqrt{\pi t^3}} \exp(-l^2/{4t})\right\} \\
                                    &= F_1 * F_2
\end{align*}

\end{document}
```

## Create posters using LaTeX

- https://tex.stackexchange.com/questions/341/how-to-create-posters-using-latex
    + beamerposter
    + fancytikzposter
    + baposter
- templates
    + https://www.latextemplates.com/cat/conference-posters
    + https://www.overleaf.com/gallery/tagged/poster

## [Latex templates](https://github.com/bamos/latex-templates)

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

# Alternatives

- https://tex.stackexchange.com/questions/120271/alternatives-to-latex

# References
