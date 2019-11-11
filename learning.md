What have I learned so far?
===
They talk about Git workflows for a reason. Workflow implies a sequence of events, not just isolated incidents. The git commands required for any given situation depend on where you're at in your agreed workflow model.  

Feature branch model (as I understand it)
---
The steps in the flow are:
1. clone the central repo (if you haven't already). This gives you a master branch and an origin pointing back to the cloned repo.
1. before you start changing anything create a branch in your local repo. If you don't, you're altering your master branch, and when it comes to pushing the changes back up to the central repo (upstream) they will be pushed directly onto origin's master. This will make your teammates sad.
1. to create a new branch do `git checkout -b [branchname]`. This will create a new branch locally and swap you into it.
1. Make whatever changes you want, `git add` and `git commit` them as usual. After that `git status` will tell you you're up to date. You are, but only with your local repo. Upstream origin still doesn't know anything about your new wacky feature in your new wacky feature branch.
1. At this point you might think you should just push your stuff up to origin. That would be ok if there were no changes to origin/master whilst you've been working on your wacky stuff. If there are changes this workflow says you should pull them into your local repo before doing a push. So you do `git pull origin master` to update your local repo's commit history. Note this does not change your files, only the .git/refs commit history info.
1. Now when you `git push origin [branchname]` you're asking git to put your branch into the central repo.
1. From the central (origin) repo you can create a `pull request` which requests that your branch changes be pulled into the master branch in such a way that you're asking nicely, rather than forcing folk to accept your changes.
1. The `pull request` creates space for comments. It also checks if the changes can be merged into master without any issues. If so, it will offer `git merge` . If you confirm the merge it then offers to delete the branch as the branch has served its purpose and is now redundant.
1. To tidy up your local repo you should `git checkout master` to move back to the master branch. Then `git branch -d [branchname]` to remove the redundant branch. Then `git pull` to bring your local master up to date with the central repo again.
1. That's the end of this workflow.