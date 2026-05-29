# Git VCS Masterclass: Basics → Professional

---
<img src="./git-cover.png" alt="git cover"/>
---

## 1. What Git Actually Is

**Git** is a **distributed version control system**.

It helps you:

* Track changes in code
* Save project history
* Work with teams
* Create branches for features
* Merge work safely
* Roll back mistakes
* Review code before production
* Connect with CI/CD pipelines

Important distinction:

| Tool                            | Meaning                                          |
| ------------------------------- | ------------------------------------------------ |
| **Git**                         | Version control system installed on your machine |
| **GitHub / GitLab / Bitbucket** | Cloud platforms for hosting Git repositories     |
| **Repository**                  | A project tracked by Git                         |
| **Commit**                      | A saved snapshot of changes                      |
| **Branch**                      | A separate line of development                   |
| **Merge**                       | Combine branches                                 |
| **Rebase**                      | Rewrite branch history on top of another branch  |
| **Remote**                      | A copy of your repo hosted somewhere else        |

---

# 2. The Core Git Mental Model

Git has **three main areas**:

```txt
Working Directory → Staging Area → Local Repository → Remote Repository
```

## Working Directory

This is your actual project folder where you edit files.

Example:

```txt
/frontend
/backend
README.md
```

## Staging Area

This is where you prepare files before committing.

```bash
git add .
```

## Local Repository

This is your local Git history.

```bash
git commit -m "Add login page"
```

## Remote Repository

This is GitHub/GitLab/Bitbucket.

```bash
git push origin main
```

---

# 3. Git Setup

Install Git, then configure your identity:

```bash
git config --global user.name "Mudasir Chandio"
git config --global user.email "your-email@example.com"
```

Check config:

```bash
git config --list
```

Set default branch name:

```bash
git config --global init.defaultBranch main
```

Set VS Code as editor:

```bash
git config --global core.editor "code --wait"
```

---

# 4. Creating a Repository

## Create a new Git repo

```bash
mkdir my-project
cd my-project
git init
```

Check status:

```bash
git status
```

Add files:

```bash
git add .
```

Commit:

```bash
git commit -m "Initial commit"
```

---

# 5. Cloning an Existing Repository

```bash
git clone https://github.com/user/project.git
```

Enter project:

```bash
cd project
```

Check remote:

```bash
git remote -v
```

---

# 6. The Daily Git Workflow

This is the workflow you will use 80% of the time:

```bash
git status
git pull origin main
git checkout -b feature/auth-system
# make changes
git add .
git commit -m "Add authentication system"
git push origin feature/auth-system
```

Then open a **Pull Request** on GitHub/GitLab.

---

# 7. Essential Git Commands

## Check current state

```bash
git status
```

Shows:

* Modified files
* Staged files
* Untracked files
* Current branch

---

## View history

```bash
git log
```

Better version:

```bash
git log --oneline --graph --decorate --all
```

Example output:

```txt
* 9f3a21c Add dashboard
* 42ab90d Fix auth bug
* 1a2b3c4 Initial commit
```

---

## Add files

Add one file:

```bash
git add app.js
```

Add all files:

```bash
git add .
```

Add interactively:

```bash
git add -p
```

Professional developers use `git add -p` to stage only clean, meaningful changes.

---

## Commit changes

```bash
git commit -m "Add user login API"
```

Better commit format:

```bash
git commit -m "feat(auth): add user login API"
```

Professional commit types:

| Type       | Use                |
| ---------- | ------------------ |
| `feat`     | New feature        |
| `fix`      | Bug fix            |
| `docs`     | Documentation      |
| `style`    | Formatting only    |
| `refactor` | Code restructuring |
| `test`     | Tests              |
| `chore`    | Maintenance        |
| `ci`       | CI/CD config       |

Examples:

```bash
git commit -m "feat(crm): add lead pipeline stage"
git commit -m "fix(auth): handle expired JWT token"
git commit -m "docs(api): update setup instructions"
git commit -m "ci(github): add backend test workflow"
```

---

# 8. Branches

Branches allow you to work without breaking the main codebase.

## Check branches

