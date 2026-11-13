<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Where the book takes a side](#where-the-book-takes-a-side)
  - [Method length](#method-length)
  - [Comments](#comments)
  - [Test-driven development](#test-driven-development)
  - [Positions argued in the book alone](#positions-argued-in-the-book-alone)
  - [What the evidence read says](#what-the-evidence-read-says)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Where the book takes a side

The book argues against several common practices. A review that leans on one
of these positions says whose it is and, where a text of the other side was
read, what the other side says. Three positions were argued out between John
Ousterhout and Robert Martin in a written discussion from September 2024 to
February 2025. Quotations from it name the speaker and the section heading.
Section numbers are those of the second edition of the book, and "1e" or "2e"
after a quotation names the edition whose wording is quoted.

None of these positions is a measured result. The last section gives the
evidence that was read.

## Method length

Ousterhout: the advice in *Clean Code* on method length "is so extreme that it
encourages programmers to create teeny-tiny methods that suffer from both
shallow interfaces and entanglement" (Method Length). The book's rule, depth
before length, is in `decisions.md`.

Martin: "It is certainly possible to over-decompose code", and he decides how
far to go by the rule that a method should do "One Thing" (Method Length).

Where they ended (Method Length Summary): both agree that over-decomposition
is possible and that *Clean Code* 1st ed. "doesn't provide much guidance on how
to recognize" it. They disagree on how far to decompose and on how much
entanglement between methods matters. Martin: "we disagree on the relative
weighting of those two values."

## Comments

Ousterhout: comments "play a fundamental and irreplaceable role in system
design", and "I would probably write 5-10x more lines of comments for a given
piece of code than you would" (Comments Summary). *Clean Code*, as Ousterhout
quotes it: "Comments are always failures" (Comments). Martin: "I prefer long
names to comments. I don't trust comments to be maintained, nor do I trust that
they will be read" (Comments).

Where they ended (Comments Summary): "We agree that implementation code only
needs comments when the code is nonobvious." On interfaces, Martin agrees for
public APIs but sees little need to comment interfaces internal to the team.

For a review: a missing interface comment is a finding under the book, and the
reader should know the book is one side. Google's reviewer guide is on the same
side for the reason a comment exists (`decisions.md`).

## Test-driven development

The book: "I am not a fan of test-driven development. The problem with
test-driven development is that it focuses attention on getting specific
features working, rather than finding the best design. This is tactical
programming pure and simple" (§19.4, 1e). Its one exception: write the tests
first when fixing bugs.

In the discussion Ousterhout withdrew his description of the practice ("guilty
as charged" of describing it inaccurately) and kept his concern: TDD "forces
developers to work too tactically, in units of development that are too small;
it discourages design thinking" (Test-Driven Development). Whether the second
edition's §19.4 keeps the first edition's sentences quoted above is not known.
His alternative, which Martin names "bundling": write a few methods or a class,
then their tests.

Martin: "I think we simply disagree that TDD discourages design" (Test-Driven
Development). Where they ended (TDD Summary): both agree that unit tests are
essential and that TDD can produce well-designed systems. The risk of bad
design under TDD stayed in dispute.

For a review: this skill reviews a design, not a process. It raises the
position only when the design shows the symptom the book names, features
accreted with no abstraction between them, and then calls the process one
candidate cause.

## Positions argued in the book alone

These were not part of the discussion. Each is the book's, at the section
given. No text of the other side was read, so none is quoted, and a finding
that rests on one of these says so.

- **Small classes.** "Classitis" (§4.6): see `principles.md`. The target is the
  belief that more classes are better, not any particular size.
- **Implementation inheritance.** It "creates dependencies between the parent
  class and each of its subclasses ... this results in information leakage
  between the classes in the inheritance hierarchy" (§19.1, 1e). "Before using
  implementation inheritance, consider whether an approach based on composition
  can provide the same benefits."
- **Agile development.** "Agile development tends to focus developers on
  features, not abstractions" (§19.2, 1e). Principle 15 follows from it: "the
  increments of development should be abstractions, not features" (§19.2, 1e).
- **Design patterns.** "The greatest risk with design patterns is
  over-application" (§19.5, 1e): do not force a problem into a pattern when a
  custom approach will be cleaner.
- **Getters and setters.** They "are shallow methods (typically only a single
  line), so they add clutter to the class's interface without providing much
  functionality" (§19.6, 1e).
- **Over-defensive exceptions.** `decisions.md` quotes the warning (§10.2, 1e).

## What the evidence read says

Neither question has a measured answer for design quality, which is the book's
concern.

**Test-driven development.**

- Rafique and Mišić, *IEEE TSE* 39(6), 2013, a meta-analysis of 27 studies. Its
  abstract finds "a small positive effect on quality but little to no
  discernible effect on productivity". The standardised analysis is narrower:
  11 quality effect sizes with a random-effects Hedges' g of -0.010 (95%
  confidence interval -0.454 to 0.433), only one industrial. The positive
  figures rest on unstandardised percentage differences: quality +24% over 24
  effect sizes (academic +10%, industrial +52%), productivity +4% over 23
  (academic +19%, industrial -22%). The authors left design quality out as
  "notoriously difficult to assess".
- Fucci and others, *IEEE TSE* 43(7), 2017: 82 data points from 39
  professionals. The order of test and production code "had no important
  influence"; the granularity and uniformity of the steps were positively
  associated with quality and productivity. Quality is functional correctness.
  Single-group study.

**Method length.** No study read isolates one method's length as a cause of
defects. Nearby work:

- Landman, Serebrenik and Vinju, ICSME 2014: in 17.8 million Java methods the
  correlation between lines of code and cyclomatic complexity is "only
  moderate".
- Fenton and Ohlsson, *IEEE TSE* 26(8), 2000: "no evidence to support previous
  claims relating module size to fault density" in two releases of one system.
  Fenton and Neil, *IEEE TSE* 25(5), 1999: the "Goldilocks conjecture", an
  optimum module size, "lacks support".
- Pascarella, Palomba and Bacchelli, SANER 2018: under realistic evaluation,
  method-level bug prediction shows "results close to that of a random
  classifier".
- Sjøberg and others, *IEEE TSE* 39(8), 2013: once file size and the number of
  changes were controlled, none of 12 code smells was significantly associated
  with more effort. Small sample.

A review states none of the positions above as a research finding. It states
them as the book's, with the section, and lets the user weigh them against the
team's practice.
