# git_lesson

notes:

- git repository is stored within directory .git
- git commit is a container carrying metadata (commit author, date, and message) and a pointer to the root project tree, which stores subdirectory and file checksums (blobs) within the git repository.
- git repository log is stored as a directed acyclic graph (dag)
- git branch is a lightweight pointer pointing to one commit container, and that is why branch creation and destruction is fast and cheap in git and it makes branching git's killer feature
- files in a repository can be one of the four states, untracked, modified, staged, unmodified (commited)
- regarding git commit, the author is the person who originally wrote the work, whereas the commiter is the person who last applied the work. So, if you send in a patch to a project and one of the core members applies the patch, both of you get credit--you as the author, and the core member as the committer
- git keeps a special pointer called HEAD, which points to the default branch or other branches.
- common workflow such as long-running branches (multi-level stability like master, develop, and topic), and topic branches (short-lived branch used for a single feature or hotfix)
- remote-tracking branches (remote/branch) are local references to the state of remote branches so they can only be moved by networking communication rather than local commits.
- remote-tracking branches highlight the "trunk" commits while local-tracking branches are "branch" commits
- `git rebase` local changes to clean up the work, but never `git rebase` anything that is already pushed to the remote (do not rebase commits that exist outside your local repository which people may have based their work on).
- `git revert` is a better choice to undo things than `git reset` for two reasons. First, it does not change the project history so it ensures the integrity of a repository, especially a shared one. Second, `git revert` is able to target an individual commit at an arbitrary point in the history, whereas `git reset` can only work backward from the current commit. That is, you would have to abandon all of the commits that occurred after the target commit and redo them all again after removing the target commit, and that is not elegant.

useful commands

- initialize a repository in an existing directory

```
git init
```

- stage a new or modified file

```
git add filename
```

- commit staged files

```
git commit -m "commit message"
```

- clone a (renamed) full copy of a repository from remote server

```
git clone git@github.com:username/repository (newRepositoryName)
```

- show file status (short, the output have two columns, staging area and working tree)

```
git status (-s or --short)
```

- show file difference between staging area and working tree (or last commit)

```
git diff (--staged or --cached)
```

- stage all tracked files and commit

```
git commit -a
```

- remove tracked file from both the tracking system and the directory

```
git rm filename
```

- remove tracked file from the tracking system but keep it in the directory

```
git rm --cached filename
```

- rename file

```
git mv old_filename new_filename
```

- show commit log (of the last 2 commits) and the difference introduced in each commit

```
git log -p (or --patch) (-2)
```

- show commit log and the abbreviated stats for each commit

```
git log --stat
```

- show commit log in different format (oneline, short, full, fuller)

```
git log (--pretty=oneline or short or full or fuller)
```

- show commit log in a customized way

```
git log --pretty=format:"%h - %an, %ar : %s"
```

- show commit log with a ASCII graph showing branch and merge history of the HEAD branch (or all branches)

```
git log --pretty=format:"%h %s" --graph (--all)
```

- show commit log with abbreviated SHA-1 checksum in one line

```
git log --oneline
```

- show commit log within a time frame

```
git log --since=2.weeks
```

- show commit log that changed the number of occurrences of a string (maybe a function name)

```
git log -S function_name
```

- show commit log that introduced a change to a file

```
git log -- path/to/file
```

- show commit log of commits modifying test files in the Git source code history were committed by Junio Hamano in the month of October 2008 and are not merge commits

```
git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" \
 --before="2008-11-01" --no-merges -- test/
```

- redo last commit, make additional changes, stage them, and commit again

```
git commit --amend
```

- unstage a staged file

```
git reset HEAD file_to_be_unstaged
```

- unmodify a modified file (dangerous command as it wipes out unstaged local modification)

```
git checkout -- file_to_be_unmodified
```

- unstage a staged file (post git version 2.23.0)

```
git restore --staged file_to_be_unstaged
```

- unmodify a modified file (dangerous, post git version 2.23.0)

```
git restore file_to_be_unmodified
```

- list existing tags (with filtering)

```
git tag (--list or -l "v1.8.5*")
```

