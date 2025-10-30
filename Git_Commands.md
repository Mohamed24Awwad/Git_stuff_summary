# Git Commands
- Inspired by [Marklodato Blog](https://marklodato.github.io/visual-git-guide)

---
## Git Architecture " 3 tier Architecture 
1- Working Tree " Local Repo"
2- Statging Tree " Indexed Repo"
3- Repo Tree " The final one "


## Quick checks

```bash
git --version
git help
```

Git Methodology to track the changes
```bash
echo "Hello, Dude" | git hash-object --stdin 
#Result --> 02fc3c47b2f548b06b485fc7541212975c790c2c
#The same way of work with SHA1 at linux
echo -e "blob 12\0Hello, Dude" | shasum
#Result --> 02fc3c47b2f548b06b485fc7541212975c790c2c  -
#Furthermore git keeps track of every change that occurred over any of the tracked file-change by the changing of the object hash

git cat-file -t <output object from SHA1>
# Will print the type of that object is it blob or image or any of git file types  #blob
# While the git preceve the type & Size & Content you can check those by changing the -t  --> -s "size" --> -p "file content"

```

To open or edit Git configuration (global):

```bash
git config --global --edit
# or show the global config:
git config --global --list
# or view the file directly (on Windows use %USERPROFILE%/.gitconfig):
cat ~/.gitconfig
git config --system   => The changed file is located at /etc/gitconfig
# To set a system user for all of your git repos on your device
git --version 
# To check your Git Version
git config --global user.name "mohamed"
# To set a global user for your device
git config --global user.email "mohamedawwad578@gmail.com"
# To set a global email for the configured user
git config --list
# To list all configuration
git config --global core.editor "vim"
# To set a default editor for Git
git config --global color.ui true
# To colorize git command outputs
git help
git help log
# also for listing help

git config --global init.defaultBranch main
#To set your default branch as main " git by default set the master branch as a default one"
```

---

## Getting started

- Initialize a repository:

```bash
git init
```

- Show the .git directory (hidden):

```bash
ls -la .git
```

- Show the files located at the staging area " indexed files at the staging tree"
```bash
git ls-files

git ls-files -s 
# To view the files type "Creation Mode" as well the SHA 1 for these files & the staging mode 
#Results exmple --> 100644 8ef4e62b348af6b6de8e9b6fc70e983992a996ef 0       file.txt

```
- Show the files located at the repo area " indexed files at the repo tree" "This is a workaround not a direct way to view the files
```bash
find .git/objects/ -type f
# To find all the files located at the repo tree
```
- Stage changes:

```bash
git add .        
# add all changes (including new files)
git add file.txt  
# stage a specific file
git add * 
# To add all the files
git add *.text
# To add all the files end with .text

```

- Commit changes:

```bash
git commit -m "first commit"
# Commit the change to the staged tree
git commit -am " commit message"
# Add and commit the change at the same command
git commit --amend -m "new message"
# To amend the most recent commit message or its content:

```
Notes:
- Git arrange the commits in a sample linked list "linear one backed to the parent till reaching the main commit tree _root commit_ which lead to a _null parent_" which named as _branch_ to easily reach the commit and all of its related tree and objects to facilitate tracking changes
---


## Basic Git workflow

1. Make change
2. Add changes (git add)
3. Commit changes (git commit)

---

## Logs and hisTory

```bash
git log                       
# Show the commit log including the "commit message & hash object)
git log -n 3                  
# show last 3 commits (use a number after -n)
git log --since=2021-05-30
git log --until=2021-05-30
git log --oneline
git log --oneline -3
git log --since="3 weeks ago" --until="3 days ago"
git log --author="mohamed"
git log -p                    
# show diffs introduced by each commit
git log --stat --summary      
# show stats about changed files per commit
git log --graph --oneline --all --decorate
git cat-file -p <the hash printed by the previous command to reah the tree hash>
#To get the hash object content 
git cat-file -p <To view the tree object hash content>
#To get whats related to each batch version of objects "Commit contains the tree with all of its objects"
```

To search commit messages for a pattern:

```bash
git log --grep="init"
```

To see changes for a specific file between commits:

```bash
git log -p <commit1>..<commit2> -- path/To/file
# or To see how a file looked at a specific commit 
git show <commit_hash>:path/To/file
```

---

## Inspecting objects

```bash
git show                    
# shows HEAD (or specify a commit)
git show --pretty=oneline --abbrev-commit  
# compact output
git show <commit_hash>
# Show a specific comment " Working smilar to git log"
```

---

## Status, diff, and basic file ops

```bash
git status
git status -s 
# A Shortcut to view the status details
git diff                    
# changes in working direcTory vs index "Staging"
git diff --staged           
# changes staged for commit (alias: --cached)
git diff --color-words
git rm <file>
# Removing files or directories is considered a change; stage and commit as usual.
rm -rf .git/
# To remove your local git repo (dangerous; irreversible on uncommitted files)
git rm --cached <filename>
# To untrack a file but keep it in the working directory (becomes untracked)
git mv <oldname> <newname>
```

Notes:
- `git commit -am "message"` only stages and commits modified and deleted tracked files; it does not add untracked/new files.
- To resTore a file from the index (unstage changes To working copy):

```bash
git checkout -- <file>
```

# To change the last commit message


---

## Reverting and resToring

```bash
git revert <commit_hash>
# revert a commit by creating a new commit that undoes the changes
git restore <filename>
# Restre the last edits you done over a file.
git restore --staged <filename>
# To unstage the last edits at the staged tree "unstage changes over the index tree"
git checkout <commit_hash> -- <file>
# Restore a file To its state in a given commit (keeps HEAD unchanged)

```

---

## Cleaning untracked files

```bash
git clean -n   
# show what would be removed
git clean -f   
# remove untracked files
```

Be careful: `git clean -f` is permanent (for untracked files). Use `-n` To preview.

---

## .gitignore basics

Use `.gitignore` To ignore files and direcTories using glob patterns (not full regex):

```gitignore
# ignore all .js files
*.js

# negate a pattern (un-ignore); e.g. un-ignore a specific file you previously ignored:
!important.js

# comments start with #
# keep an empty direcTory tracked by adding a placeholder file like .gitkeep
```

---

## Tree and ls-tree

`git ls-tree` lists the contents of a tree (files and subtrees) — not commits. Examples:

```bash
git ls-tree HEAD                
# list files and direcTories at HEAD
git ls-tree -r HEAD            
# recursively list tree entries
git ls-tree <tree-ish> <path>  
# list entries for the path at the given tree-ish
```
## HEAD Workplay

```bash
cat .git/HEAD
cd refs/heads && cat master "or the branch name you're on"
#To check the HEAD pointer on what commit hash-object
git reset HEAD~1
# To step back one commit backward _rollback_ as well for two revisions back HEAD~2 AND that will be applied at the staging tree
git reset --hard HEAD~1
# Back with one commit backward and apply the changed to the working tree as well " Be aware of that"
git reflog
# TO view the HEAD sha reference in case you need to get one of them to fast-forward or rolling back
git reset --hard HEAD@{1}
#To move to the HEAD to the first commit head reference "change the HEAD pointer allocation"
```

Note: a "tree" corresponds To a direcTory; a "blob" corresponds To a file.

---


## Tags _Annotated Tags_

```bash
git tag -a V1.0 -m " Version 1.0 "
#Gives a tag to the last commit to facilitate all the operation might done on it from reverting backl to it etc..
git show V1.0
# Show all the info related to that tag 

```

## Branches

```bash
git branch <branch_name>      
# create a new branch (locally)
git branch                    
# list local branches and show current
cat .git/HEAD                 
# shows the currently checked-out reference
git checkout <branch_name>
# switch To branch " Move the HEAD to the requested branch"
git switch <branch_name>
# switch To branch similar to checkout 
git checkout -b <branch_name> 
# create and switch To a new branch
git branch -m <old> <new>     
# rename a branch
git branch -d <branch_name>   
# delete a branch (use -D To force)
git diff master..<branch_name> 
# show differences between master and branch
```

---

## Merging

```bash
git merge <branch_name>       
# merge branch inTo current branch
git merge --abort             
# abort a conflicted merge (during merge process)
git branch --merged          
# list branches already merged inTo HEAD
git branch -d <branch name>
#To delete a branch
```

## Rebase

```bash
git checkout feature/login
git rebase main
# Rebase the current branch onto another (moves commits to base on top of target)
git rebase -i HEAD~5
# Interactive rebase (reorder, squash, edit messages)

# Common flow during rebase when conflicts occur:
# 1) resolve conflict in files
# 2) git add <files>
# 3) git rebase --continue
# Other helpers:
git rebase --abort   
# cancel the rebase and return to the original branch state
git rebase --skip    
# skip the patch that caused the conflict
git rebase --onto newbase oldbase feature/login
# Rebase onto a different base (advanced)
git pull --rebase origin main
# Pull with rebase instead of merge (keeps linear history)
```

Why rebase vs merge (short):
- Rebase rewrites commits by replaying them on top of another base. It produces a linear history without merge commits.
- Merge creates a merge commit that preserves the exact branching/merge topology and original commit hashes.

When to use which:
- Use rebase for local, private branches to clean history before merging or pushing. It makes history easier to read.
- Use merge when combining public branches or when you want to preserve the historical context (merge commits are explicit markers).

Risks & safety:
- Rebase rewrites history (commit hashes change). Never rebase commits that have been pushed and shared with others unless everyone agrees and you force-push safely.
- Always create a backup branch before large rebases: `git branch backup/feature-login` so you can recover via reflog if needed.

## Conflicts & safe resolution

Conflicts happen when two commits modify the same part of a file differently. Git will pause the merge/rebase and mark the conflicted files.

Typical conflict workflow:
1. Run `git status` to see conflicted files and state (merge or rebase).
2. Open each conflicted file. You'll see conflict markers:

<<<<<<< HEAD
your changes
=======
their changes
>>>>>>> branch-name-or-commit

3. Edit the file to resolve the conflict: choose one side, combine, or rewrite the section.
4. Test the code locally to ensure the resolution builds/runs/tests pass.
5. Mark as resolved and continue:
	- For merge: `git add <file>` then `git commit` (or Git may auto-create the merge commit after all files are staged).
	- For rebase: `git add <file>` then `git rebase --continue`.

Useful commands and tips:
- `git status` — shows which files are conflicted and what to do next.
- `git diff` / `git diff --staged` — inspect differences before staging.
- `git checkout --ours <file>` / `git checkout --theirs <file>` — take one side quickly (older Git). Alternatively use `git restore --source=HEAD -- <file>` or `git restore --source=ORIG_HEAD -- <file>` in newer Git.
- `git mergetool` — launch a merge tool (configure one via `git config --global merge.tool <tool>`).
- `git stash` your local changes before attempting risky merges or rebases to avoid losing work.
- `git rerere` (reuse recorded resolution) can help when resolving the same conflict repeatedly: `git config --global rerere.enabled true`.

Safety checklist before rewriting history or resolving many conflicts:
- Ensure you have a backup branch: `git branch backup/<name>`.
- If commits were pushed, prefer `git revert` to undo public commits rather than rewriting them.
- After a rebase that rewrites pushed commits, you will need to force-push: `git push --force-with-lease` (prefer this over `--force` to avoid clobbering others' work).
- If you get lost, `git rebase --abort` (during rebase) or `git merge --abort` (during merge) will return to the previous state. Use `git reflog` to find lost commits.

Example: resolving a simple merge conflict
1. `git checkout main`
2. `git merge feature/login` → conflict
3. `git status` → shows conflicted files
4. Edit `src/app.js`, remove conflict markers and implement the correct code
5. `git add src/app.js`
6. `git commit` → completes the merge with a merge commit

Example: resolving a conflict during rebase
1. `git checkout feature/login`
2. `git rebase main` → conflict occurs
3. `git status` → see conflicted files
4. Edit files, `git add` them
5. `git rebase --continue`

---
---


## Stashing

```bash
git stash push -m "message"
# save work on stack (recommended form)
git stash list
git stash show stash@{0}       
# summary
git stash show -p stash@{0}    
# show patch details
git stash pop                  
# apply and remove from stash
git stash apply                
# apply but keep in stash
git stash drop stash@{0}       
# remove stash entry
```

---

## Remotes

```bash
git remote -v                      
# list remotes and URLs
git remote add <name> <url>        
# add a remote
cat .git/config                    
# view remote entries and other config
git push -u <remote> <branch>      
# push branch and set upstream
git push -f <remote> <branch>      
# force push (use carefully)
git branch -r                       
# list remote branches
git checkout -b <local> origin/<remote-branch>
# To create a local branch that tracks a remote branch:
```

---

## Aliases (shortcuts)

```bash
git config --global alias.st "status"
# example: git st  -> runs git status
```

---

## Saving credentials

Recommended ways To avoid entering credentials every time:

- Use a credential helper (Windows Credential Manager, macOS keychain, or cache):

```bash
git config --global credential.helper manager-core   # Windows (Git for Windows)
```

- Use a GitHub personal access Token (PAT) as your password for HTTPS pushes. Do not paste Tokens publicly. Better: use a credential helper or SSH keys.

---
