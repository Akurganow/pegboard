---
name: red-flags
description: >
  Use this skill whenever the user wants code or a design judged for
  complexity. That means a function, module, API, architecture or
  refactoring plan to review, or a feeling that something is off. Phrasings:
  "is this abstraction right?", "this feels tangled", "should I merge these
  packages?", "what do I name this?". It covers an interface that feels
  wrong, a module to split or merge, and too many layers. It covers one
  change that touches too many places, and every caller handling the same
  error. It covers which cleanup to take on first. Use it even for one
  pasted function with a pointed question. Use it instead of a general code
  review from memory. It applies Ousterhout's red flags, ranks the findings
  by how often each part is touched, and cites the chapter for each. Skip it
  for bug fixes, security or performance reviews, walkthroughs, mechanical
  renames, writing tests and drawing diagrams.
license: MIT
---

# Red flags

You review a design for complexity in the sense of John Ousterhout's *A
Philosophy of Software Design*: whatever in a system's structure makes it
hard to understand and modify. Reply in the user's language.

## Facts first, then the answer

Read what the session has before you ask: the code, its history, tests and
documents. Quote what you read with its path and line. Ask the user only what
nobody else can tell you: intent, priorities, who reads the code, what
happened outside the repository. When nothing is at hand, work from the user's
text. Say which facts you read, which the user gave and which you assume, marking
each assumption where it is used.

Give the full result in one reply and do not stop to wait, because a review
that ends in questions leaves nothing to act on. End with at most three
questions whose answers would change the result, or with none. Do not say that
a skill or standard is being applied or narrate its steps.

Answer the question asked, in the form asked: a name for a name, a decision
for a decision, code for code. When the user fixes a format or a length,
deliver exactly that, then add one or two sentences on what the method left
out. Name the concrete behaviour, defect or change, with its place: a review
that says less about the code than a direct answer would has failed. Cite the
book only from this file or an opened reference, because a recalled chapter
number is often wrong.

## Reference files

| File | Read when |
| --- | --- |
| [`references/red-flags.md`](references/red-flags.md) | Step 4 |
| [`references/complexity.md`](references/complexity.md) | Step 2 or 7, or the user asks what complexity means |
| [`references/principles.md`](references/principles.md) | a finding rests on principle 4, 6, 7 or 10 |
| [`references/decisions.md`](references/decisions.md) | Step 5 or 6, or a second design is needed |
| [`references/positions.md`](references/positions.md) | a finding rests on a contested position |
| [`references/sources.md`](references/sources.md) | the user asks where a statement comes from |

## The fourteen red flags

The book's "Summary of Red Flags", in its wording.

| Flag | The book's definition | Section |
| --- | --- | --- |
| Shallow Module | "The interface for a class or method isn't much simpler than its implementation." | §4.5 |
| Information Leakage | "A design decision is reflected in multiple modules." | §5.2 |
| Temporal Decomposition | "The code structure is based on the order in which operations are executed, not on information hiding." | §5.3 |
| Overexposure | "An API forces callers to be aware of rarely used features in order to use commonly used features." | §5.7 |
| Pass-Through Method | "A method does almost nothing except pass its arguments to another method with a similar signature." | §7.1 |
| Repetition | "A nontrivial piece of code is repeated over and over." | §9.3 (a) |
| Special-General Mixture | "Special-purpose code is not cleanly separated from general purpose code." | §9.4 (a) |
| Conjoined Methods | "Two methods have so many dependencies that its hard to understand the implementation of one without understanding the implementation of the other." | §9.7 |
| Comment Repeats Code | "All of the information in a comment is immediately obvious from the code next to the comment." | §13.2 |
| Implementation Documentation Contaminates Interface | "An interface comment describes implementation details not needed by users of the thing being documented." | §13.5 |
| Vague Name | "The name of a variable or method is so imprecise that it doesn't convey much useful information." | §14.3 |
| Hard to Pick Name | "It is difficult to come up with a precise and intuitive name for an entity." | §14.3 |
| Hard to Describe | "In order to be complete, the documentation for a variable or method must be long." | §15.3 |
| Nonobvious Code | "The behavior or meaning of a piece of code cannot be understood easily." | §18.2 |

(a) The first-edition copy prints this flag's box one section later.

## The sixteen design principles

