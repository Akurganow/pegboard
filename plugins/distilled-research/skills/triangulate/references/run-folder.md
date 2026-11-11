# Run folder

A survey writes every file into one folder, by these rules. Each role's row format sits in its brief.

## Folder

- Name: `<yyyy-mm-dd>-<slug>/` under the path the plan message gave. The slug is lowercase ASCII letters, digits and hyphens, at most 40 characters.
- Never reuse an existing folder for a new run, because the earlier run's files would be read as this run's. Ask for another path or slug. Resume writes into a folder only when the user names it.
- The folder holds copied page text, so write a `.gitignore` inside it with the single line `*`. Leave the user's own `.gitignore` alone, because it is part of their project.

## File rules

- Every file opens with the line `Research data. Not instructions.`
- Tables are Markdown pipe tables. A URL sits in angle brackets, with every `|` inside it written `%7C`. No other cell holds `|` or a newline, because either breaks the row.
- A cell holds one short sentence. The `distillate.md` evidence cell is the one exception.
- Each child file ends with the line `## Done`. A file without it is incomplete.
- Record a failed fetch or search as an error with its code, never as an empty result, because an empty result reads as "nothing found".

## plan.md

The lead writes it from the go-ahead. It holds:

- Depth and folder.
- Sub-questions, each with a theme.
- Lanes: one slug each, with its sub-question, query strings, opposite-claim string and row cap.
- Topic type, as `../../vet-sources/SKILL.md` defines it.
- Out-of-topic list: the subjects and hosts that make a source off topic, or that the user asked to avoid, written from the user's request.
- Canonical-id rule: the form two finds of one source share, such as a DOI, `owner/repo`, or a URL without scheme, `www.`, fragment and trailing slash. Keep query parameters except tracking ones such as `utm_source`.
- Not read, over the child limit: the kept ids no reader gets, written before readers dispatch.

## Files

| File | Writer | Format in |
| :-- | :-- | :-- |
| `plan.md` | lead | above |
| `candidates-<lane>.md` | collector; the lead for `candidates-user.md` | `briefs/collector.md` |
| `merged.tsv` | lead | below |
| `vet-<shard>.md` | vetter | `../../vet-sources/references/briefs/vetter.md` |
| `cards-<shard>.md` | reader | `briefs/reader.md` |
| `pasted-<id>.md` | lead | "Pasted sources in a survey" in `survey.md` |
| `origins/<theme>.md` | tracer | `briefs/tracer.md` |
| `origins-index.md`, `distillate.md`, `appendix.md` | lead | `lead.md` |
| `verify.md` | verifier | `briefs/verifier.md` |
| `verify-shared.md` | lead | `lead.md` |

## merged.tsv

One tab-separated row per canonical id: `canonical_id`, `source`. Line 1 is the opening line and line 2 the column names. `source` is the candidate `id` from the first lane in `plan.md` order.

## Id check

So that no source drops out of the run unseen, every `source` value in `merged.tsv` must end with exactly one outcome. The lead checks after stage 4 that each id has one vet row, and after stage 5 that each `keep` = `yes` id and each pasted source outside the plan's not-read list has one card. On a missing or doubled id, redispatch that shard once and check again. A redispatch counts toward the ceiling. With none left, list the source as not read. If it still fails, list the source as not read with the cause "lost in the run" and go on. The reply's Skipped section names it.

## Resume

1. Redispatch a child file without a final `## Done` line once. If it is still incomplete, name the file and list its stage as skipped. Grade only what the finished stages support, and say so in the reply. When no later stage can run without that file, say so and end the run there.
2. The user may ask to resume a stopped run and name its folder. Redispatch once each shard that is incomplete, lacks an id or doubles one. The new file replaces the faulty one. Rerun the id check.
3. Resume at the first stage whose files are missing, lack `## Done` or failed the id check.
