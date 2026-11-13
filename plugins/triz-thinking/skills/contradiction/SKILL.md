---
name: contradiction
description: >
  Use this skill whenever the user faces a trade-off between two software
  requirements and wants more than a compromise. Phrasings: "improving X
  makes Y worse", "these two requirements look incompatible", "stricter
  checks without more friction". It covers one thing that must be long and
  short, open and closed, or frozen and editable. It covers a proposal that
  only sets a middle value, splits the difference or picks one side. Use it
  even when TRIZ is never named or the user wants a note or message drafted
  from the answer, and when a direct answer looks easy: the matrix names
  directions a plain answer misses. Skip it for
  bugs or tuning with no trade-off, sizing formulas, config precedence
  and plain refactoring. A problem that
  keeps coming back after fixes, tied tensions, or a table lookup that gave
  only generic tips belong to the ariz skill of this package.
license: MIT
---

# Contradiction

You resolve a trade-off between two software requirements with classic
TRIZ: a stated contradiction, an ideal final result, the separation of
opposite properties, and Altshuller's contradiction matrix with its 40
inventive principles. The result is the strongest solution you can find,
written as changes to the user's system. The matrix widens your options and
does not replace your judgement. Reply in the user's language. The user
asked for the answer, not the procedure: do not say that a skill or method is
being applied, and do not narrate its steps.

If a reference file cannot be read, say which and do not quote it from
memory: a remembered cell can be wrong, and the user acts on the numbers.

## Work from what is at hand

Read the code, history, logs, tests and documents the session has before
you ask, and quote what you read with its path and line. Ask only for what
only the user knows: intent, priorities, readers, what was observed outside
the system. Say which facts you read, which the user gave and which you
assume.

## Give the answer in this reply

- Give the full result in this reply and mark each assumption where it is
  used. A missing fact is a reason to assume, not to stop, unless the action
  spends the user's money, sends private data out or cannot be undone.
- Answer in the form asked: a decision, code, a ticket comment, a letter.
  Make that text match the design you recommend. When the user fixes a
  format or a length, deliver exactly that and put any method note after it
  in one or two sentences.
- Name the concrete behaviour, defect or change, and where it goes. An answer
  that leaves the question open has failed.
- End with at most three questions whose answers would change the result,
  or with none.

## Reference files

| File | Read when |
| --- | --- |
| [`references/parameters.md`](references/parameters.md), the 39 parameters with software readings | Step 5 |
| [`references/matrix/`](references/matrix/), `01.md` to `39.md`, one file per improving parameter | Step 6, one file per candidate pair |
| [`references/principles.md`](references/principles.md), the 40 principles with software readings | Step 7, for each principle you consider |
| [`references/matrix/provenance.md`](references/matrix/provenance.md), how the matrix was built and every reading of its disputed cells | a direction rests on a `(disputed)` cell, or the user asks where a cell comes from |
| [`references/sources.md`](references/sources.md), where each reference of both skills was read | the user asks where a principle or formula comes from |

## Step 1: state the contradiction

Restate the problem in the user's terms as one of two kinds.

- **Technical.** Improving one parameter worsens another. "A longer cache
  lifetime unloads the database and serves stale reads."
- **Physical.** One element must have a property and its opposite. "The
  cache entry must exist, for speed, and must not exist, for freshness."

A technical contradiction often hides a physical one, the sharper
statement: write both when you can. When no second parameter worsens and no
element needs two opposite properties, say so in one sentence and answer
directly.

## Step 2: state the ideal final result

Write one line whose subject is a named element of the user's system: it
provides the useful function itself, without the harm and without
complicating the system. "Ideal final result: the cache entry itself is
fresh whenever it is read." It is a direction, not a solution.

## Step 3: keep your own best solution

Form the solution you would give if the tables did not exist, and keep it as
a candidate. The later steps add candidates and never replace it. When it
beats everything the tables return, give it.

## Step 4: separate the opposite properties

For a physical contradiction, later TRIZ teaching gives four ways to hold
both properties.

- **In time.** A feature flag, a build-time check absent at run time.
- **In space.** A write primary and a read replica, client and server
  validation.
- **On condition.** A circuit breaker, a fast path for the common case.
- **Between the parts and the whole.** A large store made of small shards.

State each separation that fits as a concrete change to the user's system.
Go on to Step 5 when there is also a technical contradiction: the two routes
give different directions.

## Step 5: map to parameters

Read `references/parameters.md`. The improving parameter is the one the user
wants better, and the worsening parameter is the one that degrades when they
get it. Choose two or three candidate pairs, with a clause on why each fits;
the software readings show which parameter plays the role in the user's
system. Run Steps 6 and 7 for every pair in this reply, and name the pairs so
the user can correct them.

## Step 6: read the matrix

The matrix has one file per improving parameter, `references/matrix/NN.md`,
NN being its number with two digits. A file holds a heading and one line per
non-empty cell, `<worsening number>: <principles in the matrix's order>`. Open
the file and read the line that starts with the worsening number. Do not
search. Improving 9 (speed) against worsening 27
(reliability): `matrix/09.md` holds `27: 11 35 27 28`, so principles 11, 35,
27 and 28.

- Quote each line with its pair, "9 vs 27: 11 35 27 28", so the user can
  check it.
- The matrix is not symmetric: 27 vs 9 is another cell, in `27.md`. No
  parameter pairs with itself.
- A worsening number with no line is an empty cell, and the matrix recommends
  nothing. Use your other pairs, then the physical contradiction of Step 4.
  Do not read the reverse pair instead: it states a different trade-off.
- `(disputed)` ends a line on which the sources differ. Use the line. Open
  `references/matrix/provenance.md` only when a direction rests on a
  principle of that cell.

## Step 7: adapt the principles

For each principle the lines name, read its entry in `references/principles.md`
and write what it would mean in this system before you judge it: which part
changes and how. Keep the directions that remove the contradiction, so that
both requirements keep their full value. Prefer a principle that recurs
across the pairs. Drop the rest.

A direction that gives up part of one requirement is a compromise, and the
user asked for both: drop it. When no direction keeps both, say which part
cannot be kept and why, and give the best direction with its loss stated.

## Step 8: write the result

Lead with the recommendation. Follow it with the contradiction, the ideal
final result and the candidate pairs with the lines you read, assumptions
marked. Then give up to four directions as a numbered list, most direct
first.

1. State the change to a named part of the user's system: a table, a
   service, a config key, with path and line when the code is at hand.
2. Name a principle, such as "10 Preliminary action", only when it led you to
   the direction. A direction from your own reasoning or Step 3 carries none.
3. State the new trade-off the change brings, if any.

Say which direction to do first and why. When the matrix and the principles
added nothing beyond the direct solution, say so in one sentence.

## Hand-overs

- **`ariz` skill.** Load it when the problem has outlasted earlier fixes, a
  fix in one place breaks another, the tensions feed each other, or Steps 4
  to 7 left nothing usable. Pass on the technical contradiction, the ideal
  final result and the reason. A problem that came from `ariz` is not handed
  back in the same reply. Without `ariz`, finish Steps 4 to 8 and say what
  stays open.
- **`root-cause` skill of `toc-thinking`.** Offer it when symptoms tangle
  with no trade-off in sight, and only when it is installed.

## Boundaries

The matrix and the principles give directions, not guarantees. The software
readings are this skill's own, because no published mapping of the parameters
to software was found. Drop a direction that contradicts what the user knows
about their system.
