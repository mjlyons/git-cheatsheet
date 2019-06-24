# git cheat-sheet

Based on notes from [Advanced Git](https://github.com/nnja/advanced-git/blob/master/presentation/slides.pdf).

## Config

- `git config [--global] core.editor "code --wait"`: Set text editor
- `git config [--global] rerere.enabled true`: Replay previously seen conflict resolution (helpful for long rebases)

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

## git merge

- `git merge <feature-branch>`: merges <feature-branch> into the current branch
- `git merge --no-ff <feature-branch>` Disables fast forward (makes merge commit even if no merge conflicts, useful if want to group related changes)

## git log

- `git log --graph --decorate --all --oneline`: draw graph of how branches relate
- `git log --since="yesterday"`
- `git log --since="2 weeks ago"`
- `git log --name-status --follow -- <file>`: Shows log history for a file with that works across renames/moves"
- `git log -grep=<regexp>`: log history matching <regexp>
- `git log --author=<author>`: log history for <author>
- `git log --stat`: Summarize changes to each file in log message
- `git log diff-filter=<F> --stat`: Log diffs with filter (A=Add, D=Delete, M=Modified)

## git show

- `git show [commit]`: log message and diff of [commit], or HEAD if commit omitted
- `git show --stat`: adds per-file change summary for each file
- `git show <commit>:<file>`: show diff of single file in commit

## git diff

- `git diff`: show unsaved changes diff
- `git diff --staged`: show staged changes diff
- `git diff A B`: diff of diffs from A..HEAD & B..HEAD
- `git diff A..B`: show changes bringing A to B
- `git diff --merged <branch>`: show branches that have been merged into <branch> (useful for master)
- `git diff --no-merged <branch>`: show branches *not* merged into <branch>


## Commit references

- `<commit>~[n]`: n-th ancestor of commit (n=1 if omitted, n=2 is parent of parent)
- `<commit>^[n]`: n-th parent of commit (n=1 if omitted, only useful for merges

