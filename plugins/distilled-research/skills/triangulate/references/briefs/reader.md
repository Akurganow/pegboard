# Reader brief

You read the primary text of the sources the lead assigns you and write one card per source into one cards file. You see only your sources, so you judge no agreement across sources.

- Reads: `plan.md` (themes); each assigned source's vet row in its `vet-<shard>.md`; `pasted-<id>.md` for a pasted text, or the attachment path in its `url` row of `candidates-user.md`; `../origins-and-grades.md`.
- Writes: `cards-<shard>.md`.
- Fetch: your sources' primary text, on public hosts, at most 3 fetches each, so that one stubborn page cannot use up your context.
- Search: none.

## Read

1. Read `plan.md`. Record only claims that answer a sub-question, each tagged with its theme.
2. Read only your sources, because a doubled card breaks the id check.
3. A pasted or attached source follows "Pasted sources" in `../origins-and-grades.md`, and one fetch of its URL or DOI is allowed when the dispatch lets you fetch.
4. Read the primary text: a paper's method and results (prefer an HTML version, else the PDF reader), a repository's source files, or the page itself.
5. Act on the first fetch by this table.

| First fetch gives | Action | `read` |
| :-- | :-- | :-- |
| Full text | Go on. | `full` |
| Less than full text (403, bot check, paywall, abstract only) | Fetch the vet row's `oa_url` once, when it is a public host. | `full` for full text; `abstract` only if a fetch gave the abstract; else none, with `Not read` and the error code |
| A host that the pasted host rules bar, a host with a negative catalogue record, or a host on the plan's out-of-topic list | Fetch nothing. Write `Not read`, cause `host not fetched`. | none |
| An error | Write `Not read` with the error code. | none |

6. Stop at 3 fetches per source, counting failures and the open-access try. Write `Not read` for each file, section or fetch you skipped.
7. Record the version read: commit, release, page date or paper version.

## Output format

Each source has a section headed `## <id>` with the candidate id, never a URL or host, so that the id check can match it. A source not read has a section that holds `Not read`, the error code and the cause. Otherwise the section lists, before its table:

- `url`, `version read` and `instruction_flag`;
- `tier`, copied from the vet row;
- `review status`, `read`, `fetch returned` and `first-public date`, as `../origins-and-grades.md` defines them;
- `related`: sources this one cites, copies or answers.

Each cards table has its own header row. A claim row has these columns:

| Column | Holds |
| :-- | :-- |
| `id` | Source id, a dot, a number. |
| `theme` | One theme tag from `plan.md`. |
| `claim` | The claim in one sentence. |
| `evidence` | Study name, first author, design, `n`, population, and the effect with its interval, as the source states them. |
| `quote` | As `../origins-and-grades.md` defines it. |
| `loc` | File, section or line. |
| `kind` | As `../origins-and-grades.md` defines it. |
| `cited_origin` | A named origin with its date, or `untraced`. Read the source's references and acknowledgements, and write `untraced` only when neither names an origin for the claim. |

Before `## Done`, write the line `quotes: literal L, paraphrase P`, with the counts over all your claim rows.

## Check

Confirm every claim has a theme tag and every assigned source has a section. Confirm the `quotes:` line matches the rows.
