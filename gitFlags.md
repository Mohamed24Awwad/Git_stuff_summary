# Git Status Flags Reference

A quick reference guide for understanding Git status flags and indicators.

---

## Status Flags

### 📝 **A** — Added
A new file that has been staged (added to the index) and is ready to be committed.

```bash
# Example
git add newfile.txt
git status
# A  newfile.txt
```

### ✏️ **M** — Modified
An existing file that has been changed. Can appear in two contexts:
- **Staged (green M)**: Changes are in the index, ready to commit
- **Unstaged (red M)**: Changes exist in working directory but not staged

```bash
# Example
git status
# M  staged-file.txt      (staged modification)
#  M unstaged-file.txt    (unstaged modification)
```

### 🗑️ **D** — Deleted
A file that has been deleted. Can appear as:
- **Staged deletion**: File removed and deletion staged
- **Unstaged deletion**: File removed but deletion not staged

```bash
# Example
git rm oldfile.txt
git status
# D  oldfile.txt
```

### ❓ **U** / **??** — Untracked
A file that is new or has been changed but has **not been added** to the repository yet. Git is not tracking this file.

```bash
# Example
git status
# ?? untracked-file.txt
```

### ⚠️ **C** / **UU** — Conflict
There is a merge conflict in the file. Both sides modified the same lines, and Git needs manual resolution.

```bash
# Example (during merge)
git status
# UU conflicted-file.txt
```

### 🔄 **R** — Renamed
The file has been renamed (Git detected a delete + add as a rename when similarity is high).

```bash
# Example
git mv oldname.txt newname.txt
git status
# R  oldname.txt -> newname.txt
```

### 📦 **S** — Submodule
Indicates a Git submodule (a repository nested inside another repository).

```bash
# Example
git status
# Changes not staged for commit:
#   modified:   path/to/submodule (new commits)
```

---

## Two-Letter Status Codes

When using `git status --short` (or `git status -s`), Git shows two-letter codes:

| Code | Meaning |
|------|---------|
| `??` | Untracked file |
| `A ` | Staged new file |
| `M ` | Staged modification |
| ` M` | Unstaged modification |
| `MM` | Modified, staged, and then modified again |
| `D ` | Staged deletion |
| ` D` | Unstaged deletion (file deleted from working tree) |
| `R ` | Renamed |
| `C ` | Copied |
| `UU` | Both modified (merge conflict) |

**First column** = status in the index (staging area)  
**Second column** = status in the working tree

---

## Examples

### Clean working tree
```bash
$ git status -s
# (no output - everything is committed and clean)
```

### Mixed states
```bash
$ git status -s
M  README.md          # Staged modification
 M src/app.js         # Unstaged modification
A  newfile.txt        # Staged new file
?? temp.log           # Untracked file
D  oldfile.txt        # Staged deletion
```

### During a merge conflict
```bash
$ git status -s
UU conflicted.txt     # Both modified (conflict)
```

---

## Quick Tips

- Use `git status` for detailed output with hints
- Use `git status -s` or `git status --short` for compact output
- Green = staged (in index), Red = unstaged (in working tree)
- `git add` stages changes, `git restore --staged` unstages them
- During conflicts, resolve manually, then `git add` and continue

---

## Related Commands

```bash
git status                    # Show detailed status
git status -s                 # Short/compact status
git status --short            # Same as -s
git diff                      # Show unstaged changes
git diff --staged             # Show staged changes
git add <file>                # Stage changes
git restore --staged <file>   # Unstage changes
git restore <file>            # Discard unstaged changes
```

---

**See also**: [Git Status Documentation](https://git-scm.com/docs/git-status)
