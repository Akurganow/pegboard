<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Complexity, as the book defines it](#complexity-as-the-book-defines-it)
  - [Definition](#definition)
  - [The weighting](#the-weighting)
  - [Change history as a stand-in for time spent](#change-history-as-a-stand-in-for-time-spent)
  - [Three symptoms](#three-symptoms)
  - [Two causes](#two-causes)
  - [Incremental](#incremental)
  - [What this definition is not](#what-this-definition-is-not)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Complexity, as the book defines it

Section numbers are those of the second edition of *A Philosophy of Software
Design*. "1e" or "2e" names the edition whose wording is quoted.

## Definition

Complexity is "anything related to the structure of a software system that
makes it hard to understand and modify the system" (§2.1, 1e). The reader
decides: "If someone reading your code says it's not obvious, then it's not
obvious, no matter how clear it may seem to you" (ch. 18, 2e). It comes down
to information: how much a developer must hold in mind to do a task, and how
obvious that information is (`aposd-vs-clean-code`, Introductions).

## The weighting

The book gives a system's complexity as a sum over its parts of each part's
complexity c_p times t_p, "the fraction of time developers spend working on
that part" (§2.1, 1e), "a crude mathematical way" to say that complexity is
"determined by the activities that are most common". Isolating complexity where
it is never seen "is almost as good as eliminating the complexity entirely."

## Change history as a stand-in for time spent

No study read tests change frequency times complexity as a ranking, so the
ranking is this skill's judgement. The studies below bear on its ingredients
and mostly measure defects, not how hard a design is to understand or change.

- Graves and others, *IEEE TSE* 26(7), 2000 (abstract): in one large system,
  "the number of times code has been changed is a better indication of how
  many faults it will contain than is its length."
- Nagappan and Ball, ICSE 2005 (full text): on Windows Server 2003, absolute
  churn "is a poor predictor of defect density", while churn relative to size
  separates fault-prone binaries from the rest with 89.0% accuracy. Limit: one
  product, binary level, check-ins only.
- Ostrand, Weyuker and Bell, *IEEE TSE* 31(4), 2005 (abstract): a model using
  modification history placed 71 to 92% of the faults, 83% on average, in the
  20% of files it ranked worst, over two industrial systems.
- Moser, Pedrycz and Succi, ICSE 2008, and Rahman and Devanbu, ICSE 2013
  (abstracts): process metrics beat code metrics as defect predictors.
- Sjøberg and others, *IEEE TSE* 39(8), 2013 (abstract): file size and the
  number of changes explained almost all modelled variation in effort. Limit: 6
  developers, 298 files.
- Tornhill and Borg, TechDebt 2022 (full text, nearly all): in 39 proprietary
  codebases, low-quality code had 15 times more defects and took 124% more
  development time. Limits: the score comes from the first author's company's
  tool, the data cover 6 to 12 months, and the study shows association and does
  not test change frequency.

For Step 7: three studies compare history with size and favour history. Absolute
churn, a close relative of a raw commit count, predicted poorly and churn
relative to size predicted well (Nagappan and Ball).

## Three symptoms

"Complexity manifests itself in three general ways" (§2.2, 1e):

1. **Change amplification.** "A seemingly simple change requires code
   modifications in many different places."
2. **Cognitive load.** "How much a developer needs to know in order to
   complete a task."
3. **Unknown unknowns.** "It is not obvious which pieces of code must be
   modified to complete a task, or what information a developer must have to
   carry out the task successfully."

"Of the three manifestations of complexity, unknown unknowns are the worst"
(§2.2, 1e). The book gives no other overall ranking.

The book's "cognitive load" is an amount of information a developer must know,
not working-memory load. When a finding is about how many things a reader
must keep in mind at once, it belongs to the `cognitive-load` package.

## Two causes

"Complexity is caused by two things: dependencies and obscurity" (§2.3, 1e).
"A dependency exists when a given piece of code cannot be understood and
modified in isolation." "Obscurity occurs when important information is not
obvious." Dependencies "can't be completely eliminated"; the goal is fewer,
simpler and more obvious ones.

## Incremental

"Complexity is incremental: you have to sweat the small stuff" (principle 1,
2e). The book suggests spending "about 10-20% of your total development time
on investments" (§3.3, 1e). That figure is a suggestion, not a measured
result.

## What this definition is not

Brooks separates essence from accidents, "those difficulties that today attend
its production but that are not inherent", and puts design inside the essence.
Ousterhout's complexity cuts across that line: it is how hard one design makes
a system to understand and change, whichever category the cause falls in. A
removable finding is therefore not "accidental" by that fact, and the word
"accidental" is Brooks'. This reading of the two texts is the skill's own.
