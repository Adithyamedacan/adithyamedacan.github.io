---
layout: default
title: Repository Best Practices
---

Follow these industry standards and GitHub best practices for better repository management and development workflows.

### Repository Setup

#### README.md Structure

A well-structured README should include:

- **Project Title** and description
- **Table of Contents** for easy navigation
- **Installation** instructions
- **Usage** examples
- **Features** list
- **Contributing** guidelines
- **License** information

Example structure:
```
# Project Name
Brief description of what this project does

## Table of Contents
- Installation
- Usage
- Features
- Contributing
- License

## Installation
Step-by-step installation guide

## Usage
Examples of how to use the project

## Features
Key features of the project

## Contributing
How to contribute to this project

## License
This project is licensed under MIT License
```

#### Essential Repository Files

```
repository/
├── README.md              # Project overview
├── LICENSE                # License file
├── CONTRIBUTING.md        # Contribution guidelines
├── CODE_OF_CONDUCT.md     # Community guidelines
├── .gitignore            # Ignored files
├── .github/
│   ├── ISSUE_TEMPLATE/   # Issue templates
│   ├── PULL_REQUEST_TEMPLATE.md
│   ├── workflows/        # GitHub Actions
│   └── CODEOWNERS        # Code ownership
└── SECURITY.md           # Security policy
```

### Commit Best Practices

#### Conventional Commits

Format: `<type>(<scope>): <description>`

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code restructuring
- `test`: Tests
- `chore`: Maintenance

**Examples:**
```bash
feat(auth): add JWT authentication
fix(api): resolve timeout issue in user endpoint
docs(readme): update installation instructions
refactor(database): optimize query performance
test(user): add unit tests for user service
```

#### Commit Message Rules

1. **Subject line:**
   - 50 characters or less
   - Capitalize first letter
   - No period at end
   - Imperative mood

2. **Body (if needed):**
   - Wrap at 72 characters
   - Explain what and why
   - Separate from subject with blank line

3. **Footer:**
   - Reference issues
   - Note breaking changes

**Example:**
```
feat(payment): integrate Stripe payment gateway

Add Stripe SDK integration for processing payments.
This replaces the old payment system and provides
better security and more payment options.

- Add Stripe configuration
- Implement payment processing
- Add webhook handlers
- Update payment models

BREAKING CHANGE: Old payment API endpoints removed
Refs: #123, #456
```

### Branch Management

#### Naming Conventions

```
feature/user-authentication
feature/add-payment-integration
bugfix/fix-login-error
bugfix/resolve-memory-leak
hotfix/critical-security-patch
release/v1.2.0
docs/update-api-documentation
refactor/optimize-database-queries
```

#### Branch Lifecycle

```bash
# Create branch
git checkout -b feature/new-feature

# Regular updates
git fetch origin
git rebase origin/main

# Before PR
git rebase -i origin/main  # Clean up commits
git push --force-with-lease origin feature/new-feature

# After merge
git checkout main
git pull origin main
git branch -d feature/new-feature
git push origin --delete feature/new-feature
```

### Pull Request Best Practices

#### PR Size Guidelines

**Ideal PR:**
- 200-400 lines changed
- Single responsibility
- Reviewable in 30 minutes
- Focused scope

**If PR is too large:**
- Split into multiple smaller PRs
- Use feature flags for gradual rollout
- Create sub-tasks and dependencies
- Implement incremental delivery

#### PR Description Template

```markdown
## Summary
Brief overview of changes

## Motivation
Why this change is needed

## Changes
- Bullet point list
- Of what changed
- And why

## Testing
How this was tested:
- [ ] Unit tests
- [ ] Integration tests
- [ ] Manual testing

## Screenshots/Videos
[If UI changes]

## Breaking Changes
None / List any breaking changes

## Checklist
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No console errors
- [ ] Code reviewed by myself
- [ ] Ready for review

## Related Issues
Closes #123
Related to #456
```

### Code Review Best Practices

#### For Authors

**Before requesting review:**
```bash
# Self-review checklist
git diff main...feature-branch

# Run tests
npm test

# Run linter
npm run lint

# Check for console.logs
grep -r "console.log" src/
```

**During review:**
- Respond within 24 hours
- Accept constructive criticism
- Ask for clarification
- Thank reviewers

#### For Reviewers

**Review checklist:**
- [ ] Code logic is correct
- [ ] Tests are adequate
- [ ] Documentation is updated
- [ ] No security vulnerabilities
- [ ] Follows style guide
- [ ] Performance is acceptable
- [ ] Error handling is proper

**Feedback guidelines:**

❌ **Not helpful:** "This is bad."

