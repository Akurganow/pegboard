<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Cognitive load theory: the working definitions](#cognitive-load-theory-the-working-definitions)
  - [Intrinsic and extraneous load](#intrinsic-and-extraneous-load)
  - [Element interactivity](#element-interactivity)
  - [Germane load and the additive model](#germane-load-and-the-additive-model)
  - [Chunks and capacity](#chunks-and-capacity)
  - [Three effects, used by analogy](#three-effects-used-by-analogy)
  - [Where the theory stops](#where-the-theory-stops)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Cognitive load theory: the working definitions

The definitions below are the ones `SKILL.md` counts and sorts with, each with
its primary citation. A statement marked "this skill's reading" is the skill's
own adaptation to code, not a finding of the theory. `sources.md` records which
copy of each paper was read.

## Intrinsic and extraneous load

Sweller (1994, *Learning and Instruction* 4, 295-312,
[full text](https://mrbartonmaths.com/resourcesnew/8.%20Research/Explicit%20Instruction/CLT,%20learning%20difficulty%20and%20instructional%20design.pdf))
proposes that "total
cognitive load is an amalgam of at least two quite separate factors:
extraneous cognitive load which is artificial because it is imposed by
instructional methods and intrinsic cognitive load over which instructors
have no control". Sweller, van Merriënboer and Paas (2019, *Educational
Psychology Review* 31, 261-292,
[full text](https://rd.springer.com/article/10.1007/s10648-019-09465-5),
p. 264) give the current definitions.
Intrinsic load is determined by "both the complexity of the information and
the knowledge of the person processing that information". Extraneous
cognitive load "is not determined by the intrinsic complexity of the
information but rather, how the information is presented and what the
learner is required to do by the instructional procedure".

Two consequences. The same material has a different intrinsic load for readers
who know different things, so every count is relative to a named reader. And
extraneous load is the part a designer can change without changing what is to
be learned. This skill's reading: for code, the "instructional procedure" is
the structure and presentation of the code, and the task is what the reader
came to do.
Chandler and Sweller (1991, *Cognition and Instruction* 8, 293-332,
[full text](https://ro.uow.edu.au/edupapers/128), p. 296)
state the design aim in these terms: "Ideal formats for initial instruction
should reduce extraneous cognitive load."

## Element interactivity

Sweller, van Merriënboer and Paas (1998, *Educational Psychology Review* 10,
251-296, [full text](https://docdrop.org/static/drop-pdf/SwellerMerrienboerPaas1998-93QJw.pdf))
tie load to element interactivity. The load depends on "the number
of elements that must be processed simultaneously in working memory", which
"in turn, depends on the extent of element interactivity" (p. 259). "An
element is anything that has been or needs to be learned, most frequently a
schema" (p. 259). The count is relative to the person: "Element
interactivity can be determined only by counting the number of interacting
elements with which people at a particular level of expertise are likely to
deal" (p. 261).

The 1998 paper assumed that element interactivity matters for intrinsic load.
Sweller (2010, *Educational Psychology Review* 22, 123-138,
[abstract](https://rd.springer.com/article/10.1007/s10648-010-9128-5)) calls it "the basic, defining mechanism of intrinsic cognitive load" and
adds that it "underlies extraneous cognitive load as well". The 2019 paper
says that "In 1998, it was assumed that element interactivity only was
relevant to intrinsic cognitive load" (p. 264).

This skill's reading: Step 3 of `SKILL.md` counts the elements a reader must
relate to one another to do the task at one place, in units that reader
already holds as one. Elements that can be taken one at a time do not add.
The 2010 abstract draws the line the skill sorts by: element interactivity
is either "essential to the task at hand" or "a function of instructional
procedures".

## Germane load and the additive model

The 1998 paper defines germane load as the effort that contributes to schema
construction (p. 259) and states the additive model: the sum of
the three loads "stays within working memory limits" (p. 264). Paas, Renkl
and Sweller (2003, *Educational Psychologist* 38(1), 1-4,
[full text](https://www.uky.edu/~gmswan3/544/Cognitive_Load_%26_ID.pdf)) say the three
"are additive in that, together, the total load cannot exceed the working
memory resources available if learning is to occur".

The definition has since moved, and both the model and the distinction among
the three loads have been questioned:

- Sweller (2010, abstract above) writes that germane load "can be defined in terms
  of intrinsic cognitive load".
- Kalyuga (2011, *Educational Psychology Review* 23, 1-19,
  [abstract](https://rd.springer.com/article/10.1007/s10648-010-9150-7)) writes
  that "germane load is essentially indistinguishable from intrinsic load,
  and therefore this concept may be redundant".
- de Jong (2010, *Instructional Science* 38, 105-134,
  [full text](https://ris.utwente.nl/ws/files/6597420/Jong10cognitive.pdf))
  questions "another
  pillar upholding the theory", that a clear distinction can be made among
  the three loads. He notes that intrinsic load refers to "objects" and
  germane load to "processes".
- Sweller, van Merriënboer and Paas (2019, p. 264) now assume that "rather
  than contributing to the total load, germane cognitive load redistributes
  working memory resources from extraneous activities to activities
  directly relevant to learning by dealing with information intrinsic to the
  learning task". On p. 281 they write that "only intrinsic and extraneous
  cognitive load are distinguished as basic categories".

This skill's reading: it sorts into two piles, intrinsic and extraneous.
Germane load is the working memory a reader spends on the elements the task
needs, so it belongs to the intrinsic pile and has no instruction of its
own. A rule to protect or increase germane load would rest on the 1998 form that the
authors have since replaced.

## Chunks and capacity

Cowan (2001, *Behavioral and Brain Sciences* 24, 87-114,
[full text](https://doi.org/10.1017/S0140525X01003922)) defines a chunk as
"a collection of concepts that have strong associations to one another and
much weaker associations to other chunks concurrently in use" (section 1.3,
p. 89). His abstract reports: "A single, central capacity limit
averaging about four chunks is implicated". It shows when "other steps are
taken specifically to block the recoding of stimulus items into larger chunks".
Miller
(1956, *Psychological Review* 63, 81-97,
[full text](https://psychclassics.yorku.ca/Miller/)) describes chunking as
"building larger and larger chunks, each chunk containing more information
than before". Of the recurrence of the number seven in his data he writes: "I
suspect that it is only a pernicious, Pythagorean coincidence".

The 2019 paper states the same point for learning: novel information is
processed by a "capacity and duration limited working memory", and "the
capacity and duration limits of working memory disappear" once the
information is stored in long-term memory (p. 261).

This skill's reading, an inference and not a finding on code:

- The limit binds on what the reader does not already know. A pattern the
  reader holds as one schema costs one chunk, and the same code costs a
  newcomer several.
- Code reading does not block recoding the way the experiments behind the
  four do, so four is not a budget to count code elements against. The
  skill states no element budget.
- Experience can also hurt. Hansen, Goldstone and Lumsdaine (2013,
  [full text](https://arxiv.org/abs/1304.5257)) report
  that experience "may hurt performance significantly when underlying
  assumptions about related code statements are violated" (`measures.md`).
  The author of code therefore judges its load poorly, and a newcomer is the
  default reader.

## Three effects, used by analogy

The theory states its findings as effects: a change to instructional material
that changed learning. Sweller, van Merriënboer and Paas (2019, Table 1) list
seventeen. The skill uses three, each as an analogy for code. Each was
established on instructional material for learners, and no study found tested
any on code reading, so each use below is the skill's reading.

- **Worked-example effect.** First reported by Sweller and Cooper (1985,
  *Cognition and Instruction* 2, 59-89; date from the 2019 Table 1). The 2019 paper says that "studying
  worked examples may facilitate knowledge construction and transfer
  performance more than actually solving the equivalent problems", and that
  "Worked examples are less effective for high-expertise learners" (p. 265).
  For code: a solved example beside an interface should spare a first-time
  caller the search that reading the reference alone demands.
- **Split-attention effect.** First reported by Tarmizi and Sweller (1988,
  *Journal of Educational Psychology* 80, 424-436; date from the 2019 Table 1). The 2019 account:
  "Learners must mentally integrate the two sources of information in order
  to understand the solution, a process that yields a high cognitive load and
  hampers learning". The remedy is "physically integrating the diagram and
  the solution statements" (p. 268). The 1998 paper calls the load
  extraneous because it "occurs purely because of the particular format
  conventionally used" (p. 278). For code: the fact a reader needs sits in
  another file, a wiki page, a sheet or a configuration, and must be held
  while reading this one. The remedy is to put the fact where it is used.
- **Expertise reversal effect.** Named by Kalyuga, Ayres, Chandler and
  Sweller (2003, *Educational Psychologist* 38(1), 23-31,
  [full text](https://ndownloader.figshare.com/files/50479548)): "Instructional
  techniques that are highly effective with inexperienced learners can lose
  their effectiveness and even have negative consequences when used with more
  experienced learners". The 2019 paper calls it "in essence, a variant of
  the more general element interactivity effect" (p. 277). For code: a
  comment that walks a newcomer through a loop can slow an expert, so the
  same guidance should be skippable.

## Where the theory stops

Cognitive load theory is a theory of learning. A developer reading code is
not always learning it. This skill's reading: they are often trying to
finish a task with the least understanding that suffices. No study of that
case was found.

The essay behind `patterns.md` ([full text](https://github.com/zakirullin/cognitive-load/tree/d2d60d2311c3854f16d87bf34f38c829667be2a4)) says of its own use of the term:

> We are going to use "cognitive load" in an informal sense; sometimes it
> lines up with the specific scientific concept of Cognitive Load, but we
> don't know enough about where it does and doesn't match.

This skill keeps that distinction. Where it says "load", it means what a reader
must keep in mind to do a task, and it says which sense it is in when the
difference matters.

A review of the theory in computing education found that authors "predominantly
cite old versions of the theory" and that "hypotheses phrased in terms of
cognitive load components are rare" (Duran, Zavgorodniaia and Sorva 2022,
*ACM Transactions on Computing Education* 22(4),
[abstract](https://doi.org/10.1145/3483843)). The skill therefore cites no
effect as if it had been shown on code.
