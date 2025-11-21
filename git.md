## Stash magic
git stash list
git checkout stash@{2} -- Content/BuilderPawnSystem/Blueprints/BP_BuildGameMode.uasset

## Need to be done after checkout of a repo with submodules
git submodule init
git submodule update --init
git submodule update --init --force
git submodule update --init -- Plugins/VVRCoreMechanics

## Add a submodule from VVR/Plugins
git submodule add -b VVROnlineSubsystem https://dev.azure.com/VictoriaVR/VictoriaVR/_git/VVRPlugins Plugins/VVROnlineSubsystem

## Remove a submodule
git submodule deinit Plugins/VVRKeyboard
git rm Plugins/VVRKeyboard
rm -rf .git/modules/<path-to-submodule>
git config --remove-section submodule.<path-to-submodule>.

## Rebase remote
git rebase Development
git push origin --force

## select the my/theirs version for merge
-- when rebasing my branch on Development, local/remote are backwards!
git checkout --theirs FILE # my changes on my Dev_XX branch
git checkout --ours FILE # changes on Development
git add FILE

## Restart/undo conflict resolution in a single file
git checkout --merge FILE

## Restore local changes
git checkout .
git clean # this will delete new files...

## Rebase sub-branch
git rebase --onto TARGET PARENT CHILD

## Cherry-pick
log of commits to copy from:
    333 <- last
    222
    111 <- first
    bbb <- based from

git switch TargetBranch
git cherry-pick bbb..333
git cherry-pick bbb..333 -n # to not commit the changes

## Bisect
https://stackoverflow.com/questions/5638211/how-do-you-get-git-bisect-to-ignore-merged-branches
git bisect start --first-parent  # to don't travel branch individual commits, but only the merge's parent
git bisect bad                   # Current version is bad
git bisect good v2.6.13-rc2      # v2.6.13-rc2 is known to be good
... then it checkout automatically and you say good/bad
git bisect reset                 # to end it

## To revert changes introduced by commit
https://git-scm.com/docs/git-revert
git revert <commit-B-SHA>
... to undo changes on a single file or directory from commit B, but retain them in the staged
git checkout <commit-B-SHA> <file>

## change origin/remote
git remote get-url "origin"   # to check
git remote set-url "origin" git@github.com:User/UserRepo.git
