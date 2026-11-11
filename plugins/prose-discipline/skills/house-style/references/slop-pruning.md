# Slop pruning: depth

Extends "Replies" and "Vocabulary" in the core rules. Delete a pattern and keep the fact it stood in front of. A pattern is a signal (see `vocabulary.md`), so check that a fact is left.

- **Negative parallelism** ("This isn't just X, it's about Y"). Wikipedia's field guide and OpenAI's GPT-6 guide both name it.
- **Setups that delay the fact** ("The catch?", "Here's the thing"). No published list was found, so these are examples of the shape. The rule they break has a source: lead with what matters most (Microsoft style guide).
- **Filler openers and closers** ("It's worth noting that", "In summary", "I hope this helps", "Would you like me to..."). The sentence after an opener is the content, and a closing summary restates what the reader just read.
- **Significance tails and vague attribution** ("highlighting its role", "Experts argue"). Replace the tail with the consequence or number, and name the source or delete the claim.
- **Coined labels** ("the sweep", "mode B"). Anthropic's Fable 5.2 guide says not to use a term made up during the work. Say what the thing is.
- **Session-process narrative** ("An independent agent reviewed the change and returned PASS") in text that outlives the session. Anthropic's Fable 5 guide lists references to thinking the user never saw among the causes of hard-to-follow text. Delete the machinery and keep the result.
