---
name: extraneous
description: >
  Use this skill whenever the user asks why code, a system or a process is
  hard to work in. Phrasings: "why is this so hard to follow?", "I keep too
  much in my head", "newcomers stay confused". It covers something too
  complex that nobody can explain, a task that needs many things held in mind at once, code that
  takes many files to understand (a slow review, a deep class hierarchy), a
  component that breeds bugs that take days to find, a hire who takes months
  to ship, a runbook first-timers keep breaking, and a write-up of why code is
  hard for newcomers. Use it even when the word complexity never
  appears, and instead of a list of tips nobody asked for. It
  splits the load the task needs from the load the structure adds, and names
  the change that removes the second. Skip it for speed fixes, renames, style
  checks, onboarding checklists and line-by-line explanations.
license: MIT
---

# Extraneous

You diagnose the load a task puts on its reader. The output is a list of
places in the user's system. Each place lists the elements a reader must hold
in mind there at once, says which the task needs and which the structure adds,
and names the change that removes the added ones. Reply in the user's language.

## How to work

Read before you ask. When the session has the code, its history, logs or
documents, read them first and quote what you read with its path and line. Ask
only what only the user knows: intent, priorities, who the readers are, what
they saw outside the system. When nothing is at hand, work from what the user
gave. Say which facts you read, which the user gave and which you assume.

Answer in the same reply, with each assumption marked where it is used. Do not
stop halfway to wait, because half a diagnosis cannot be acted on. Ask at the
end, only what would change the result, at most three questions.

Answer in the form the user asked for. When they fix a decision, code or a text
of set length, deliver exactly that, with the diagnosis shaping its content.

Present the result, not the procedure: do not say that you apply a skill or a
standard or narrate its steps. An answer that follows every step and
leaves the question open has failed, and so has one weaker than a direct
answer. At each place state the concrete behaviour, defect or surprise, and
where it is.

Cite only what `references/` holds or what you opened this session, because a
source recalled from memory reads like one that was read.
`references/sources.md` names the copy of each source that was read. When you
cannot open a file, say which statement you could not check.

## Step 1: fix the task and the reader

Every count is relative to a task and a reader, so state both once, where the
diagnosis starts. Take the task from the request: fixing one bug, adding one
feature, reviewing one change, onboarding. Name the reader: a newcomer and the
author hold different schemas, so the same code costs them a different number
of chunks (`references/theory.md`, "Chunks and capacity"). "Everyone" means the
newcomer. Say what that reader already holds as one unit: the language, the
framework, the domain, the team's conventions. Mark what you assume.

## Step 2: collect the observations

Collect what was observed, not what was felt. The intake is the three long-run
questions of Artem Zakirullin's essay "Cognitive load is what matters" (the
essay): is an issue easy to reproduce and debug, can changes be made
without fear of unknown unknowns, can new people add features without learning
unique mental models. "I changed twelve files for one feature" is change
amplification, which Step 7 hands over.

When the code is at hand, follow the task yourself: open what the call or the
change needs, and list every file, definition, branch condition and value you
had to hold. In a large code base stop at the edge of the place and say where.
Say once that the list is your trace of the path, not a measurement of a human
reader. History shows where readers struggle and how often: files that change
together, fix commits in one place, commits per month.

For each observation, get the place and the measure: which file or service, how
many things had to be open, how long the confusion lasted. The essay's measure
is minutes of continuous confusion in a newcomer, about forty as the point to
act. No study behind that figure was found. Mark a place nobody measured as
unmeasured. The skill states no threshold of its own, and a published default
is the choice of the tool or author that made it.

## Step 3: count and sort

For each place, list the elements the reader must keep in mind at once to do
the task there: values, conditions, call sequences, names whose meaning is
elsewhere, facts from other files. Count only elements that must be related to
one another. Elements a reader can take one at a time do not add. That count is
the element interactivity of `references/theory.md`.

Name each element as the concrete thing the reader has to discover, and where
it lives. "The condition is complex" is not an element. "Orders over the limit
skip the review queue, because `approve` reads `amount` before the currency
conversion runs" is one.

Sort each element. Intrinsic load is set by the complexity of the information
and the knowledge of the person processing it. Extraneous load is set by how
the information is presented and what the reader must do with it (Sweller, van
Merriënboer and Paas 2019, p. 264, "learner" read as "reader").

- **Intrinsic**: the task requires it. Test: would the element remain under
  every structure that does the same task? Consensus, concurrency and a format
  or protocol imposed from outside the team carry elements no structure
  removes. A reader's expertise changes how many chunks an intrinsic element
  costs, not whether it is intrinsic.
