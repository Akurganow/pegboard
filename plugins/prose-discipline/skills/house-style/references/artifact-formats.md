# Artifact formats: depth

Extends "Artifact formats" and the sections on progress updates, final reports, briefs and unverified claims in the core rules.

## Review comments

Conventional Comments: `<label> [decorations]: <subject>`, then an optional discussion.

The labels are `praise:`, `nitpick:`, `suggestion:`, `issue:`, `todo:`, `question:`, `thought:`, `chore:` and `note:`. The site recommends pairing `issue:` with a suggestion, and `question:` stands in for `issue:` when you are unsure the problem exists. It warns that false praise does damage.

Decorations go in parentheses: `(blocking)`, `(non-blocking)`, `(if-minor)`. The site leaves the default to each organization.

Google's guide leaves open how explicit a reviewer should be. A known fix as an instruction spares the author a round trip. When the fix is unknown, write `question:`. Label every comment, because without labels authors may read each one as mandatory.

## Commit message

Subject: imperative, at most 50 characters, no full stop (Git SubmittingPatches, Tim Pope). Body: only when the why is not obvious from the diff, wrapped near 72 characters (Tim Pope). The Linux kernel documents 75, so the column is a project choice.

## Change description

Google's guide asks for a first line that says what is being done. The body gives the problem, the reason for this approach and its shortcomings. This standard adds the verification, because a reader who must trust a change needs the evidence.

- What changed: the contract-level difference, one bullet per change.
- Why: the defect, requirement or decision behind it.
- Verification: commands and results, and what was not verified, in one to three lines.

Leave out effort, apologies, thanks and the session process (see `slop-pruning.md`). A stricter format, such as a commit message, governs. A host or repository template, such as a pull-request form, outranks these formats: fill its fields and add nothing above them.

## Error message

Microsoft's Windows guide asks for the problem, the reason and the solution, and allows leaving out a solution that is trivial to deduce. GOV.UK asks for what happened and how to fix it. A developer message may name the code or setting. An end-user message states the cause in the user's terms, because the user cannot act on an internal code.

## Agent instructions and briefs

Each step is one imperative action of at most 20 words, with the context above the steps. A reason may follow in its own sentence, because Google's procedures guide says action first, justification second. Anthropic's guide and the Agent Skills guide say a stated purpose lets an agent decide unforeseen cases.

## Progress updates

Anthropic's guide for Fable 5.2 wants updates that say what the model found and does next. A text-only client can look silent in a long turn. The guide for Opus 5 asks for one when something important turns up or the direction changes. So write one at a finding or a change of plan, and after a long stretch with none.

## Final reports and handoffs

Anthropic's guide for Fable 5 says a final message is the reader's first look at the work. It asks for the outcome first, then the one or two things needed from the reader, each explained as if new. The guide for Fable 5.2 adds that readers have not seen the tool calls or files.

## What was not verified

Anthropic's guide for Fable 5 asks the model to say explicitly what is not yet verified and to state a verified result plainly. The guide for Sonnet 5.5 asks it to name the check it did not run and not to report the change as done. A gap stated as a fact tells the reader what to check. "Probably" and "should work" in place of a check are deleted.

## Rules of this package

No published source was found for three rules. They are the severity words `major`, `minor` and `nit`, the quoted phrases in a report of cuts, and the verification line of a change description. The nearest practice is Google's review labels. Drop each if the reason in the core rules stops holding.
