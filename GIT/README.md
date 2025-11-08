1. Basic Git Questions

Q1. What is Git and why is it used in DevOps?

Git is a distributed version control system that tracks changes in code.

Use in DevOps: Enables collaboration, rollback, branch management, and CI/CD pipeline integration.

Q2. Difference between Git and GitHub?

Git: Version control system installed locally.

GitHub: Cloud-based repository hosting service.

Q3. What are branches in Git?

Branches allow multiple parallel lines of development.

Example: master/main for production, dev for development, feature/* for new features.

Q4. What is a Git commit?

A snapshot of code changes.

Command: git commit -m "message"

2. Intermediate Git Questions

Q5. Difference between git merge and git rebase?

Merge: Combines branches creating a merge commit.

Rebase: Moves or replays commits from one branch onto another; creates a cleaner history.

Scenario:

Merge: Integrate feature1 into dev.

Rebase: Keep feature1 up-to-date with dev before merging.

Q6. How do you resolve conflicts in Git?

Identify conflicts using git status

Open conflicting files → manually edit → git add <file> → git commit

Scenario: Two devs modified the same line in a file; you need to resolve before merging.

Q7. Difference between git pull and git fetch?

Fetch: Downloads updates without merging.

Pull: Fetches and merges updates into the current branch.

Scenario: Use fetch if you want to review changes before merging.

3. Advanced Git / Real-time Scenarios

Q8. How do you revert a commit that has been pushed?

Commands:

<pre>git revert <commit-id>
git push origin <branch></pre>


Scenario: A commit with a bug was already pushed to main. Use revert to create a new commit that undoes changes without altering history.

Q9. How do you handle a feature branch when it’s behind main?

Scenario: You are working on feature/login while main has new commits.

Solution:

<pre>git checkout feature/login
git fetch origin
git rebase origin/main
git push -f</pre>


Q10. How to delete a remote branch safely?

Command:

<pre>git push origin --delete feature/old</pre>


Scenario: Feature is merged; the remote branch is no longer needed.

Q11. How do you check what files changed between two commits?

Command:

<pre>git diff <commit1> <commit2></pre>


Scenario: DevOps engineer needs to check changes before deploying to staging.

Q12. Git Stash scenario

Scenario: You are working on feature/payment, but a hotfix needs to be applied on main.

Solution:

<pre>git stash
git checkout main
# apply hotfix
git checkout feature/payment
git stash pop</pre>


Q13. Undo local changes

Scenario: Accidentally modified files but want to discard changes:

<pre>git checkout -- <file>
git reset --hard</pre>


Q14. Git Tagging for releases

Scenario: You want to deploy version 1.2 to production:

<pre>git tag -a v1.2 -m "Release v1.2"
git push origin v1.2</pre>


Q15. Git Hooks

Scenario: Ensure code passes linting before every commit using pre-commit hook.

Command: Place scripts in .git/hooks/pre-commit.

4. DevOps Pipeline Git Scenarios

CI/CD Integration: Git triggers Jenkins pipeline on push to main.

Rollback Scenario: git revert is used to undo the bad deployment.

Multiple Environment Workflow:

dev branch → staging → production

Merge changes to main after testing on staging.
