git branch -d the_local_branch
git push origin --delete the_remote_branch
git rebase -i HEAD~4
git rebase -i origin/master
git remote show origin

Ex. How to add github as push url
git remote add -f github https://github.obps.io/OperationalPlatform/common-database.git
git push github <branch-name>
 

git commit --amend
git reset —soft HEAD^ : uncommit local

Branch rename local/server:
git branch -m <old-branch> <new-branch> or just<new-branch> if already on current branch
git push origin :<old-branch>
git push —set-upstream origin <new-branch>

git cherry-pick -x  SHA_ID
git cherry-pick —continue
git cherry-pick —quit
git cherry-pick —abort

git format-patch HEAD~1 --stdout > patchfile
git patch --stat / --check patchfile
git am --signoff patchfile

// when git gui crash
git config --local --unset gui.geometry
