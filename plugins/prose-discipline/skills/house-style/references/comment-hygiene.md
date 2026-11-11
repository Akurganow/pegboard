# Comment hygiene: depth

Extends "Code comments" in the core rules. A comment earns its place by saying what the code cannot. That is a reason, a contract callers rely on, or an outside constraint such as a rate limit.

## Why comments are not banned

Published guidance agrees on which comments are worth having. Google's C++ guide says not to state the obvious and to explain why. Ousterhout and Martin both hold that some information cannot live in code. Git's guidelines warn that comments invariably tend to stale out, so each must carry something the code cannot.

## What to delete

- **Narrator comments** ("This function handles", "Here we"). The name and signature already say it, and the comment rots when the code changes.
- **Step and trivial markers** (`// Step 1:`, `// Increment the counter`). Order and names speak. A numbered comment inside a non-obvious algorithm may stay when it states the purpose of the step.
- **Committed doubt** ("should work", "probably", "hopefully"). A reader cannot tell a real doubt from a forgotten one. Check the behavior, delete the comment and pin the behavior with a test.
- **Section dividers** (`// =====`). A region that needs a banner needs its own file, class or export.

An accurate comment that states the obvious is deleted too.