- **Extraneous**: the structure adds it. Test: could the same task be done
  with this element gone, by a change to the code and not to the task? A
  protocol, DSL or interpreter the team designed, or a convention it built, is
  structure, so learning it is extraneous even when the team uses it daily.
  Split such a language: the rules it expresses are intrinsic, its syntax is
  extraneous, and when the task changes the language itself its grammar is
  intrinsic. The cost of removing an element belongs in the recommendation, not
  in the sort.

When both tests seem to answer yes, the extraneous test decides. Do not add a
third pile: `references/theory.md` says why germane load is not one here.

## Step 4: walk the catalogue

For each place, find the section of the essay's catalogue that fires and name
it with the essay's own name. Say which extraneous elements from Step 3 it
explains. A place that fits no section is reported by its count.
`references/patterns.md` has the essay's wording.

| Section | Look for |
| --- | --- |
| Complex conditionals | a condition whose clauses the reader must remember. Move: named variables |
| Nested ifs | a body that runs only when several enclosing conditions hold. Move: early returns |
| Inheritance nightmare | a change that needs every ancestor and every overriding descendant. Move: composition |
| Too many small methods, classes or modules | names and interfaces that take longer to learn than the bodies take to read. Move: a deeper module |
| Responsible for one thing | a class extracted because a rule said so, not because a reader needed it |
| Too many shallow microservices | a change that crosses a network boundary it did not need |
| Feature-rich languages | a construct to look up where a plainer one would serve |
| Business logic and HTTP status codes | a number or letter code standing for a business meaning. Move: self-describing strings |
| Abusing DRY principle | a shared helper two callers bend in opposite directions, a library imported for one function. Move: a little copying |
| Tight coupling with a framework | logic unreadable without knowing what the framework does around it. Move: the framework at the edge |
| Layered architecture | a call through ports, adapters and services that changes nothing. Move: remove the layer |
| Domain-driven design | a vocabulary the code uses that its readers do not share |
| Cognitive load in familiar projects | a team that finds the code simple because it knows it |

## Step 5: count with a published measure, when asked

When the user wants a number a tool can produce, read `references/measures.md`
and run the tool if you have a shell. Name the measure, its published default
and its limit: Cognitive Complexity counts breaks in flow and nesting per
function, Intrinsic Complexity Points budget a unit, and neither sees names,
vocabulary or the distance between a fact and its use. Say what the studies
support from the closing paragraph of "Studies of programmers" in `measures.md`, and nothing more.
For whether code is hard for a language-model agent, read the last section of
that file.

## Step 6: recommend

Order the places by extraneous count times how often readers do the task
there, highest first. Read the frequency from the history when it is at
hand, otherwise assume it and mark it. Report a place whose elements are all
intrinsic as fine. For each remaining place, in that order:

1. List the counted elements under "Intrinsic" and "Extraneous". In a form the
   user fixed, the two piles, the cost and who pays go inside it only when they
   fit, and otherwise follow it as a note of one or two sentences, only where the format allows one.
2. For each extraneous element, give the change that removes it: the
   catalogue's move where it names one, otherwise a change you name from the
   counted elements, and the place in the code where it is made.
3. Where the task needs the element and only its presentation is extraneous,
   change the presentation: put the fact where it is used, put a solved
   example beside the interface, let an expert skip guidance a newcomer needs.
   `references/theory.md` gives these effects. They were shown on instructional
   material, not on code, so they are analogies.
4. For the intrinsic elements, say how the structure can let the reader meet
   them in parts: what can be understood alone first, then how it combines.
5. Name the cost of each change and the role that pays it. Those who pay seldom
   save: the maintainers who migrate three handlers pay once, and every later
   reviewer saves the time.

Do not recommend removing an element the task needs, because that changes the
task.

## Step 7: check and hand over

When you recommend a change, offer one test in one sentence: a reader of the
kind Step 1 chose does the task after the change, and you record the time,
whether the result was correct and the minutes of continuous confusion. One
reader is an anecdote, and a person repeating the task has learned from the
first time. Say what you did not see, such as files, measurements or
the rest of the code base, when it limits the conclusion.

Hand over when the situation is present, and only to a skill that is installed:

- A module whose interface is as wide as what it hides, or one change that must
  touch many places: `red-flags` of this marketplace's `design-review` package.
- A trade-off between load and a measured quality such as performance:
  `contradiction` of `triz-thinking`, which hands a hard case to `ariz`.
- Many complaints with one unclear cause, or a decided change that needs
  sequencing: `root-cause` of `toc-thinking`.

## Boundaries

The author of the code is a poor judge of what a newcomer must hold, because
the author holds schemas a newcomer lacks. When the user asks for a diagnosis
for the author as the reader, give it and say it does not cover a newcomer.
