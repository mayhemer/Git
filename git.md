## Stash magic
```bash
git stash list
git checkout stash@{2} -- Path/To/File.ext
```

## Need to be done after checkout of a repo with submodules
```bash
git submodule init
git submodule update --init
# or, to replace according cursors
git submodule update --init --force
git submodule update --init -- Path/To/Subrepo
```

## Add a submodule from Repo/Branch
```bash
git submodule add -b Branch https://dev.azure.com/Org/Proj/_git/Repo 
```

## Remove a submodule
```bash
git submodule deinit PathTo/Submodule
git rm PathTo/Submodule
rm -rf .git/modules/{path-to-submodule}
git config --remove-section submodule.{path-to-submodule}.
```

## Rebase remote
```bash
git switch MyBranchIWantToRebas
git rebase TargetBranchToRebaseOnto
git push origin --force # pushes my changes, dangerous: overrides other's changes, not for coop
```

## select the my/theirs version for merge
-- when rebasing my branch on `main`, local/remote are backwards!
```bash
git checkout --theirs FILE # my changes on my Dev_XX branch
git checkout --ours FILE # changes on Development
git add FILE
```

## Restart/undo conflict resolution in a single file
```bash
git checkout --merge FILE
```

## Restore local changes
```bash
git checkout .
git clean # this will delete new files...
```

## Rebase sub-branch
```bash
git rebase --onto TARGET PARENT CHILD
```

## Cherry-pick
```
log of commits to copy from:
    333 <- last
    222
    111 <- first
    bbb <- based from
```
```bash
git switch TargetBranch
git cherry-pick bbb..333
git cherry-pick bbb..333 -n # to not commit the changes
```

## Bisect
https://stackoverflow.com/questions/5638211/how-do-you-get-git-bisect-to-ignore-merged-branches
```bash
git bisect start --first-parent  # to don't travel branch individual commits, but only the merge's parent
git bisect bad                   # Current version is bad
git bisect good v2.6.13-rc2      # v2.6.13-rc2 is known to be good
... then it checkout automatically and you say good/bad
git bisect reset                 # to end it
```

## To revert changes introduced by commit
https://git-scm.com/docs/git-revert
```bash
git revert <commit-B-SHA>
# ... to undo changes on a single file or directory from commit B, but retain them in the staged
git checkout <commit-B-SHA> <file>
```

## change origin/remote
```bash
git remote get-url "origin"   # to check
git remote set-url "origin" git@github.com:User/UserRepo.git
```
