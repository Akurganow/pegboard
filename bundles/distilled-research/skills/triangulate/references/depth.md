# Depth

Depth applies to survey mode only and sets how wide it searches and how many child tasks it may start. The child ceiling counts every child task, collectors, vetters, readers, tracers and the verifier, and a run never exceeds it, because it is the cost the user agreed to.

| Depth | Lanes x rows | Child ceiling | Opens per tracer |
| :-- | :-- | :-- | :-- |
| quick | 2 x 12 | 12 | 0; the lead traces origins |
| standard | 4 x 25 | 30 | 3 |
| deep | 6 x 30 | 40 | 5 |

## Choosing the depth

Choose without asking. The user may change it in the reply to the plan.

- Quick for up to four sub-questions.
- Standard for a survey of a field or five or more sub-questions.
- Deep only when the user asks for exhaustive coverage, because the ceiling, and so the cost, rises with depth.

## Rules for every depth

- The verifier always runs when child tasks exist, because it is the only check on the grades that starts with no context from the run. Without child tasks, `lead.md` gives the shared-context check.
- Kept sources never exceed lanes x rows. A row cut by a lane's row cap goes to the overflow-leads list.
- Readers allowed = ceiling − collectors − vetters − tracers − 1 verifier. Size the reader set last, best tier first, and record the sources over the limit in `plan.md`.
- At quick depth an origin that the lead cannot date from the cards is a gap. Standard and deep have one tracer per theme, with at most 6 themes at standard and 8 at deep, so that tracers leave readers a share of the ceiling. Merge surplus sub-questions when you write the plan.

## Shards

- A vetter takes at most 25 rows and a reader at most 5 sources, so that a child's context holds its rows in full.
- Vetter shards follow `merged.tsv` and are named `v1`, `v2` and so on. Reader shards are the kept vet rows, best tier first, named `r1`, `r2` and so on. A pasted run uses the order of `candidates-user.md`.
