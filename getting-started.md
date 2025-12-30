---
layout: default
title: Getting Started
---

## Getting Started with GitHub

This guide will help you set up and start using GitHub for your projects.

### Prerequisites

Before you begin, ensure you have:
- A GitHub account ([Sign up here](https://github.com/join))
- Git installed on your local machine
- Basic understanding of command line/terminal

### Setting Up Git

1. **Install Git**
   - Windows: Download from [git-scm.com](https://git-scm.com)
   - Mac: Install via Homebrew: `brew install git`
   - Linux: `sudo apt-get install git` (Ubuntu/Debian)

2. **Configure Git**
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

3. **Verify Installation**
   ```bash
   git --version
   ```

### Creating Your First Repository

#### On GitHub.com

1. Click the **+** icon in the top right corner
2. Select **New repository**
3. Enter a repository name
4. Choose public or private
5. Initialize with a README (optional)
6. Click **Create repository**

#### From Command Line

```bash
# Create a new directory
mkdir my-project
cd my-project

# Initialize Git
git init

# Create a README file
echo "# My Project" >> README.md

# Add and commit
git add README.md
git commit -m "Initial commit"

# Connect to GitHub (replace with your repo URL)
git remote add origin https://github.com/username/repository.git
git branch -M main
git push -u origin main
```

### Cloning an Existing Repository

```bash
git clone https://github.com/username/repository.git
cd repository
```

### Basic Git Commands

| Command | Description |
|---------|-------------|
| `git status` | Check the status of your repository |
| `git add <file>` | Stage files for commit |
| `git commit -m "message"` | Commit staged changes |
| `git push` | Push commits to remote repository |
| `git pull` | Pull latest changes from remote |

### Authentication

**Personal Access Token (Recommended)**

1. Go to Settings → Developer settings → Personal access tokens
2. Generate new token (classic)
3. Select scopes (repo, workflow, etc.)
4. Copy and save the token securely
5. Use token as password when pushing

**SSH Keys**

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Add to ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard
cat ~/.ssh/id_ed25519.pub
```

Then add the SSH key to your GitHub account in Settings → SSH and GPG keys.

### Next Steps

- Learn about [Repository Basics]({{ '/repository-basics' | relative_url }})
- Understand [Branching & Merging]({{ '/branching-merging' | relative_url }})
- Explore [Pull Requests]({{ '/pull-requests' | relative_url }})

### Common Issues

**Authentication Failed**
- Use personal access token instead of password
- Check if SSH keys are properly configured

**Permission Denied**
- Verify you have access to the repository
- Check your authentication method

**Merge Conflicts**
- Pull latest changes before starting work
- Communicate with team members
