
```markdown
# DeepSeek Linux Tips

## Git Workflow Essentials

### Repository Setup
```bash
# Initialize new repo
git init

# Connect to remote (GitHub/GitLab)
git remote add origin https://github.com/user/repo.git

# First push (sets upstream)
git push -u origin main
```

### Branch Management
```bash
# Create and switch to new branch
git checkout -b feature_branch

# Merge branches
git merge source_branch

# Delete local branch
git branch -d old_branch
```

### Version Control
```bash
# Tag a release
git tag -a v1.0 -m "Release version"

# Revert to tag
git checkout v1.0
```

## Common Git Issues & Fixes

### Merge Conflicts
1. Identify conflicted files with `git status`
2. Edit files to resolve conflicts
3. Mark as resolved:
```bash
git add resolved_file
git commit
```

### Detached HEAD Recovery
```bash
git checkout -b temp-branch  # Save changes
git merge temp-branch main   # Apply to main
```

## Linux System Tips

### File Operations
```bash
# Secure copy
scp file.txt user@remote:/path

# Bulk rename
rename 's/old/new/' *.txt
```

### Process Management
```bash
# Find and kill process
pgrep -f "process_name" | xargs kill

# Persistent services
sudo systemctl enable service_name
```

### Network Tools
```bash
# Test connectivity
ping -c 4 google.com

# Check open ports
ss -tulnp
```

## Advanced Git

### Rewriting History
```bash
# Interactive rebase (last 3 commits)
git rebase -i HEAD~3

# Amend last commit
git commit --amend
```

### Submodules
```bash
git submodule add https://github.com/user/repo
git submodule update --init --recursive
```

---

> Pro Tip: Always `git pull` before pushing to avoid conflicts!  
> Remember: `--force` pushes should be used sparingly.
```

To add this to your repo:

1. Save the file as `deepseek_linux_tips.md` in your repo directory
2. Run:
```bash
git add deepseek_linux_tips.md
git commit -m "Add comprehensive Linux/Git tips file"
git push origin main
```

The file covers:
- All Git commands we've used
- Troubleshooting scenarios
- General Linux commands
- Best practices

