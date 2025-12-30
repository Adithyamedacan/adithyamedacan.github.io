---
layout: default
title: Collaboration
---

## Collaboration

Learn how to work effectively with teams using GitHub's collaboration features.

### Team Organization

#### Organization Structure

```
Organization
├── Teams
│   ├── Frontend Team
│   ├── Backend Team
│   └── DevOps Team
├── Repositories
│   ├── Public Repos
│   └── Private Repos
└── Projects
    ├── Sprint Planning
    └── Release Tracking
```

#### Creating Teams

1. Go to Organization → **Teams**
2. Click **New team**
3. Set team name and description
4. Choose parent team (optional)
5. Set team visibility

#### Team Permissions

GitHub provides several permission levels for team members and repository access:

##### Repository-Level Permissions

- **All-repository read**: View and clone all repositories in the organization
- **All-repository write**: Push to all repositories, create branches, and manage some repository settings
- **All-repository triage**: Manage issues and pull requests without write access to code
- **All-repository maintain**: Manage repositories without access to sensitive or destructive actions
- **All-repository admin**: Full administrative access to all repositories

##### Individual Repository Permissions

- **Read**: View and clone the repository
- **Triage**: Manage issues and pull requests
- **Write**: Push to repository and manage issues/PRs
- **Maintain**: Manage repository settings without access to sensitive actions
- **Admin**: Full access including repository deletion and settings

##### Organization-Level Permissions

- **Apps manager**: Manage GitHub Apps and OAuth apps for the organization
- **CI/CD Admin**: Manage CI/CD pipelines and workflows
- **Security manager**: Manage security alerts and settings across the organization
- **Enterprise Security Manager**: Manage security policies at the enterprise level

### Repository Access

#### Collaborators

Add collaborators to repositories:
1. Go to **Settings** → **Collaborators**
2. Click **Add people**
3. Search for username
4. Select permission level

#### Branch Protection

Protect important branches:
```
Settings → Branches → Add rule

✓ Require pull request reviews
✓ Require status checks to pass
✓ Require signed commits
```

### Code Review Process

#### Review Workflow

1. **Author creates PR**
   - Clear description
   - Self-review first
   - Link to issues

2. **Reviewers notified**
   - Automatic or manual assignment
   - Review requested

3. **Review conducted**
   - Code examination
   - Testing
   - Feedback provided

4. **Changes requested/approved**
   - Author makes updates
   - Re-review if needed

5. **PR merged**
   - Approved by required reviewers
   - All checks pass

#### Code Owners

The `CODEOWNERS` file is a powerful feature that automatically assigns reviewers to pull requests based on which files are being changed. This ensures that the right people review changes to specific parts of the codebase.

**Why use CODEOWNERS?**
- **Automatic review assignment**: Automatically requests reviews from the appropriate team members based on file paths
- **Expertise routing**: Ensures code is reviewed by people with domain expertise in that area
- **Quality control**: Prevents code from being merged without approval from designated owners
- **Reduced bottlenecks**: Distributes review responsibilities across teams
- **Documentation**: Clearly defines who is responsible for different parts of the codebase

Create `CODEOWNERS` file in `.github/` directory:

```
# Global owners
* @team/core-team

# Frontend code
/frontend/ @team/frontend-team
*.css @team/design-team

# Backend code
/backend/ @team/backend-team
*.py @team/python-experts

# Documentation
/docs/ @team/docs-team
*.md @team/docs-team

# Infrastructure
/.github/ @team/devops
/deploy/ @team/devops
```

### Issue Management

#### Issue Templates

Create `.github/ISSUE_TEMPLATE/bug_report.md`:

```markdown
---
name: Bug Report
about: Report a bug
title: '[BUG] '
labels: bug
assignees: ''
---

## Bug Description
Clear description of the bug

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- OS: [e.g., Windows 10]
- Browser: [e.g., Chrome 96]
- Version: [e.g., 1.2.3]

## Screenshots
If applicable

## Additional Context
Any other context
```

#### Issue Labels

Common label categories:

**Type:**
- `bug`: Bug reports
- `feature`: Feature requests
- `enhancement`: Improvements
- `documentation`: Doc updates

**Priority:**
- `critical`: Urgent issues
- `high`: High priority
- `medium`: Medium priority
- `low`: Low priority

**Status:**
- `needs-triage`: Needs review
- `in-progress`: Being worked on
- `blocked`: Blocked by dependencies
- `ready`: Ready for work

