---
name: git-workflow
description: Use when doing any git operations (branching, committing, pushing) so the repo history stays clean and matches the preferred workflow
---

# Git Workflow

## Overview

This skill defines the default git workflow for this environment: work directly on `master` unless explicitly asked otherwise, keep branches unprefixed, and commit only complete, verified slices with short commit messages.

**Important:** git work (staging/committing/pushing, etc) is not a signal to stop or report progress. After any commit, immediately return to the continuous loop: pick the next top-most unchecked `PLAN.md` **Now** item and keep going.

Only stop to report progress under exactly two conditions:

- All `PLAN.md` **Now** work is complete, or
- A hard blocker / high-risk gate / product decision is encountered.

## Defaults (Rules)

- Work on `master` unless the human explicitly asks for a new branch.
- Do not create branches “just in case”.
- If asked to create a branch, use a plain branch name with no tool/model prefixes.
  - Do not prefix with `codex/`, `claude/`, `agent/`, etc.
- Commit only complete slices: done, verified, and ready to ship.
- Commit messages are short plain sentences (no `feat:`, `chore:`, etc.).
  - Prefer a single sentence.
  - If needed, use 2–3 short sentences total (no paragraphs).
- Never use `git add .`. Always stage by explicit filenames to avoid accidental commits.

## Before Any Commit

Confirm the slice is complete:

- The intended outcome is achieved.
- Verification was run (tests or the project’s chosen verification step).
- Any required checklist/docs updates for the slice are included.

Then:

- Check working tree state: `git status`
- Review diff: `git diff` (and `git diff --staged` after staging)

## Branching Rules

- Only create a branch when explicitly asked.
- Keep branch names simple and descriptive, like:
  - `fix-login-timeout`
  - `billing-webhook-hardening`
  - `upgrade-rails-8`

## Commit Rules

- One commit per completed slice whenever feasible.
- Do not commit partial work, experiments, or “WIP” unless the human explicitly asks.
- If a change is essentially “more of the same” as the most recent commit (tight follow-up, fixup, small adjustment), prefer amending the most recent commit instead of making a new commit.
  - If it is unclear whether to amend vs make a new commit, ask.
- Do not add co-authoring trailers (no `Co-authored-by:`). The human is the sole author.

## Commit Message Style

Good:

- `Fix login redirect loop`
- `Add read-only admin audit view`
- `Reduce flaky checkout test timeouts`

Avoid:

- `feat: add admin audit view`
- `chore: stuff`
- Long multi-paragraph explanations

## Pushing

**Pushing to `master` triggers a deploy.** Treat `git push` as a production operation.

Hard gate:

- Do not push to `master` unless you are intentionally deploying to production.

Rules:

- Only push to `master` when all unpushed commits are complete, verified, and safe for production.
- Do not push if there are missing dependencies, unfinished work, or “it should work” assumptions.
- If the change set is not ready to deploy, keep commits local until it is ready.
- If the work is finished and verified, prefer pushing and deploying rather than accumulating completed work locally without a reason.

Gems/libraries:

- Only push to `master` when ready to release a new version.
- It is acceptable to keep collecting local commits until release-ready.

## Safety Defaults

- Never run destructive git commands (`git reset --hard`, forced checkouts, force pushes) unless explicitly requested and confirmed.
- If unrelated changes exist in the worktree, do not revert them unless asked. Keep your work focused.
