<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [ARIZ-85C, part by part](#ariz-85c-part-by-part)
  - [The name](#the-name)
  - [Part 1. Analysis of the problem](#part-1-analysis-of-the-problem)
  - [Part 2. Analysis of the problem model](#part-2-analysis-of-the-problem-model)
  - [Part 3. The ideal final result and the physical contradiction](#part-3-the-ideal-final-result-and-the-physical-contradiction)
  - [Part 4. Mobilising and applying the resources](#part-4-mobilising-and-applying-the-resources)
  - [Part 5. Applying the information fund](#part-5-applying-the-information-fund)
  - [Part 6. Changing or replacing the problem](#part-6-changing-or-replacing-the-problem)
  - [Part 7. Analysis of the way the physical contradiction was removed](#part-7-analysis-of-the-way-the-physical-contradiction-was-removed)
  - [Part 8. Applying the answer](#part-8-applying-the-answer)
  - [Part 9. Analysis of the course of the solution](#part-9-analysis-of-the-course-of-the-solution)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ARIZ-85C, part by part

The algorithm Altshuller published in 1985, in his order of steps,
paraphrased in English. The formulas are quoted: the Russian ones from the
Altshuller Foundation's text of ARIZ-85-В, the English patterns from MATRIZ's
English text unless a line names another copy. The software glosses are this
skill's own. [`sources.md`](../../contradiction/references/sources.md) says
which pages and copies were read.

One English copy opens with a warning: "ARIZ is a complicated tool. Do not
apply it to solve new practical problems without at least 80 academic hours
of preliminary study." Of the three texts read, only the 33-page copy carries it. The Foundation's
Russian text and MATRIZ's English text do not.

## The name

ARIZ is the Russian acronym for Algorithm of Inventive Problem Solving.
Altshuller's history (1986) lists ARIZ-85-А, -Б and -В. English texts write
the Cyrillic В as C, by position, or V, by sound: the Foundation says
"АРИЗ-85-В", MATRIZ "ARIZ-85-C", the 33-page copy "ARIZ 85c".

The algorithm has nine parts and forty steps. The text does not name the contradiction matrix. Altshuller's history says
ARIZ-77 kept that table «в качестве вспомогательного материала» [as auxiliary
material]. This reference does not equate the «приемы» [techniques] of step
9.2 with the 40 principles.

## Part 1. Analysis of the problem

**1.1** Write the mini-problem without special terms, in this form:

> Техническая система: для (указать назначение) включает (перечислить
> основные части системы).
> Техническое противоречие 1 (ТП-1): (указать).
> Техническое противоречие 2 (ТП-2): (указать).
> Необходимо при минимальных изменениях в системе (указать результат,
> который должен быть получен).

MATRIZ's pattern: "A Technical System for (state the purpose of the
system) includes (list the main parts of the system). Technical
Contradiction 1 (TC-1): (identify). Technical Contradiction 2 (TC-2):
(identify). It is necessary, with minimum changes to the system, to (state
the required result)."

Neither text fixes the wording of a contradiction. Both examples write it as
"if ..., then ..., but ...": «если молниеотводов много, они надежно
защищают антенну от молний, но поглощают радиоволны» [if there are many
lightning rods, they protect the antenna from lightning, but absorb radio
waves]. This skill uses that shape because it keeps the state, the good effect
and the bad effect apart.

Software gloss: the tool is the component whose setting is in question, and
the product is what it acts on. TC-1: "If the cache holds an entry for an
hour, then the database is idle, but readers see old data."

**1.2** Name the conflicting pair: the product (изделие), which is acted
upon, and the tool (инструмент), which acts on it.

**1.3** Draw the schemes of TC-1 and TC-2 with Table 1, "Typical Graphical
Models of Technical Contradictions" (MATRIZ's heading). Its nine shapes, in
MATRIZ's names, with A the tool and B the product:

1. Counteraction: A acts usefully on B, and at some stage B acts back on A
   harmfully.
2. Conjugated action: A's useful action on B also harms B.
3. Conjugated action: it harms another part of B.
4. Conjugated action: it harms C, a third part of the system.
5. Conjugated action: it harms A itself.
6. Incompatible action: A's useful action on B is incompatible with C's
   useful action on B.
7. Incomplete or missing action: A gives one useful action where two are
   required, or does not act on B at all. The Foundation says the two are
   «равных» [equal], MATRIZ "different".
8. "Silence": there is no information about A, B or their interaction.
9. Uncontrollable (in particular, excessive) action: A acts on B in a way
   that cannot be controlled where control is required.

In software A and B are components or data, and the actions are calls and
events.

**1.4** Choose the contradiction whose good effect is the system's main
function. Note 12 forbids replacing the chosen state with an "optimal" middle
one: the algorithm sharpens the conflict and does not smooth it.

**1.5** Intensify the conflict: push the tool's state to its extreme. Rule 3
turns "few elements" into "no element": not "a long TTL" but "an entry that
is never evicted".

**1.6** Write the problem model: the conflicting pair, the intensified
conflict, and what the X-element must keep and what it must remove, improve
or provide. The X-element (икс-элемент) is the change not yet known and the
subject of the ideal final result. It need not be a new part (note 16).

**1.7** Check whether a standard solution resolves the model. The package
carries none: go on to Part 2, as the algorithm recommends in any case.

## Part 2. Analysis of the problem model

**2.1** Define the operating zone (ОЗ): where the conflict happens.

**2.2** Define the operating time (ОВ): when it happens, and what precedes it.

**2.3** List the substance-field resources (ВПР, SFR) of the system, its
environment and the product: what the solution may use. In software: data held, events emitted, idle capacity, a clock, a log, a
version number, a client that already polls.

## Part 3. The ideal final result and the physical contradiction

**3.1** Write IFR-1:

> икс-элемент, абсолютно не усложняя систему и не вызывая вредных явлений,
> устраняет (указать вредное действие) в течение оперативного времени
> (ОВ) в пределах оперативной зоны (ОЗ), сохраняя способность инструмента
> совершать (указать полезное действие).

MATRIZ's pattern: "The introduction of the X element does not complicate
the system in any way, does not create any harmful effects, and eliminates
(indicate the harmful action) during the Operating Time inside the
Operating Zone, while maintaining the ability of the tool to perform
(indicate the useful action)."

**3.2** Strengthen IFR-1: no new substances and no new fields, so the
solution uses the resources of 2.3. In software: no new service, store or
protocol before the existing ones have been tried.

**3.3** Write the physical contradiction at the macro level. MATRIZ's
pattern: "The Operating Zone during the Operating Time should be (indicate
the physical macro-state, for example, "hot") in order to perform (indicate
one of the conflicting actions), and should be (indicate the opposite
physical macro-state, for example, "cold") to perform (indicate another
conflicting action or requirement)." The Foundation's template writes the
second half as «и не должна (...)» [and must not (...)], which read literally
states no contradiction. Its own example does not read it that way: the air
column must be conducting and must be non-conducting. Use the English form.

**3.4** Write the physical contradiction at the micro level. MATRIZ's
pattern: "The particles of a substance (indicate their physical state or
action) should be in the Operating Zone in order to provide (indicate the
required macro-state according to step 3.3) and should not be there ... in
order to provide (indicate another macro-state)." In software the particles
are the records, requests or cells that make up the zone.

**3.5** Write IFR-2:

> оперативная зона (указать) в течение оперативного времени (указать)
> должна сама обеспечивать (указать противоположные физические макро- или
> микросостояния).

MATRIZ's pattern: "The Operating Zone (indicate) during the Operating Time
(indicate) should, on its own, provide (indicate the opposite macro- or
micro-state)."

**3.6** Check whether a standard solution resolves the physical problem as
IFR-2 states it. The package carries none: go on to Part 4.

## Part 4. Mobilising and applying the resources

**4.1** Model the conflict with Small Smart People (MATRIZ; «маленькие
человечки»): draw the zone as a crowd
of agents, redraw it so that they act without conflict, then translate the
drawing back into a technical scheme. The Foundation's step has these three
actions. MATRIZ's text lists the first two.

**4.2** Take a step back from the IFR when the finished system is known:
draw it and make the smallest change that breaks it.

**4.3 to 4.7** Check in turn whether the problem is solved by a mixture of
resource substances (4.3); a void in place of a resource, or of a mixture
(4.4); a substance derived from a resource (4.5); an electric field in place
of a substance, or two interacting electric fields (4.6); a pair of a field
and an additive that responds to it (4.7).

Software gloss for 4.3 to 4.7: substances are data and components, fields are
the interactions between them. A "void" is an absence used on purpose, such as
a gap in a schedule or a missing entry that means something. A "derived
substance" is a projection, a hash, a digest or a version of data already
held. A field with a responsive additive is a signal plus a marker that reacts
to it, such as a tag a sweep recognises. In 4.6 the field is a signal, such as
an event or a heartbeat, that does the work a stored copy or a poll did.

## Part 5. Applying the information fund

**5.1** Try the standard solutions on the problem as IFR-2 states it, with
the resources refined in Part 4. The Foundation lists 76 in five classes. The
package carries none.

**5.2** Try analogy with non-standard problems solved earlier by ARIZ. The
package carries none.

**5.3** Try the typical transformations for removing a physical
contradiction, in Table 2, "Principles for Eliminating Physical
Contradictions" (Foundation: «Разрешение физических противоречий»). MATRIZ
names the step "Separation Principles", gives only Rule 11 and prints no
table. The table is the Foundation's Table 2, with its standard numbers, in
the 33-page copy's English.

| # | Transformation | Standard |
| --- | --- | --- |
| 1 | Separation of conflicting properties in space | none given |
| 2 | Separation of conflicting properties in time | 2.2.3 |
| 3 | System transition 1a: combination of homogeneous or heterogeneous systems into a super-system | 3.1.1 |
| 4 | System transition 1b: transition from a system to an anti-system, or combination of a system with an anti-system | 3.1.3 |
| 5 | System transition 1c: the entire system has a property X while its parts have a property opposite to X (anti-X) | 3.1.5 |
| 6 | System transition 2: transition to a system that works on the micro-level | 3.2.1 |
| 7 | Phase transition 1: substitution of the phase state of a system's part or external environment | 5.3.1 |
| 8 | Phase transition 2: dual phase state of a system part (using substances capable of converting from one phase to another according to the operating conditions) | 5.3.2 |
| 9 | Phase transition 3: using phenomena associated with phase transitions | 5.3.3 |
| 10 | Phase transition 4: substitution of a mono-phase substance with a dual-phase state | 5.3.4 and 5.3.5 |
| 11 | Physical-chemical transition: substance appearance-disappearance as a result of decomposition-combination, ionization-recombination | 5.5.1 and 5.5.2 |

The 33-page copy cites 2.3.3 for row 2 and 3.2 for row 6. The rule beside the
step: "Only solution concepts that completely match the IFR or come close to
it are acceptable." The four separations of `contradiction`, Step 4, come from
later teaching ([`principles.md`](../../contradiction/references/principles.md)).

Software gloss. Rows 3 to 6 are system-level moves: services clustered as one
system, a service and its inverse, a rigid whole of loose parts, a finer
grain. Rows 7 to 11 are changes of state: a representation that switches with
the conditions, a resource that exists only while needed. Row 9 uses what
accompanies the change, such as the invalidation a commit triggers. Row 10
holds two states at once, such as a live and an archived record. Row 11
builds and decomposes a thing, such as a derived table.

**5.4** Consider removing the physical contradiction with the «Указатель
применения физических эффектов и явлений» [Pointer to the Application of
Physical Effects and Phenomena]. Note 42 says its sections were published in
the journal «Техника и наука» (1981, nos. 1-9; 1983, nos. 3-8) and the book
«Дерзкие формулы творчества» (Petrozavodsk: Karelia, 1987). MATRIZ calls it
a "library of scientific effects and phenomena". The package does not carry
it. The nearest software counterpart, this skill's own reading, is a
catalogue of known mechanisms, such as algorithms and protocols.

## Part 6. Changing or replacing the problem

**6.1** If solved, go from the physical answer to a technical one: state the
method and give the scheme of the device that carries it out. If not solved:
**6.2** check whether step 1.1 combined several problems, split them and solve
the main one; **6.3** choose the other technical contradiction at step 1.4;
**6.4** return to 1.1 and restate the mini-problem at the level of the
supersystem, repeating as needed.

## Part 7. Analysis of the way the physical contradiction was removed

**7.1** Check the solution concept. MATRIZ's text: "Consider each introduced
substance and field. Is it possible to apply available or derived SFR
instead of introducing the substance/field? Can self-controlling substances
be applied?" In software: for each component the solution adds, ask whether a
resource from 2.3 does the same job, and whether a part can change its state
by itself.

**7.2** Assess the solution with four questions, and return to 1.1 if one
fails.

- Does it meet the main requirement of IFR-1, that the element does it
  itself?
- Which physical contradiction did it remove, and did it?
- Does the system contain at least one well-controlled element, and how is it
  controlled?
- Does a solution found for one cycle hold under many cycles?

**7.3** Check the formal novelty of the solution against patent data, in
software against published designs.

**7.4** Write the sub-problems the idea raises: inventive, design,
calculation and organisational.

## Part 8. Applying the answer

**8.1** Say how the supersystem that contains the changed system must change.

**8.2** Check whether the changed system, or the supersystem, can be used in
a new way.

**8.3** Use the answer for other problems: state the principle in general
form, apply it directly, try its inverse, build a morphological table of its
variants, and see how it changes as the system's size goes to zero and to
infinity.

## Part 9. Analysis of the course of the solution

**9.1** Compare the real course of the solution with the theoretical one and
write down the deviations.

**9.2** Compare the solution with the information fund. The Foundation names
«стандарты, приемы, физэффекты» [standards, techniques, physical effects] and
says to record a principle the fund lacks in the preliminary store
(«предварительный накопитель»). MATRIZ: "(Standard Inventive Solutions,
Separation Principles, effects, and phenomena libraries, etc.)". The 33-page
copy: "(Inventive Principles, Inventive Standards, and Pointer to Physical
Effects and Phenomena)". The step compares after the solution and is no
source of solutions.