**Component:**
- `frontend`: Frontend code
- `backend`: Backend code
- `api`: API changes
- `database`: Database related

### Project Management

#### GitHub Projects

Create project boards:
1. Go to **Projects** → **New project**
2. Choose template (Board, Table, Roadmap)
3. Add columns/fields
4. Link issues and PRs

**Example Board:**
```
To Do | In Progress | Review | Done
```

#### Milestones

Group issues by milestone:
1. Go to **Issues** → **Milestones**
2. Create milestone (e.g., "v1.2.0")
3. Set due date
4. Add issues to milestone

### Communication

#### Discussions

Enable GitHub Discussions:
1. **Settings** → **Features**
2. Enable **Discussions**
3. Create categories:
   - Announcements
   - Q&A
   - Ideas
   - General
   - Polls
   - Show and tell

#### Mentions and Notifications

**Mention users:**
```markdown
@username can you review this?
@team/frontend-team please take a look
```

**Reference issues:**
```markdown
Related to #123
Fixes #456
See also #789
```

**Notification settings:**
- Watch: All activity
- Participating: When mentioned
- Ignore: No notifications
- Custom: Select specific events

### Collaborative Workflows

#### Forking Workflow

For open source contributions:

1. **Fork repository**
2. **Clone your fork**
   ```bash
   git clone https://github.com/your-username/repo.git
   ```
3. **Add upstream remote**
   ```bash
   git remote add upstream https://github.com/original/repo.git
   ```
4. **Keep fork updated**
   ```bash
   git fetch upstream
   git merge upstream/main
   ```
5. **Create PR from fork**

#### Feature Branch Workflow

For team collaboration:

1. **Create feature branch**
   ```bash
   git checkout -b feature/new-feature
   ```
2. **Make changes and commit**
3. **Push to origin**
   ```bash
   git push -u origin feature/new-feature
   ```
4. **Create PR**
5. **Code review**
6. **Merge to main**

### Handling Conflicts

#### Communication First

- Discuss changes before starting
- Use draft PRs for visibility
- Comment on related issues
- Regular team sync meetings

#### Technical Resolution

```bash
# Update your branch
git fetch origin
git merge origin/main

# Resolve conflicts
# Edit conflicted files
git add .
git commit -m "Resolve conflicts"
git push
```

### Team Best Practices

#### Daily Workflow

1. **Start of day:**
   ```bash
   git checkout main
   git pull origin main
   git checkout -b feature/daily-task
   ```

2. **During work:**
   - Commit frequently
   - Push to remote regularly
   - Update team on progress

3. **End of day:**
   - Push all commits
   - Update issue status
   - Create/update PR if ready

#### Code Review Guidelines

**For Authors:**
- Keep PRs small and focused
- Provide context and testing steps
- Respond to feedback promptly
- Don't take criticism personally

**For Reviewers:**
- Review within 24 hours
- Be constructive and specific
- Ask questions, don't demand
- Approve when satisfied

### Security and Access

#### Two-Factor Authentication

Enable 2FA for organization:
1. **Settings** → **Security**
2. **Require 2FA** for all members
3. Members have 7 days to enable

#### Security Policies

Create `SECURITY.md`:

```markdown
# Security Policy

## Supported Versions
| Version | Supported          |
| ------- | ------------------ |
| 1.x.x   | :white_check_mark: |
| 0.x.x   | :x:                |

## Reporting a Vulnerability
Email security@example.com

Do not create public issues for security vulnerabilities.
```

#### Secret Scanning

Enable in repository settings:
- Detects committed secrets
- Alerts administrators
- Prevents new secrets

### Integrations

#### Useful Apps

**CI/CD:**
- GitHub Actions
- CircleCI
- Travis CI

**Code Quality:**
- CodeClimate
- SonarQube
- Codecov

**Project Management:**
- Jira
- Trello
- Linear

**Communication:**
- Slack
- Microsoft Teams
- Discord

### Metrics and Insights

#### Repository Insights

View in **Insights** tab:
- Contributors
- Commit activity
- Code frequency
- Network graph
- Pulse (summary)

#### Team Performance

Track:
- PR merge time
- Review response time
- Issue resolution time
- Code coverage trends
- Deployment frequency

### Next Steps

- Review [Best Practices]({{ '/docs/best-practices' | relative_url }})
- Learn about [Pull Requests]({{ '/docs/pull-requests' | relative_url }})
- Understand [Branching & Merging]({{ '/docs/branching-merging' | relative_url }})
