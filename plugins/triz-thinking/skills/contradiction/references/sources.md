<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Sources](#sources)
  - [The contradiction matrix](#the-contradiction-matrix)
  - [The 40 principles](#the-40-principles)
  - [Parameter names](#parameter-names)
  - [Separation principles](#separation-principles)
  - [ARIZ-85C](#ariz-85c)
  - [Standard solutions](#standard-solutions)
  - [Software analogies of the principles](#software-analogies-of-the-principles)
  - [Evidence on TRIZ with language models](#evidence-on-triz-with-language-models)
  - [Not read](#not-read)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Sources

What the references of this skill and of the `ariz` skill rest on. Dates are
the day of reading. "The Foundation" is the Altshuller Foundation. Its pages
are the publisher's own (documentation) and were read in full. How the matrix
was settled is in [`matrix/provenance.md`](matrix/provenance.md).

## The contradiction matrix

- The Foundation's table, <https://www.altshuller.ru/triz/technique2.asp>,
  documentation, 2026-11-11. What it claims to be, and how it differs from the
  matrix here, is in `matrix/provenance.md`.
- L1, an English spreadsheet, in
  <https://github.com/kamil-szczepanik/TRIZ-Agents/tree/23d5deb78a892a3dbb256b8c563a1b3c6f4a3fe2>
  and, unchanged, in three other repositories, 2026-09-23. Its metadata names
  an author and a creation date in 1997. One cell repeats a principle number.
  The WUMM project labels it "Matrix 1985".
- L2, two transcriptions of the Foundation's table that agree on every
  cell, 2026-09-23: a Russian CSV in
  <https://github.com/Meekl-e/workshop6_TRIZ/tree/9503eb38d2b9df126c3a84cce4aa85d69fd7c568>,
  which names no source, and `Matrix/Matrix1971.json` in
  <https://github.com/wumm-project/RDFData/tree/305000d4646e29d7170e4ddc0254502d4742fba4>,
  whose README names the Foundation's page and labels the table "Matrix 1971".
- L3, known only through the 29 disagreements with L1 that
  <https://github.com/The-Leach/triz/blob/f83ab4647d9e714d8cbbdfd03468307de2d6bd09/data/matrix-crosscheck.md>
  records against "an independently published copy", 2026-09-23.
- L4, a fragment from lecture notes in
  <https://github.com/cowdedroyal/Creative_thinking/tree/1687f559a051d261a34dabd2da7ed303c4b88e46>,
  2026-09-23.
- Altshuller, «Творчество как точная наука» (Moscow: Sovetskoe radio, 1979),
  Russian original, copy at
  <https://github.com/wumm-project/OpenDiscovery/blob/eff06517637079619c97d598135cd5c9a409f615/Sources/Altshuller_GS/Altshuller-1979-ru.pdf>,
  2026-09-23. The table came from about 40,000 descriptions of high-level
  inventions and was corrected for three years.
- Altshuller, history of ARIZ, 1986,
  <https://www.altshuller.ru/triz/ariz-about1.asp>, 2026-11-11. ARIZ-71
  completed the table. ARIZ-77 kept it «в качестве вспомогательного
  материала» [as auxiliary material].
- Darrell Mann and Simon Dewulf, "Updating the Contradiction Matrix" (2003),
  copy at
  <https://github.com/arvindvenkatadri/teachingtriz/blob/e10f20c61a4907b453fd8863a8cff7bd98247a73/content/TRIZ/Modules/400-TRIZ-References/TRIZ-Related/Updating_the_Contradiction_Matrix.pdf>,
  2026-09-23. It notes a "lack of data concerning the detailed make-up of
  the classical Matrix" and that the classic parameters do not fit software.

None of the transcriptions is a scan of a printed edition. No published
mapping of the 39 parameters to software and no study of the classic matrix
on software problems was found, so the software readings in `parameters.md`
and `principles.md` are this skill's own. The transcriptions that speak to it
say the matrix, the parameters and the principles are public domain, and no
legal source for that was read. Matrix 2003 and Matrix 2010 are separate
works, and nothing from them is carried.

## The 40 principles

The sub-items in `principles.md` paraphrase the Foundation's list,
<https://www.altshuller.ru/triz/technique1.asp>, headed «© Альтшуллер Г.С.,
1973», 2026-11-11. It gives the 1979 wording of some principles beside the
1973 one, from «Творчество как точная наука», pp. 85-89. An entry says which
wording it follows. The Foundation's Russian names of 9, 10, 16, 22 and 28
differ from the English ones, and `principles.md` says how. Ten further
techniques, 41 to 50, are at
<https://www.altshuller.ru/triz/technique1a.asp>, with no date of writing.
The matrix uses 1 to 40, and nothing more is carried.

## Parameter names

The names in `parameters.md` match the row labels of the Foundation's table in
all 39 numbers and their order, 2026-11-11. Parameters 10, 18 and 37 differ
from some English lists, as the table there says.

## Separation principles

- The four of ARIZ-77, step 4.1,
  <https://www.altshuller.ru/triz/ariz77.asp>, 2026-11-11. They agree with the
  four of the 1979 book above.
- The eleven of ARIZ-85-В Table 2,
  <https://www.altshuller.ru/triz/ariz85v-t2.asp>, 2026-11-11.
- The four of later teaching: Valeri Souchkov, *Glossary of TRIZ and
  TRIZ-Related Terms*, version 1.0, MATRIZ, 2014, and *Teaching TRIZ at
  School*, TETRIS handbook, 2009, chapter 5, copies in
  <https://github.com/arvindvenkatadri/teachingtriz/tree/e10f20c61a4907b453fd8863a8cff7bd98247a73/content/TRIZ/Modules/400-TRIZ-References>,
  2026-09-23. The tables of Litvin and of Zlotin and Zusman that attach
  principles to each separation are in
  <https://github.com/Robert-Adunka/triz-skills/tree/3d78740eac639a39f19a95a9aaa17c521497a3b9/physical-contradictions/references>,
  2026-09-23.

## ARIZ-85C

All read on 2026-11-11.

- The Foundation's Russian text of АРИЗ-85-В, documentation, from
  <https://www.altshuller.ru/triz/ariz85v.asp>, its pages `ariz85v-1.asp` to
  `ariz85v-9.asp`, and the tables `ariz85v-t1.asp` and `ariz85v-t2.asp`,
  headed «© Альтшуллер Г.С., 1985». It has nine parts and 40 steps, counted
  from the pages: 7, 3, 6, 7, 4, 4, 4, 3 and 2. The Russian formulas in
  [`ariz-85c.md`](../../ariz/references/ariz-85c.md) are from it.
- MATRIZ's English text, translation, full text, 25 pages,
  <https://matriz.org/wp-content/uploads/2025/09/Altshuller_ARIZ-85-C_en.pdf>.
  It names no translator, says it is based on Philatov, Zusman, Altshuller and
  Zlotin, *Tools of Classical TRIZ* (Southfield: Ideation Intl Inc, 1999), and
  has the same 40 step numbers. It prints no Table 2 and no warning about
  hours of study. The English patterns in `ariz-85c.md` are from it, unless a
  line says otherwise.
- A 33-page English copy, translation, full text, "Algorithm of Inventive
  Problem Solving, © G.S. Altshuller, 1956-1985", translator not named,
  <https://github.com/arvindvenkatadri/teachingtriz/blob/e10f20c61a4907b453fd8863a8cff7bd98247a73/content/TRIZ/Modules/400-TRIZ-References/TRIZ-Related/ariz85c_en.pdf>.
  It is the only copy read with the warning about at least 80 academic hours
  of study and with the English wording of Table 2.
- Altshuller's 1986 history of ARIZ, above, for the version names. The count
  of 40 steps in nine parts is from the Foundation's pages and MATRIZ's text.

The printed editions «Найти идею» (Novosibirsk: Nauka, 1986) and «АРИЗ — значит
победа» (in «Правила игры без правил», Petrozavodsk: Karelia, 1989, pp.
11-50) were not opened.

## Standard solutions

The package carries none. The Foundation's page
<https://www.altshuller.ru/triz/standards.asp>, headed «© Альтшуллер Г.С. В
сб. «Нить в лабиринте». - Петрозаводск: Карелия, 1988. - С. 165-230»,
2026-11-11, lists 76 in five classes: 13, 23, 6, 17 and 17.

Two software readings were found, neither a mapping. Lee, Shim and Kim,
"Software Engineering Performance and Quality Assessment by TRIZ", *Acta
Technica Napocensis* 63 (special issue), October 2020,
<https://atna-mam.utcluj.ro/index.php/Acta/article/download/1394/1188>, paper
full text, 2026-11-11: su-field model and the 76 standards applied to KPI
dashboards at one advertisement service. Li Munan, "Research on the
Improvement of Software Design Pattern Based on Substance-field Analysis and
Standard Solutions of TRIZ", *Journal of Applied Sciences* 13(12), 2013, DOI
10.3923/jas.2013.2217.2224: Crossref record only, abstract not read.

## Software analogies of the principles

- Kevin C. Rea, "TRIZ and Software - 40 Principle Analogies", *TRIZ
  Journal*, September and November 2001,
  <https://www.metodolog.ru/triz-journal/archives/2001/09/e/index.htm> and
  <https://www.metodolog.ru/triz-journal/archives/2001/11/e/index.htm>, paper
  full text, 2026-11-11. No analogy for 29, 31, 36, 37, 38 and 39. The
  "Published (Rea)" lines in `principles.md` are his.
- Ron Fulbright, "TRIZ and Software Fini", *TRIZ Journal*, August 2004,
  <https://whereinnovationbegins.net/wp-content/uploads/2017/01/TRIZandSoftwareFini.pdf>,
  paper full text, 2026-11-11. Analogies for 31, 36, 37, 38 and 39, none for
  29. The "Published (Fulbright)" lines are his.
- Hartmut Beckmann, *Procedia Engineering* 131 (2015), pp. 993-1001, DOI
  10.1016/j.proeng.2015.12.413: Crossref record, 2026-11-11. Full text not
  read.
- Umakant Mishra, *TRIZ Principles for Information Technology* (2010, ISBN
  9788184651843) and Darrell Mann, *Systematic (Software) Innovation* (IFR
  Press, 2007 per Mann's own
  [paper](https://www.aitriz.org/articles/TRIZFeatures/323031312D30382D4D616E6E.pdf),
  read 2026-11-11): not read. No software parameter list was found in an open
  source.

## Evidence on TRIZ with language models

Software-specific evidence for the classic matrix with a language model, 2023
to 2026, was searched for and not found.

- AutoTRIZ, <https://arxiv.org/abs/2403.13002>, full text, 2026-11-11. Ten
  textbook cases, GPT-4: seven of ten match or half-match the textbook's
  contradiction analysis in the top three detections. The authors report no
  objective measure of solution quality.
- TRIZ-GPT, <https://arxiv.org/abs/2408.05897>, and TRIZ Agents,
  <https://arxiv.org/abs/2506.18783>, abstracts, 2026-11-11. Mechanical and
  engineering cases, no software case.
- TRIZ^a, <https://arxiv.org/abs/2610.04555>, preprint of 2026-10-03, abstract,
  2026-11-11. The 40 principles and the matrix guide an agent's code
  transformations on three cybersecurity datasets: F1 gains of 2.88, 4.23 and
  0.15 points, and a campaign that raised macro-F1 from 0.8325 to 0.8483 and
  did not pass its promotion gate. It compares no matrix lookup by a person
  and no direct answer.
- TRIZBench, <https://aclanthology.org/2026.findings-acl.1798/>, abstract,
  2026-11-11. Contradictions are easier to detect than to recover as
  trade-off pairs.

## Not read

- Altshuller, *40 Principles: TRIZ Keys to Technical Innovation* (1997), *The
  Innovation Algorithm* (1999, the translation of «Алгоритм изобретения»,
  1973, whose Appendix 1 the Foundation's table page claims to be) and
  *Creativity as an Exact Science* (1984, the translation of the 1979 book
  read in Russian).
- Г. Альтов, «И тут появился изобретатель» (1984), English *And Suddenly the
  Inventor Appeared* (1996).
- The 1973 printing of «Алгоритм изобретения». `matrix/provenance.md` says what
  it would settle.
