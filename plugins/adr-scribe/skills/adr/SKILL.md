---
name: adr
description: Create or supersede an Architecture Decision Record in docs/adr based on the current conversation
disable-model-invocation: true
argument-hint: "[title] | supersede <number> [title]"
---

Create an Architecture Decision Record (ADR) for the decision discussed in this conversation.

Arguments: $ARGUMENTS

## Steps

1. Find the ADR directory: use `docs/adr/` if it exists, otherwise `doc/adr/` or `adr/`.
   If none exists, create `docs/adr/`.
2. Determine the next number by listing existing files named `NNNN-*.md`
   and adding 1. Start at `0001` if there are none.
3. Build the title from the arguments if given; otherwise derive a short
   imperative title from the discussion (e.g. "Use Service Bus sessions for ordered processing").
   The filename is `NNNN-kebab-case-title.md`.
4. Fill in [template.md](template.md). Rules:
   - Context: describe the forces at play (requirements, constraints, team skills, cost), not the solution.
   - Options: list every option that was seriously discussed, with honest pros and cons.
     Do not invent options that were never considered.
   - Decision: state it in one or two sentences, in active voice ("We will…").
   - Consequences: include negative consequences and follow-up work, not just benefits.
   - If something important is unclear from the conversation, ask before writing
     rather than guessing.
5. If the arguments start with `supersede <number>`:
   - Set the new ADR's status to "Accepted" and add "Supersedes ADR-<number>".
   - Edit the old ADR: change its status to "Superseded by ADR-<new number>".
6. If `docs/adr/README.md` exists with an index table, add a row for the new ADR.
7. Show the file path and a 2–3 line summary. Do not commit.