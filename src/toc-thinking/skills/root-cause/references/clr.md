<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Categories of Legitimate Reservation](#categories-of-legitimate-reservation)
  - [Seven or eight](#seven-or-eight)
  - [Level I](#level-i)
    - [1. Clarity](#1-clarity)
  - [Level II](#level-ii)
    - [2. Entity existence](#2-entity-existence)
    - [3. Causality existence](#3-causality-existence)
  - [Level III](#level-iii)
    - [4. Cause insufficiency](#4-cause-insufficiency)
    - [5. Additional cause](#5-additional-cause)
    - [6. Cause-effect reversal](#6-cause-effect-reversal)
    - [7. Predicted effect existence](#7-predicted-effect-existence)
    - [8. Tautology](#8-tautology)
  - [Running a check](#running-a-check)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Categories of Legitimate Reservation

The rules for scrutinising a sufficiency tree. `sources.md` says where each source was read.
Quotations marked TOCICO are from the *TOCICO Dictionary*, second edition, and those marked Dettmer
from *The Logical Thinking Process* (2007).

## Seven or eight

TOCICO counts seven in three levels and treats tautology as a synonym of cause-effect reversal.
Dettmer lists tautology on its own and counts eight. This file follows Dettmer's eight with TOCICO's
levels. Scrutinise from level I to level III (TOCICO). Reservations are offers: "the tree builder is
free to accept or reject any reservation at any level." The categories apply primarily to sufficiency
trees (Dettmer, chapter 2).

## Level I

### 1. Clarity

The meaning of a word, an entity or a connection is in doubt. A link that skips several steps is a
clarity problem.

Fails: "The service is slow." Passes: "The API's p95 response time exceeds 2 seconds at 10 requests
per second."

## Level II

### 2. Entity existence

TOCICO: it challenges "the validity of a proposed statement of fact". The question: "Does this entity
really exist in your world as you have stated it?" Dettmer tests each entity for completeness (a full sentence), structure (one idea) and validity (it exists and can be
evidenced).

Fails: "Tight coupling exists." Passes: "OrderService imports five internal classes of
ShippingService." The shared table is a second entity.

### 3. Causality existence

Dettmer reads the link aloud in *if-then* form and asks how the cause produces the effect.

Fails: "If we added caching then users see stale data." Passes: "If the status cache keeps an entry
for five minutes without invalidation on write, then a status read within five minutes of a write
returns the old value."

## Level III

### 4. Cause insufficiency

The proposed cause alone cannot explain the effect, so a co-cause joined with *and* is missing.

Fails: "If there are no tests then deployments fail." Passes: "If there are no tests and no staging
environment and deployments run unattended, then a defect reaches production undetected."

### 5. Additional cause

A second, independent cause of the same effect exists. Dettmer describes two forms. In the basic form
the reservation "signifies a missing 'or' condition", and his test is: "If I eliminate the stated
cause, is there any other circumstance under which the same degree of effect would occur?" In the
magnitudinal form, drawn as a bow-tie, each cause accounts for part of the effect. TOCICO's entry
shows only the magnitudinal form.

Example. "If the connection pool is exhausted then p95 exceeds 2 seconds" may be true, yet an N+1
query pattern also raises p95. In the basic form either cause alone produces the effect. In the
magnitudinal form the two add up, and removing the pool problem alone leaves part of the latency.

### 6. Cause-effect reversal

Dettmer: "Is the stated cause really a reason why, or just how we know the effect exists?"

Fails: "If the error rate dashboard is red then the service is failing." The red dashboard is how the
failure is known, not why it happens. A loop, where an effect feeds a cause below it, is a different
structure and a legitimate part of a tree (`tools.md`, Current Reality Tree).

### 7. Predicted effect existence

Defined under "Running a check", below.

Example. Claimed cause: "a memory leak in the image handler." Then heap use must rise with the
number of images processed and fall after a restart. Flat heap use across a day of image traffic
refutes the cause.

### 8. Tautology

Dettmer: "The effect is offered as a rationale for the existence of the cause." Example: "The deploy
failed because the team was careless." How is the carelessness known? Only from "The deploy failed."
Ask for a predicted effect that shows on its own: skipped checks in the log, a missing review.

## Running a check

A link is a hypothesis, and its predicted effect is the test. `SKILL.md`, "Scrutiny becomes checks",
gives the procedure. Three published statements shape it.

- Zeller, *The Debugging Book*, "Introduction to Debugging", "The Scientific Method" (online text, read
  2026-11-11): from a hypothesis, "formulate a *prediction* that can *support* or *refute* the
  hypothesis. Ideally, the prediction would distinguish the hypothesis from likely alternatives." Then
  test it: "If the prediction holds, confidence in the hypothesis increases; otherwise, it decreases."
- TOCICO, *predicted effect reservation*: it can prove or disprove an entity or relationship "very
  difficult, perhaps even impossible to prove by direct observation". Its example: if a car's battery
  charge is low, the lights must be very dim, and bright lights show the charge is not low.
- Dettmer, chapter 2: a predicted effect is judged on three tests: expectation ("Is it there?"),
  coexistence ("Is it there at the same time?") and magnitude ("Is it all there?"). The reservation
  "is always invoked to substantiate a reservation for causality existence." In chapter 6, a negative
  branch of a Future Reality Tree is "a kind of predicted effect existence reservation".

Check facts, not the story of the incident: an account written after a failure selects the facts that
fit it. Cook calls hindsight bias "the primary obstacle to accident investigation" (*How Complex
Systems Fail*, point 8, read 2026-11-11). Read the log of the time, not the memory of it.
