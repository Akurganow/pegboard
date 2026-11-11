<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Sources](#sources)
  - [The practitioner essay](#the-practitioner-essay)
  - [The theory](#the-theory)
    - [Which paper introduced what](#which-paper-introduced-what)
  - [The measures](#the-measures)
  - [The studies of programmers](#the-studies-of-programmers)
  - [LLM agents as readers](#llm-agents-as-readers)
  - [Not read](#not-read)
  - [What the skill adds on its own](#what-the-skill-adds-on-its-own)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Sources

What each reference rests on, which copy was read, when, and what was not read.
"Full" means the full text was read, "abstract" the abstract only,
"documentation" and "source" a vendor's documentation or code. Papers were read
on 2026-11-11 unless a date says otherwise. Quotations were matched against the
copy named, and nothing is quoted from a text that was not opened.

## The practitioner essay

Artem Zakirullin, "Cognitive load is what matters", copyright (c) 2023, CC BY
4.0, "a living document, last update: June 2026" by its status line. Read whole,
with its agent-facing summary and license, on 2026-09-24 at
<https://github.com/zakirullin/cognitive-load/tree/d2d60d2311c3854f16d87bf34f38c829667be2a4>.
Every quotation in `patterns.md` is from its `README.md` at that commit.

On 2026-11-11 the head was
<https://github.com/zakirullin/cognitive-load/tree/cb0ca8643e7d625de0705aae631f23f07dbd5a04>
(2026-10-26). Its `README.md` differs by one line, a link to a French
translation, and no quoted sentence changed. `README.agents.md` is identical.

The essay's "roughly four such chunks" links to
[issue 16](https://github.com/zakirullin/cognitive-load/issues/16). The author's
first comment (2023-05-30) cites Miller 1956 and Cowan 2001 and ends "So I chose
four". The essay's own text cites neither.

## The theory

All papers. The copy column names where the text was read.

| Paper | Read | Copy |
| :-- | :-- | :-- |
| Chandler and Sweller, "Cognitive Load Theory and the Format of Instruction", *Cognition and Instruction* 8(4), 1991, 293-332, [DOI](https://doi.org/10.1207/s1532690xci0804_2) | full | [University of Wollongong](https://ro.uow.edu.au/edupapers/128) |
| Sweller, "Cognitive load theory, learning difficulty, and instructional design", *Learning and Instruction* 4(4), 1994, 295-312, [DOI](https://doi.org/10.1016/0959-4752(94)90003-5) | full | [OCR scan](https://mrbartonmaths.com/resourcesnew/8.%20Research/Explicit%20Instruction/CLT,%20learning%20difficulty%20and%20instructional%20design.pdf), third-party; quotations come from its clean lines |
| Sweller, van Merriënboer and Paas, "Cognitive Architecture and Instructional Design", *Educational Psychology Review* 10(3), 1998, 251-296, [DOI](https://doi.org/10.1023/a:1022193728205) | full | [third-party copy](https://docdrop.org/static/drop-pdf/SwellerMerrienboerPaas1998-93QJw.pdf) |
| Paas, Renkl and Sweller, "Cognitive Load Theory and Instructional Design: Recent Developments", *Educational Psychologist* 38(1), 2003, 1-4, [DOI](https://doi.org/10.1207/s15326985ep3801_1) | full | [course-page copy](https://www.uky.edu/~gmswan3/544/Cognitive_Load_%26_ID.pdf) |
| Kalyuga, Ayres, Chandler and Sweller, "The Expertise Reversal Effect", *Educational Psychologist* 38(1), 2003, 23-31, [DOI](https://doi.org/10.1207/s15326985ep3801_4) | full | [repository copy](https://ndownloader.figshare.com/files/50479548) |
| Sweller, "Element Interactivity and Intrinsic, Extraneous, and Germane Cognitive Load", *Educational Psychology Review* 22(2), 2010, 123-138, [DOI](https://doi.org/10.1007/s10648-010-9128-5) | abstract | [publisher](https://rd.springer.com/article/10.1007/s10648-010-9128-5); full text behind a paywall |
| de Jong, "Cognitive load theory, educational research, and instructional design: some food for thought", *Instructional Science* 38, 2010, 105-134, [DOI](https://doi.org/10.1007/s11251-009-9110-0) | full | [open-access copy](https://ris.utwente.nl/ws/files/6597420/Jong10cognitive.pdf) |
| Kalyuga, *Educational Psychology Review* 23(1), 2011, 1-19, [DOI](https://doi.org/10.1007/s10648-010-9150-7) | abstract | [publisher](https://rd.springer.com/article/10.1007/s10648-010-9150-7), [ERIC](https://eric.ed.gov/?id=EJ916566); full text behind a paywall |
| Sweller, van Merriënboer and Paas, "Cognitive Architecture and Instructional Design: 20 Years Later", *Educational Psychology Review* 31, 2019, 261-292, [DOI](https://doi.org/10.1007/s10648-019-09465-5) | full | [publisher](https://rd.springer.com/article/10.1007/s10648-019-09465-5), open access |
| Cowan, "The magical number 4 in short-term memory", *Behavioral and Brain Sciences* 24, 2001, 87-114, [DOI](https://doi.org/10.1017/S0140525X01003922) | full | [Cambridge University Press](https://doi.org/10.1017/S0140525X01003922) |
| Miller, "The Magical Number Seven, Plus or Minus Two", *Psychological Review* 63, 1956, 81-97 | full | [Classics in the History of Psychology](https://psychclassics.yorku.ca/Miller/) |
| Duran, Zavgorodniaia and Sorva, "Cognitive Load Theory in Computing Education Research: A Review", *ACM Transactions on Computing Education* 22(4), 2022, [DOI](https://doi.org/10.1145/3483843) | abstract | [OpenAlex](https://api.openalex.org/works/doi:10.1145/3483843) |

Page numbers cited in `theory.md` for the 1998, 2019 and Cowan texts come from
the page headers in those copies.

### Which paper introduced what

- **Extraneous load.** Chandler and Sweller 1991, p. 296: "Ideal formats for
  initial instruction should reduce extraneous cognitive load." The 1991 text
  has no "intrinsic" and no "germane". The 2019 Table 1 dates the
  split-attention effect to Tarmizi and Sweller 1988.
- **Intrinsic load.** The earliest text read that uses the pair is Sweller 1994
  (no "germane"); its abstract says intrinsic load "is constant for a given area
  because it is a basic component of the material". Wikipedia's article on
  cognitive load (revision 1384085501, 2026-11-06) credits the 1991 paper with
  the term, which the 1991 text does not support. De Jong 2010 agrees that the
  early papers "do not distinguish between intrinsic and germane load". No
  earlier use than 1994 was found.
- **Germane load.** Sweller, van Merriënboer and Paas 1998, p. 259: "A further
  distinction can be made between extraneous cognitive load and germane
  cognitive load." The 2019 paper, p. 269, says the distinction "was
  introduced" on the strength of Paas and van Merriënboer 1994a, which was not
  read.

## The measures

- Campbell, "Cognitive Complexity", SonarSource, version 1.7, 29 August 2023.
  Full, publisher's [PDF](https://www.sonarsource.com/docs/CognitiveComplexity.pdf).
  The rules, increments and sentence on methods are verbatim.
- PMD rule `CognitiveComplexity`, `design.xml` at
  [`4a1d37d`](https://github.com/pmd/pmd/blob/4a1d37d3eb785695084393fcc7315b0aca123809/pmd-java/src/main/resources/category/java/design.xml#L299).
  Source. The text is the same at the head.
- SonarSource, Java rule S3776, at
  [`ceb8058`](https://github.com/SonarSource/sonar-java/blob/ceb8058cc5d60196c6b7641d748a079bbd473c00/sonar-java-plugin/src/main/resources/org/sonar/l10n/java/rules/java/S3776.html).
  Documentation shipped in the plugin, current at that commit.
- SonarJS `rule.ts` at
  [`793d14c`](https://github.com/SonarSource/SonarJS/blob/793d14cc05902a65682f8d59f4edf9e9d19b6334/packages/analysis/src/jsts/rules/S3776/rule.ts#L39),
  line 39, `DEFAULT_THRESHOLD = 15`. Source. The earlier home,
  `eslint-plugin-sonarjs`, is archived (last push 2024-10-03) and its
  [rule document](https://github.com/SonarSource/eslint-plugin-sonarjs/blob/fa48884330437fab852b9a52256183b7d140259b/docs/rules/cognitive-complexity.md)
  has the same default.
- Muñoz Barón, Wyrich and Wagner, ESEM 2020,
  [arXiv 2007.12520](https://arxiv.org/abs/2007.12520). Full. The table in
  `measures.md` is from its section 4.
- Tavares de Souza and Costa Pinto, ICSME 2020,
  [DOI](https://doi.org/10.1109/ICSME46990.2020.00087). Full, three pages, from
  the first author's
  [copy](https://github.com/asouza/pilares-design-codigo/blob/a693d8001b787e9e3762fdebb6f0dfc3a0784175/ICSME-2020-cognitive-driven-development.pdf).
  Quotations were matched with spacing ignored.
- Google, "Small CLs", at
  [`3bb3ec2`](https://github.com/google/eng-practices/blob/3bb3ec25b3b0199f4940b1aa75f0ac5c5753301c/review/developer/small-cls.md).
  Documentation, identical at the head on 2026-11-11.

## The studies of programmers

- Peitek and others, ICSE 2021, [DOI](https://doi.org/10.1109/icse43902.2021.00056).
  Abstract, from the [OpenAlex record](https://api.openalex.org/works/doi:10.1109/icse43902.2021.00056).
- Hansen, Goldstone and Lumsdaine, 2013, [arXiv 1304.5257](https://arxiv.org/abs/1304.5257).
  Full. The counts are from its participants section.
- Fakhoury and others, ICPC 2018, [DOI](https://doi.org/10.1145/3196321.3196347).
  Abstract, from the
  [conference page](https://conf.researchr.org/details/icpc-2018/icpc-2018-Technical-Research/35/The-Effect-of-Poor-Source-Code-Lexicon-and-Readability-on-Developers-Cognitive-Load);
  the PDF has no text layer. The extension, *Empirical Software Engineering*
  25(3), [DOI](https://doi.org/10.1007/s10664-019-09751-4), full, from the
  [submitted manuscript](https://par.nsf.gov/servlets/purl/10135165). Its first
  15 participants come from the 2018 paper.
- Baum, Schneider and Bacchelli, *Empirical Software Engineering* 24(4), 2019,
  [DOI](https://doi.org/10.1007/s10664-018-9676-8). Full, from the
  [authors' manuscript](https://tobiasbaum.github.io/rp/memoryCodeOrderAndReview.pdf).
- Crichton, Agrawala and Hanrahan, CHI 2021,
  [arXiv 2101.06305](https://arxiv.org/abs/2101.06305). Abstract.
- da Costa and others, 2026, [arXiv 2602.18579](https://arxiv.org/abs/2602.18579).
  Abstract.
- Harsch, Bye, Rus and Kendeou, Cognitive Science Society 2025. Full, from the
  [proceedings](https://journalpub.escholarship.org/cognitivesciencesociety/article/49876/galley/37838/download).
- Gonçales and others, ICPC 2019, [DOI](https://doi.org/10.1109/icpc.2019.00018).
  Abstract, from the [OpenAlex record](https://api.openalex.org/works/doi:10.1109/icpc.2019.00018).
- Wyrich, Bogner and Wagner, *ACM Computing Surveys* 56(4), 2023,
  [DOI](https://doi.org/10.1145/3626522). The text read is the full
  [arXiv preprint](https://arxiv.org/abs/2206.11102), not the journal version.
  Crossref lists a 2026 corrigendum, [DOI](https://doi.org/10.1145/3838282),
  not read, so the count of 95 experiments is the preprint's.

## LLM agents as readers

Abstracts from arXiv, read 2026-11-11, cited in the last section of
`measures.md`: [2510.03178](https://arxiv.org/abs/2510.03178),
[2601.12951](https://arxiv.org/abs/2601.12951),
[2602.07882](https://arxiv.org/abs/2602.07882) and
[2606.21804](https://arxiv.org/abs/2606.21804). They are preprints, and the
bodies were not read. The statement that no controlled study varies a code
structure and measures agent success rests on arXiv searches made on the same
day. Their queries were not recorded, and they are not a systematic review.

## Not read

- Sweller and Cooper, *Cognition and Instruction* 2, 1985, 59-89, and Tarmizi
  and Sweller, *Journal of Educational Psychology* 80, 1988, 424-436. `theory.md`
  cites them as first reports of their effects, with dates and pages from
  Table 1 of the 2019 paper.
- Paas and van Merriënboer 1994a.
- Sweller 2010, Kalyuga 2011 and Fakhoury 2018 beyond their abstracts; Peitek,
  Gonçales, Duran and the LLM papers beyond their abstracts.

## What the skill adds on its own

Not any source's text: the order of the steps; the rule that every count is
relative to a task and reader, newcomer by default; the count of elements that
must be related to one another, the two structural tests, the tie-break and the
rule that a team-built interpreter, DSL or convention is structure; the trace of
a path through code; the ranking by extraneous count times frequency, with
history as the frequency; every "this skill's reading" paragraph in `theory.md`,
including the choice of two loads; the cautions on Intrinsic Complexity Points
in `measures.md`; and the hand-overs to `red-flags`, `contradiction` and
`root-cause`.
