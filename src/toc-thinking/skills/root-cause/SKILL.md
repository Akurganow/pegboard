---
name: root-cause
description: >
  Use this skill whenever the user has software problems and wants the real
  cause, or wants a plan or proposal tested. Phrasings: "is it one thing or
  four?", "this keeps happening again", "anything it could make worse?". It
  covers many symptoms with an unclear cause, and a failure that keeps
  coming back. It covers two teams or requirements that want opposite things
  while one side always gives way. It covers a migration, decommissioning or
  rollout that needs a sequenced plan, even when only the plan is asked for.
  It covers a proposed change to check before it is built. Use it even when
  the word root cause never appears. Use it instead of a quick fix or a list
  of tips. It traces the symptoms to the core problem, resolves the conflict
  that holds it, and names what the change could break. Skip it for one bug
  with a stack trace, a slow query, estimates, a postmortem write-up or a
  guide to 5 Whys.
license: MIT
---

# Root cause

Apply Goldratt's Thinking Processes to the user's software system. Reply in the user's language.
Present the result, not the procedure: do not say that a skill or method is being applied or narrate
its steps. Name a tool where you show its output.

## Evidence and delivery

When the session has the code, history, logs, metrics, tests, tickets or documents at hand, read
them before asking, and quote what you read with its path and line, or with the command and its
figure. Ask the user only for what only they know: intent, priorities, owners, what they saw outside
the system. When nothing is at hand, work from what the user gave. Say which facts you read, which
the user gave and which you assume, marking each assumption where it is used.

Give the whole result in one reply: the tree, the core problem where the analysis finds one and,
when the user asked what to change, the proposed change, as a draft with its assumptions marked.
Pause only before an action that spends the user's money,
sends their private data out, loads a shared system or cannot be undone.

Answer the question asked, in the form asked: a decision, a slide, talking points, a message. When
the user fixes a format or a length, deliver exactly that, then a note on the method in one or two
sentences only where the format allows it. An answer that follows every step and leaves the question open has failed, and so has one
weaker than a direct answer: name the concrete behaviour, defect or change with its place (file and
line, service, query). End with questions only when an answer would change the result, at most
three, and say what you did not see when it limits the conclusion.

## Step 1: classify the problem

The Thinking Processes answer three questions in order: what to change, to what, and how to cause the
change (TOCICO Dictionary). Pick the entry point from the description.

- Many symptoms, unclear cause: Current Reality Tree (CRT).
- Two requirements that block each other: Evaporating Cloud (EC).
- A known change that needs a plan: Prerequisite Tree (PRT).
- A proposed change that needs checking: Future Reality Tree (FRT).

When unsure, start with the CRT, and stop at the tool that answers the question. A symptom list with
"what should we change?" goes from the CRT to the EC when a conflict holds the core problem, then to
the FRT on its injection, then to the PRT and the Transition Tree (TT). A request for a plan alone
takes the user's change as the PRT objective. Read `references/tools.md` before building any tree or
cloud, and `references/sources.md` before attributing a statement to Goldratt, Dettmer or TOCICO.

## Scrutiny becomes checks

Treat each causal link on a path from a root cause to the undesirable effects (UDEs) as a hypothesis,
not every link of a large tree. The CRT, FRT and TT use sufficiency logic (*if* cause *then* effect)
and take the checks below. The EC and PRT use necessity logic: question the assumption under each
arrow and name what would be observed if it were false.

1. State the predicted effect: something else that must be true if the link is true, at the same time
   and place and in the size the link implies, ideally one that tells your cause from likely rivals.
   If pool exhaustion makes checkout slow, requests also wait for a connection in the same
   minutes, which slow queries alone would not cause. No waiting refutes the link.
2. Check it. When logs, metrics, code or history are at hand, run the check and report the result
   with its source. Otherwise name a check the user can run (a command, a query, a comparison) and
   say what each outcome means.
3. Record the result as present, absent or not yet checked. An absent effect counts against the link:
   rewrite or drop it. A present effect raises confidence without proof, because a rival cause may
   predict the same effect.

The eight Categories of Legitimate Reservation name the ways a link fails. Read `references/clr.md`
before the first check. A reservation is an offer: accept it by rewording the link, or reject it and
give the observation that answers it.

## Step 2: Current Reality Tree

A UDE is a complete present-tense sentence that states a condition that exists, not a suspected
cause. "p99 latency exceeds 5 seconds during concurrent writes" qualifies. "The system is slow" does
not. One UDE is enough to start (Dettmer, chapter 4).

A root cause is an entity at the bottom of the tree with no cause below it. Several may exist, and the
tree joins co-causes with *and* (`references/tools.md`). The core problem is
the root cause whose branches reach most of the UDEs, including the most serious: weigh them, do not
only count them.

