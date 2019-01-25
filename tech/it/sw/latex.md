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


# Alternatives

- https://tex.stackexchange.com/questions/120271/alternatives-to-latex

# References
