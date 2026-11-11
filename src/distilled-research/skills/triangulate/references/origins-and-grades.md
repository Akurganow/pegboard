# Origins and grades

Two axes grade each point: how many independent origins state it, and how good the best one is. In a direct run "the reader" and "the tracer" below mean you.

- A **point** is one claim graded in the reply. In a survey it is a row of `distillate.md`.
- A **claim row** is one claim that one source makes, with its quote, `kind` and cited origin. In a survey it is a row of a card's table.
- A **cluster** is a group of claim rows that state the same idea, with their origins counted together. A direct run keeps its clusters in its notes.

## Fields of a claim row and an origin

- `kind`: `technique` (a method the source describes), `measured` (the source reports its own measurement or dataset) or `opinion` (a judgement with no measurement).
- `quote`: at most 15 words, literal or starting `paraphrase:` ("Literal quote" below).
- `read`: `full` (the whole page was fetched, even if the tool returned a summary of it; for a paper the method and results, for a repository the source files the claim rests on), `abstract` (the abstract alone), `snippet` (a search excerpt only, with `quote` empty) or `as pasted` (pasted text the run could not open).
- `fetch returned`: `page text` when the tool returned the page's own words, else `summary`.
- `review status`: `peer-reviewed`, `preprint` or `not a paper`.
- `first-public date`: from the opened page, else `unconfirmed`.

## Origins

| Term | Meaning |
| :-- | :-- |
| Traced origin | Its identity is recorded, its first-public date comes from a page the run opened, and one of three holds: (a) it reports its own measurement or dataset; (b) it cites a named origin that the reader or tracer resolved and dated; (c) it is a tier A or B document of record that states the claim. |
| States the claim | The origin's own opened text says it. A source that cites the origin does not. |
| Unconfirmed | A date, claim or link known only from memory, a search result or a snippet. It is never a traced origin, never collapses a family, and counts toward `K`. |
| Independent | The tracer found no counted origin that it copies, cites for the claim or forks, and shares no author, organisation or dataset with one. A family collapses to one origin, on evidence from a card or an opened page. |
| Untraced | Any other source whose own opened text states the claim. `K` counts them. They show spread and never support a grade. |
| Measured | A traced origin read `full` that reports its own measurement, with a literal quote on file: one of its claim rows, or the quote in the file of the tracer that opened it. Without one it counts toward `N`, never `M`. One read at `abstract`, and an as-pasted source, also count toward `N` and never `M`. |

## Output form

Each point shows `N (M) + K` and its best tier, taken among the traced origins. `M` is a subset of `N`, and `M` = 0 reads as unmeasured. Each count counts an origin id once across the point's clusters. `K` never enters a grade. A measurement with review status `preprint` is unreviewed. Tier names come from `../../vet-sources/references/tiers.md`.

Counts legend text: `N (M) + K: N is independent origins. M is measurements among them, read in full with a literal quote. K is sources that repeat the claim without a traced origin.`

## Literal quote

A quote is literal in two cases only: the fetch tool returned the page's own text, or the quote is copied from text the user pasted. When the tool returned a summary or rewrite, the quote starts with `paraphrase:`, whatever quote marks the summary shows. When you cannot tell, mark `paraphrase:`.

## Pasted sources

A pasted excerpt is not a page the run opened, because anyone can paste a fabricated one with a made-up URL.

- When a pasted source carries a URL or a DOI and a fetch tool is at hand, open it once. If the page opens and holds the quoted words, treat the source like any other. Otherwise it stays "as pasted".
- Rate an as-pasted source by `../../vet-sources/references/tiers.md`, "Pasted sources". Its author, date and URL are "as pasted, not confirmed". For the Traced origin row, its identity and date as pasted stand in for an opened page.
- An as-pasted source may count toward `N` and never toward `M`, because a measurement counts only when the run read it at its source. So no point reaches Established on pasted text alone. The reply marks such sources and points (`output.md`).

## Grade table

Apply the rows in order, and the first row that fits sets the grade. The ladder, highest first: Established, Probable, Tentative, Not established. Contested stands outside it. The reply copies the Legend text of each grade it shows.

| Grade | Rule | Legend text |
| :-- | :-- | :-- |
| Contested | Two positions rest on different traced origins, at least one side tier A or B or measured. A finding that only narrows the claim edits the claim text instead. | Contested: independent origins on both sides, at least one side tier A, tier B or measured. It is no rank and does not weigh the sides. |
| Established | At least one claim row is not `opinion`. `N` >= 3. `M` >= 1 from tier A, or on a topic other than science or health from tier A or B. On a science or health topic, a measurement from an unreviewed preprint counts as tier B. Without an independent verifier the reply shows it as Probable. | Established: three or more independent origins, one a tier A or B measurement, and the verifier agreed. On a science or health topic the measurement is tier A and no unreviewed preprint. |
| Probable | At least one claim row is not `opinion`. `N` >= 2 with a tier A or B origin. | Probable: two or more independent origins, one from a tier A or B source. |
| Tentative | `N` >= 1 and no row above fits. Every point whose claim rows are all `opinion` lands here. | Tentative: one origin, an opinion, or only lower-tier origins. |
| Not established | `N` = 0, or the point has no cluster ids. | Not established: no independent origin was traced, or the verifier found the point unsupported. |
