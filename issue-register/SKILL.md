---
name: issue-register
description: >
  Revise a project's register of open problems (defects, technical debt, open questions, owner
  decisions) against the current state of the code, the tests and the servers: cut what is
  closed, keep only what remains, separate items by type of work, order them by product impact,
  word every item as a task, and report. Always use it when the owner asks whether a problems
  document is still current or already stale, what is left open in it, to clean it out and
  rewrite what remains, to merge several overlapping registers into one, or to add a found bug
  as an item: "is this document outdated or current", "what's left open here", "clean it out
  and write down what still needs doing", "bring this document up to date", "update this md
  file: what's done, what's left, what came up", "merge these two files into one", "add this
  bug to the register as an item", "what's left in the issues and what's closed". The owner
  may phrase this in another language; match on meaning.
---

# Register of open problems

In every large session the same cycle repeats and breaks the same way: the agent appends
instead of rewriting, and creates new files instead of updating the existing one. The owner's
words, three times over: "you've spawned even more files; there's bound to be a pile of files
with stale information in there"; "you've mixed everything into a heap: one file about account
rotation, one about the refresh-token gap, and the refresh-token one talks about accounts and
the digest again, so which of it is current?"; "can you merge these two files into one, so I
work from one?". This skill keeps one register, verified against the project, holding only what
is left to do.

## How far to go

The wording of the request sets the depth.

- **Assess**: "is this document stale or current?", "what's left open here?". Check every item
  and report. Do not edit the document.
- **Revise**: "clean it out and write down what still needs doing". The full pass below; the
  document is rewritten.
- **Add an item**: "put this bug in as one of the items". One entry, in the right block, in
  task form. Nothing else in the document changes.

When it is unclear whether editing is wanted, assess and ask one question.

## One register, no new files

The owner names the document, or you find the one in `docs/` that lists the project's open
problems. Never create a new file: not a "fresh version", not a "summary next to it", not a
"history". If several files cover the same ground and overlap, merging is part of the revision:
fold them into the one the owner works from, delete the others, and name in the report what was
merged and what was deleted. Git keeps the old files. Do not mix unrelated subjects in one file
either: one file, one subject.

## Verify against the project, not against the document

For every item find evidence in the current state that can be checked: the line of code, the
test, the migration, the configuration, the version running on the server, the closed issue in
the tracker. Only evidence closes an item. "I think we fixed that" and "the register says it
was fixed" are not evidence. When a fact lives on a server, read it without changing anything;
a revision never touches a running system.

An item that cannot be verified right now stays in the register with an exact note of what to
check and where. A bare "needs re-check" carries no information and hangs for weeks.

Stale items count as closed: the problem they describe no longer exists. A real case: an item
claimed a date-format defect; 376 dates in 139 files were checked and none was affected; the
item was removed.

## Cut what is closed

Closed and stale items are removed from the register. They are not marked done, not moved to a
"history" or "closed" section, not kept "just in case". The register holds only what remains to
be done; history lives in git.

One exception: when the project's own written rule keeps an archive of closed items in another
document, move one line there, with the code, the title, the evidence and the date, and nothing
more. The project's documented rule outranks this default.

Replace status stamps of any kind (emoji, "confirmed", "closed", "needs re-check") with one line
per item: "verified <date>: <evidence>" or "to verify: <what exactly, where>". There is no
"closed" line, because closed items are not in the document. If the document keeps a
"last revised" date at the top, update it.

## Separate by type of work

A typical register mixes four kinds of entries that are worked differently, and mixing them
further is not allowed:

- **ready engineering tasks**: the behaviour is defined, the work can be built;
- **records to re-confirm by code first**: the problem is claimed, not yet shown;
- **owner decisions**: the agent does not make them and does not take them into work; state
  what the choice is and what each option costs;
- **live checks and operational actions on production**.

Plus, kept apart: **legacy** that must not be removed before persisted data is checked.

Label every item with its kind. Group by kind inside a priority block, or keep the project's
own structure when it already separates them.

## Order by product impact

Order items by what they do to users, data, money and limits, and explain the order in one line
per block. If the owner named the axis ("finish off the problems caused by the hard tax-ID
binding"), that axis comes first.

## Word every item as a task

Verb first: build, fix, remove, decide, check. Then what is broken now from the user's point of
view. Then the criterion by which the item counts as closed. Keep the project's existing item
structure (for example: what happens, what it threatens, what to do) and add the done criterion
where it is missing.

## Summary table by topic

Where the document already has a summary table, update it; otherwise add one at the bottom.
Group related items under one topic so the owner does not repeat the same thing a hundred times
and can hand a whole topic over as one piece of work.

## The tracker

If the project instructions name an issue tracker, match the register items to its open issues
and say which are already tracked, with their codes, and which are not. Do not create, close or
relabel issues: statuses are the owner's.

## Do not fix anything

The revision ends with the updated document and the report. A bug found while verifying becomes
an item, not a patch.

## Before you report, check yourself

The number of files in the project did not grow. No item in the register is marked done. No
"history" or "closed" section appeared. Every remaining item has a kind, a place in the order,
a task wording and a done criterion. If any of these fails, the revision is not finished.

## The report

1. **Counts**: how many items there were, how many were closed and removed, how many remain.
2. **Removed**: each with one short piece of evidence.
3. **Remaining**: in priority order, with the kind of each.
4. **Owner decisions**: which items wait for the owner and what exactly the choice is.
5. **Could not verify**: what and why.