- create annotated tag which contains the checksum, tagger name and email, and date

```
git tag -a v1.4 -m "my version 1.4"
```

- show tag data along with the commit that was tagged

```
git show v1.4
```

- create lightweight tag which contains only the checksum

```
git tag v1.4-lw
```

- create tag on previous commit

```
git tag -a v1.2 9fceb02
```

- push tag to remote

```
git push remote_name v1.5
```

- push all tags at once

```
git push remote_name --tags
```

- delete local tag

```
git tag -d v1.4-lw
```

- delete remote tag

```
git push remote_name --delete v1.4-lw
```

- create a new branch from existing tag

```
git checkout -b version2 v.2.0.0
```

- create a new branch without switching to it

```
git branch branch_name
```

- switch to another branch

```
git checkout branch_name
```

- create a new branch and switch to that new branch

```
git checkout -b branch_name
```

- switch to another branch (post git version 2.23)

```
git switch branch_name
```

- create a new branch and switch to that new branch (post git version 2.23)

```
git switch -c branch_name
```

- merge test branch back into master branch

```
git checkout master
git merge test
```

- delete a branch

```
git branch -d branch_name
```

- resolve merge conflict in a file and merge two branches

```
vim filename
git add filename
git commit -m "message"
```

- list out all branches

```
git branch
```

- show the last commit on each branch

```
git branch -v
```

- show branches already merged into the current branch

```
git branch --merged
```

- show branches not merged into the current branch yet

```
git branch --no-merged
```

- delete a branch by force

```
git branch -D branch_name
```

- change a branch name locally, push it to remote and delete the old one on remote

```
git branch --move old_branch_name new_branch_name
git push --set-upstream remote_name new_branch_name
git push remote_name --delete old_branch_name
```

- show remote references (or a particular remote)

```
git remote show (remote_name)
```

- show remote server name (with URL for r/w)

```
git remote (-v)
```

- fetch from remotes and show local branches (both tracking and non-tracking) and what remote-tracking branches they are tracking and if local branches are ahead, behind of both

```
git fetch --all
git branch -vv
```

- add a new remote reference and name it remote_name

```
git remote add remote_name url
```

- fetch from a remote reference to update remote-tracking branch

```
git fetch remote_name
```

- merge remote-tracking branch into current working branch

```
git merge remote_name/remote_branch_name
```

- do git fetch followed by git merge

```
git pull
```

- delete remote branches

```
git push remote_name --delete remote_branch_name
```

- create a local branch based on remote-tracking branch

```
git checkout -b local_branch_name remote_name/remote_branch_name
```

- create a local branch based on remote-tracking branch and have the same name

```
git checkout --track remote_name/remote_branch_name
```

- create a local branch based on remote-tracking branch and have the same name if (a) this new local branch does not exist and (b) there is exactly one remote has the same branch name

```
git checkout remote_branch_name
```

- set an existing branch to track a remote-tracking branch

```
git branch -u (or --set-upstream-to) remote_name/remote_branch_name
```

- take local master branch and push it to update the remote's master branch

```
git push remote_name master
```

- take local hotfix branch and push it to update the remote's master branch

```
git push remote_name hotfix:master
```

- inspect a remote named origin

```
git remote show origin
```

- rename a remote

```
git remote rename old_name new_name
```

- remove a remote

```
git remote rm (or remove) remote_name
```

- take all the changes that were committed on the experiment branch and replay them on the master branch, known as rebase

```
git checkout experiment
git rebase master
```

- take the client branch, figure out the patches since it diverged from the server branch (keep the server branch in other words), and replay these patches in the client branch as if it was based directly off the master branch instead.

```
git rebase --onto master server client
```

- rebase the server branch onto the master branch without having to check it out first

```
git rebase master server
```

- fetch and rebase on top of force-pushed rebase work

```
git fetch
git rebase remote_name/remote_branch_name
```

- fetch and rebase on top of force-pushed rebase work using git pull

```
git pull --rebase
```

- revert the target commit

```
git revert target_commit_hash
```

- move both the HEAD and branch refs to the specified commit

```
git reset --hard|mixed|soft
```