✅ **Helpful:** "This could cause a memory leak with large datasets. Consider using a WeakMap instead."

❌ **Demanding:** "Change this immediately."

✅ **Suggesting:** "Suggestion: We could simplify this by using array destructuring."

Example of constructive feedback:
```javascript
// Instead of:
for (let i = 0; i < items.length; i++) {
  const item = items[i];
  // ...
}

// Consider:
const [first, ...rest] = items;
```

### Security Best Practices

#### Sensitive Data

**Never commit:**
- API keys
- Passwords
- Private keys
- Tokens
- Database credentials

**Use environment variables:**
```bash
# .env (add to .gitignore)
API_KEY=your-api-key
DATABASE_URL=postgres://...

# .env.example (commit this)
API_KEY=your-api-key-here
DATABASE_URL=your-database-url-here
```

#### Secrets Management

```bash
# Use GitHub Secrets for CI/CD
Settings → Secrets and variables → Actions

# Access in workflows
env:
  API_KEY: ${{ secrets.API_KEY }}
```

#### Security Scanning

Enable in repository settings:
- Dependabot alerts
- Code scanning
- Secret scanning

### Testing Best Practices

#### Test Coverage

**Aim for:**
- 80%+ overall coverage
- 100% critical paths
- All edge cases
- Error scenarios

**Test structure:**
```javascript
describe('UserService', () => {
  describe('createUser', () => {
    it('should create user with valid data', () => {
      // Arrange
      const userData = { name: 'John', email: 'john@example.com' };
      
      // Act
      const user = createUser(userData);
      
      // Assert
      expect(user).toBeDefined();
      expect(user.name).toBe('John');
    });

    it('should throw error with invalid email', () => {
      const userData = { name: 'John', email: 'invalid' };
      expect(() => createUser(userData)).toThrow();
    });
  });
});
```

### Documentation Best Practices

#### Code Documentation

```javascript
/**
 * Calculates the total price including tax
 * @param {number} price - The base price
 * @param {number} taxRate - Tax rate as decimal (e.g., 0.08 for 8%)
 * @returns {number} Total price with tax
 * @throws {Error} If price is negative
 * @example
 * calculateTotal(100, 0.08) // Returns 108
 */
function calculateTotal(price, taxRate) {
  if (price < 0) throw new Error('Price cannot be negative');
  return price * (1 + taxRate);
}
```

#### API Documentation

Use OpenAPI/Swagger:
```yaml
/api/users:
  get:
    summary: Get all users
    parameters:
      - name: page
        in: query
        schema:
          type: integer
    responses:
      200:
        description: Success
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/User'
```

### Performance Best Practices

#### Optimize Repository Size

```bash
# Check repository size
git count-objects -vH

# Remove large files from history
git filter-branch --tree-filter 'rm -f large-file.zip' HEAD

# Better: use BFG Repo-Cleaner
bfg --delete-files large-file.zip
```

#### Git LFS for Large Files

```bash
# Install Git LFS
git lfs install

# Track large files
git lfs track "*.psd"
git lfs track "*.mp4"

# Commit .gitattributes
git add .gitattributes
git commit -m "Track large files with Git LFS"
```

### CI/CD Best Practices

#### GitHub Actions Workflow

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint
      
      - name: Run tests
        run: npm test
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info
```

### Maintenance Best Practices

#### Regular Tasks

**Weekly:**
- Review open PRs
- Triage new issues
- Update dependencies
- Check security alerts

**Monthly:**
- Clean up stale branches
- Review project board
- Update documentation
- Analyze metrics

#### Dependency Management

```bash
# Check outdated packages
npm outdated

# Update with caution
npm update

# Major version updates
npm install package@latest

# Use Dependabot
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
```

### Quick Reference

#### Git Aliases

```bash
# Add to ~/.gitconfig
[alias]
  co = checkout
  br = branch
  ci = commit
  st = status
  unstage = reset HEAD --
  last = log -1 HEAD
  visual = log --graph --oneline --all
  amend = commit --amend --no-edit
```

#### Useful Commands

```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Interactive rebase last 3 commits
git rebase -i HEAD~3

# Cherry-pick commit
git cherry-pick <commit-hash>

# Find commit that introduced bug
git bisect start
git bisect bad
git bisect good <commit-hash>
```

### Next Steps

- Review [Getting Started]({{ '/docs/getting-started' | relative_url }})
- Understand [Collaboration]({{ '/docs/collaboration' | relative_url }})
- Master [Pull Requests]({{ '/docs/pull-requests' | relative_url }})
- Explore [Organization Best Practices]({{ '/docs/organization-enterprise-practices' | relative_url }})
