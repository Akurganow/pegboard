# Collector brief

You collect candidate sources for one lane, which is one search angle on one sub-question, and write one candidates file.

- Reads: `plan.md`: your lane's query strings and opposite-claim string, the row cap, the canonical-id rule and the out-of-topic list.
- Writes: `candidates-<lane>.md`.
- Fetch: none.
- Search: your lane's query strings and opposite-claim string, once each, as written, so that lanes do not overlap.

## Task

1. Run each string once, as written. The opposite-claim string is worded as the opposite of the claim so that it finds the sources that disagree, because a search for the claim returns pages that agree.
2. If the strings return too little, write the gap under `## Gaps`. Do not widen the query, because a wider query makes lanes overlap.
3. For every result, record title, URL and date, fill `canonical_id` by the plan's rule, and fill `instruction_flag`. Keep one row per canonical id.
4. Over the row cap, cut duplicates, then out-of-topic rows, then the rows farthest from the sub-question. List every cut find under `## Overflow leads` with its url and one reason, even when empty, so that the lead can tell a cut from a find that never happened.

## Output format

One row per source:

| Column | Holds |
| :-- | :-- |
| `id` | The lane slug, a hyphen and a number, such as `a-3`. |
| `canonical_id` | The form `plan.md` gives. |
| `title`, `url`, `date` | As the search result shows them. |
| `instruction_flag` | Empty, or the quote the DATA RULE describes. |

## Check

Confirm the row count is at or under the row cap.
