# Git Exercises

This file contains hands-on exercises grouped by difficulty (Beginner, Intermediate, Advanced). Each exercise includes a real-world scenario, goal, suggested commands or steps to try, hints, and verification criteria.

How to use
- Work in a disposable test repository (create a new folder and run `git init`).
- Make a commit for each step so you can practice history commands.
- Try to solve the exercise before looking at hints.
- Verification shows one or more ways to check you completed the task.

---

## Beginner

1) Initialize repo and make first commit
- Scenario: Start a new project. Create README.md, add initial content, and make a first commit.
- Goal: Repo initialized and first commit created with an appropriate message.
- Suggested commands:
  - `git init`
  - `echo "# Project" > README.md`
  - `git add README.md`
  - `git commit -m "chore: initial commit"
- Verification: `git log --oneline` shows one commit with your message.

2) Stage specific file and unstage it
- Scenario: You staged the wrong file by accident and need to unstage it.
- Goal: Stage a file then unstage it while keeping it in the working directory.
- Suggested commands:
  - `git add file.txt`
  - `git reset -- file.txt`  or `git restore --staged file.txt`
- Verification: `git status --short` shows the file as untracked/modified but not staged.

3) Make and inspect a small change
- Scenario: Modify a file and view what will be committed.
- Goal: View the exact changes and commit them.
- Suggested commands:
  - Edit file
  - `git diff` (to view working vs index)
  - `git add .`
  - `git commit -m "fix: update content"`
- Verification: `git show --name-only HEAD` and `git log -p -1`.

4) Create and switch branches
- Scenario: Start a feature on a new branch.
- Goal: Create `feature/login` and switch to it.
- Suggested commands:
  - `git checkout -b feature/login`
- Verification: `git branch --show-current` returns `feature/login`.

5) View file content at previous commit
- Scenario: You accidentally removed some content and want to see how a file looked two commits ago.
- Goal: Display file content from a previous commit without changing the working tree.
- Suggested commands:
  - `git log --oneline -- path/to/file`
  - `git show <commit_hash>:path/to/file`
- Verification: Output shows prior file content.

---

## Intermediate

6) Amend last commit safely
- Scenario: You forgot to include a small change or mistyped the commit message in the most recent commit.
- Goal: Add the missing change and update the commit message.
- Suggested commands:
  - Make changes
  - `git add file`
  - `git commit --amend -m "feat: correct message and include fix"`
- Hint: Do not amend commits that have already been pushed to a shared remote.
- Verification: `git log -1 --pretty=%B` shows the amended commit message. The commit hash changed.

7) Create a remote branch and set upstream
- Scenario: You've created a local branch and now want to push it and set the remote tracking branch.
- Goal: Push branch and configure upstream to `origin/feature/login`.
- Suggested commands:
  - `git push -u origin feature/login`
- Verification: `git branch -vv` shows the upstream branch.

8) Resolve a simple merge conflict
- Scenario: Two branches changed the same line and a merge conflict occurs.
- Goal: Merge feature into main and resolve conflict.
- Suggested commands:
  - `git checkout main`
  - `git merge feature/login`
  - Edit conflicting file, remove conflict markers, `git add` and `git commit`
- Hint: Use `git status` to see conflict state; `git merge --abort` to cancel.
- Verification: `git log --merges` or `git show` shows the merge commit.

9) Use stash to save work and switch context
- Scenario: You started a change but need to quickly switch branches.
- Goal: Save changes with a message, switch branch, then re-apply.
- Suggested commands:
  - `git stash push -m "WIP: partial feature"`
  - `git checkout main`
  - `git stash pop`
- Hint: `git stash list` and `git stash show -p stash@{0}` are useful.
- Verification: Changes reappear in working tree; stash entry removed after pop.

10) Inspect the commit history with graphs and filters
- Scenario: You want a concise visual of branches and commits by author.
- Goal: Use `git log` to print a compact graph for quick inspection.
- Suggested commands:
  - `git log --graph --oneline --all --decorate --author="yourname"`
- Verification: Output shows colorized decorations and commit graph.

11) Undo a commit but keep changes (soft reset)
- Scenario: You committed too early and want the changes back into the index or working tree.
- Goal: Move HEAD back one commit while keeping changes staged or in working tree.
- Suggested commands:
  - `git reset --soft HEAD~1` (keeps changes staged)
  - or `git reset --mixed HEAD~1` (keeps changes unstaged)
- Safety: Prefer `--soft`/`--mixed` for local-only history changes.
- Verification: `git log` shows older HEAD; `git status` shows files staged/unstaged.

---

## Advanced / Real-world scenarios

12) Rebase interactive to squash and clean commits
- Scenario: You've made many small commits in a feature branch and want to squash them into a few tidy commits before merging.
- Goal: Use interactive rebase to reorder and squash commits.
- Suggested commands:
  - `git checkout feature/login`
  - `git rebase -i origin/main` (or `HEAD~N`)
  - Mark commits `s` to squash and edit messages.
- Hint: If conflicts occur, resolve them and `git rebase --continue`.
- Verification: `git log --oneline` shows squashed commits.

13) Recover lost commits using reflog
- Scenario: You accidentally reset or deleted a branch and lost a commit.
- Goal: Find commit via reflog and restore it (create a branch at that hash).
- Suggested commands:
  - `git reflog`
  - `git checkout -b recovered <reflog-hash>`
- Verification: `git log` shows the recovered commit and history.

14) Revert a pushed commit safely (public history)
- Scenario: A faulty change was pushed to `main` and you need to undo it without rewriting history.
- Goal: Create a new commit that undoes the change.
- Suggested commands:
  - `git revert <bad_commit_hash>`
  - Provide a commit message and push
- Verification: History shows a new revert commit; code behaves as expected.

15) Cherry-pick a commit between branches
- Scenario: A bugfix was committed on `hotfix` and you need it applied to `main` without merging the entire branch.
- Goal: Cherry-pick the specific commit onto `main`.
- Suggested commands:
  - `git checkout main`
  - `git cherry-pick <commit_hash>`
- Hint: Resolve conflicts if needed and commit.
- Verification: `git log --oneline` on `main` includes the cherry-picked commit.

16) Tagging and release workflow
- Scenario: You're preparing a release and want to create an annotated tag and push it.
- Goal: Create an annotated tag and push to origin.
- Suggested commands:
  - `git tag -a v1.2.0 -m "Release v1.2.0"`
  - `git push origin v1.2.0`
- Verification: `git tag -n` shows the tag with message; the remote lists the tag.

17) Bisect to find a regression
- Scenario: A test started failing somewhere in history; use git bisect to find the bad commit.
- Goal: Narrow to the commit that introduced the regression.
- Suggested commands:
  - `git bisect start`
  - `git bisect bad` (current)
  - `git bisect good <known-good-hash>`
  - Follow the bisection instructions, run tests, then `git bisect reset`
- Verification: Git prints the first bad commit at the end of bisection.

18) Rewriting author info for last few commits
- Scenario: You used the wrong author email for several recent commits and want to correct them locally.
- Goal: Use interactive rebase and `git commit --amend --author` to fix the author info for those commits.
- Suggested commands:
  - `git rebase -i HEAD~N`
  - For each commit: `git commit --amend --author="Correct Name <correct@example.com>" --no-edit`
  - `git rebase --continue`
- Safety: If commits are already pushed, coordinate with your team or prefer `git revert` approach.
- Verification: `git log --pretty=fuller` shows corrected author/committer fields.

19) Handle large files and .gitignore
- Scenario: A large binary was accidentally committed; you want to remove it from the repo history and avoid future commits.
- Goal: Remove the file from history (use BFG or git filter-repo) and add to `.gitignore`.
- Suggested commands (high-level):
  - Add filename to `.gitignore`
  - Use BFG or `git filter-repo` to remove the file from history
  - Force-push to remote (coordinate first): `git push --force --all` and `git push --force --tags`
- Warning: Rewriting history requires coordination and is destructive for collaborators.
- Verification: `git rev-list --objects --all | grep <filename>` returns no results after removal.

20) Setup SSH remote and authenticate (practice)
- Scenario: Instead of HTTPS, set up SSH keys and add the remote SSH URL for GitHub/GitLab.
- Goal: Generate a key, add it to GitHub, and push to the SSH remote.
- Suggested commands:
  - `ssh-keygen -t ed25519 -C "your.email@example.com"`
  - Add the public key to your GitHub/GitLab account
  - `git remote add origin git@github.com:username/repo.git`
  - `git push -u origin main`
- Verification: Push succeeds without prompting for username/password.

---

## Hints & tips
- Use `git status -s` for a compact status view.
- Use `git log --oneline --graph --all` to quickly understand history layout.
- Prefer `git stash push -m "msg"` over the older `git stash save`.
- Use `git help <command>` whenever unsure of flags.

---

## Suggested solutions (brief)
- Many commands above already include the primary solution; for advanced history rewriting tasks consider reading the `git-rebase`, `git-filter-repo` (or BFG), and `git-reflog` docs before you proceed.

---

If you want, I can now:
- Add a separate `Git_Exercises_answers.md` with step-by-step solutions.
- Convert these into interactive scripts that set up repositories and run checks.
- Add small unit-tests (shell scripts) to auto-verify some exercises.


