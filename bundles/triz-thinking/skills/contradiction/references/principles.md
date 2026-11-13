<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [The 40 inventive principles](#the-40-inventive-principles)
  - [1. Segmentation](#1-segmentation)
  - [2. Taking out](#2-taking-out)
  - [3. Local quality](#3-local-quality)
  - [4. Asymmetry](#4-asymmetry)
  - [5. Merging](#5-merging)
  - [6. Universality](#6-universality)
  - [7. Nested doll](#7-nested-doll)
  - [8. Anti-weight](#8-anti-weight)
  - [9. Preliminary anti-action](#9-preliminary-anti-action)
  - [10. Preliminary action](#10-preliminary-action)
  - [11. Beforehand cushioning](#11-beforehand-cushioning)
  - [12. Equipotentiality](#12-equipotentiality)
  - [13. The other way round](#13-the-other-way-round)
  - [14. Spheroidality and curvature](#14-spheroidality-and-curvature)
  - [15. Dynamics](#15-dynamics)
  - [16. Partial or excessive solutions](#16-partial-or-excessive-solutions)
  - [17. Another dimension](#17-another-dimension)
  - [18. Mechanical vibration](#18-mechanical-vibration)
  - [19. Periodic action](#19-periodic-action)
  - [20. Continuity of useful action](#20-continuity-of-useful-action)
  - [21. Skipping](#21-skipping)
  - [22. Convert harm into benefit](#22-convert-harm-into-benefit)
  - [23. Feedback](#23-feedback)
  - [24. Intermediary](#24-intermediary)
  - [25. Self-service](#25-self-service)
  - [26. Copying](#26-copying)
  - [27. Cheap short-living objects](#27-cheap-short-living-objects)
  - [28. Replacement of a mechanical scheme](#28-replacement-of-a-mechanical-scheme)
  - [29. Pneumatics and hydraulics](#29-pneumatics-and-hydraulics)
  - [30. Flexible shells and thin films](#30-flexible-shells-and-thin-films)
  - [31. Porous materials](#31-porous-materials)
  - [32. Colour changes](#32-colour-changes)
  - [33. Homogeneity](#33-homogeneity)
  - [34. Discarding and recovering](#34-discarding-and-recovering)
  - [35. Parameter changes](#35-parameter-changes)
  - [36. Phase transitions](#36-phase-transitions)
  - [37. Thermal expansion](#37-thermal-expansion)
  - [38. Strong oxidants](#38-strong-oxidants)
  - [39. Inert atmosphere](#39-inert-atmosphere)
  - [40. Composite materials](#40-composite-materials)
  - [Separation principles for a physical contradiction](#separation-principles-for-a-physical-contradiction)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# The 40 inventive principles

Numbered as the matrix numbers them. An entry holds the name as the matrix
tables carry it, with variants; the sub-items, paraphrased from the
Altshuller Foundation's list of 1973 (`sources.md`); a "1979:" line for a
sub-item only the 1979 wording has; a "Software:" reading, which is this
skill's own and not Altshuller's text; and a "Published" analogy by Rea
(2001) or Fulbright (2004) where it adds to the software reading. Read a
principle as a direction and state what it would mean in the user's system.

## 1. Segmentation

Divide an object into independent parts. Make it easy to take apart.
Increase the degree of fragmentation.

Software: split a module, a store or a request by tenant, by time, by
version. Partition a table. Break a batch into records.

## 2. Taking out

Variants: extraction, separation. Extract the disturbing part or property
from an object, or extract the only part that is needed.

Software: pull the slow path out of the hot loop. Move a side effect out of
a pure function. Isolate the one operation that needs a lock.

## 3. Local quality

Go from a uniform structure to a non-uniform one. Let different parts do
different jobs. Give each part its own best conditions.

Software: tiered caching, graded validation by field, a different retry
policy per endpoint, strict types at the boundary and loose ones inside.

## 4. Asymmetry

Replace a symmetric form with an asymmetric one.

1979: if the object is already asymmetric, increase the degree of
asymmetry.

Software: a discriminated union instead of one shape for all cases. A
read model that differs from the write model. Unequal replicas.

## 5. Merging

Variants: consolidation, combining. Join like objects, or objects meant for
adjacent operations. Join like or adjacent operations in time.

Software: batch writes, coalesce events, bundle requests, run similar jobs
in one pass.

Published (Rea): parallel processes; a thread monitor that merges threads of
different priority under one arbitrator.

## 6. Universality

One object performs several different functions, so that other objects
become unnecessary.

Software: one handler for several message types, a plugin interface, a
generic component in place of a family of specific ones.

Published (Rea): one object with several classifications by context, set by
the user's login preferences.

## 7. Nested doll

Variants: nesting, matryoshka. Put one object inside another, and that
inside a third. Pass one object through a cavity in another.

Software: recursive types, nested transactions, a hierarchy of stores,
middleware that wraps middleware.

## 8. Anti-weight

Variants: counterweight. Compensate the weight of an object by joining it
to something that lifts, or by using the environment.

Software: an index that offsets the cost of a scan, a cache that offsets
latency, a CDN that offsets distance.

Published (Rea): one shared object across many contexts, to carry many
fine-grained objects under dynamic load.

## 9. Preliminary anti-action

Variants: prior counter-action. The Foundation's 1973 list calls it
«предварительного напряжения» [pre-stress]: give the object stresses
opposite to the unwanted working stresses in advance. The name here and the
sub-item below are the 1979 form.

1979: when an action has to be performed, perform the counter-action first.

Software: a circuit breaker armed before the call, a rollback plan written
before the migration, a reservation before the write.

Published (Rea): preliminary processing that speeds a later step, such as
reversing lines of text before matching line breaks.

## 10. Preliminary action

Variants: prior action; the 1973 list says «предварительного исполнения»
[prior execution]. Perform the required change, or part of it, in advance.
Arrange things so they act without delay, from the most convenient place.

Software: precomputation, prefetching, warm caches, connection pools,
ahead-of-time compilation.

## 11. Beforehand cushioning

Variants: in-advance cushioning, beforehand compensation. Compensate for
low reliability with countermeasures prepared in advance.

Software: rate limits, input validation at the edge, error boundaries,
backups, a dead-letter queue.

## 12. Equipotentiality

Change the working conditions so that the object need not be raised or
lowered.

Software: keep data at the level where it is used instead of moving it up
and down layers. Level the load with a queue. Keep latency budgets even.

## 13. The other way round

Variants: inversion, reverse. Do the opposite of what the task prescribes.
Make the fixed part move and the moving part fixed. Turn it upside down.

Software: pull instead of push, lazy instead of eager, let the consumer
call back, invert a dependency.

Published (Rea): transactions stored in reverse order so they can be backed
out; recovery and backtracking in a database.

## 14. Spheroidality and curvature

Variants: spheroidality. Replace straight and flat with curved. Use
rollers, balls and spirals. Replace linear motion with rotation and use
centrifugal force.

Software: exponential backoff instead of a fixed interval, a ring buffer
instead of a list, smoothing instead of thresholds.

## 15. Dynamics

Variants: dynamization, dynamicity. Let the object or its environment
adjust to the best state at each phase. Divide the object into parts that
move relative to each other.

1979: if the object as a whole is immobile, make it movable.

Software: adaptive limits, autoscaling, feature flags, a strategy chosen at
run time from the data's shape.

## 16. Partial or excessive solutions

Variants: partial or excessive actions, the form many English lists use;
the Russian says «решения» [solution]. When 100% of the required effect is
hard to get, get a little less or a little more. The task may become much
simpler.

Software: over-fetch and filter, over-provision and trim, validate the
common fields now and the rest later.

Published (Rea): perturbation analysis, which changes a measured computation
a little to approximate its true performance.

## 17. Another dimension

Variants: transition to another dimension. Move from a line to a plane to
a volume. Use several layers. Tilt the object or lay it on its side. Use
the other side.

Software: index by time as well as by key, add a tier, shard along a second
axis, render on the server as well as on the client.

## 18. Mechanical vibration

Set the object oscillating. Raise the frequency, up to ultrasound. Use
resonance. Use piezo vibrators in place of mechanical ones. Combine
ultrasound with electromagnetic fields.

Software: periodic health checks, jittered retries, a heartbeat, a sampling
rate tuned to the signal.

## 19. Periodic action

Replace continuous action with pulses. Change the frequency. Use the
pauses for something else.

Software: batch jobs, polling on a schedule, debouncing, work done between
frames.

## 20. Continuity of useful action

Keep all parts working at full load without pauses. Remove idle time.

Software: streaming instead of request and reply, background workers,
pipelining, a pool that never drains.

## 21. Skipping

Variants: rushing through. Do a harmful or dangerous step at high speed.

Software: an atomic swap instead of an incremental update, a fast cut-over,
a migration in one short window.

## 22. Convert harm into benefit

Variants: blessing in disguise, an English idiom; the Russian is «Обратить
вред в пользу» [turn harm into benefit]. Use a harmful factor to get a
useful effect. Remove one harm by adding another. Amplify a harm until it
stops being one.

Software: treat errors as signal for observability, use load to warm the
cache, turn a duplicate delivery into an idempotency check.

Published (Rea): against a distributed denial of service, each attacking
machine solves a small puzzle before it connects, which limits the connection
requests it can make at the same time.

## 23. Feedback

Introduce feedback, or change the feedback that exists.

Software: metrics that drive a controller, backpressure, an adaptive
timeout, user-visible progress.

## 24. Intermediary

Variants: mediator. Use an intermediate carrier object. 1979: the
intermediate object carries or performs the action, and a temporary object
that is easy to remove is attached for a while.

Software: a gateway, a queue, an adapter, a proxy, a facade over a legacy
interface.

## 25. Self-service

The object serves and repairs itself by performing auxiliary and repair
operations. Use waste of energy and of substance.

Software: a cache that refreshes itself on write events, self-healing
workers, garbage collection, logs that compact themselves.

## 26. Copying

Use a simplified, cheap copy instead of an object that is unavailable,
complex, expensive, inconvenient or fragile. Replace an object with its
optical copy and change the scale. If visible optical copies are used,
move to infrared or ultraviolet ones.

Software: a mock, a replica, a snapshot, synthetic data, a shadow deploy.

Published (Rea): a shallow copy that holds references to the original's
parts instead of building a new object.

## 27. Cheap short-living objects

Variants: cheap disposables. Replace an expensive durable object with
several cheap ones, giving up some property.

Software: ephemeral containers, disposable environments, short-lived
tokens, immutable builds thrown away after use.

Published (Rea): throwaway prototypes, built fast to learn which stated
requirements are real.

## 28. Replacement of a mechanical scheme

Variants: mechanics substitution, replacement of a mechanical system.
Replace a mechanical system with an optical, acoustic or odour-based one
(«запаховой»). Use electric, magnetic and electromagnetic fields to
interact with the object. Move from static fields to moving ones, from
fixed to time-varying, from unstructured to structured. Use fields together
with ferromagnetic particles.

Software: replace polling with events, a manual step with a signal, a
timer with a trigger, a scan with a subscription.

## 29. Pneumatics and hydraulics

Replace solid parts with gas or liquid.

Software: replace a rigid structure with a flow: a stream instead of a
buffer, a pipeline instead of stages that hand off files.

## 30. Flexible shells and thin films

Variants: flexible membranes. Replace a rigid construction with a flexible
shell. Isolate an object with a thin film.

Software: a thin interface layer over a core, a thin client, an
anti-corruption layer.

## 31. Porous materials

Make the object porous, or fill existing pores with something useful.

Software: sparse indexes, probabilistic structures, gaps in a schedule kept
free on purpose, room left in a format for later fields.

Published (Fulbright): deliberately imperfect software, as a chess tutor that
errs on purpose to play down to the student.

## 32. Colour changes

Variants: optical property changes. Change the colour or transparency of
an object or its surroundings. Use marker additives.

Software: feature flags that mark a path, tracing tags, colour in a
dashboard, a visible marker on a record.

## 33. Homogeneity

Make interacting objects of the same material.

Software: one error format everywhere, one serialisation, one language on
both sides of a boundary.

## 34. Discarding and recovering

Variants: rejecting and regenerating parts. Discard a part once it has
done its job. Restore used parts during operation.

Software: purge stale entries, rotate keys, regenerate a derived table,
drop a temporary index after the migration.

## 35. Parameter changes

Variants: changing properties, transformation of properties; the Russian is
«изменение физико-химических параметров» [change of physical and chemical
parameters]. Change the state of aggregation. Change the concentration or the
consistency. Change the degree of flexibility. Change the temperature.

Software: change the representation: denormalise, serialise, change the
encoding, change the consistency level, change the granularity.

Published (Rea): an application that changes its service when its properties
change at run time, as multi-role objects do.

## 36. Phase transitions

Use the effects that occur during a change of state.

Software: use the moment of a state change: on commit, on deploy, on
connection, on rollover.

## 37. Thermal expansion

Use expansion and contraction with temperature. Use materials with
different coefficients.

Software: let a structure grow and shrink with load: elastic pools, dynamic
arrays, adaptive sampling.

## 38. Strong oxidants

Variants: accelerated oxidation. Replace air with enriched air, then
oxygen. Use ionised oxygen and ozone.

Software: a more capable runtime, managed services, a stronger consistency
guarantee where it pays. A loose reading: the principle intensifies a
process with a stronger reagent.

Published (Fulbright): mixing something in to randomise an output, as salt
does in password encryption. Rea has none.

## 39. Inert atmosphere

Replace the usual medium with an inert one. Carry out the process in a
vacuum.

Software: a sandbox, an isolated container, a read-only mode, a clean
environment for a test.

## 40. Composite materials

Replace a uniform material with a composite one.

Software: hybrid storage, a cache in front of a log, polyglot persistence,
a component built from parts with different properties.

Published (Rea): composite design patterns, whose integration shows a
synergy.

## Separation principles for a physical contradiction

Step 4 uses four separations: in space, in time, on condition, and between
the parts and the whole. They come from later teaching texts, the MATRIZ
glossary (2014) and the TETRIS handbook (2009). Altshuller's own lists
differ. ARIZ-77, step 4.1, gives four, as the Foundation's page prints them:

- in space
- in time
- through transitional states in which the opposite properties coexist or
  alternate
- by restructuring, so that the particles of the zone have one property and
  the whole zone the other

ARIZ-85-В gives the eleven of its Table 2, listed under step 5.3 of
[`ariz-85c.md`](../../ariz/references/ariz-85c.md). "On condition" is in
neither list. Authors attach lists of the 40 principles to each separation,
and the lists differ, so this skill attaches none.
