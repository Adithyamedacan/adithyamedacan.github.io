---
layout: default
title: Repository Basics
---

Understanding the fundamentals of Git repositories and version control.

### What is a Repository?

A repository (repo) is a storage location for your project that tracks all changes made to files over time. It contains:
- All project files and folders
- Complete history of changes
- Branches and tags
- Configuration files

### Repository Structure

```
my-repository/
├── .git/                 # Git metadata and history
├── .gitignore           # Files to ignore
├── README.md            # Project documentation
├── src/                 # Source code
├── tests/               # Test files
└── docs/                # Documentation
```

### Working with Files

#### Adding Files

```bash
# Add specific file
git add filename.txt

# Add all files in directory
git add .

# Add all modified files
git add -u

# Add with pattern
git add *.js
```

#### Committing Changes

```bash
# Commit with message
git commit -m "Add feature X"

# Commit all tracked changes
git commit -am "Update feature Y"

# Amend last commit
git commit --amend -m "Corrected commit message"
```

#### Viewing History

```bash
# View commit history
git log

# Compact log view
git log --oneline

# View specific file history
git log -- filename.txt

# View changes in commit
git show <commit-hash>
```

### The .gitignore File

Specify files and directories that Git should ignore:

```gitignore
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.exe

# Environment files
.env
.env.local

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/
```

### Checking Repository Status

```bash
# See current status
git status

# Short status
git status -s

# See what changed
git diff

# See staged changes
git diff --staged
```

### Undoing Changes

#### Unstage Files

```bash
# Unstage specific file
git reset HEAD filename.txt

# Unstage all files
git reset HEAD
```

#### Discard Changes

```bash
# Discard changes in working directory
git checkout -- filename.txt

# Discard all changes
git checkout -- .

# Remove untracked files
git clean -fd
```

#### Revert Commits

```bash
# Revert specific commit (creates new commit)
git revert <commit-hash>

# Reset to previous commit (destructive)
git reset --hard HEAD~1
```

### Remote Repositories

#### Managing Remotes

```bash
# View remote repositories
git remote -v

# Add remote
git remote add origin https://github.com/user/repo.git

# Change remote URL
git remote set-url origin https://github.com/user/new-repo.git

# Remove remote
git remote remove origin
```

#### Syncing with Remote

```bash
# Fetch changes (doesn't merge)
git fetch origin

# Pull changes (fetch + merge)
git pull origin main

# Push changes
git push origin main

# Push all branches
git push --all origin
```

### Tags

Tags mark specific points in repository history (e.g., releases):

```bash
# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# List tags
git tag

# Push tags to remote
git push origin --tags

# Delete tag
git tag -d v1.0.0
```

### Best Practices

1. **Commit Often**: Make small, logical commits
2. **Write Clear Messages**: Describe what and why, not how
3. **Use .gitignore**: Don't commit sensitive or generated files
4. **Pull Before Push**: Always sync before pushing changes
5. **Review Before Commit**: Use `git status` and `git diff`

### Commit Message Guidelines

Good commit message format:

```
Short summary (50 chars or less)

More detailed explanation if needed. Wrap at 72 characters.
Explain the problem this commit solves and why this approach
was chosen.

- Bullet points are okay
- Use imperative mood: "Add feature" not "Added feature"

Fixes #123
```

### Next Steps

- Learn about [Branching & Merging]({{ '/docs/branching-merging' | relative_url }})
- Understand [Pull Requests]({{ '/docs/pull-requests' | relative_url }})
- Explore [Collaboration]({{ '/docs/collaboration' | relative_url }}) workflows
