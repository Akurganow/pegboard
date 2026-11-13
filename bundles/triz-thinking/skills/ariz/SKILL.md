---
name: ariz
description: >
  Use this skill whenever a hard software problem has outlasted the obvious
  fixes and the user wants a way out. Phrasings: "we keep going back and
  forth on this", "every compromise failed", "what is the way out?". It covers
  a setting flipped back and forth between two teams who each hold a rule, a
  fix that breaks something else while the next fix brings the first problem
  back, an issue that keeps returning, two or three tied tensions, a problem
  that may be stated wrong, and a contradiction-matrix lookup that gave
  nothing usable. Use it even when TRIZ is never named. It walks the problem through ARIZ-85C,
  Altshuller's nine-part algorithm. For a trade-off seen at first sight,
  before any fix was tried, use contradiction. Skip it for interview-style
  puzzles, document rewrites and plain bugs or incidents.
license: MIT
---

# ARIZ

You walk a hard software problem through ARIZ-85C. The result is the
strongest solution direction you can find, reached through the algorithm's
own formulations. Reply in the user's language. The user asked for the answer,
not the procedure: do not say that a skill or an algorithm is being applied,
and do not narrate its steps.

If a reference file cannot be read, say which and do not quote it from
memory: the wording carries the method.

## Work from what is at hand

Read the code, history, logs, tests and documents the session has before you
ask anything, and quote what you read with its path and line. Ask only for
what only the user knows: intent, priorities, readers, what was observed
outside the system. Say which facts you read, which the user gave and which
you assume.

## Give the answer in this reply

- The first reply walks Parts 1 to 3 compactly and goes on to directions
  from Parts 4 and 5. Never end after Part 1, or with questions in place of
  the walk. Write each formulation from what you have, mark the assumed
  facts, and let the user correct it.
- A missing fact is a reason to assume, not to stop, unless the action spends
  the user's money, sends private data out or cannot be undone.
- Answer in the form asked: a decision, a summary, a message, a number of
  lines. Deliver exactly that, with any method note after it in one or two
  sentences.
- Name the concrete behaviour, defect or change, and where it goes. An answer
  that fills every formulation and leaves the problem open has failed.
- End with at most three questions whose answers would change the result,
  or with none.

## Reference files

The last two files belong to `contradiction`.

| File | Read when |
| --- | --- |
| [`references/ariz-85c.md`](references/ariz-85c.md), formulas, tables and software glosses | before Part 1, and at each part as you reach it |
| [`../contradiction/references/principles.md`](../contradiction/references/principles.md), the 40 principles | the user asks for them at step 5.3, or you compare the solution with them at step 9.2 |
| [`../contradiction/references/sources.md`](../contradiction/references/sources.md), where each reference was read | the user asks where a formula or step comes from |

## Step 1: take the problem in

When `contradiction` hands the problem over, keep its technical
contradiction, ideal final result and reason. Part 1 restates it all the
same.

Keep the solution you would give without the algorithm as a candidate. The
algorithm adds candidates and never replaces your best one. A problem with no
contradiction is not an ARIZ problem: say so in one sentence and answer
directly.

## Step 2: walk the parts

Write each part as a short block holding the formulation, with the user's
facts in the wording `references/ariz-85c.md` gives. Head each block with what
it states, not with a part number. A part that adds nothing gets one line
saying so. The default depth is Parts 1 to 5. Add Part 6 when
nothing came out and Part 7 for the direction you recommend. Add Parts 8 and
9 only when the user asks.

- **Part 1.** Write the mini-problem (1.1), with TC-1 and TC-2 as "if <state
  of the tool>, then <good effect>, but <bad effect>". Name the tool and the
  product (1.2) and the shape of each contradiction (1.3). Choose the one
  whose good effect is the main function, and keep its state: no middle value
  (1.4). Write it at its limit, in the user's own parameter (1.5), then the
  model with the X-element (1.6).
- **Part 2.** Name the operating zone, the operating time and the resources
  the system already holds.
- **Part 3.** Write IFR-1, the macro-level physical contradiction and IFR-2.
  The micro-level statement is one line.
- **Parts 4 and 5.** Write at least one direction for the user's system.
  Part 5 applies the table of eleven typical transformations (5.3). The
  package does not carry the standard solutions (1.7, 3.6, 5.1), the earlier
  solved problems (5.2) or the pointer to physical effects (5.4), and no
  published software reading of the standards was found. Say this once. Read
  the 40 principles at 5.3 only when the user asks.
- **Parts 6 to 9.** Part 6 restates the problem. Part 7 checks the recommended
  direction, and a failed check sends you back to 1.1.
  Parts 8 and 9 apply the answer and review the walk.

## Step 3: write the result

Lead with the recommended direction. Then give the formulations and the
directions, most direct first, each a change to a named part of the user's
system, with path and line when the code is at hand, and the new trade-off it
brings. Name an algorithm element, such as a transformation of
Table 2, only when it led you to the direction. When the algorithm added
nothing beyond the direct solution, say so in one sentence. State when the
direction fails, and which parts you did not walk when that limits the
conclusion.

## Step 4: hand back

- When Part 6 restates the problem as a new technical contradiction between
  two parameters, load `contradiction` for it: the matrix may crack it in one
  lookup. A problem that came from `contradiction` is not handed back to it
  in the same reply.
- When the physical contradiction of Part 3 fits a separation of later
  teaching, use Step 4 of `contradiction`.
- Offer the `root-cause` skill of `toc-thinking` when the problem is a tangle
  of symptoms rather than a trade-off, and only when it is installed.

## Boundaries

ARIZ gives directions, not guarantees. The software glosses are this skill's
own. Drop a direction that contradicts what the user knows about their
system.
