<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [What can be counted, and what the studies on code found](#what-can-be-counted-and-what-the-studies-on-code-found)
  - [Cognitive Complexity](#cognitive-complexity)
  - [Intrinsic Complexity Points](#intrinsic-complexity-points)
  - [Studies of programmers](#studies-of-programmers)
  - [A size that reviewers use](#a-size-that-reviewers-use)
  - [LLM agents as readers of code](#llm-agents-as-readers-of-code)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# What can be counted, and what the studies on code found

Two published counts of a unit of code, the studies of programmers, and the
studies of language-model agents. `sources.md` gives the copy read for each,
and whether it was the full text or the abstract. This skill measured nothing.
Every default or threshold below is the choice of the tool or authors named.

## Cognitive Complexity

G. Ann Campbell, SonarSource, "Cognitive Complexity: A new way of measuring
understandability", version 1.7, 29 August 2023
([PDF](https://www.sonarsource.com/docs/CognitiveComplexity.pdf)). It counts
per function: one for each break in linear flow (`if`, `else if`, `else`,
ternary, `switch`, loops, `catch`, labelled jumps, runs of binary logical
operators, each method in a recursion cycle), plus one per nesting level of an
`if`, ternary, `switch`, loop or `catch`. `else if` and `else` get no nesting
increment (Appendix B3). Shorthand adds nothing: "Cognitive Complexity does not
increment for methods", so extracting a method lowers the count.

PMD "reports methods with a
complexity of 15 or more"
([`design.xml`](https://github.com/pmd/pmd/blob/4a1d37d3eb785695084393fcc7315b0aca123809/pmd-java/src/main/resources/category/java/design.xml#L299),
source). The ESLint rule moved from the archived `eslint-plugin-sonarjs` into
SonarJS, default threshold 15
([`rule.ts`](https://github.com/SonarSource/SonarJS/blob/793d14cc05902a65682f8d59f4edf9e9d19b6334/packages/analysis/src/jsts/rules/S3776/rule.ts#L39),
source). SonarSource's Java rule calls it "a measure of how hard it is to
understand the control flow of a unit of code"
([`S3776.html`](https://github.com/SonarSource/sonar-java/blob/ceb8058cc5d60196c6b7641d748a079bbd473c00/sonar-java-plugin/src/main/resources/org/sonar/l10n/java/rules/java/S3776.html),
documentation) and claims no validation.

Validation: Muñoz Barón, Wyrich and Wagner, ESEM 2020, a random-effects
meta-analysis of 10 earlier studies, 427 snippets, about 24,000 human
evaluations. The abstract reports a positive correlation with comprehension
time and subjective ratings, and "mixed results" for correctness. Weighted mean
correlations:

| Variable | Studies | Snippets | Range | Weighted mean |
| :-- | --: | --: | :-- | --: |
| Time | 9 | 327 | -0.03 to 0.94 | 0.54 |
| Subjective rating (higher means easier) | 4 | 203 | -0.57 to -0.04 | -0.29 |
| Correctness | 6 | 269 | -0.52 to 0.57 | -0.13 |
| Time and correctness combined | 6 | 269 | -0.10 to 0.68 | 0.40 |

Limit: it counts control flow only. It does not see names, vocabulary or the
distance between a fact and its use. Use it for the "complex conditionals" and
"nested ifs" entries of `patterns.md`.

## Intrinsic Complexity Points

Tavares de Souza and Costa Pinto, "Toward a Definition of Cognitive-Driven
Development", ICSME 2020
([DOI](https://doi.org/10.1109/ICSME46990.2020.00087)), three pages. Points
per element: `if`-`else` 2, `case` 1, `try`-`catch`-`finally` 3, contextual
coupling 1, a function passed as an argument 1, crosscutting infrastructure 0.
The limit per implementation unit is "five plus or minus two points, where
seven would be the limit" for web applications and mixed teams, and "ten and
twelve points" for frameworks and libraries, offered as "recommendations based
on the experiences aforementioned". The abstract says preliminary results
indicate lower maintenance effort. The paper reports no data for that claim.

Limits. The paper's "intrinsic" is not the theory's: it counts branches and
coupling, which Step 3 of `SKILL.md` would often sort as extraneous. Its
grounding treats Miller's span as a budget of weighted syntax points, which
neither Miller nor Cowan measured. Use it as a hand count per unit.

## Studies of programmers

| Study | What was measured | Finding | Limit |
| :-- | :-- | :-- | :-- |
| Peitek, Apel, Parnin, Brechmann, Siegmund, ICSE 2021 ([DOI](https://doi.org/10.1109/icse43902.2021.00056)) | fMRI, 19 participants, short snippets | "a code's textual size drives programmers' attention, and vocabulary size burdens programmers' working memory"; supports doubts about metric validity | abstract only |
| Hansen, Goldstone, Lumsdaine, 2013 ([arXiv 1304.5257](https://arxiv.org/abs/1304.5257)) | 162 participants (94 with a year or less of Python) predict the output of ten Python programs | small notational changes changed correctness and response times; experience "may hurt performance significantly" when assumptions about related statements are violated | full text |
| Fakhoury, Ma, Arnaoudova, Adesope, ICPC 2018, 286-296 ([DOI](https://doi.org/10.1145/3196321.3196347)) | fNIRS and eye tracking, 15 participants | linguistic antipatterns "significantly" raise cognitive load | abstract only |
| Same authors, "Measuring the Impact of Lexical and Structural Inconsistencies on Developers' Cognitive Load during Bug Localization", *Empirical Software Engineering* 25(3), 2140-2178 | 25 participants, bug localization | lexical inconsistencies raise load across the snippet; both kinds lower time and success rate; "We did not find statistical evidence that structural inconsistencies increase the average cognitive load"; self-reported difficulty, load and fixation duration "do not correlate" | full text of the submitted manuscript |
| Baum, Schneider, Bacchelli, *Empirical Software Engineering* 24(4), 1762-1798, 2019 ([manuscript](https://tobiasbaum.github.io/rp/memoryCodeOrderAndReview.pdf)) | 50 participants, review of code with seeded defects | working memory span correlated with delocalized defects found, defects only findable by combining several parts of the code (tau-b 0.24, p=0.0186); with all defects 0.05 (n=45), with localized defects -0.01; small changes were reviewed more effectively | one experiment |
| Crichton, Agrawala, Hanrahan, CHI 2021 ([arXiv 2101.06305](https://arxiv.org/abs/2101.06305)) | tracing programs | "about 7 variable/value pairs" held in working memory; associations get swapped under load | abstract only |
| da Costa and others, 2026 ([arXiv 2602.18579](https://arxiv.org/abs/2602.18579)) | eye tracking, 32 Java novices, extract vs inline method | extraction cut time by up to 78.8% in two tasks and raised it by up to 166.9% in simpler ones; novices switched between call sites and extracted methods even with meaningful names. Bears on "Too many small methods" | abstract only |
| Harsch, Bye, Rus, Kendeou, Cognitive Science Society 2025 ([paper](https://journalpub.escholarship.org/cognitivesciencesociety/article/49876/galley/37838/download)) | novices and experts; a text-comprehension effect in which cohesion helps novices and not experts | "fail to find robust evidence for a reverse cohesion effect" in code | full text |

Three more are maps and give no finding about code. Gonçales and others, ICPC
2019 ([DOI](https://doi.org/10.1109/icpc.2019.00018)): 33 of 2,612 articles on
measuring developers' load, 55% using EEG. Wyrich, Bogner and Wagner, *ACM
Computing Surveys* 56(4), 2023 ([DOI](https://doi.org/10.1145/3626522), text
read as the [arXiv preprint](https://arxiv.org/abs/2206.11102)): 95 code
comprehension experiments from 1979 to 2019. Duran, Zavgorodniaia and Sorva,
*ACM Transactions on Computing Education* 22(4), 2022
([DOI](https://doi.org/10.1145/3483843)): how computing-education papers use
the theory.

No study found tests a named cognitive load effect (split attention, worked
example, expertise reversal) on code reading, and none measures intrinsic,
extraneous or germane load as such. They measure time, correctness, ratings
and physiological signals.

## A size that reviewers use

Google's guide for authors of changes: "100 lines is usually a reasonable size
for a CL, and 1000 lines is usually too large, but it's up to the judgment of
your reviewer", and a change spread across many files counts as larger
([`small-cls.md`](https://github.com/google/eng-practices/blob/3bb3ec25b3b0199f4940b1aa75f0ac5c5753301c/review/developer/small-cls.md),
documentation). The reason given is reading, not load: a small change is
"Reviewed more thoroughly" and "Less likely to introduce bugs".

## LLM agents as readers of code

Abstracts of preprints, read 2026-11-11. Removing identifier names degrades
summarization and execution tasks ([2510.03178](https://arxiv.org/abs/2510.03178)).
Classical complexity metrics correlate minimally or not at all with model
success on code benchmarks (AUROC 0.63, against 0.86 for trained shadow models:
[2601.12951](https://arxiv.org/abs/2601.12951),
[2602.07882](https://arxiv.org/abs/2602.07882)). Agents building on agent code
resolve fewer tasks than on human code: "task resolve rate drops of up to 13.1%"
([2606.21804](https://arxiv.org/abs/2606.21804)). Not found: a controlled study
that varies one code structure (nesting, indirection, file layout) and measures
agent success. The searches were not recorded, so this is a gap in them. The
skill cannot say that the structures in `patterns.md` cost an agent what they
cost a newcomer.
