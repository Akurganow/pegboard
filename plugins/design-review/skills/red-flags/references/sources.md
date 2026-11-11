<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Sources](#sources)
  - [The book](#the-book)
  - [Ousterhout and Martin](#ousterhout-and-martin)
  - [Parnas](#parnas)
  - [Brooks](#brooks)
  - [Google's reviewer guide](#googles-reviewer-guide)
  - [Go names](#go-names)
  - [Nygard's decision record](#nygards-decision-record)
  - [Studies on change history](#studies-on-change-history)
  - [Studies on test-driven development and method length](#studies-on-test-driven-development-and-method-length)
  - [Not read](#not-read)
  - [What the skill adds on its own](#what-the-skill-adds-on-its-own)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Sources

Where each text was read, its kind, and what it supports. Dates are the day of
reading, 2026-09-24 or 2026-11-11; a source read on the first date was
re-checked on the second. A quotation in a reference names the book's section
or the study.

## The book

John Ousterhout, *A Philosophy of Software Design*. First edition, Yaknyam
Press, April 2018, ISBN 978-1732102200. Second edition, Yaknyam Press, July
2021, ISBN 978-1732102217 (Open Library record,
<https://openlibrary.org/api/books?bibkeys=ISBN:9781732102200,ISBN:9781732102217&format=json&jscmd=data>,
read 2026-11-11; the author's extract prints ISBN 978-1-7321022-2-4 for the
second edition, and the two forms were not reconciled). Section numbers here
are the second edition's.

No copy of either edition was bought. Kinds of copy read:

- The author's extract of the second edition, which holds chapter 6, §9.8,
  §9.9, §12.6 and chapter 21 (<https://web.stanford.edu/~ouster/cgi-bin/aposd2ndEdExtract.pdf>,
  20 pages, read by optical character recognition, 2026-11-11). The author's
  page (<https://web.stanford.edu/~ouster/cgi-bin/aposd.php>, read 2026-11-11)
  says what the second edition changed.
- The second edition's English text in a public translation repository,
  <https://github.com/yingang/aposd2e-zh/tree/4362314d5bb8eedbe2a088f950850a187b3f8641/docs/en>
  (read 2026-11-11). Its `summary.md` is the source of the sixteen principles
  and fourteen flags, compared item by item with the extract and the first
  edition's list, all matching. The book's list reads "its hard" in the
  Conjoined Methods definition, and `SKILL.md` quotes it as printed.
  Quotations marked **2e** come from this copy or the extract. Whether the copy
  is authorised was not established.
- The first edition's English text,
  <https://github.com/Cactus-proj/A-Philosophy-of-Software-Design-zh/tree/20d96914b82f02c225cc1530022555d84c27b096/docs>
  (read 2026-11-11). Quotations marked **1e** come from it, at the section the
  second edition gives the same text. The first edition numbers Conjoined
  Methods §9.8, not §9.7, because chapter 6 absorbed §9.7 and §10.9 and §9.8
  and §12.6 were added. It prints the flag boxes of Repetition (p. 68) and
  Special-General Mixture (p. 71) one section after the section that argues
  them, so `SKILL.md` cites §9.3 and §9.4. The sections of eleven flags were
  checked against its chapter headings. The Overexposure box follows §5.7
  "Example: defaults in HTTP responses".
- Principles lists in <https://github.com/dmahr1/quick-reference/blob/6330aea52335dcc9c788b3c0475f1684194aae50/index.md>
  and <https://github.com/farzinnasiri/learning-hub/blob/6e62cdcda06d5396f9f622a945d13ae93b8a6891/software-engineering/philosophy-of-software-design.md>,
  read 2026-09-24 and compared with the second edition's. The first edition's
  fifteen were read in <https://github.com/haiiiiiyun/haiiiiiyun.github.io/blob/78ed1d4140ace5e703f3eb08c0eb0b9118126cc1/_posts.bak/2019-02-27-tips-from-a-philosophy-of-software-design.md>.
  Nothing is quoted from these.

Principle 6 lists pp. 61 and 74; the page numbers could not be tied to
second-edition sections without the printed book, so the skill cites chapter 8
and says p. 74 is in chapter 9. The second edition's §14.6 was read by heading
there and by body in the first edition's §14.5. Its §19.4 body was not read.
The preface calls the book "an opinion piece", so nothing in the skill is
described as research. Course notes restating the definition, symptoms and
causes: <https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=complexity>
(read 2026-11-11).

## Ousterhout and Martin

"A Philosophy of Software Design vs Clean Code", a written discussion from
September 2024 to February 2025, <https://github.com/johnousterhout/aposd-vs-clean-code/blob/2ce0742228fbf850e15101f83308de2cd72144b2/README.md>
(full text, read 2026-09-24 and 2026-11-11; the commit was the head of `main`
on the second date). Quotations name its section headings: Introductions,
Method Length, Method Length Summary, Comments, Comments Summary,
Test-Driven Development and TDD Summary. The one *Clean Code* sentence quoted
is the one Ousterhout quotes there.

## Parnas

D. L. Parnas, "On the Criteria To Be Used in Decomposing Systems into
Modules", *Communications of the ACM* 15(12), 1972, pp. 1053-1058, the scan at
<https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf>
(full text, optical character recognition, read 2026-11-11). Both quotations
are from its "Conclusion". Volume, issue and pages from the Crossref record,
<https://api.crossref.org/works/10.1145/361598.361623>.

## Brooks

Frederick P. Brooks, Jr., "No Silver Bullet", 1986, read 2026-11-11 in two
copies: the anniversary-edition reprint of *The Mythical Man-Month* (1995),
<https://worrydream.com/refs/Brooks_1986_-_No_Silver_Bullet.pdf>, whose wording
`complexity.md` uses, and the UNC technical report TR86-020,
<https://www.cs.unc.edu/techreports/86-020.pdf>, which words the accident
definition "those difficulties which today attend its production but which are
not inherent". The 1975 *Mythical Man-Month* was not read.

## Google's reviewer guide

Google, "What to look for in a code review" and "The Standard of Code Review",
`eng-practices` at commit `3bb3ec2`:
<https://github.com/google/eng-practices/blob/3bb3ec25b3b0199f4940b1aa75f0ac5c5753301c/review/reviewer/looking-for.md>
and
<https://github.com/google/eng-practices/blob/3bb3ec25b3b0199f4940b1aa75f0ac5c5753301c/review/reviewer/standard.md>
(documentation, read 2026-09-24, re-checked 2026-11-11). The quotations are
from the first.

## Go names

Andrew Gerrand, "What's in a name?", 2014 (slides,
<https://talks.golang.org/2014/names.slide>, read 2026-11-11). Ousterhout's
reply is in the first edition's §14.5.

## Nygard's decision record

Michael Nygard, "Documenting Architecture Decisions", 15 November 2011
(full post, <https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions>,
read 2026-11-11). Its parts are Title, Context, Decision, Status and
Consequences, in that order. The two questions that a repository's template
page prints under Context and Consequences are not in the post, so the skill
does not quote them.

## Studies on change history

Read as the kind named, 2026-11-11.

- Nagappan and Ball, ICSE 2005 (full text,
  <https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/icse05churn.pdf>).
- Graves, Karr, Marron and Siy, *IEEE TSE* 26(7), 653-661, 2000 (abstract,
  <https://doi.org/10.1109/32.859533>).
- Ostrand, Weyuker and Bell, *IEEE TSE* 31(4), 340-355, 2005 (abstract,
  <https://doi.org/10.1109/tse.2005.49>).
- Moser, Pedrycz and Succi, ICSE 2008 (abstract,
  <https://doi.org/10.1145/1368088.1368114>). Rahman and Devanbu, ICSE 2013
  (abstract, <https://doi.org/10.1109/icse.2013.6606589>).
- Sjøberg, Yamashita, Anda, Mockus and Dybå, *IEEE TSE* 39(8), 1144-1156,
  2013 (abstract, <https://doi.org/10.1109/tse.2012.89>).
- Tornhill and Borg, "Code Red", TechDebt 2022 (nearly all of the full text,
  <https://arxiv.org/abs/2203.04374>). The paper prints Tornhill at CodeScene,
  whose tool produces the score, and Borg at RISE and Lund University.
- No peer-reviewed test of change frequency multiplied by complexity as a
  ranking was found in a search of OpenAlex and the web on 2026-11-11.

## Studies on test-driven development and method length

- Rafique and Mišić, *IEEE TSE* 39(6), 835-856, 2013 (author manuscript, full
  text, <https://raidoninc.com/assets/research/tddMetaAnalysis.pdf>; abstract,
  <https://ieeexplore.ieee.org/document/6197200>).
- Fucci and others, *IEEE TSE* 43(7), 597-614, 2017 (arXiv full text,
  <https://arxiv.org/abs/1611.05994>).
- Landman, Serebrenik and Vinju, ICSME 2014, 221-230 (abstract,
  <https://doi.org/10.1109/icsme.2014.44>).
- Fenton and Ohlsson, *IEEE TSE* 26(8), 797-814, 2000 (abstract,
  <https://doi.org/10.1109/32.879815>). Fenton and Neil, *IEEE TSE* 25(5),
  675-689, 1999 (abstract, <https://doi.org/10.1109/32.815326>).
- Pascarella, Palomba and Bacchelli, SANER 2018, 592-601 (abstract,
  <https://doi.org/10.1109/saner.2018.8330264>).

## Not read

Nothing in this skill is quoted from these.

- Robert C. Martin, *Clean Code*, Prentice Hall, 2008, beyond the sentence
  Ousterhout quotes.
- The text of chapters 2 to 5, 7, 8, 10, 11 and 13 to 19 of the book in print,
  beyond the translation copies above; the second edition's §14.6 and §19.4
  bodies.
- Tornhill's SREcon24 slides and book *Software Design X-Rays*.

## What the skill adds on its own

These parts of `SKILL.md` and the references are this skill's adaptation, not
the book's text:

- The order of the steps, the frame step, and the routing of a one-question
  user to a step.
- Reading the frame and weights from the code and its history, and change
  history as a proxy for the book's time spent (§2.1). The studies bear on the
  ingredients, not on the ranking.
- The depth step as what a caller must know against what the module does. The
  cost and benefit wording is the book's (§4.4). The list of what a caller must
  know, and the calibration that a small utility or thin adapter is shallow by
  nature, are the skill's.
- Recording a reason the user gives beside the finding, and dropping the finding
  when it outweighs the flag.
- Ranking by the part's weight, and giving no other overall ranking.
- Every "Look for" in `red-flags.md`.
- The reading of principle 7 as bounded by Google's over-engineering line, and
  of principles 6 and 10 as one idea from two sides, in `principles.md`.
- The reading of Brooks against Ousterhout, and the line between the book's
  "cognitive load" and the theory's, in `complexity.md`.
- The "For a review" paragraphs in `positions.md`.
- The hand-overs to `extraneous`, `contradiction` and `root-cause`.
