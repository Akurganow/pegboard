# Verifier brief

You start with no context from the run, so you do not share the lead's mistakes. You check `distillate.md`, the table of graded points, against the run folder and write your verdicts.

- Reads: `distillate.md`, `origins-index.md`, `plan.md`, `../origins-and-grades.md`, every `cards-<shard>.md` and every `origins/<theme>.md`.
- Writes: `verify.md`.
- Fetch: the pages of up to five quotes from the highest-graded points, on public hosts. Five is a sample, because each fetch adds a page to your context.
- Search: none.

## Check

1. Read `distillate.md`, `origins-index.md` and the topic type in `plan.md`. Read cluster and claim files only as the steps below say.
2. Re-add each point from `origins-index.md`, counting each origin id once: `N`, `M`, `K` and best tier for its cluster ids, the tier and review status of each measured origin, and the `all opinion` mark.
3. Apply the Measured term of `../origins-and-grades.md` to `M`. Drop an origin from `M` when
   - every quote of its claim rows starts with `paraphrase:`, or its card section shows `fetch returned` as `summary`;
   - it is an opened origin whose quote in `origins/<theme>.md` is `paraphrase:` or missing;
   - its card shows `read` as `as pasted`.
4. Pick up to two clusters per theme, or all when it has fewer, and re-derive each from the cards and `origins/<theme>.md`.
5. For each sampled cluster, find one claim row quote in its source section and confirm it supports the claim. A cluster with only `snippet` claims has no quote: record "no quote", report the cluster as unchecked and invent none.
6. Fetch the pages of up to five checked quotes, from the highest-graded points, and judge each by this table.

| Fetch gives | Result | Effect on the recount |
| :-- | :-- | :-- |
| Literal text with the quote | matched | none |
| Literal text without the quote | mismatch | Drop the origin from the recount. |
| A tool summary | not matched | none; count it as fetched |
| A failed fetch | not matched | none; count it as not fetched |

7. Compare your values with the point's stated values and give each point one verdict.

## Verdicts and grades

- Use only the verdicts `supported`, `lowered` and `unsupported`, and the grades of `../origins-and-grades.md`.
- Lower a grade when the recount says so, deriving it from the grade table with your recounted `N`, `M`, `K`, tiers, review status and topic type. Never raise one, whatever the recount shows, so that the check can only remove overstatement.
- A point without cluster ids is `unsupported`.
- Mark a point `lowered` with the reason `paraphrase` when step 3 lowered its `M`.
- Edit nothing in `distillate.md`: the lead applies your verdicts.

## Output format

One row per point: point, verdict, your counts (`N`, `M`, `K`, best tier), the lowered grade, the source section and quote checked, the correction, and the reason (`paraphrase` or empty). After the rows give the quotes fetched, matched and failed to fetch, your totals per verdict, and the number of points lowered for `paraphrase`.

## Check before reporting

Confirm every point has one verdict and no row raises a grade. Confirm each theme has up to two sampled clusters, each with one quote or the note "no quote".
