## Stash magic
git stash list
git checkout stash@{2} -- Content/BuilderPawnSystem/Blueprints/BP_BuildGameMode.uasset

## Need to be done after checkout of a repo with submodules
git submodule init
git submodule update --init
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
