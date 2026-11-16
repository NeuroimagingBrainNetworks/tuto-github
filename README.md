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

1. **Get the repository**
   - First time: clone it
     ```bash
     git clone https://github.com/NeuroimagingBrainNetworks/tuto-github.git
     cd tuto-github
     ```
   - Already cloned: update `main` before starting
     ```bash
     git switch main
     git pull
     ```
2. **Create a branch** with your team and your name
   ```bash
   git switch -c team-choux/<your-name>    # or team-crema/<your-name>
   ```
3. **Edit** `recipe.md`: replace your placeholder comments with your part of the recipe.
4. **Check** what changed
   ```bash
   git status
   git diff          # or visually: git difftool (see the demo below)
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
7. **Open a pull request** on GitHub (**Compare & pull request**) targeting `main`, and ask a student **from the other team** to review it. Add a short description: what was missing, and what you added.
8. **Review** a pull request from the other team, then merge once approved (the author clicks **Merge**). If `main` moved and your branch conflicts, update your branch and resolve the conflict.
9. **Update** your local `main`
   ```bash
   git switch main
   git pull
   ```
10. **Delete the finished branch** (optional but recommended)
    ```bash
    git branch -d team-choux/<your-name>              # delete locally
    git push origin --delete team-choux/<your-name>   # delete on the remote
    ```
    `-d` refuses to delete unmerged branches, which is a useful safety net.

## Demo: visual diff with `git difftool` (meld)

`git diff` prints changes in the terminal. `git difftool` opens them side by side in a graphical tool such as [Meld](https://meldmerge.org/).

1. **Install Meld**: Windows installer from meldmerge.org, macOS `brew install --cask meld`, Linux `sudo apt install meld`.
2. **Configure it once**
   ```bash
   git config --global diff.tool meld
   git config --global difftool.prompt false    # do not ask before opening each file
   # Windows only, if meld is not on your PATH:
   git config --global difftool.meld.path "C:/Program Files/Meld/Meld.exe"
   ```
3. **Try it**: edit `recipe.md` without committing, then
   ```bash
   git difftool                    # unstaged changes
   git difftool --staged           # staged changes
   git difftool main..<branch>     # a branch (or a PR) compared with main
   git difftool -d                 # directory mode: one window for all files
   ```
4. **Bonus, for the merge conflict**: the same idea works for conflicts.
   ```bash
   git config --global merge.tool meld
   git config --global mergetool.keepBackup false    # no *.orig files
   git mergetool
   ```

## Bonus: add a photo to the recipe with Claude Code

You can also let [Claude Code](https://claude.com/claude-code) do the work, as long as it follows the same rules as you.

1. **Start in plan mode.** Open Claude Code in the repository and press `Shift+Tab` until *plan mode* is shown (or type `/plan`). Claude then only reads and proposes a plan: nothing is modified until you approve it. **Read the plan before approving.**
2. **Paste this prompt** (replace the `<...>` parts):
   ````text
   Follow the rules in README.md strictly. Task: add a photo of the finished pastry (<pastry-name>) to recipe.md.
   - First `git switch main` and `git pull`, then create my own branch `team-<choux|crema>/<my-name>`. Never edit or push to `main`.
   - Download a freely licensed image of <pastry-name> (e.g. from Wikimedia Commons) into `images/pastry.jpg`, under 1 MB, and add its credit in `images/CREDITS.md`.
   - In recipe.md, show it right under the title with `![Finished pastry](images/pastry.jpg)`. Do not touch any other line. The recipe text stays in Spanish.
   - Keep the change small. Show me `git status` and `git diff` before committing.
   - Make a single commit with a short, imperative English message (e.g. `Add pastry photo`).
   - Push with `git push -u origin <branch>`, then open a pull request into `main` with a short description (what was missing, what you added). Do not merge it: someone from the other team must review it.
   Plan first, and wait for my approval before running anything.
   ````
3. **Check the result**: review the plan, approve it, then inspect the change with `git diff` (or `git difftool`) and look at the pull request on GitHub.

The prompt encodes the rules of this repository: your own branch, never `main`, a small change, one commit and one pull request, an English imperative commit message, a recipe in Spanish, and a review by the other team.

## Golden rules

- ✅ Always create a branch
- ✅ Always open a pull request
- ✅ Keep changes small
- ❌ Never work on `main`
- ❌ Never push directly to `main`

## Rules and conventions

- One branch and one pull request per participant.
- Never commit directly to `main`.
- Branch names: `team-choux/<your-name>` or `team-crema/<your-name>`. (In real projects use `type/short-description`, e.g. `fix/typo-methods`, `feature/add-classifier`, `exp/test-svm`.)
- Commit messages: short, imperative, in English (e.g. `Add praliné steps`).
- The recipe itself is written in Spanish.
- Review rules: one approval from a student of the other team; the author merges.

## Command cheat sheet

| Command | What it does |
| --- | --- |
| `git status` | Show modified and staged files |
| `git branch` | List branches |
| `git switch <branch>` | Switch to an existing branch |
| `git switch -c <branch>` | Create and switch to a new branch |
| `git add <file>` | Stage a file |
| `git commit -m "<msg>"` | Record staged changes |
| `git push -u origin <branch>` | Publish a branch |
| `git pull` | Fetch and merge remote changes |
| `git log --oneline --graph` | Visualise history |
| `git diff` | Show unstaged changes |
| `git difftool` | Show changes in a visual tool (meld) |


## Contributors

Everyone who adds a part to the recipe! 👩‍🍳👨‍🍳
