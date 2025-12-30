---
layout: default
title: Branching & Merging
---

## Branching & Merging

Master Git branching strategies and merge workflows for effective version control.

### What are Branches?

Branches allow you to diverge from the main line of development and work independently without affecting the main codebase.

### Branch Basics

#### Creating Branches

```bash
# Create new branch
git branch feature-name

# Create and switch to new branch
git checkout -b feature-name

# Modern syntax (Git 2.23+)
git switch -c feature-name
```

#### Switching Branches

```bash
# Switch to existing branch
git checkout branch-name

# Modern syntax
git switch branch-name

# Switch to previous branch
git checkout -
```

#### Listing Branches

```bash
# List local branches
git branch

# List all branches (local + remote)
git branch -a

# List remote branches
git branch -r

# Show last commit on each branch
git branch -v
```

#### Deleting Branches

```bash
# Delete merged branch
git branch -d branch-name

# Force delete unmerged branch
git branch -D branch-name

# Delete remote branch
git push origin --delete branch-name
```

### Common Branching Strategies

#### Git Flow

```
main (production)
├── develop (development)
    ├── feature/user-authentication
    ├── feature/payment-integration
    ├── release/v1.2.0
    └── hotfix/critical-bug
```

**Branch Types:**
- `main`: Production-ready code
- `develop`: Integration branch
- `feature/*`: New features
- `release/*`: Release preparation
- `hotfix/*`: Production fixes

#### GitHub Flow (Simpler)

```
main
├── feature/add-login
├── feature/update-ui
└── fix/navigation-bug
```

**Workflow:**
1. Create branch from `main`
2. Make changes and commit
3. Open pull request
4. Review and test
5. Merge to `main`

#### Trunk-Based Development

- Single `main` branch
- Short-lived feature branches
- Frequent integration
- Feature flags for incomplete features

### Merging Branches

#### Fast-Forward Merge

When no divergent commits exist:

```bash
git checkout main
git merge feature-branch
```

#### Three-Way Merge

When branches have diverged:

```bash
git checkout main
git merge feature-branch -m "Merge feature branch"
```

#### Squash Merge

Combine all commits into one:

```bash
git checkout main
git merge --squash feature-branch
git commit -m "Add feature: description"
```

#### Rebase and Merge

Create linear history:

```bash
git checkout feature-branch
git rebase main
git checkout main
git merge feature-branch
```

### Handling Merge Conflicts

#### When Conflicts Occur

```bash
$ git merge feature-branch
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
Automatic merge failed; fix conflicts and then commit the result.
```

#### Resolving Conflicts

1. **Check conflicted files:**
   ```bash
   git status
   ```

2. **Open conflicted file:**
   ```
   <<<<<<< HEAD
   Current branch content
   =======
   Incoming branch content
   >>>>>>> feature-branch
   ```

3. **Edit to resolve:**
   ```
   Final merged content
   ```

4. **Mark as resolved:**
   ```bash
   git add file.txt
   git commit -m "Resolve merge conflict"
   ```

#### Conflict Resolution Tools

```bash
# Use merge tool
git mergetool

# Abort merge
git merge --abort

# Keep their version
git checkout --theirs file.txt
git add file.txt

# Keep our version
git checkout --ours file.txt
git add file.txt
```

### Rebasing

#### Interactive Rebase

Clean up commit history:

```bash
# Rebase last 3 commits
git rebase -i HEAD~3
```

Options:
- `pick`: Keep commit
- `reword`: Change commit message
- `edit`: Modify commit
- `squash`: Combine with previous
- `drop`: Remove commit

#### Rebase onto Another Branch

```bash
# Update feature branch with main
git checkout feature-branch
git rebase main

# If conflicts occur
git rebase --continue
# or
git rebase --abort
```

### Cherry-Picking

Apply specific commits to current branch:

```bash
# Cherry-pick single commit
git cherry-pick <commit-hash>

# Cherry-pick multiple commits
git cherry-pick <hash1> <hash2>

# Cherry-pick without committing
git cherry-pick -n <commit-hash>
```

### Branch Management Best Practices

1. **Naming Conventions**
   ```
   feature/description
   bugfix/issue-number
   hotfix/critical-fix
   release/version-number
   ```

2. **Keep Branches Short-Lived**
   - Merge or delete after completion
   - Reduces merge conflicts
   - Easier to review

3. **Regular Synchronization**
   ```bash
   # Update feature branch regularly
   git checkout feature-branch
   git fetch origin
   git rebase origin/main
   ```

4. **Branch Protection Rules**
   - Require pull request reviews
   - Require status checks
   - Prevent force pushes
   - Require linear history

### Working with Remote Branches

```bash
# Push new branch to remote
git push -u origin feature-branch

# Track remote branch
git branch --track feature-branch origin/feature-branch

# Fetch and checkout remote branch
git fetch origin
git checkout -b feature-branch origin/feature-branch

# Update remote branch list
git fetch --prune
```

### Common Scenarios

#### Start New Feature

```bash
git checkout main
git pull origin main
git checkout -b feature/new-feature
# Make changes
git add .
git commit -m "Add new feature"
git push -u origin feature/new-feature
```

#### Update Feature Branch

```bash
git checkout feature-branch
git fetch origin
git rebase origin/main
git push --force-with-lease
```

#### Quick Hotfix

```bash
git checkout main
git pull origin main
git checkout -b hotfix/critical-bug
# Fix the bug
git add .
git commit -m "Fix critical bug"
git push -u origin hotfix/critical-bug
# Create PR and merge quickly
```

### Next Steps

- Learn about [Pull Requests]({{ '/docs/pull-requests' | relative_url }})
- Understand [Collaboration]({{ '/docs/collaboration' | relative_url }}) workflows
- Review [Best Practices]({{ '/docs/best-practices' | relative_url }})
