# Lead formats

Only the lead of a survey reads this file, which holds the files the lead writes itself.

## origins-index.md

One line per cluster: id, theme, claim, `N`, `M`, `K`, best tier, traced origin ids and untraced source ids. Mark each measured origin with its tier and review status, and copy the `all opinion` mark. The lead reads the index for counts and opens a theme file only to copy evidence, dissent, the Caveats line and the gaps.

## distillate.md

One row per point. A point is one cluster, except that the two sides of a Contested pair form one point. A row holds the point, grade, `N`, `M`, `K`, best tier, cluster ids, evidence and dissent. An evidence cell holds at most 25 words per origin. The file ends with one `## Caveats` line per theme, copied from the theme files.

## Stage 8 without subagents

The lead cannot drop its transcript, so its check shares its mistakes.

1. Run the steps of `briefs/verifier.md`.
2. Write the result as `verify-shared.md`, labelled "shared-context check".
3. Offer a fresh session that names the run folder, to run stage 8 with an independent verifier.
4. `distillate.md` keeps Established, so a later independent verifier can confirm or lower it.

## appendix.md

Copy these lists from the files, each entry with its reason: excluded (vet rows with `keep` = `no`, and overflow leads); read (each source with its `read` level); not read (each source with its error code, and each source on the over-limit list in `plan.md`); lane gaps (each collector's `## Gaps`).

## Verifier verdicts

Only a survey has an independent verifier. The lead edits each point's row in `distillate.md` in place.

| Verdict | Effect |
| :-- | :-- |
| supported | The grade stands. |
| lowered | Replace the grade, `N`, `M`, `K` and best tier with the verifier's values. The verifier derives the grade from the grade table in `origins-and-grades.md`, and it is Not established only when `N` = 0. |
| unsupported | The grade is Not established. |

A Contested point keeps its grade on `supported`. On `lowered`, the lead tests the Contested row again with the verifier's origins. If both positions still rest on different traced origins, it stays Contested and the lead narrows its claim text. Otherwise the verifier's grade stands for the one position left.
