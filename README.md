# Git Commands & Deep Dive

**A comprehensive guide to Git—from fundamentals to advanced concepts, with a focus on Git's internal architecture.**

---

## Overview

This repository is different from typical Git resources. While most guides focus on surface-level commands, this repo takes you **deeper into Git's architecture**—covering the 3-tier structure (Working Tree, Staging/Index, Repository), object types (blobs, trees, commits), hash-based tracking, and the internal mechanics that power version control.

Whether you're a beginner learning `git add` and `git commit`, or an advanced user mastering rebasing, conflict resolution, stashing, and history rewriting, this guide provides:

- **Clear command references** with explanations and real-world examples
- **Visual diagrams** (SVGs) illustrating Git workflows, branching, merging, rebasing, and conflicts
- **Hands-on exercises** with real-world scenarios (see `Git_Exercises.md`)
- **Deep insights** into how Git tracks changes using SHA-1 hashes, tree/blob objects, and refs

---

## What's Inside

- **`Git_Commands.md`**: Comprehensive command reference covering configuration, basic workflows, logs, branching, merging, rebasing, conflict resolution, stashing, remotes, and more—with inline diagrams.
- **`Git_Exercises.md`**: Practical exercises grouped by difficulty (Beginner, Intermediate, Advanced) with hints, verification steps, and real-world scenarios.
- **`images/`**: Simple SVG illustrations for each major section to help visualize concepts.

---

## Why This Repo is Different

Most Git tutorials teach *what* to do. This repo teaches *what*, *why*, and *how Git works under the hood*:

- Understand Git's **3-tier architecture**: how changes flow from working tree → staging index → repository.
- Learn how Git uses **SHA-1 hashing** to track every change and ensure integrity.
- Explore Git's **object model**: blobs (file content), trees (directory structure), commits (snapshots + metadata).
- Master advanced workflows like **interactive rebasing**, **cherry-picking**, **bisecting**, and **history rewriting**.
- Safely resolve **merge conflicts** and understand when to use merge vs. rebase.

---

## Getting Started

1. Clone or download this repository.
2. Start with `Git_Commands.md` for a structured walkthrough of commands.
3. Try the exercises in `Git_Exercises.md` to practice what you've learned.
4. Refer back to the command reference and diagrams whenever you need a quick lookup.

---

## References

This repository draws inspiration and knowledge from excellent Git resources:

- **[Pro Git Book](https://git-scm.com/book/en/v2)** — The definitive guide to Git, covering everything from basics to internals. Free and comprehensive.
- **[Mark Lodato's Visual Git Guide](https://marklodato.github.io/visual-git-guide/index-en.html)** — Clear visual diagrams explaining Git concepts and commands.

---

## Contributing

Feel free to fork the repo, suggest improvements, or submit pull requests. Contributions are welcome!

---

## Authors

- [@Mohamed24Awwad](https://github.com/Mohamed24Awwad)
[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)
[![AGPL License](https://img.shields.io/badge/license-AGPL-blue.svg)](http://www.gnu.org/licenses/agpl-3.0)



## Deployment

To download this project run

```bash
 git clone https://github.com/Mohamed24Awwad/Git_stuff_summary.git
```

Using SSH

```bash
 git@github.com:Mohamed24Awwad/Git_stuff_summary.git
```

Gitub CLI

```bash
gh repo clone Mohamed24Awwad/Git_stuff_summary
```