```bash
git branch
```

## Create branch

```bash
git branch feature/payment
```

## Switch branch

```bash
git checkout feature/payment
```

Modern command:

```bash
git switch feature/payment
```

## Create and switch

```bash
git checkout -b feature/payment
```

Or:

```bash
git switch -c feature/payment
```

## Delete branch

```bash
git branch -d feature/payment
```

Force delete:

```bash
git branch -D feature/payment
```

---

# 9. Professional Branch Naming

Use clear branch names.

| Type     | Example                     |
| -------- | --------------------------- |
| Feature  | `feature/user-auth`         |
| Bug fix  | `fix/login-error`           |
| Hotfix   | `hotfix/payment-crash`      |
| Refactor | `refactor/dashboard-layout` |
| Chore    | `chore/update-dependencies` |
| Docs     | `docs/api-guide`            |
| CI       | `ci/docker-build`           |

For your SaaS project:

```bash
feature/social-post-scheduler
feature/email-campaign-builder
feature/crm-lead-pipeline
feature/ai-agent-workflows
fix/oauth-refresh-token
ci/backend-docker-deploy
```

---

# 10. Merging

Merge combines one branch into another.

Example:

```bash
git checkout main
git pull origin main
git merge feature/auth-system
```

Then push:

```bash
git push origin main
```

## Fast-forward merge

When Git can simply move the branch pointer forward.

```txt
main:     A---B
feature:      C---D

after merge:

main:     A---B---C---D
```

## Three-way merge

When both branches changed separately.

```txt
main:     A---B---E
feature:      C---D
```

Git creates a merge commit.

---

# 11. Merge Conflicts

A conflict happens when Git cannot automatically decide which change to keep.

Example conflict:

```txt
<<<<<<< HEAD
const title = "Dashboard";
=======
const title = "CRM Dashboard";
>>>>>>> feature/crm
```

Fix manually:

```js
const title = "CRM Dashboard";
```

Then:

```bash
git add .
git commit
```

Professional conflict process:

```bash
git status
# open conflicted files
# resolve conflicts
git add .
git commit
```

Abort merge:

```bash
git merge --abort
```

---

# 12. Rebase

Rebase moves your branch on top of another branch.

```bash
git checkout feature/auth
git rebase main
```

Before:

```txt
main:    A---B---C
feature:     D---E
```

After:

```txt
main:    A---B---C
feature:         D'---E'
```

## Merge vs Rebase

| Merge                        | Rebase                          |
| ---------------------------- | ------------------------------- |
| Keeps full history           | Creates cleaner linear history  |
| Safer for shared branches    | Good for local feature branches |
| Creates merge commits        | Rewrites commits                |
| Better for team transparency | Better for clean PRs            |

Professional rule:

> Use **rebase before opening PR**. Use **merge when integrating approved PRs**.

Safe rebase workflow:

```bash
git checkout feature/auth
git fetch origin
git rebase origin/main
git push --force-with-lease
```

Use this, not plain force:

```bash
git push --force-with-lease
```

Avoid:

```bash
git push --force
```

---

# 13. Pulling Changes

Basic:

```bash
git pull origin main
```

Equivalent to:

```bash
git fetch origin
git merge origin/main
```

Professional safer workflow:

```bash
git fetch origin
git status
git log --oneline --graph --all
git rebase origin/main
```

Pull with rebase:

```bash
git pull --rebase origin main
```

Set globally:

```bash
git config --global pull.rebase true
```

---

# 14. Remote Repositories

## Add remote

```bash
git remote add origin https://github.com/user/repo.git
```

## View remotes

```bash
git remote -v
```

## Push first time

```bash
git push -u origin main
```

After that:

```bash
git push
```

## Change remote URL

```bash
git remote set-url origin https://github.com/user/new-repo.git
```

---

# 15. Forks and Upstream

Common in open source.

```txt
Original repo → upstream
Your fork      → origin
```

Clone your fork:

```bash
git clone https://github.com/yourname/project.git
```

Add upstream:

```bash
git remote add upstream https://github.com/original/project.git
```

Sync with upstream:

