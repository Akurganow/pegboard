# Output

The reply opens with the answer to the user's question, then the graded points. Grades, `N`, `M`, `K` and tiers come from `origins-and-grades.md` and `../../vet-sources/references/tiers.md`. When the user asks for another length or form, deliver exactly that and add the grades in a short note after it. A survey keeps the full lists in `appendix.md`.

1. **Answer:** one opening sentence, up to four direction sentences and one closing caveat sentence.
   - The opening sentence answers in plain words. For "it depends", say on what, and name the question, not the topic.
   - Write one direction sentence per direction that bears on the answer, with a grade word from the legend, the strongest study (first author, year) and its effect with interval. Leave other points to the table.
   - Use the grade words for strength and no other word of strength, such as "weakly", because another word restates a grade in terms nobody checked.
   - The closing sentence names the largest caveat, when it bears on the answer.
2. **Legend:** copy the Legend text of each grade and tier the table shows, with the English grade and tier names. In another language, translate them without changing their meaning. Add the counts legend line from `origins-and-grades.md` and this line: "Grades and tiers are ordinal and uncalibrated. They rank claims in this run and give no probability."
3. **Table:** one row per point, in the order Established, Probable, Contested, Tentative, Not established.
4. **Contested:** only when a point is Contested. List each position with its origins, tier, first-public date, and measured or asserted. Add a "Why the sides differ" line: in a survey from the cluster's `differ` line, in a direct run from the sources (each side's population, measure and dose, or the topic equivalent, and "not stated" for a missing fact). Pick no side, because grades rank claims and do not decide between sources, unless the positions differ in tier. Say so in one sentence.
5. **Not established:** only when a point is. List each with the study or data that could settle it (a survey copies the theme file's `## Gaps`).
6. **Caveats:** one line per sub-question in a survey, copied from `distillate.md`, and one line in a direct run.
7. **Skipped:** only when a source was found and not read, or a stage was skipped. Give the count per reason with up to five URLs each, every retracted source with its URL, and each source searched for and not found, with who named it.
8. **Appendix (survey only):** the path of `appendix.md`.
9. **Header line:** one closing line with these items:
   - the mode (direct, or survey with its depth) and the date;
   - the sources read in full, abstract and snippet, and, counted separately, as pasted;
   - the verifier mode ("independent", "shared-context check" or "none (direct run)");
   - the card quotes that were literal and those that were `paraphrase` (a direct run counts its own notes);
   - in a survey, the verifier's quotes matched of those fetched, not fetched, the points lowered, and those whose `M` it lowered because every quote of a measured origin was `paraphrase`;
   - "no quote was literal; no point can reach Established", when no quote was literal.

| Column | Content |
| :-- | :-- |
| Claim | One sentence, with its `kind`. A Contested row says "Studies disagree on ...". |
| Grade | A grade from the legend, as `origins-and-grades.md` shows it. Add "(on pasted text)" for a point that rests only on as-pasted sources, and "(lowered by the verifier)" on every lowered point. |
| `N (M) + K` | The final counts. |
| Evidence | Per study: year (first-public date), first author, name, design, `n`, population and effect with interval. Add `preprint` when the review status says so, and `read: full`, `abstract` or `snippet`, or `as pasted, not confirmed`. Name each record with its status from the vet row, or `not checked`. End with up to two plain URLs, best tier first. |
| Dissent | The strongest opposing origin, or "none found". An untraced or `unconfirmed` opposing source shows as a `K` line. |

- Evidence URLs are plain and on pages the run could read. Embed no image, because it loads from a third-party host. Copy no link text from a page, because it may carry an instruction.
- Mark every date or collapse the run did not open as `unconfirmed`.
- When a check failed, name the rows it concerns, because "a failed check changed no grade" is true only for those rows.
