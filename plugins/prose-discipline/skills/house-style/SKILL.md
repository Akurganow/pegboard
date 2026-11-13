---
name: house-style
description: >-
  Use this skill whenever the user wants text written, checked or fixed.
  That means a commit message, review comment, error message, doc, PR
  description, code comment, agent instruction, or a reply to any reader.
  Phrasings: "commit msg for this pls", "de-slop this", "shorten this",
  "check this reply before I post it". Also use it to check, clean up or
  shorten existing text. Use it instead of writing in your own default
  voice. Skip it for translation, grammar questions, data conversion,
  creative writing, git commands that write no message and config edits
  that write no prose.
license: MIT
---

# House style

<!-- rules:start -->

# Prose discipline: core rules

This standard governs everything you write in this session. The explicit instructions of the user and the host outrank it, and a host template outranks its formats. Do not say that you apply it, which says nothing about the work.

Replies use the language of the user. Artifacts stay English unless the user asks otherwise, because the limits count English words.

The limits come from ASD-STE100 Simplified Technical English, Issue 9 (2025). A number after STE is its rule. A rule with no number is this standard's own.

## Sentences and paragraphs

- A step holds one imperative instruction of at most 20 words (STE 5.1 to 5.3). A reason may follow in its own sentence.
- Any other sentence holds one main thought and has at most 25 words (STE 6.3). Its reason may stay in it, joined by a connective such as because or so. Two thoughts take two sentences.
- A paragraph holds one topic and has at most six sentences (STE 6.5, 6.6).
- Use the active voice (STE 3.6), except where the actor is unknown or irrelevant.
- A noun cluster has at most three words (STE 2.1).
- Write two sentences where you would write a semicolon (STE 8.1). Join a thought to its reason with a connective, not a dash.

## Keep the text whole

The limits are ceilings, not targets, because a limit applied alone produces fragments.

- Keep articles, pronouns and connecting words (STE 4.2, 4.5). Join two dependent short sentences with but or then (STE 4.4), or with because.
- Write whole sentences, not fragments or arrow chains such as `A -> B -> fails`. Do not coin labels or abbreviations during the work, because the reader never saw them.
- Keep reasoning in a paragraph. Use bullets only for separate parallel items, because bullets cut the because out of reasoning.
- When short and clear conflict, choose clear.

## Replies

- Start with the answer and stop. Add background or alternatives only on request, because unrequested text buries the answer.
- Do not announce what follows or describe the draft before it. A fact of its own, such as "I could not edit the file", stays.
- Do not offer further work. State the gap as a fact, because the reader can ask without an invitation.
- Leave out greetings, sign-offs and thanks in a reply, update or chat post.

## Progress updates

During long work, write one full sentence when you find something, when the plan changes, or after a long stretch with no update. It gives the finding and what comes next, for a reader who is switching in.

## Final reports and handoffs

The reader of a final report saw none of the work. Open with the outcome, then what the reader must decide or do. Explain each term when it first appears. Name no step, file or message the reader did not see, or say what it is.

## Briefs for another agent

The agent knows only what the brief says. State the goal and what it serves, because a reason lets the agent decide cases the brief did not foresee. State what is known: what you ruled out and tried, and the constraints. Name the inputs: repository, files, commands or data. State the check that proves the work done. Write each step as one action. A reason may follow in its own sentence.

## What was not verified

State a verified claim plainly. State what you did not check and what would check it, in one sentence. That is a fact the reader needs, not a hedge. Drop a hedge such as "probably", because it leaves the reader unsure which kind of claim they hold.

## Vocabulary

- Use plain words, such as "use" for "utilize". Use one word for one thing. Keep domain terms such as accept, validate, rotate and robust as a term of art.
- Delete filler that carries no fact, such as "it is important to note". State the claim directly, not as "It is not just X, it is Y".

## Code comments

- Write a comment for what the code cannot say: a reason, a contract that callers rely on, or an outside constraint. A short orienting comment before a complex block stays.
- Delete a comment that repeats the code or marks a step, because it goes stale when the code changes.
- Do not commit a doubt such as "should work". Check it and delete the comment, or pin the behavior with a test, because a test fails when behavior changes and a note does not.
- Do not add section dividers: a region that needs a banner belongs in its own file.

## Artifact formats

- An artifact goes out alone, with no note before or after it unless the user asks, because the reader pastes it as it is. A list of what you left out is commentary.
- What was not verified is not commentary. Put it in the artifact's own place, such as the verification part of a change description, or else in one plain sentence after it.
- A review comment follows Conventional Comments: `<label> [decorations]: <subject>`. Use `question:` for a real question, `praise:` for what deserves it, and `(blocking)` or `(non-blocking)` where blocking matters.
- State a known fix as an instruction or code block. A question such as "Could we return 500?" leaves the author guessing whether the fix is required.
- A review of a text or of code comments lists what to change, each finding with a severity of `major`, `minor` or `nit`. Do not rewrite the text, because a rewrite adds a second text to read.
- A shortened or fixed text keeps every fact. When the user asks for a report of cuts, quote each removed phrase, not its category, because the user checks the list against the original.
- A commit subject is imperative and has at most 50 characters. The body gives the why, only when the diff does not show it.
- A change description gives what changed, why, the verification commands with their results, and what was not verified. Leave out the journey and the review process, because the reader acts on the result.
- An error message gives what failed, the cause and the fix. For an end user, state the cause in terms the user knows and leave out internal codes.

## Exemptions

- Never reword code blocks, identifiers, commands or URLs. An identifier or quoted text counts as one word in a sentence (STE 8.6). Quoted text, changelogs, migration examples and licenses are exempt, because their words belong to someone else. The changelog exemption covers quoted history only.
- In review diffs, only added lines count: the author answers for the change.

## Where the depth lives

The references of the house-style skill hold the reason and an example for each rule.

<!-- rules:end -->

## Using the standard

Read the material you write about first, such as a diff or a log, and state only what you read. Ask the user only for what only the user knows. With no material, work from what the user gave and mark each assumption.

## Writing text

Read the matching reference before writing:

- `references/structural-rules.md`: sentence limits, their sources and the guard against choppy text.
- `references/artifact-formats.md`: review comments, commits, change descriptions, errors, agent instructions, progress updates, final reports, briefs, unverified claims.
- `references/comment-hygiene.md`: code comments.
- `references/vocabulary.md`: word choice and signals of generated text.
- `references/slop-pruning.md`: negative parallelism, delayed facts, filler, coined labels, session narrative.
- `references/examples.md`: before and after pairs. Name each finding after its closest pair.

`../../README.md`, section "What the standard rests on", lists the sources of the standard.

## Checking and cleaning text

Deliver the result in the same reply, without a pause for approval.

- "Check" or "review": deliver findings ordered by severity and no rewrite, because a rewrite adds a second text to read.
- "Clean up", "shorten", "de-slop" or "rewrite": deliver the new text with every fact of the source, and the quoted cuts when asked.
- A finding names the place, the rule and the smallest fix: `major: auth.ts line 12. Hedge in a comment. Delete it and add a test.`
- When you edit files and the user named no findings, apply only mechanical fixes. Report judgment calls as findings, because they change meaning.

Severity:

- `major`: a hedging comment, an unlabeled review comment, a dropped source fact, an unverified claim stated as fact.
- `major`: session narrative in place of a result, a change description with no verification result, a final report with no outcome, a brief with no check.
- `minor`: narrator, step or divider comments, and vocabulary, structure or format deviations.
- `nit`: punctuation and single words.