```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

Or cleaner:

```bash
git fetch upstream
git checkout main
git rebase upstream/main
git push origin main
```

---

# 16. Undoing Changes

This is where many developers become dangerous. Learn it properly.

## Undo unstaged changes

```bash
git restore file.js
```

Undo all unstaged changes:

```bash
git restore .
```

## Unstage a file

```bash
git restore --staged file.js
```

## Amend last commit

Use when you forgot something:

```bash
git add .
git commit --amend
```

Change last commit message:

```bash
git commit --amend -m "fix(auth): validate login input"
```

## Revert a commit

Safe for shared branches:

```bash
git revert <commit-hash>
```

This creates a new commit that undoes the old one.

## Reset commits

Dangerous but useful.

Soft reset keeps changes staged:

```bash
git reset --soft HEAD~1
```

Mixed reset keeps changes but unstaged:

```bash
git reset HEAD~1
```

Hard reset deletes changes:

```bash
git reset --hard HEAD~1
```

Professional rule:

| Situation                    | Command              |
| ---------------------------- | -------------------- |
| Undo public/shared commit    | `git revert`         |
| Fix local unpublished commit | `git commit --amend` |
| Remove local commits         | `git reset`          |
| Clean working tree           | `git restore`        |

---

# 17. Git Stash

Use stash when you need to temporarily save work without committing.

```bash
git stash
```

List stashes:

```bash
git stash list
```

Apply latest stash:

```bash
git stash apply
```

Apply and remove stash:

```bash
git stash pop
```

Stash with message:

```bash
git stash push -m "WIP: auth form"
```

Stash including untracked files:

```bash
git stash -u
```

Drop stash:

```bash
git stash drop stash@{0}
```

Clear all stashes:

```bash
git stash clear
```

---

# 18. Tags and Releases

Tags are used for versions.

```bash
git tag v1.0.0
git push origin v1.0.0
```

Annotated tag:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

List tags:

```bash
git tag
```

Delete local tag:

```bash
git tag -d v1.0.0
```

Delete remote tag:

```bash
git push origin --delete v1.0.0
```

Professional release style:

```txt
v1.0.0
v1.1.0
v1.1.1
v2.0.0
```

Using semantic versioning:

```txt
MAJOR.MINOR.PATCH
```

Example:

| Version | Meaning              |
| ------- | -------------------- |
| `1.0.0` | First stable release |
| `1.1.0` | New feature          |
| `1.1.1` | Bug fix              |
| `2.0.0` | Breaking change      |

---

# 19. Git Ignore

`.gitignore` tells Git which files not to track.

Example for Node/Next.js/FastAPI:

```gitignore
# dependencies
node_modules/
venv/
.env
.env.local
.env.production

# build output
.next/
dist/
build/
__pycache__/
*.pyc

# logs
*.log

# database
*.sqlite3

