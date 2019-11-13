What have I learned so far?
===
They talk about Git workflows for a reason. Workflow implies a sequence of events, not just isolated incidents. The git commands required for any given situation depend on where you're at in your agreed workflow model.  

Feature branch model (as I understand it)
---
The steps in the flow are:
1. Clone the central repo (if you haven't already). This gives you a master branch and an origin pointing back to the cloned repo. Use `git clone <url>`
1. Before you start changing anything create a branch in your local repo. If you don't, you're altering your master branch, and when it comes to pushing the changes back up to the central repo (upstream) they will be pushed directly onto origin's master. This will make your teammates sad.
1. To create a new branch do `git checkout -b <branchname>`. This will create a new branch locally and swap you into it. You can check the branches you've created locally using `git branch`. There will be one branch in the list that's starred - this is your current branch.
1. In your nice new feature branch, make whatever changes you want, `git add` and `git commit` them as usual. After that `git status` will tell you you're up to date. You are, but only with your local repo. Upstream origin (the repo you cloned from Github) still doesn't know anything about your changes or your new feature branch.
1. At this point, if you were using a centralised workflow, you would a) be working on the master branch in your local repo and b) pull your teammates changes into your repo before pushing your changes into the central repo using `git pull --rebase origin master`. We're using feature branches to manage changes, though, so you *can* just push your stuff up to origin -  on it's own branch - using  `git push origin <branchname>`.
1. From the central (origin) repo you can now create a `pull request` which requests that your branch changes be pulled into the master branch in such a way that you're asking nicely, rather than forcing folk to accept your changes.
1. The `pull request` functionality creates space for comments. It also checks if the changes can be merged into master without any issues. If so, it will offer `git merge` . If you confirm the merge it then offers to delete the branch (in the central repo) as the branch has served its purpose (to separate proposed changes from master) and is now redundant.
1. To tidy up your local repo you should `git checkout master` to move back to the master branch. Then `git branch -d [branchname]` to remove the redundant branch. Then `git pull` to bring your local master up to date with the central repo again.
1. If you forget to tidy up (or wonder if you did or not) you can use `git remote show origin` to get info about where origin is pointing to. It will also tell you about redundant branches locally, and suggest you use `git prune remote` to remove them. You can use `git prune --dry-run remote` to check what the prune will do before you run it for real.
1. That's the end of this workflow.