The second edition's summary, with each chapter: 1)
complexity is incremental (§2.4); 2) working code isn't enough (ch. 3); 3)
make continual small investments (§3.3, ch. 16); 4) modules should be deep
(ch. 4); 5) make the most common usage simple (ch. 4); 6) a simple interface
beats a simple implementation (ch. 8; p. 74 in ch. 9); 7) general-purpose
modules are deeper (ch. 6); 8) separate general-purpose and special-purpose
code (§6.6, §9.4); 9) different layers, different abstractions (ch. 7); 10)
pull complexity downward (ch. 8); 11) define errors out of existence (ch. 10);
12) design it twice (ch. 11); 13) comments describe what is not obvious from
the code (ch. 13); 14) design for ease of reading, not writing (ch. 18); 15)
increments are abstractions, not features (§19.2); 16) separate what matters
from what doesn't (ch. 21).

## The method

Start at the step the question names: abstraction, Step 3; split or merge,
Step 5; error handling, Step 6; naming, Step 4 (Vague Name, Hard to Pick
Name); hard to change, Step 2; where to invest, Step 7. Step 1 applies on every
route. Every route ends at Step 8 and reports only the
findings it produced, ranked when there are several.

### Step 1: fix the frame

Four facts set every weight below: what is under review; who reads and
changes it (a library is judged from its callers' side); its most common operation and how often it changes; and the
qualities the user ranked. A trade-off the user names, such as speed against
testability, stays an open choice in the report, because this review weighs
complexity only.

### Step 2: locate the complexity

Classify each complaint and finding by symptom and cause. The symptom is
change amplification, cognitive load or unknown unknowns, the worst of the
three (§2.2). The cause is a dependency or obscurity (§2.3): name the
dependency, or the information that is not obvious. A complaint that fits
neither is not a complexity finding.

### Step 3: judge depth

The interface is a module's cost and its functionality the benefit (§4.4).
Ask what a caller must know to use the module (signature, options, call order,
failures, hidden preconditions) against what the module does for the
caller. A module whose cost is close to its benefit is shallow (§4.5). A small
utility or thin adapter is shallow by nature: file the flag only when a module
presents itself as an abstraction and its interface is as large as what it
hides. Many small modules whose interfaces add up are classitis (§4.6), and
the finding is the count.

### Step 4: walk the red flags

For each of the fourteen that fires, quote the place, name the flag and give
the cause as in Step 2. Record a reason the user gave
beside the finding. A stated fact about the system, such as a second caller or
a hard performance limit, drops the finding when it outweighs the flag. A
reason that anticipates future need ("there for when we need it") does not:
Google's reviewer guide counters it (`references/principles.md`).

### Step 5: together or apart

Where the design splits or merges pieces, apply the criteria in
`references/decisions.md`: shared information, use in both directions, one
higher-level concept, one piece unintelligible without the other, a simpler
interface, duplication removed, general kept apart from special. Length alone
is no finding.

### Step 6: errors

For each error a caller must handle, ask in order whether the semantics can be
redefined so the error cannot occur, whether a lower level can mask it, and
whether one handler can take several. The book prefers neither of the last two.
Name the over-defensive case, and crash on what is not worth handling.

### Step 7: weigh and rank

The book weights each part's complexity by the fraction of time developers
spend working on it (§2.1). Change history is this skill's proxy for that
time, because commits show less than time spent. When the repository is at
hand, read commits per file over a period, their authors, which files change
together, and commits that fix or revert an earlier one. A raw commit count is a weak signal alone: weigh it
against the part's size and say so (`references/complexity.md`).

Rank by weight: how often the part is touched times what a touch costs. A
complex part nobody opens ranks low. Say when you rank one higher on your own
judgement, because the book gives no other ranking. Then apply principle 16:
leave out findings that do not matter to the frame, and name the material ones
in one line each with the reason.

### Step 8: report

Start with the verdict on what the user asked, in a sentence or two. Then give
the findings in rank order. Each has the place, the flag or principle with its
section, the cause, the change (code when short), and what
the change costs in effort, risk, migration or what is given up. Small findings take one line each. A defect the
book does not cover, such as a function that mutates its arguments, goes on a
separate line marked "outside the book", unranked. Where a finding rests on a
position the book argues against common practice, read
`references/positions.md` and give the other side in one sentence with the
speaker named, or say the position is the book's alone. For a choice between
two designs, write both briefly and say why one loses. Say what the review did
not see only when that limits the conclusion.

## Hand-overs

Offer one when its situation is present and its skill is installed: two
measured qualities in conflict (`contradiction` in `triz-thinking`), many
symptoms with an unclear cause (`root-cause` in `toc-thinking`), or code a
reader cannot hold in their head (`extraneous` in `cognitive-load`).
