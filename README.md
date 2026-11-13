# tuto-github 🥐

A hands-on tutorial to learn how to work as a team with Git and GitHub.

Together we will write a recipe for a French pastry. **Each participant adds one line to the recipe**, using the same workflow you would use on a real project: branch, commit, push, pull request, review, merge.

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

The recipe lives in [`recipe.md`](recipe.md). The pastry is: a surprise, revealed at the end.

Each participant adds **exactly one line**: an ingredient or a preparation step, in a sensible place in the recipe.

## Workflow, step by step

1. **Clone** the repository
   ```bash
   git clone https://github.com/NeuroimagingBrainNetworks/tuto-github.git
   cd tuto-github
   ```
2. **Create a branch** named after you
   ```bash
   git switch -c add-line-<your-name>
   ```
3. **Edit** `recipe.md`: add your line.
4. **Check** what changed
   ```bash
   git status
   git diff
   ```
5. **Stage and commit**
   ```bash
   git add recipe.md
   git commit -m "Add <ingredient or step> to the recipe"
   ```
6. **Push** your branch
   ```bash
   git push -u origin add-line-<your-name>
   ```
7. **Open a pull request** on GitHub targeting `main`, and ask a teammate to review it.
8. **Review** a teammate's pull request, then merge once approved.
9. **Update** your local `main`
   ```bash
   git switch main
   git pull
   ```

## Rules and conventions

- One line per participant, one branch per participant.
- Never commit directly to `main`.
- Branch names: `add-line-<your-name>`.
- Commit messages: short, imperative, in English (e.g. `Add 250 g of butter`).
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

Everyone who adds a line to the recipe! 👩‍🍳👨‍🍳
