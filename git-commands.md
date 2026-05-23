#git commands#

git config --global user.name "Sonali26Khushi"
git config --global user.email "khushipramanik3026@gmail.com"
git config --list
git status
git remote -v
git add .
git commit -m "message"
git push origin main

git branch
git branch feature-1
git switch feature-1
git checkout -b feature-2
git switch feature-1

Fast Forward Merge
if main has no changes and other branch feature3 merge to main
What is a fast-forward merge?
A fast-forward merge occurs when the branch being merged has no new commits since it diverged from the main branch, allowing Git to simply move the reference pointer forward

git checkout main
git merge feature-3
git push

Merge commit 
if both the branches has changes 
When does Git create a merge commit instead?
Git creates a merge commit when both branches have new commits and a conflict needs to be resolved in the merge process.

git checkout main
git merge feature-2
git add .
git commit -m ""
git push origin main

merge conflict
What is a merge conflict?
A merge conflict arises when changes in two branches conflict with each other, such as when edits are made to the same line in a file.

Rebase branch
What does rebase actually do to your commits?
Rebase takes the commits from your current branch and replays them on top of the target branch, effectively rewriting their commit history.

How is the history different from a merge?
A rebase creates a linear history, while a merge can result in a more complex graph due to non-linear merging of branches.

Why should you never rebase commits that have been pushed?
Rebasing alters commit history, which can confuse collaborators who have already based their work on those commits

When would you use rebase vs merge?
Rebase is useful for keeping a clean history in a feature branch before merging into the main branch. Merge is ideal for combining integration branches where history should be preserved.