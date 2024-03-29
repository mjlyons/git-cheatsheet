# git cheat-sheet

Based on notes from [Advanced Git](https://github.com/nnja/advanced-git/blob/master/presentation/slides.pdf).

## Config

- `git config [--global] core.editor "code --wait"`: Set text editor
- `git config [--global] rerere.enabled true`: Replay previously seen conflict resolution (helpful for long rebases)
- `git config [--global] branch.<branch>.rebase true`: always rebase branch instead of merging
- `git config [--global] help.autoCorrect <#>`: auto-correct typos after #/10 seconds
- `git config [--global] alias.<aliasname> "git <args>"`: Alias a git command
    * `git config --global alias.lg "log --graph --pretty=format:'%C(auto)%h -%d %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'"`: pretty log (run `git lg`)

## Commit references

- `<commit>~[n]`: n-th ancestor of commit (n=1 if omitted, n=2 is parent of parent)
- `<commit>^[n]`: n-th parent of commit (n=1 if omitted, only useful for merges

## Git commands

### git add

- `git add -p`: interactively stage commits by hunk

### git stash

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

### git tag

- `git tag <tagname>`: Create a tag and use message from last commit
- `git tag -a <tagname>`: Create an "annotated" tag with your own message, author, date.
- `git tag`: list tagnames
- `git tag --points-at <commit>`: list tagnames that point to a commit
- `git show <tagname>`: Show message & diff for tag
- `git push <tagname>`: push <tagname> to remote

### git branch

- `git branch`: list local branches
- `git branch -r`: list remote branches
- `git branch <new-branchname> <commit>`: Create a branch with <commit> at HEAD (useful for dangling commits)
- `git branch -vv`: list branches with upstream and commit msg

### git merge

- `git merge <feature-branch>`: merges <feature-branch> into the current branch
- `git merge --no-ff <feature-branch>` Disables fast forward (makes merge commit even if no merge conflicts, useful if want to group related changes)

### git log

- `git log --graph --decorate --all --oneline`: draw graph of how branches relate
- `git log --since="yesterday"`
- `git log --since="2 weeks ago"`
- `git log --name-status --follow -- <file>`: Shows log history for a file with that works across renames/moves"
- `git log -grep=<regexp>`: log history matching <regexp>
- `git log --author=<author>`: log history for <author>
- `git log --stat`: Summarize changes to each file in log message
- `git log diff-filter=<F> --stat`: Log diffs with filter (A=Add, D=Delete, M=Modified)
- `git log -n #`: Show the last # of commits

### git show

- `git show [commit]`: log message and diff of [commit], or HEAD if commit omitted
- `git show --stat`: adds per-file change summary for each file
- `git show <commit>:<file>`: show diff of single file in commit

### git diff

- `git diff`: show unsaved changes diff
- `git diff --staged`: show staged changes diff
- `git diff A B`: diff from A to B
- `git diff A..B`: diff from A&B's common ancestor to B
- `git diff --merged <branch>`: show branches that have been merged into <branch> (useful for master)
- `git diff --no-merged <branch>`: show branches *not* merged into <branch>

### git checkout

- `git checkout -- <filename>`: overwrites file changes in working area with staging area version
- `git checkout <commit> -- <filename>`: copies file at commit to staging area & working area
- `git checkout -tb <branch>`: Create <branch> off HEAD and use HEAD as upstream
- `git checkout -t origin/<branch>`: Checkout branch from origin and track origin's version

### git push

- `git push -u origin <branch>`: push HEAD to <branch> on origin

### git cherry

- `git cherry -v`: Show which commits haven't been pushed yet (are local only)

### git fetch

- `git fetch`: get changes without applying any

### git pull

- `git pull`: git fetch && git merge
- `git pull --rebase`: git fetch && git rebase

### git clean

- `git clean -i`: remove untracked file changes, interactively
- `git clean -i -d`: also remove untracked folder changes
- `git clean --dry-run`: see what would be removed without removing
- `git clean --dry-run -f`: remove changes after checking with dry-run

### git reset

- `git reset --soft <commit>`: moves HEAD to <commit> and stages changes to go back
- `git reset [--mixed] <commit>`: moves HEAD to <commit> and moves changes to go back to working area
- `git reset --hard <commit`: moves HEAD to <commit> and changes to go back disappear (use ORIG_HEAD to get it back)
- `git reset [commit] -- <file>`: stages change to revert file to state at [commit] or HEAD if not supplied
- `ORIG_HEAD` pointer to change after doing a reset (handy if need to revert a bad reset)
- `git reset --merge ORIG_HEAD`: Reset a merge commit (--merge) preserves uncommitted changes
- `git reflog && git reset --hard HEAD@{#}`: jump back to previous state

### git revert

- `git revert <commit>`: creates a commit reverting <commit>

### git rebase

- `git rebase <branch>`: Rebase current branch on top of <commit>
- `git rebase -i <branch>`: interactive rebase
	* `pick`: keep this commit
	* `reword`: keep commit but reword message
	* `edit`: keep but modify commit
	* `squash`: combine commit with previous, edit message
	* `fixup`: combine commit with previous and keep previous message
	* `exec`: run command with previous commit
	* `drop`: remove this commit
- `git commit --fixup <SHA> && git rebase -i --autosquash <SHA>^`: makes new commit a "fixup!" of <SHA> and squashes fixup into <SHA>
- `git rebase -i --exec "<cmd>" <commit>`: Runs <cmd> after each commit (useful for unit testing)
- `git rebase --abort`: Back out a rebase
- `git branch my_branch_backup` -> `git reset --hard my_branch_backup`: Create a copy of branch before rebasing, restore it later

### git remote

- `git remote -v`: Show remotes
```
origin git@github.com:username/repo.git (fetch)
origin git@github.com:username/repo.git (push)
```
- `git remote add upstream https://github.com/ORIG_OWNER/REPO.git`: Add upstream (from fork)
- `git remote rename origin upstream`: Rename origin remote to upstream
- `git pull --rebase <remote> <branch>`: Pull in changes from <remote>'s <branch>

### git clone

- `git clone git@github.com:username/repo.git`

### git grep

- `git grep -e <regexp>`: Searches tracked files including working area
- `git grep --cached -e <regexp>`: Only searches staged and commited changes
- `git grep -e <regexp> -- <file or path>`: limits regex to file/path
- `git grep --line-number --heading --break -e <regexp>`: Better formatting

### git cherrypick

- `git checkout <branch> && git cherry-pick <SHA>`: Creates commit on <branch> with <SHA>

### git blame

- `git blame <filename>`: show who last touched a file line by line
- `git blame -w -M -C <filename>`: better format
	* `-w`: ignore whitespace
	* `-M`: follow moved/copied lines *within* file
	* `-C`: follow moved/copied lines *outside* file
- `git log -diff-filter=D -- <deleted_file>`: See what commit(s) deleted a file
    * `git blame <commit>^ -- <deleted_file>`: Blame on file before it was deleted
- `git blame -L#,# -- <file>`: Limit blame for lines #-# 
- `git blame -L'/<regexp>/' <file>`: Limit blame to lines matching regexp

### git bisect

- `git bisect start <BAD_SHA> <GOOD_SHA>`: Find which commit broke something
    * If good: `git bisect good`
    * If bad: `git bisect bad`
- `git bisect run <test-cmd> <arguments>`: Automate bisect by providing <test-cmd> to determine pass/fail (pass=retval0)
	* `git bisect run "grep -c <BAD_TEXT> <FILENAME>" <BAD_SHA> <GOOD_SHA>`: finds which commit added <BAD_TEXT> to <FILENAME>

### git init

- `git init --template=<.git-tempalte path>`: initializes .git with .git settings from <.git-template path> (hooks, set up .gitignore)

## Git Hooks

- executable located in .git/hooks
- common: .git/hooks/pre-commit, .git/hooks/post-merge, .git/hooks/post-checkout
- git hook examples:
    * https://github.com/pre-commit/pre-commit
    * https://github.com/typicode/husky (javascript focused)

## Misc

- premade .gitignores: https://github.com/github/gitignore
- `git lint`: https://github.com/sk-/git-lint

## Github

### Source code browsing

- `t`: activate file finder
- `l`: jump to line
- `w`: switch branch/tag
- `y`: expand URL to canonical form (useful for permalink)
- `i`: show/hide all inline notes

### hub command line

Setup:

- Install: `brew install hub`
- Add to .bash_profile: `alias git=hub`

Usage:

- Open a pull request: `git pull-request -h <branch>`
- Open browser with issues: `git browse -- issues`

### .github/ templates

- `ISSUE_TEMPLATE.md`: default contents when creating an issue
- `PULL_REQUEST.md`: default contents when sending a PR
- `CONTRIBUTING.md`: link to this doc in sidebare when creating a PR