1. Collect the UDEs from the environment first (alerts, dashboards, logs, tickets, incident history),
   then add the user's. List them in the reply, one present-tense sentence each, with what is
   measured or seen, where, and its source: "Android login takes 8 seconds (user)." A label such as "reliability gap" is not a UDE.
2. For each UDE, ask what condition produces it, reading the code and history that touch it. Write
   each link as a full sentence: *if* cause *then* effect, with the measured values, or mark it
   assumed when nothing was measured. Join causes needed together with *and*, and draw causes that
   suffice alone as separate arrows. Check the links and show each predicted effect with its result.
3. Mark a loop, an effect that feeds a cause below it. Removing the root cause behind a loop is among
   the most effective changes (`references/tools.md`).
4. Build down until each branch ends in a root cause, and note which ones someone within the user's
   reach can change. A core problem can be too broad to act on or outside the decision maker's
   control (Dettmer): then name the narrower root causes someone can change.
5. When the branches do not meet, report separate root causes, because an invented common cause points
   the fix at nothing.
6. Show the tree as if-then sentences, and add a Mermaid diagram when it has more than a handful of
   entities (`references/tools.md`). When the analysis runs over several turns and the session can
   write files, offer to keep the tree in one Markdown file and update it instead of restating it.
7. Name the core problem, or say there are several and give the UDEs of each.

## Step 3: Evaporating Cloud

A conflict usually keeps a core problem in place.

```
A  objective      what both sides want
B  requirement    a need that must be met to reach A
C  requirement    a second need that must be met to reach A
D  prerequisite   what is wanted to meet B
D' prerequisite   what is wanted to meet C, and cannot coexist with D
```

Read each arrow from its head: "to have A, we must have B". The conflict is between D and D'. To build
the cloud from Step 2, put the practice the core problem describes in D and the opposite practice in
D', and name what each satisfies as B and C and what both serve as A. Make D and D' practices someone
can do, because a vague cloud has no assumption to attack.

1. Fill the five boxes from Step 2 and the environment. Mark a box you could not read as assumed.
2. Write each necessity arrow with its own endpoints, followed by "because" and its assumption: "In
   order to have A, we must have B" (likewise A-C, B-D, C-D'), and "We cannot have both D and D',
   because" for D-D'. An assumption is open to attack only in the "because" clause.
3. State a likely assumption for any arrow that has none, marked assumed. Question each assumption
   and name what would be observed if it were false.
4. State the injection: a condition or action that invalidates one or more assumptions, so the
   conflict disappears.
5. Reject a compromise between D and D'. It gives each side part of what it wants and leaves the
   assumptions standing, so the conflict returns.

## Step 4: Future Reality Tree

Dettmer sets additional cause aside here: the question is whether the injection produces the effect,
not whether something else also could.

1. Put the injection at the bottom and build sufficiency chains upward: *if* injection *then* effect.
   Continue until the majority of the UDEs are replaced by desired effects.
2. Look for a negative branch: a chain to a new undesirable effect. Search the code, when at hand,
   for where it would show: call sites, queues, limits, callers.
3. Write each one out as a Negative Branch Reservation, and trim it with a second injection where the
   branch turns negative. When a serious branch cannot be trimmed, reconsider the main injection.
4. Check the links. Nothing has run yet, so a check is a prediction to confirm on a staging run, a
   canary or after release, or evidence from a similar past change.

When the user brought a proposed change, it is the injection. Spend the answer on the negative
branches: each chain, its place and its trimming injection.

## Step 5: Prerequisite Tree

1. State the objective: the injection, or the change the user named.
2. List every obstacle that blocks it today as a condition in the system, such as "fifteen call sites
   import the module directly". Find them in code, configuration, schedules and ownership files when
   those are at hand.
3. For each obstacle, state the intermediate objective that overcomes it, and order the objectives.
4. Write each arrow as "In order to reach X, we must first reach Y, because" and the obstacle it
   overcomes, for the reason in Step 3. Question the assumption under each arrow.

## Step 6: Transition Tree

For each intermediate objective, in the order from Step 5, write the five elements of Goldratt's later
form as Dettmer reports it: the existing reality, the need, the specific action, the expected effect,
and the rationale (why the action is needed and why the previous effect was not enough). Read it as
sufficiency, *if* the existing reality *and* the action *then* the expected effect, and check the
links. The tree is the implementation plan. Add "Observed by:" to each step, naming the command, test
or metric that shows its expected effect.

## Hand-over

A cloud that reduces to a trade-off between two measurable parameters belongs to the `contradiction`
skill of this marketplace's `triz-thinking` package, which resolves it with the contradiction matrix
and hands a hard case to `ariz`. Offer it then, if `contradiction` is installed.
