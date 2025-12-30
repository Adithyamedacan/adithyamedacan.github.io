---
layout: default
title: Pull Requests
---

## Pull Requests

Learn how to create, review, and manage pull requests effectively.

### What is a Pull Request?

A pull request (PR) is a method of submitting contributions to a project. It lets you:
- Propose changes to a repository
- Request code review from team members
- Discuss and iterate on code before merging
- Maintain quality through peer review

### Creating a Pull Request

#### Step 1: Push Your Branch

```bash
git checkout -b feature/new-feature
# Make changes
git add .
git commit -m "Add new feature"
git push -u origin feature/new-feature
```

#### Step 2: Open PR on GitHub

1. Go to your repository on GitHub
2. Click **Pull requests** tab
3. Click **New pull request**
4. Select base branch (usually `main`) and compare branch (your feature branch)
5. Click **Create pull request**

#### Step 3: Fill PR Details

**Title**: Clear, concise summary
```
Add user authentication feature
```

**Description**: Detailed explanation
```markdown
## Description
Implements JWT-based user authentication system.

## Changes
- Add login/logout endpoints
- Implement JWT token generation
- Add authentication middleware
- Update user model

## Testing
- Unit tests for auth service
- Integration tests for login flow
- Manual testing completed

## Screenshots
[If applicable]

## Related Issues
Closes #123
```

### PR Templates

Create `.github/pull_request_template.md`:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex code
- [ ] Documentation updated
- [ ] Tests added/updated
- [ ] All tests passing
- [ ] No new warnings

## Testing Steps
1. Step one
2. Step two
3. Expected result

## Screenshots (if applicable)

## Related Issues
Fixes #(issue number)
```

### Reviewing Pull Requests

#### As a Reviewer

1. **Understand the Context**
   - Read the description
   - Check related issues
   - Understand the goal

2. **Review the Code**
   - Check for logic errors
   - Verify code style
   - Look for security issues
   - Assess performance impact
   - Check test coverage

3. **Provide Feedback**
   - Be constructive and specific
   - Explain the "why"
   - Suggest alternatives
   - Praise good solutions

#### Comment Types

**Request Changes:**
```markdown
This approach might cause performance issues with large datasets.
Consider using pagination here instead:
```

**Suggestions:**
```markdown
Suggestion: Use a more descriptive variable name
```javascript
const userData = await fetchUser(id);
```

**Approve:**
```markdown
LGTM! Great work on the error handling. ✅
```

**Questions:**
```markdown
Could you explain why we're using setTimeout here instead of a Promise?
```

### Responding to Reviews

#### Making Changes

```bash
# Make requested changes
git add .
git commit -m "Address review comments"
git push origin feature/new-feature
```

#### Addressing Comments

- Mark resolved discussions as resolved
- Reply to questions clearly
- Thank reviewers for feedback
- Update PR description if scope changes

### PR Best Practices

#### Size and Scope

✅ **Good PR:**
- Focuses on single feature/fix
- 200-400 lines changed
- Easy to review in 15-30 minutes

❌ **Bad PR:**
- Multiple unrelated changes
- 1000+ lines changed
- Difficult to understand scope

#### Writing Good Descriptions

**Before:**
```
Updated code
```

**After:**
```
Refactor authentication middleware for better error handling

- Extract validation logic into separate functions
- Add detailed error messages
- Improve test coverage from 60% to 95%
- Fix edge case with expired tokens

Closes #456
```

#### Commit Organization

**Option 1: Squash commits** (for feature branches)
```bash
git rebase -i HEAD~5
# Squash related commits
```

**Option 2: Keep logical commits**
- Each commit is a logical unit
- Helpful for reviewing
- Easier to troubleshoot

### Advanced PR Workflows

#### Draft Pull Requests

Use for work in progress:
1. Create PR
2. Select "Create draft pull request"
3. Mark as "Ready for review" when done

Benefits:
- Get early feedback
- Show progress
- Run CI/CD checks

#### PR Labels

Common labels:
- `bug`: Bug fixes
- `enhancement`: New features
- `documentation`: Doc updates
- `needs-review`: Awaiting review
- `work-in-progress`: Not ready
- `breaking-change`: Breaking changes

#### Linked Issues

Link PRs to issues:
```markdown
Closes #123
Fixes #456
Resolves #789
```

### Merging Strategies

#### Merge Commit

Preserves all commits and history:
```
git merge --no-ff feature-branch
```

**When to use:**
- Want complete history
- Feature branches with logical commits

#### Squash and Merge

Combines all commits into one:
```
git merge --squash feature-branch
```

**When to use:**
- Many small commits
- Want clean main branch history
- Single logical change

#### Rebase and Merge

Creates linear history:
```
git rebase main
git checkout main
git merge feature-branch
```

**When to use:**
- Want linear history
- No merge commits
- Well-organized commits

### Handling Merge Conflicts in PRs

1. **Update your branch:**
   ```bash
   git checkout feature-branch
   git fetch origin
   git merge origin/main
   ```

2. **Resolve conflicts:**
   ```bash
   # Fix conflicts in files
   git add .
   git commit -m "Resolve merge conflicts with main"
   git push origin feature-branch
   ```

3. **Alternative - Rebase:**
   ```bash
   git fetch origin
   git rebase origin/main
   git push --force-with-lease origin feature-branch
   ```

### PR Checklist

Before creating PR:
- [ ] Code is self-reviewed
- [ ] Tests added and passing
- [ ] Documentation updated
- [ ] Branch is up to date with base
- [ ] Commit messages are clear
- [ ] No debugging code left
- [ ] No console.logs or similar

Before merging:
- [ ] All reviews approved
- [ ] CI/CD checks passing
- [ ] Conflicts resolved
- [ ] Related issues linked
- [ ] Documentation reviewed

### Automation with GitHub Actions

Example workflow for PRs:

```yaml
name: PR Checks
on:
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: npm test
      - name: Run linter
        run: npm run lint
      - name: Check coverage
        run: npm run coverage
```

### Common PR Issues

**Large PRs:**
- Break into smaller PRs
- Use feature flags
- Split by component

**Long Review Time:**
- Smaller, focused PRs
- Add clear descriptions
- Tag appropriate reviewers
- Follow up politely

**Stale PRs:**
- Set up branch protection
- Regular team check-ins
- Use labels and milestones
- Automate reminders

### Next Steps

- Learn about [Collaboration]({{ '/docs/collaboration' | relative_url }}) workflows
- Explore [Best Practices]({{ '/docs/best-practices' | relative_url }})
- Review [Repository Basics]({{ '/docs/repository-basics' | relative_url }})
