# Issue Register Skill

[![Download Skill](https://img.shields.io/badge/Download-issue--register.skill-blue?style=for-the-badge)](https://github.com/nyxandro/issue-register-skill/raw/main/dist/issue-register.skill)

A skill for Claude Code and OpenCode: revise a project's register of open problems (defects,
technical debt, open questions, owner decisions) against the current state of the code, the
tests and the servers. Cut what is closed, keep only what remains, separate items by type of
work, order them by product impact, word every item as a task, report.

Every project with an agent ends up with a document of open problems, and every long session
breaks it the same way: the agent appends instead of rewriting, marks items "done" instead of
removing them, and creates new files next to the old ones until nobody knows which is current.
This skill keeps one register, verified against the project, holding only what is left to do.

## What the agent does

1. Reads the depth from the request: assess only, revise fully, or add one item. When editing
   is not clearly wanted, it assesses and asks one question.
2. Works in the existing register. It never creates a new file. When several files overlap, it
   merges them into the one the owner works from and deletes the rest, and says so in the
   report. Git keeps history.
3. Verifies every item against the project, not the document: a line of code, a test, a
   migration, a configuration, the version running on a server (read-only), a closed issue.
   Only evidence closes an item. An item that cannot be verified now stays, with an exact note
   of what to check and where.
4. Removes closed and stale items. No "done" marks, no "history" or "closed" section, nothing
   kept "just in case". If the project's own written rule keeps an archive elsewhere, one line
   moves there. Status stamps are replaced by "verified <date>: <evidence>" or "to verify:
   <what, where>".
5. Separates items by type of work: ready engineering tasks, records to re-confirm by code,
   owner decisions the agent never takes on, live checks on production, and legacy that must not
   go before persisted data is checked.
6. Orders by product impact with a one-line reason per block, words every item as a task with a
   done criterion, and keeps or adds a summary table by topic.
7. Matches items against the project's issue tracker when one is named, saying what is tracked
   and what is not. It never creates or closes issues.
8. Fixes nothing. A bug found while verifying becomes an item, not a patch.

## The report

Counts before and after; what was removed, each with one piece of evidence; what remains, in
priority order with its kind; which items wait for the owner's decision and what the choice is;
what could not be verified and why.

## Install

Download `dist/issue-register.skill` (the badge above) and unpack it into the skills folder of
your agent, or clone this repository and link the `issue-register/` folder there. The skill is
a single `SKILL.md`; no scripts, no build step.

## Repository layout

```text
issue-register/SKILL.md     the skill
dist/issue-register.skill   downloadable archive of the skill folder
```

## License

MIT.
