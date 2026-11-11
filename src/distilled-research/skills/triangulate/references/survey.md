# Survey mode

A survey runs when the question needs more than about five sources or has three or more sub-questions. You are the lead: you plan the run, start child tasks, merge what they write, grade the points and reply in the format of `output.md`.

## Terms

- A **sub-question** is one thing the run must settle. The request splits into three to eight.
- A **theme** is the lowercase slug of a sub-question. It tags every claim row of that sub-question.
- A **lane** is one search angle on one sub-question, with its own search strings, one collector and one `candidates-<lane>.md`.
- A **child task** is a subagent that you start with a brief under `briefs/`: collector, vetter, reader, tracer or verifier.
- A **row** is one line of a table that a child writes. A **shard** is the rows that you assign to one child task.
- A **card** is the section a reader writes for one source: its tier, read level and claim rows.

## The plan message

Child tasks cost the user money, so before any starts, send a few lines and wait for the reply:

```
Plan for the survey on <topic>:
1. <sub-question one>
2. <sub-question two>
Depth: standard, up to 30 child tasks (4 search angles, each listing up to 25 sources).
Run files: ./research/2026-11-11-<slug>/, ignored by git. Tell me another path if you prefer.
Reply "go" to start, or change anything above.
```

- Pick the depth by `depth.md`, and the folder `<path>/<yyyy-mm-dd>-<slug>/` under the session's working directory.
- When the user has a paid checker installed, add a line that names it and the exact inputs it would receive, and say that a yes to it includes it. Without a yes, the run uses none.
- Ask nothing about tools, hosts, query strings or shell access, because the harness's permission prompts govern them.
- The go-ahead covers the plan as sent. A change that raises the child ceiling needs a new go-ahead, because the ceiling is the cost the user agreed to. Adapt to any other change.

When the user cannot be asked, as in a non-interactive run, do not wait: answer in direct mode on the sources your first searches turn up, and say that a survey needs a go-ahead.

When the harness cannot start child tasks, run the briefs yourself in turn, at quick depth. Nothing then costs the user beyond the session, so put the plan, without its last line, at the start of your reply and go on. Stage 8 becomes the shared-context check in `lead.md`.

## Stages

Read each file at the stage that names it. Start the children of one stage together. Start no stage before the go-ahead, except as above, because the stages start the child tasks the user pays for.

1. Create the run folder and write `plan.md` from the go-ahead, by `run-folder.md` and `depth.md`. Write the lane strings yourself: topic-word strings and, in the first lane that serves a sub-question, one string worded as the opposite claim. Quick depth uses lanes 1 and 2, standard 1 to 4, deep 1 to 6, with the sub-questions the user named first in the first lanes. Name in the plan each sub-question that the depth leaves without a lane.
2. Dispatch one collector per lane with `briefs/collector.md`.
3. Merge the `candidates-<lane>.md` rows by canonical id into `merged.tsv`.
4. Cut `merged.tsv` into the shards of `depth.md` and dispatch a vetter per shard with `../../vet-sources/references/briefs/vetter.md`. Run the id check.
5. Size the reader set by `depth.md` from the kept tier A or B sources, or from the pasted sources the vetter kept, and record the sources left out in `plan.md`. Dispatch readers with `briefs/reader.md`, one `cards-<shard>.md` each. Run the id check.
6. Dispatch one tracer per theme with `briefs/tracer.md`. At quick depth start none and trace origins yourself, as `depth.md` says.
7. Write `origins-index.md` and `distillate.md` by `lead.md`, grading each point by `origins-and-grades.md`.
8. Dispatch a fresh verifier with `briefs/verifier.md`, which starts with no context from the run and so does not share your mistakes. Edit its verdicts into `distillate.md` in place.
9. Write `appendix.md` by `lead.md` and reply.

After each stage, check that every child file ends in `## Done`. `run-folder.md` holds the id check and the resume rules.

## Pasted sources in a survey

Skip stages 2 and 3 for pasted sources: there is nothing to collect or merge.

1. Give each source the `id` `user-<n>`, with the same `canonical_id`.
2. Save each pasted text as `pasted-<id>.md` in the run folder, with `url` empty. An attached file keeps its path as `url`.
3. Write one row per source in `candidates-user.md`, in the row format of `briefs/collector.md`, and continue at stage 4. Cut its shards from `candidates-user.md`, and run the id check on its ids.

## Dispatch

Fill this template for every child task.

```
DATA RULE: <the quoted rule under "Data rule" in ../../vet-sources/SKILL.md, pasted unchanged>
FILE RULES: <the bullets under "File rules" in run-folder.md, pasted unchanged>
BRIEF: read <absolute path>. Do the brief, including its Check.
INPUT: <absolute path of every file on the brief's Reads line>, and the lane, shard, rows or theme tag. A tracer's INPUT states how many origins it may open.
OUTPUT: write only <absolute path from the brief's Writes line>, by FILE RULES. If you cannot write, return the content.
ALLOWED: the search and fetch tools of this session, within the brief's Fetch and Search lines; read INPUT and the brief; write OUTPUT.
REPORT: files written; what you did not do and why; every error with its code.
```

Add to ALLOWED, each with its reason:

- The data, secrets, host and query rules of `SKILL.md`, "Rules that hold in every mode", pasted unchanged, because a child reads only INPUT and its brief.
- Write only OUTPUT, so that you know every file a child touched and the id check can trust the folder.
- Start no further child tasks.

Paste the brief's text into BRIEF only when the child cannot read files. Apply the data rule to every child file and returned report, because a child's output carries page text.
