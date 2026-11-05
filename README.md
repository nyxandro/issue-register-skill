<div align="center">

# Issue Register

**A Claude Code skill that keeps your project's list of open problems true to the code, in one file, with only what's left to do.**

[![Release](https://img.shields.io/github/v/release/nyxandro/issue-register-skill)](https://github.com/nyxandro/issue-register-skill/releases)
[![License](https://img.shields.io/github/license/nyxandro/issue-register-skill)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-SKILL.md-6f42c1)](https://agentskills.io/specification)
[![Claude Code plugin](https://img.shields.io/badge/Claude%20Code-plugin-d97757)](#install)

**English** · [Русский](README.ru.md)

</div>

Issue Register is a skill for Claude Code, Codex, OpenCode, Cursor and other agents that read Agent
Skills. It revises a project's register of open problems (bugs, technical debt, open questions and
owner decisions) against the current code, tests and servers. It cuts what is closed, keeps what
remains, sorts items by type of work, orders them by impact on the product and words each one as
a task.

## Why

Every project worked on by an agent ends up with a document of open problems, and every long
session breaks it the same way.

- The agent appends instead of rewriting.
- It marks items "done" instead of removing them.
- It creates new files next to the old ones until nobody knows which one is current.

This skill keeps one register, checked against the project, that holds only what is left to do.

## Install

| Agent | Command |
|---|---|
| Claude Code, as a plugin | `/plugin install issue-register --marketplace nyxandro/skills` |
| Claude Code, Codex, OpenCode, Cursor and others | `npx skills add nyxandro/issue-register-skill` |
| Any agent, by hand | Download the [latest `.skill` archive](https://github.com/nyxandro/issue-register-skill/releases/latest/download/issue-register.skill) and unpack it into the agent's skills folder |

Pick one. If you install it two ways, Claude Code loads the skill twice.

<details>
<summary>More install options</summary>

<br>

- The one-line plugin install needs Claude Code 2.1.275 or later. On an older version, add the
  catalog first with `/plugin marketplace add nyxandro/skills` and then run
  `/plugin install issue-register@nyxandro`.
- The catalog pins no version, so every commit here reaches plugin users as an update. Run
  `claude plugin marketplace update nyxandro` and `claude plugin update issue-register@nyxandro`,
  or turn on auto-update under `/plugin` → Marketplaces.
- With `npx skills`, add `-g` to install the skill for every project. To install a given version,
  add its tag, as in `nyxandro/issue-register-skill@v1.0.0`.
- You can also clone this repository and link the `issue-register/` folder into your agent's
  skills folder. The skill is a single `SKILL.md`, with no scripts and no build step.

</details>

## Usage

The wording of your request sets how deep the agent goes.

| You ask | The agent |
|---|---|
| *Is this document stale or current? What's left open here?* | Checks every item and reports, without editing |
| *Clean it out and write down what still needs doing.* | Revises the whole register |
| *Add this bug to the register as an item.* | Adds one entry in the right place, nothing else |
| *Merge these two files into one.* | Folds overlapping files into the one you work from |

When it isn't clear whether you want edits, the agent assesses and asks one question.

## How it works

1. It works in the existing register and never creates a new file. When several files overlap, it
   merges them into the one you use, deletes the rest and says so in the report. Git keeps the
   history.
2. It checks every item against the project, not the document. A line of code, a test, a
   migration, a config, the version running on a server (read-only) or a closed issue. Only
   evidence closes an item. An item it can't check now stays, with a note on exactly what to check
   and where.
3. It removes closed and stale items. No "done" marks, no "history" section, nothing kept just in
   case. Status stamps become "verified on a date, with evidence" or "to verify, what and where".
4. It sorts items by type of work. Ready engineering tasks, records to confirm in code first, owner
   decisions it never takes on, live checks on production, and legacy that must not go before
   stored data is checked.
5. It orders items by impact on users, data, money and limits, with a one-line reason per block,
   words each item as a task with a done criterion, and keeps a summary table by topic.
6. It matches items to your issue tracker when the project names one, but never creates or closes
   issues.
7. It fixes nothing. A bug found while checking becomes an item, not a patch.

## Example

Two items from a made-up register, before and after. The removed one is a real case.

```text
Before
  D-12  Dates in the wrong format   ✅ fixed?
  D-14  Refresh token gap           (needs re-check)

After
  Removed D-12. Verified 2026-11-06, 376 dates in 139 files checked, none affected.

  Fix the logout every 24 hours (D-14, ready engineering task)
    Users get logged out mid-session when the refresh token expires.
    Done when a session older than 24 hours survives a token refresh.
    To verify whether api/auth.ts still calls the old refresh endpoint.
```

The report then gives counts before and after, what was removed with one piece of evidence each,
what remains in priority order, which items wait for your decision and what could not be checked.

## Versions

The current version sits in `metadata.version` of `issue-register/SKILL.md`, so any installed copy
tells you which one it is. Every version has a git tag and a
[release](https://github.com/nyxandro/issue-register-skill/releases) with its own archive.
[CHANGELOG.md](CHANGELOG.md) lists what changed.

<details>
<summary>Repository layout</summary>

<br>

```text
issue-register/SKILL.md     the skill
dist/issue-register.skill   the skill folder as a downloadable archive
CHANGELOG.md                what changed in each version
README.md, README.ru.md     this page in English and in Russian
```

</details>

## License

[MIT](LICENSE)