# system
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
```

Never commit:

```txt
.env
API keys
database passwords
private keys
node_modules
large build folders
```

If you already tracked a file and then added it to `.gitignore`, remove it from Git tracking:

```bash
git rm --cached .env
git commit -m "chore: remove env file from tracking"
```

---

# 20. Viewing Changes

## See unstaged diff

```bash
git diff
```

## See staged diff

```bash
git diff --staged
```

## Compare branches

```bash
git diff main..feature/auth
```

## See changed files only

```bash
git diff --name-only
```

## Show commit details

```bash
git show <commit-hash>
```

---

# 21. Searching History

## Search commits by message

```bash
git log --grep="auth"
```

## Search code changes

```bash
git log -S "loginUser"
```

## See who changed each line

```bash
git blame file.js
```

Use `git blame` to understand history, not to blame people.

---

# 22. Cleaning Files

Show files Git would delete:

```bash
git clean -n
```

Delete untracked files:

```bash
git clean -f
```

Delete untracked files and directories:

```bash
git clean -fd
```

Dangerous:

```bash
git clean -fdx
```

This also removes ignored files.

---

# 23. Cherry Pick

Apply one commit from another branch.

```bash
git cherry-pick <commit-hash>
```

Example:

```bash
git checkout main
git cherry-pick 9f3a21c
```

Useful when:

* You need one bug fix from another branch
* You do not want the full branch
* You need a hotfix

---

# 24. Bisect: Finding Bugs Like a Pro

`git bisect` helps find which commit introduced a bug.

Start:

```bash
git bisect start
```

Mark current commit as bad:

```bash
git bisect bad
```

Mark old working commit as good:

```bash
git bisect good <commit-hash>
```

Git checks commits one by one. You test each one:

```bash
git bisect good
# or
git bisect bad
```

Finish:

```bash
git bisect reset
```

This is highly professional debugging.

---

# 25. Reflog: Recover “Lost” Work

`git reflog` shows where HEAD has been.

```bash
git reflog
```

Example:

```txt
a1b2c3d HEAD@{0}: reset: moving to HEAD~1
d4e5f6g HEAD@{1}: commit: Add auth system
```

Recover:

```bash
git checkout d4e5f6g
```

Or create branch from it:

```bash
git checkout -b recovery-auth d4e5f6g
```

Professional lesson:

> Most Git mistakes are recoverable if you know `git reflog`.

---

# 26. Professional Git Workflows

## Workflow 1: Feature Branch Workflow

Best for most startups, SaaS teams, and freelancers.

```txt
main
 └── feature/auth
 └── feature/crm-pipeline
 └── fix/email-bug
