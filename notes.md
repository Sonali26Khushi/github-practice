ay-25-notes.md
# Day 25 – Git Reset vs Revert & Branching Strategies

---

# Task 1: Git Reset — Hands-On

## Step 1: Create 3 commits

```bash
echo "Commit A" > file.txt
git add .
git commit -m "Commit A"

echo "Commit B" >> file.txt
git add .
git commit -m "Commit B"

echo "Commit C" >> file.txt
git add .
git commit -m "Commit C"
git reset --soft HEAD~1
git reset --soft HEAD~1
Observation
Git moved HEAD back by one commit
Commit C disappeared from history
Changes from Commit C stayed staged
git status showed changes ready to commit
Use Case

Useful when:

You want to rewrite the previous commit
Combine commits
Edit commit messages
Re-commit Changes
git commit -m "Commit C again"
git reset --mixed HEAD~1
git reset --mixed HEAD~1
Observation
Commit removed from history
Changes remained in working directory
Changes became unstaged
git status showed modified files
Use Case

Useful when:

You want to keep code changes
Reorganize staging before committing again
Re-commit Again
git add .
git commit -m "Commit C third time"
git reset --hard HEAD~1
git reset --hard HEAD~1
Observation
Commit removed from history
Changes deleted completely
Working directory reverted
No modified files remained
Use Case

Useful when:

You want to completely discard changes
Local experimentation failed
Difference Between --soft, --mixed, and --hard
Reset Type	Commit History	Staging Area	Working Directory
--soft	Reset	Keeps staged changes	Keeps changes
--mixed	Reset	Unstages changes	Keeps changes
--hard	Reset	Clears staging	Deletes changes
Which One is Destructive?

git reset --hard is destructive because it permanently removes commits and local changes from the working directory.

When Would You Use Each One?

--soft

Modify previous commit
Squash commits

--mixed
Reorganize staged files
Keep edits but unstage them

--hard
Throw away unwanted local work
Reset broken experiments
Should You Use git reset on Pushed Commits?

Usually NO.

Because reset rewrites commit history, it can create problems for teammates working on shared branches.

If absolutely necessary:

git push --force

But force pushing should be used carefully.

Task 2: Git Revert — Hands-On
Create 3 Commits
echo "Commit X" > demo.txt
git add .
git commit -m "Commit X"

echo "Commit Y" >> demo.txt
git add .
git commit -m "Commit Y"

echo "Commit Z" >> demo.txt
git add .
git commit -m "Commit Z"
Revert Commit Y

Find commit hash:

git log --oneline

Revert:

git revert <commit-hash-of-Y>
Observation
Git created a NEW commit
Changes from Commit Y were undone
Commit Y still existed in history
History remained intact and traceable
Is Commit Y Still in History?

YES.

git revert does not remove commits.
It creates another commit that reverses the changes.

git revert vs git reset
git reset
Moves branch pointer backward
Can remove commits from history
Alters commit history
git revert
Creates a new commit
Preserves history
Safely undoes changes
Why is revert safer for shared branches?

Because it does not rewrite commit history.

Everyone keeps the same commit timeline, avoiding conflicts caused by force pushing.

When to Use revert vs reset?
Use revert
Shared branches
Public repositories
Undoing bad commits safely
Use reset
Local cleanup
Before pushing commits
Rewriting local history
Task 3: Reset vs Revert Summary
Feature	git reset	git revert
What it does	Moves HEAD backward	Creates inverse commit
Removes commit history?	Yes	No
Safe for shared branches?	No	Yes
Safe after pushing?	Usually no	Yes
Best use case	Local cleanup	Undoing public commits
Task 4: Branching Strategies
1. GitFlow
How It Works

Uses multiple long-lived branches:

main
develop
feature/*
release/*
hotfix/*
Flow Diagram
main
 └── develop
      ├── feature/login
      ├── feature/payment
      └── release/v1.0
Used In
Enterprise projects
Large teams
Scheduled releases
Pros


Pros
Organized release management
Stable production branch
Good for versioned software
Cons
Complex workflow
Too heavy for fast-moving startups
Many branches to manage
2. GitHub Flow
How It Works

Simple workflow:

main branch always deployable
Create feature branch
Open Pull Request
Merge into main
Flow Diagram
main
 ├── feature/navbar
 ├── feature/api
 └── bugfix/login
Used In
SaaS products
Web apps
Continuous deployment teams
Pros
Simple and fast
Easy collaboration
Great for CI/CD
Cons
Less structured
Harder for large release cycles
3. Trunk-Based Development
How It Works

Everyone works directly on:

main (trunk)
Very short-lived branches

Frequent merges are encouraged.

Flow Diagram
main
 ├── small-fix
 ├── tiny-feature
 └── quick-merge
Used In
Google
Facebook
High-speed engineering teams
Pros
Fast integration
Fewer merge conflicts
Excellent for CI/CD
Cons
Requires strong testing
Risky without automation
Which Strategy Would You Use?
Startup Shipping Fast

GitHub Flow or Trunk-Based Development

Because:

Fast deployment
Simpler workflow
Continuous delivery friendly
Large Team with Scheduled Releases

GitFlow

Because:

Better release management
Structured branching
Stable production handling
Open Source Project Example
Kubernetes

Uses a GitHub-style workflow with:

Pull requests
Main branch
Release branches

Task 5: Git Commands Reference Update
Setup & Config
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init
Basic Workflow
git status
git add .
git commit -m "message"
git log --oneline
git diff
Branching
git branch
git branch feature-x
git checkout feature-x
git switch main
Remote
git clone <url>
git remote -v
git push origin main
git pull origin main
git fetch
Merge & Rebase
git merge feature-x
git rebase main
Stash & Cherry Pick
git stash
git stash pop
git cherry-pick <commit-hash>
Reset & Revert
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1

git revert <commit-hash>
Extra Notes
git reflog
git reflog

Useful for recovering lost commits after reset or rebase.

Git keeps track of every HEAD movement.


# Suggested Commands to Run

```bash
git log --oneline --graph --all
git reflog
git status
Suggested File Structure
devops-git-practice/
├── git-commands.md
├── day-25-notes.md
└── practice-files/
Bonus Tip

Before experimenting with git reset --hard, always remember:

git reflog can often recover "lost" commits.