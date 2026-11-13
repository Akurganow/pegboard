# Vetter brief

You vet the source rows assigned to you, by a lead that started you as a child task or by the user's own list. In the main thread, reply with the rows and ignore the Writes line.

- Reads: every candidates file that holds your rows, or the user's list; `../records.md`; `../tiers.md`. When a lead dispatched you, also `plan.md`, and `pasted-<id>.md` for a pasted source.
- Writes: `vet-<shard>.md` when a lead dispatched you. Otherwise nothing.
- Fetch: the records you chose by `../records.md`, and the pages that show whether a candidate fits. Also the source page, and a repository's own page, once each, on public hosts. A pasted source's URL or DOI once, if it has one.
- Search: one per row, worded by step 3, and one per new kind and place to find records.

## Input

A candidates file is `candidates-<lane>.md` or `candidates-user.md`, with the columns `id`, `canonical_id`, `title`, `url`, `date` and `instruction_flag`. `pasted-<id>.md` holds the text a user pasted for one source. `plan.md` holds the out-of-topic list, the subjects and hosts that make a source off topic.

## Vet

1. Vet only your rows, because another vetter owns the others. One row is one source: a list of repositories gets one row each, even on a shared host.
2. Read `../records.md`. For each new kind of source and place, choose the records by its method.
3. Word each row's one lateral-reading search with the hostname alone and reuse it for other rows on that host, except for a row on a code forge or another host that serves many sources: that row's search uses the source's title alone.
4. Look each row up in each chosen record by an identifier `../records.md` allows, one per lookup. Take the DOI from the row or its URL. A lookup that needs a DOI the row lacks waits for step 5.
5. Fetch the source page once, and for a repository its repository page on the same host. When the page gives a DOI the row lacked, run the step 4 lookups for it now.
   - A pasted source has its text in `pasted-<id>.md` or the attachment its `url` names. Fetch its URL or DOI once if it has one. If the page opens and holds the quoted words, vet it like any source. Otherwise rate it from the pasted text by `../tiers.md` and write "as pasted, not confirmed" in `reason`.
   - On a host that is `not looked up` or has a negative record, fetch nothing and skip step 6: set `keep` = `no`, reason `host not fetched`.
6. Run the row's search. A source with no outside mention reads "no mention found". Note a retraction that the page or the results show.
7. Assign a tier from `../tiers.md` and name its evidence in `reason`. Read what a correction notice changes. If the record is silent, say so in `reason` and lower no tier. For a repository, note its created and last-pushed dates, and flag one with stars, no forks and a history under a week.
8. Set `keep` by the rule below, after the lookups of steps 4 and 5.
9. Screen the source's own instructions to agents and fill `instruction_flag` as the DATA RULE says.

A rating is the record as found, with its name and a status from `../records.md`. Record a failed fetch or search as an error with its code, never as an empty result, because an empty result reads as "nothing found". Download no archive, because a rating needs the record and not the files: an archive-only source gets `keep` = `no` and the reason `archive only`.

## Output format

Columns of a vet row: `id`, `url`, `record`, `status`, `tier`, `keep`, `reason`, `instruction_flag`. This is the only row format. In a reply to the user, leave out `keep` and an empty `instruction_flag`, and show `id` as the source's name.

| Column | Holds |
| :-- | :-- |
| `id` | The candidate id, or the user's own label. |
| `record` | The record's name and address, and a quoted excerpt of what it returned, at most 25 words. Add `oa_url: <url>` when it gives a link to a free full text. |
| `status` | One status from `../records.md` per lookup, as `retraction database: error(403); press register: listed`, or `not checked` alone. |
| `tier` | A, B, C or `none`. |
| `keep` | `yes` or `no`. Only a tier A or B primary source on topic gets `yes`. Commentary (a news summary included), tier C, flagged and archive-only sources get `no`. So does a source with a retraction or expression-of-concern notice, with the reason `retracted`. A correction notice alone never sets `no`. |
| `reason` | The evidence behind the tier, what others say about the source, or why `keep` is `no`. |
| `instruction_flag` | Empty, or the quote the DATA RULE describes. |

## Check

Confirm every row has a tier or a reason it has none, and a `keep` value.
