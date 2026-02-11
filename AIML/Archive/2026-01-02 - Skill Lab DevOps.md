DevOps is a set of flows and automated processes that makes deploying software easier.
- no downtime
- continuously running

version control -> build -> unit test -> deploy to test -> ato test -> deploy to prod -> measure validate

DevOps engineer:
- communicate with teams
- manage servers/infra/cloud resources
- automate tasks etc
- manage data, databases, cloud storage
- monitor and catch issues, bugs etc logging analytics etc

Devops pipeline
1. Plan - Jira, Confluence. follow agile methodology
2. Code - git. Version control for collab, review etc
3. Build - docker, jenkins. Source code to executable artifacts. 
4. Test - pytest, selenium. unit tests and integration tests.
5. Release - github actions, jfrog, artifactory. release timing and documentatio
6. Deploy - kubernetes, aws ecs. 
7. Operate - terraform, ansible. 
8. Monitoring - prometheus, grafana. log and track system metrics

# Git
## Git merge
merge 2 branches together
- conflicts. resolving conflicts -> keep original, keep new, keep both in some manner
## Git rebase
In simple terms, **Git rebase** is the process of moving or "replaying" a sequence of commits onto a new base commit.1

While `git merge` combines two branches by creating a new "merge commit," `git rebase` rewrites history to make it look like you started your work from a different point in time.
### How Rebase Works (Step-by-Step)
Imagine you have a `feature` branch that was created from `main`. 2While you were working, other developers added new commits to `main`. 3Your history now looks like a "fork."
When you run `git rebase main` while on your feature branch, Git performs the following steps:
1. **Find the common ancestor:** It identifies where your branch first diverged from `main`.4
2. **Save your work:** It temporarily "lifts" the commits you made on your feature branch and saves them as temporary patches.
3. **Reset the branch:** It moves your feature branch pointer to the very latest commit on `main`.5 (fast forward)
4. **Replay the commits:** It applies your saved patches one by one on top of the new base.
> **Important:** Because the parent of your commits has changed, Git creates **brand-new commits** (with new SHA hashes) during this process.
### Rebase vs. Merge
The goal of both commands is the same (integrating changes), but the resulting history is very different.

|**Feature**|**Git Merge**|**Git Rebase**|
|---|---|---|
|**History**|Non-linear (shows exactly when branches joined).|**Linear** (looks like a straight line).|
|**Commit Logs**|Includes a "Merge commit."|No extra merge commits; very clean.|
|**Traceability**|Preserves the original context of the branch.|Rewrites history (original commits are replaced).|
|**Risk**|Safe; doesn't change existing history.|Can be dangerous if used on shared branches.6|

### The "Golden Rule" of Rebasing
**Never rebase a branch that has been pushed to a public repository.7**
Because rebase rewrites history, if you rebase a shared branch, you are effectively deleting commits that other people are working on and replacing them with new ones. This causes major synchronization issues for your teammates. Only rebase **local** branches to clean up your own work before sharing it.
### Useful Commands
- **Standard Rebase:** `git rebase <branch-name>` — Moves your current branch onto the tip of the target branch.
- **Interactive Rebase:** `git rebase -i HEAD~3` — Opens an editor to "squash" (combine), edit, or delete the last 3 commits.8
- **Continue/Abort:** If you hit a conflict during rebase, use `git rebase --continue` after fixing it, or `git rebase --abort` to undo the whole operation.