```

Process:

```bash
git checkout main
git pull origin main
git checkout -b feature/crm-pipeline
# work
git add .
git commit -m "feat(crm): add pipeline stages"
git push origin feature/crm-pipeline
```

Then open PR.

---

## Workflow 2: Trunk-Based Development

Used by high-performing engineering teams.

```txt
main = always deployable
small branches
frequent merges
CI required
```

Rules:

* Small PRs
* Feature flags
* Strong tests
* Fast CI
* No long-lived branches

Good for:

* SaaS
* DevOps teams
* CI/CD-heavy companies

---

## Workflow 3: GitFlow

Older but still used in enterprise.

Branches:

```txt
main
develop
feature/*
release/*
hotfix/*
```

Example:

```bash
git checkout develop
git checkout -b feature/payment
```

Good for:

* Long release cycles
* Enterprise software
* Versioned products

Less ideal for fast SaaS.

---

# 27. Pull Requests / Merge Requests

A PR is a request to merge your branch into another branch.

A good PR contains:

```md
## What changed
- Added login API
- Added JWT token validation
- Added auth middleware

## Why
Needed for secure user authentication.

## Testing
- Tested login with valid credentials
- Tested invalid password
- Tested expired token

## Screenshots
Optional for frontend changes

## Checklist
- [ ] Code builds
- [ ] Tests pass
- [ ] No secrets committed
- [ ] Documentation updated
```

Professional PR rules:

| Rule                       | Why                  |
| -------------------------- | -------------------- |
| Keep PR small              | Easier review        |
| One purpose per PR         | Reduces bugs         |
| Write clear description    | Saves reviewer time  |
| Add tests                  | Prevents regressions |
| Link issue/task            | Better traceability  |
| Avoid unrelated formatting | Cleaner review       |

---

# 28. Commit Message Standards

Bad:

```bash
git commit -m "changes"
git commit -m "fix"
git commit -m "update"
git commit -m "final"
```

Good:

```bash
git commit -m "feat(auth): add refresh token rotation"
git commit -m "fix(crm): prevent duplicate leads"
git commit -m "refactor(api): extract email service"
git commit -m "test(auth): add login validation tests"
```

Best format:

```txt
type(scope): action
```

Examples:

```txt
feat(email): add campaign scheduler
fix(agent): handle failed tool execution
docs(readme): add deployment guide
ci(api): add Docker build workflow
```

---

# 29. GitHub Professional Setup

For serious projects, enable:

## Branch protection

Protect `main` branch:

* Require pull request before merge
* Require approvals
* Require status checks
* Require branch up to date
* Prevent force pushes
* Prevent direct commits to `main`

## CODEOWNERS

Example:

```txt
# Global owners
* @mudasir

# Frontend
/frontend/ @frontend-lead

# Backend
/backend/ @backend-lead

# DevOps
/.github/ @devops-lead
/docker/ @devops-lead
```

## Pull request template

`.github/pull_request_template.md`

```md
## Summary

## Changes

## Testing

## Screenshots

## Checklist
- [ ] Tests pass
- [ ] No secrets exposed
- [ ] Documentation updated
- [ ] Code reviewed
```

## Issue templates

`.github/ISSUE_TEMPLATE/bug_report.md`

```md
## Bug Description

## Steps to Reproduce

## Expected Behavior

## Actual Behavior

## Environment

## Screenshots
```

---

# 30. Git with CI/CD

Git is the trigger for automation.

Example flow:

```txt
Developer pushes code
→ GitHub Actions runs tests
→ Docker image builds
→ Security scan runs
→ Deploy to staging
→ Manual approval
→ Deploy to production
```

Example GitHub Actions trigger:

```yaml
name: CI

on:
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test
```

Professional Git + CI/CD rule:

> No code should enter `main` unless tests, linting, and security checks pass.

---

# 31. Git Hooks

Git hooks run scripts before or after Git actions.

Example hooks:

| Hook         | Purpose                      |
| ------------ | ---------------------------- |
| `pre-commit` | Run lint/tests before commit |
| `commit-msg` | Validate commit message      |
| `pre-push`   | Run tests before push        |

For JavaScript projects, use Husky:

```bash
npm install husky --save-dev
npx husky init
```

Example pre-commit:

```bash
npm run lint
npm run test
```

Professional usage:

```txt
Before commit:
- Format code
- Run lint
- Run typecheck
- Run unit tests
```

---

# 32. Git LFS

Git is bad for large binary files.

Use **Git LFS** for:

* Videos
* Large images
* ML models
* Design files
* Datasets

Install:

```bash
git lfs install
```

Track files:

```bash
git lfs track "*.psd"
git lfs track "*.mp4"
git lfs track "*.zip"
```

Commit `.gitattributes`:

```bash
git add .gitattributes
git commit -m "chore: configure git lfs"
```

---

# 33. Submodules

Submodules let you include another Git repo inside your repo.

Add submodule:

```bash
git submodule add https://github.com/user/shared-lib.git libs/shared-lib
```

Clone repo with submodules:

```bash
git clone --recurse-submodules https://github.com/user/project.git
```

Update submodules:

```bash
git submodule update --init --recursive
```

Use carefully. Submodules can become painful in teams.

---

# 34. Git Worktree

Worktree lets you work on multiple branches at the same time without stashing.

```bash
git worktree add ../project-hotfix hotfix/payment-bug
```

Now you have:

```txt
/project
/project-hotfix
```

List worktrees:

```bash
git worktree list
```

Remove:

```bash
git worktree remove ../project-hotfix
```

Professional use case:

* You are working on feature branch
* Urgent production bug appears
* Create separate worktree for hotfix
* No need to stash your current work

---

# 35. Sparse Checkout

Use sparse checkout when a repo is huge and you only need part of it.

```bash
git sparse-checkout init --cone
git sparse-checkout set frontend backend
```

Useful for monorepos.

---

# 36. Signed Commits

Professional teams may require signed commits.

Generate GPG key:

```bash
gpg --full-generate-key
```

List keys:

```bash
gpg --list-secret-keys --keyid-format=long
```

Configure Git:

```bash
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true
```

Signed commit:

```bash
git commit -S -m "feat(auth): add login"
```

Purpose:

* Verifies commit author
* Improves supply-chain security
* Useful in enterprise/open-source projects

---

# 37. Handling Secrets

Never commit:

```txt
OPENAI_API_KEY
DATABASE_URL
JWT_SECRET
AWS_SECRET_ACCESS_KEY
PRIVATE_KEY
```

Use:

```txt
.env
GitHub Actions Secrets
Doppler
1Password
Vault
AWS Secrets Manager
GCP Secret Manager
```

If secret was committed:

```bash
git rm --cached .env
git commit -m "chore: remove env file"
```

Then rotate the secret immediately.

For full removal from history, use tools like:

```bash
git filter-repo
```

or BFG Repo-Cleaner.

Important:

> Removing a secret from the latest commit is not enough. If it was pushed, assume it is leaked.

---

# 38. Professional Repository Structure

Example for your fullstack/AI SaaS:

```txt
saas-platform/
├── frontend/
│   ├── app/
│   ├── components/
│   ├── package.json
│   └── README.md
├── backend/
│   ├── app/
│   ├── tests/
│   ├── pyproject.toml
│   └── README.md
├── docs/
│   ├── architecture.md
│   ├── api.md
│   └── development-flow.md
├── .github/
│   ├── workflows/
│   └── pull_request_template.md
├── docker-compose.yml
├── .gitignore
├── README.md
└── LICENSE
```

---

# 39. Professional Git Rules for Teams

## Rule 1: Never commit directly to `main`

Bad:

```bash
git checkout main
# edit files
git commit -m "fix"
git push origin main
```

Good:

```bash
git checkout -b fix/login-error
git commit -m "fix(auth): handle invalid login"
git push origin fix/login-error
```

Then PR.

---

## Rule 2: Pull before starting work

```bash
git checkout main
git pull origin main
git checkout -b feature/new-work
```

---

## Rule 3: Keep commits meaningful

Bad:

```txt
fix
more changes
again
final final
```

Good:

```txt
feat(crm): add lead status filter
fix(email): prevent duplicate follow-up
test(api): add pipeline stage tests
```

---

## Rule 4: Keep PRs small

Bad PR:

```txt
Added auth, billing, dashboard, email system, Docker, and refactored backend.
```

Good PRs:

```txt
PR 1: Add auth API
PR 2: Add auth UI
PR 3: Add protected routes
PR 4: Add auth tests
```

---

## Rule 5: Use rebase carefully

Safe:

```bash
git rebase main
```

Dangerous on shared branch:

```bash
git rebase shared-team-branch
git push --force
```

---

## Rule 6: Use `--force-with-lease`

Professional:

```bash
git push --force-with-lease
```

Avoid:

```bash
git push --force
```

---

# 40. Common Git Mistakes and Fixes

## Mistake: Committed to wrong branch

```bash
git log --oneline
git checkout correct-branch
git cherry-pick <commit-hash>
git checkout wrong-branch
git reset --hard HEAD~1
```

---

## Mistake: Forgot to create branch

You made changes on `main`.

Fix:

```bash
git checkout -b feature/my-work
```

Now your changes are on a new branch.

---

## Mistake: Need to undo last commit but keep changes

```bash
git reset --soft HEAD~1
```

---

## Mistake: Need to undo last commit and unstage changes

```bash
git reset HEAD~1
```

---

## Mistake: Need to completely remove last commit

```bash
git reset --hard HEAD~1
```

Only do this if not pushed.

---

## Mistake: Pushed secret

Immediate action:

```bash
git rm --cached .env
git commit -m "chore: remove env file"
git push
```

Then:

1. Rotate secret
2. Remove from history
3. Check logs
4. Add `.env` to `.gitignore`

---

## Mistake: Merge conflict too messy

Abort:

```bash
git merge --abort
```

Or for rebase:

```bash
git rebase --abort
```

---

## Mistake: Deleted branch accidentally

Find commit:

```bash
git reflog
```

Recover:

```bash
git checkout -b recovered-branch <commit-hash>
```

---

# 41. Git Command Cheat Sheet

## Setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

## Start

```bash
git init
git clone <repo-url>
```

## Status

```bash
git status
git log --oneline --graph --all
git diff
git diff --staged
```

## Stage and commit

```bash
git add .
git add file.js
git add -p
git commit -m "message"
git commit --amend
```

## Branch

```bash
git branch
git checkout -b feature/name
git switch -c feature/name
git checkout main
git branch -d feature/name
```

## Remote

```bash
git remote -v
git push origin branch-name
git pull origin main
git fetch origin
```

## Merge and rebase

```bash
git merge feature/name
git rebase main
git rebase --continue
git rebase --abort
```

## Undo

```bash
git restore file.js
git restore --staged file.js
git reset --soft HEAD~1
git reset HEAD~1
git reset --hard HEAD~1
git revert <commit>
```

## Stash

```bash
git stash
git stash list
git stash pop
git stash apply
```

## Recovery

```bash
git reflog
git checkout -b recovery <commit-hash>
```

---

# 42. Professional Git Workflow Example

Imagine you are building a SaaS CRM feature.

## Step 1: Update main

```bash
git checkout main
git pull origin main
```

## Step 2: Create feature branch

```bash
git checkout -b feature/crm-lead-pipeline
```

## Step 3: Work and commit in small chunks

```bash
git add backend/app/models/lead.py
git commit -m "feat(crm): add lead model"
```

```bash
git add backend/app/routes/leads.py
git commit -m "feat(crm): add lead API routes"
```

```bash
git add frontend/app/dashboard/crm
git commit -m "feat(crm): add lead pipeline UI"
```

```bash
git add backend/tests/test_leads.py
git commit -m "test(crm): add lead API tests"
```

## Step 4: Sync with main

```bash
git fetch origin
git rebase origin/main
```

## Step 5: Push

```bash
git push origin feature/crm-lead-pipeline
```

## Step 6: Open PR

PR title:

```txt
feat(crm): add lead pipeline management
```

PR description:

```md
## Summary
Adds CRM lead pipeline management with backend APIs and frontend dashboard UI.

## Changes
- Added lead model
- Added lead CRUD APIs
- Added pipeline dashboard UI
- Added API tests

## Testing
- Ran backend tests
- Tested lead creation
- Tested stage movement
- Tested invalid payload validation
```

---

# 43. Git for DevOps and Deployment

Professional deployment usually follows this model:

```txt
feature branch
→ pull request
→ CI tests
→ merge to main
→ build Docker image
→ deploy to staging
→ tag release
→ deploy to production
```

Example branch strategy:

| Branch      | Purpose                      |
| ----------- | ---------------------------- |
| `main`      | Production-ready             |
| `develop`   | Integration branch, optional |
| `feature/*` | New features                 |
| `fix/*`     | Bug fixes                    |
| `hotfix/*`  | Urgent production fixes      |
| `release/*` | Release preparation          |

Deployment triggers:

| Git action     | Automation         |
| -------------- | ------------------ |
| Push to PR     | Run tests          |
| Merge to main  | Deploy staging     |
| Create tag     | Deploy production  |
| Push to hotfix | Emergency pipeline |

---

# 44. GitHub Actions Branch Example

```yaml
name: Production Deploy

on:
  push:
    tags:
      - "v*.*.*"

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Build Docker image
        run: docker build -t my-saas:${{ github.ref_name }} .

      - name: Deploy
        run: echo "Deploying release ${{ github.ref_name }}"
```

Then release:

```bash
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0
```

---

# 45. Git for Freelancers

As a freelancer, Git proves professionalism.

Use it to show:

* Clean commits
* Structured branches
* Client-safe deployments
* Rollback capability
* Professional documentation
* Issue tracking
* Release history

For client projects, use:

```txt
main          → production
staging       → client testing
feature/*     → development
hotfix/*      → urgent fixes
```

Good client delivery flow:

```txt
1. Create feature branch
2. Push changes
3. Open PR
4. Deploy preview/staging
5. Client reviews
6. Merge to main
7. Deploy production
8. Tag release
```

---

# 46. Git Exercises: Beginner to Professional

## Level 1: Basics

Create a repo:

```bash
mkdir git-practice
cd git-practice
git init
echo "# Git Practice" > README.md
git add .
git commit -m "docs: add readme"
```

Practice:

```bash
git status
git log
git diff
```

---

## Level 2: Branching

```bash
git checkout -b feature/homepage
echo "Homepage" > homepage.txt
git add .
git commit -m "feat: add homepage"
git checkout main
git merge feature/homepage
```

---

## Level 3: Conflicts

Create two branches and edit the same line.

```bash
git checkout -b feature/title-a
echo "Title A" > title.txt
git add .
git commit -m "feat: add title a"

git checkout main
echo "Title Main" > title.txt
git add .
git commit -m "feat: add main title"

git merge feature/title-a
```

Resolve the conflict manually.

---

## Level 4: Rebase

```bash
git checkout -b feature/rebase-practice
# make commits
git fetch origin
git rebase origin/main
```

---

## Level 5: Recovery

```bash
git reset --hard HEAD~1
git reflog
git checkout -b recovered <commit-hash>
```

---

## Level 6: Professional PR Simulation

Create:

```txt
feature/auth-api
feature/auth-ui
fix/login-validation
ci/add-test-workflow
```

Each branch should have:

* Clean commits
* Proper messages
* PR description
* Tests or docs

---

# 47. What You Must Master to Become Professional

| Skill                           | Level        |
| ------------------------------- | ------------ |
| `add`, `commit`, `push`, `pull` | Basic        |
| Branching and merging           | Basic        |
| Conflict resolution             | Intermediate |
| Rebase                          | Intermediate |
| Reset/revert/restore            | Intermediate |
| Reflog recovery                 | Advanced     |
| Clean commit history            | Professional |
| PR workflow                     | Professional |
| Branch protection               | Professional |
| CI/CD with Git                  | Professional |
| Signed commits                  | Advanced     |
| Git LFS/submodules/worktree     | Advanced     |
| Release tagging                 | Professional |

---

# 48. The Best Professional Git Workflow

Use this as your default:

```bash
# 1. Start from updated main
git checkout main
git pull origin main

# 2. Create branch
git checkout -b feature/clear-feature-name

# 3. Work in small commits
git add -p
git commit -m "feat(scope): meaningful message"

# 4. Sync before PR
git fetch origin
git rebase origin/main

# 5. Push branch
git push origin feature/clear-feature-name

# 6. Open PR
# 7. Pass CI
# 8. Get review
# 9. Merge
# 10. Delete branch
```

---

# 49. The Git Rules You Should Never Break

## Never commit secrets

```txt
.env
API keys
tokens
private keys
passwords
```

## Never force push shared branches

Avoid:

```bash
git push --force
```

Use:

```bash
git push --force-with-lease
```

## Never make huge random commits

Bad:

```txt
update everything
```

Good:

```txt
feat(auth): add login endpoint
fix(auth): validate password length
test(auth): add login tests
```

## Never work directly on production branch

Use feature branches.

## Never ignore failed CI

Fix tests before merge.

---

# 50. Your 14-Day Git Learning Plan

## Days 1–2: Fundamentals

Learn:

```bash
git init
git add
git commit
git status
git log
git diff
```

Build small repo.

---

## Days 3–4: Branches

Learn:

```bash
git branch
git checkout -b
git switch
git merge
```

Practice feature branches.

---

## Days 5–6: Remote GitHub

Learn:

```bash
git remote
git push
git pull
git fetch
```

Push to GitHub.

---

## Days 7–8: Conflicts and Undo

Learn:

```bash
git restore
git reset
git revert
git merge --abort
```

Create and fix conflicts.

---

## Days 9–10: Rebase and Clean History

Learn:

```bash
git rebase
git commit --amend
git push --force-with-lease
```

Practice clean PR history.

---

## Days 11–12: Team Workflow

Practice:

* Pull requests
* Code reviews
* Branch protection
* PR templates
* Conventional commits

---

## Days 13–14: Advanced Professional Git

Learn:

```bash
git stash
git cherry-pick
git reflog
git bisect
git tag
git worktree
```

Create release tags and recovery practice.

---

# Final Practical Standard

Professional Git is not about memorizing commands.

It means you can:

1. **Work without losing code**
2. **Collaborate without breaking team work**
3. **Create clean commit history**
4. **Recover from mistakes**
5. **Use PRs and CI/CD properly**
6. **Protect production branches**
7. **Ship reliable releases**

Master this workflow and you can work confidently in real software teams:

```bash
git checkout main
git pull origin main
git checkout -b feature/my-task
git add -p
git commit -m "feat(scope): clear message"
git fetch origin
git rebase origin/main
git push origin feature/my-task
```

That is the professional Git foundation.
