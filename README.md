# tuto-github 🥐

A hands-on tutorial to learn how to work as a team with Git and GitHub.

Together we will write a recipe for a French pastry whose name will be revealed at the end of the exercise. Six participants work in **two teams of three**, each holding only *part* of the recipe. Only by collaborating (review, merge, communicate) will you end up with the complete recipe, using the same workflow you would use on a real project: branch, commit, push, pull request, review, merge.

> **Status:** draft. Sections marked `TODO` will be completed before the class.

## Learning goals

By the end of the session you will know how to:

- clone a repository
- create and switch between branches
- stage and commit changes with clear messages
- push a branch to a remote
- open, review and merge a pull request
- keep your local copy up to date (`fetch` / `pull`)
- resolve a merge conflict (we will create one on purpose!)

## Prerequisites

- [Git](https://git-scm.com/downloads) installed (`git --version`)
- A GitHub account that is a member of the **NeuroimagingBrainNetworks** organisation
- A text editor
- `TODO`: authentication setup (HTTPS token or SSH key)

## The exercise

The recipe lives in [`recipe.md`](recipe.md), written **in Spanish**. It is an empty skeleton: each placeholder comment names the participant (`S1` to `S6`) who must fill it in.

Your instructions are in the file of your team. **Read only your own team's file.**

| Team | File | Part of the recipe | S-numbers |
| --- | --- | --- | --- |
| 1 · Choux | [`teams/team-1-choux.md`](teams/team-1-choux.md) | Choux pastry and final assembly | S1, S2, S3 |
| 2 · Crema | [`teams/team-2-crema.md`](teams/team-2-crema.md) | Praliné and crème mousseline | S4, S5, S6 |

Rules of the game:

- Each student works on their own branch and opens their own pull request.
- Each pull request is **reviewed by someone from the other team**.
- Both teams add their tools to the same `Materiales` list, so expect a **merge conflict** there. Resolve it together.
- The assembly steps (13-14) depend on the other team's work: talk to each other and pull the latest `main` before writing them.
- At the end, the recipe in `main` should be complete and in the right order.

## Workflow, step by step

1. **Clone** the repository
   ```bash
   git clone https://github.com/NeuroimagingBrainNetworks/tuto-github.git
   cd tuto-github
   ```
2. **Create a branch** with your team and your name
   ```bash
   git switch -c team-choux/<your-name>    # or team-crema/<your-name>
   ```
3. **Edit** `recipe.md`: replace your placeholder comments with your part of the recipe.
4. **Check** what changed
   ```bash
   git status
   git diff
   ```
5. **Stage and commit**
   ```bash
   git add recipe.md
   git commit -m "Add choux pastry ingredients"
   ```
6. **Push** your branch
   ```bash
   git push -u origin team-choux/<your-name>
   ```
7. **Open a pull request** on GitHub targeting `main`, and ask a student **from the other team** to review it.
8. **Review** a pull request from the other team, then merge once approved. If `main` moved and your branch conflicts, update your branch and resolve the conflict.
9. **Update** your local `main`
   ```bash
   git switch main
   git pull
   ```

## Rules and conventions

- One branch and one pull request per participant.
- Never commit directly to `main`.
- Branch names: `team-choux/<your-name>` or `team-crema/<your-name>`.
- Commit messages: short, imperative, in English (e.g. `Add praliné steps`).
- The recipe itself is written in Spanish.
- `TODO`: review rules (number of approvals, who merges).

## Command cheat sheet

| Command | What it does |
| --- | --- |
| `git status` | Show modified and staged files |
| `git switch -c <branch>` | Create and switch to a new branch |
| `git add <file>` | Stage a file |
| `git commit -m "<msg>"` | Record staged changes |
| `git push -u origin <branch>` | Publish a branch |
| `git pull` | Fetch and merge remote changes |
| `git log --oneline --graph` | Visualise history |
| `git diff` | Show unstaged changes |


## Contributors

Everyone who adds a part to the recipe! 👩‍🍳👨‍🍳
