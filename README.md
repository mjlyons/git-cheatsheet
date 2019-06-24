# git cheat-sheet

Based on notes from [Advanced Git](https://github.com/nnja/advanced-git/blob/master/presentation/slides.pdf).

## Config

- `git config --global core.editor "code --wait"`: Set text editor

## git add

- `git add -p`: interactively stage commits by hunk

## git stash

- `git stash --include-untracked`: stashes tracked *and* untracked changes
- `git stash save "DESCRIPTION"`: sets stash description (instead of last commit msg)
- `git stash list`: list changes
- `git stash show stash@{#}`: show contents of a stash
- `git stash apply`: apply the latest stash without removing it
- `git stash apply stash@{#}`: apply a stash
- `git stash drop <optional stash@{#}>`: Remove a stash
- `git stash clear`: Remove *all* stashes
- `git stash branch <branchname> [optional stash@{#}]`: Start new branch from stash
- `git checkout <stash name> -- <filename>`: Grab a single file from a stash

## git tag

- `git tag <tagname>`: Create a tag and use message from last commit
- `git tag -a <tagname>`: Create an "annotated" tag with your own message, author, date.
- `git tag`: list tagnames
- `git tag --points-at <commit>`: list tagnames that point to a commit
- `git show <tagname>`: Show message & diff for tag

## git branch

- `git branch`: list local branches
- `git branch -r`: list remote branches
- `git branch <new-branchname> <commit>`: Create a branch with <commit> at HEAD (useful for dangling commits)
