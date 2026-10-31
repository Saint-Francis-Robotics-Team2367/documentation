---
title: Git Workflow
parent: Programming
nav_order: 2
---

# Git Workflow

How we make changes to team code. It applies to the robot code and to these docs. If any of these
words are new, see [Git terms in the glossary](../glossary.md#dev-tools--workflow).

## The short version

1. **Update `main`:** `git checkout main` then `git pull`.
2. **Make a branch:** `git checkout -b yourname/short-description`.
3. **Make your change** and test it (`robotpy test`, `pyright`, `black --check .`).
4. **Commit:** `git add <files>` then `git commit -m "Describe what changed"`.
5. **Push:** `git push -u origin yourname/short-description`.
6. **Open a pull request** on GitHub and ask a lead to review it.
7. **Fix review comments**, push again, and a reviewer merges when CI is green.

## Rules

- **Never commit directly to `main`.** Every change goes through a pull request.
- **One PR, one idea.** "Add intake subsystem" is one PR. Don't mix it with a drivetrain fix or a
  formatting cleanup of unrelated files.
- **CI must pass.** Every robot-code PR runs `black`, `pyright`, and `robotpy test`. Run them
  yourself before pushing so you aren't surprised.
- **Test in sim before asking for review.** Say in the PR description how you tested it.
- **Don't merge your own PR** unless a lead has approved it.

## Branch names

Use `yourname/what-it-does`, for example `andy/square-auto` or `sam/fix-deadband`. Short,
lowercase, hyphens.

## Commit messages

- Start with a verb and describe the change: "Add square auto routine", "Fix inverted steer on BR
  module".
- Not good: "stuff", "fix", "asdf", "final final v2".
- Commit often. Small commits are easier to review and easier to undo.

## Writing a pull request

The description should answer three questions:

1. **What** does this change?
2. **Why?** Link the task or issue if there is one.
3. **How did you test it?** For example: "Ran `robotpy test`. Ran the new auto in sim, and the
   robot ends within 5 cm of its start pose."

Screenshots or short clips from the sim or AdvantageScope help a lot.

## Reviewing a pull request

Everyone reviews, including new members. Reading other people's code is one of the fastest ways to
learn.

- **Ask questions.** "Why is this 0.02?" is a good review comment.
- **Look for:** magic numbers that belong in `constants.py`, wrong units, old pre-2027 API names,
  missing `add_requirements`, and anything you can't follow.
- **Be kind and specific.** Comment on the code, not the person.

## Keeping your branch up to date

If `main` has moved on while you worked:

```powershell
git checkout main
git pull
git checkout yourname/your-branch
git merge main
```

If Git reports a **merge conflict**, open the files it lists in VS Code. VS Code highlights the
conflicting sections and gives you buttons to pick a version. Ask a lead the first few times.

## Oh no

| Situation | What to do |
|-----------|-----------|
| I committed to `main` by accident | Don't push. Ask a lead, who will help you move the commit onto a branch. |
| I want to throw away uncommitted changes to a file | `git restore <file>` |
| `git push` was rejected | Someone pushed first. Run `git pull`, then push again. |
| Everything is broken | Stop and ask a lead before running commands you found online. |

## GUI option

Prefer buttons over commands? VS Code's **Source Control** panel and
[GitHub Desktop](https://desktop.github.com/) both work. The workflow is the same: branch,
commit, push, PR.
