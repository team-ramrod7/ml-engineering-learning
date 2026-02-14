# Git Cheat Sheet for ML Engineering

## Daily Workflow
```bash
# Check what's changed
git status

# Stage files
git add filename.py      # Specific file
git add .                # Everything in current directory

# Commit (save snapshot)
git commit -m "Descriptive message about what you did"

# Push to GitHub
git push
```

## Viewing History
```bash
git log --oneline        # Compact history
git log --graph          # Visual branch diagram
git diff                 # See unstaged changes
git diff --staged        # See staged changes
```

## Undoing Things (Use Carefully!)
```bash
# Unstage a file (keep changes)
git reset filename.py

# Discard changes to a file (PERMANENT!)
git checkout -- filename.py

# Undo last commit (keep changes)
git reset --soft HEAD~1

# View a previous version
git show commit_hash:filename.py
```

## Branching (For Later)
```bash
# Create new branch
git branch feature-name

# Switch to branch
git checkout feature-name

# Create and switch in one command
git checkout -b feature-name

# Merge branch into main
git checkout main
git merge feature-name
```

## GitHub Operations
```bash
# Clone a repository
git clone https://github.com/username/repo.git

# Pull latest changes
git pull

# View remote info
git remote -v
```

## Useful Aliases (Add to ~/.zshrc)
```bash
alias gs='git status'
alias ga='git add'
alias gc='git commit -m'
alias gp='git push'
alias gl='git log --oneline'
```

## Emergency: "I Messed Up!"
```bash
# See what you can recover
git reflog

# Go back to a previous state
git reset --hard commit_hash
```

## Good Commit Message Examples

✅ "Add hypersonic solver Python translation"
✅ "Fix bug in Reynolds number calculation"
✅ "Complete Week 1 Python fundamentals"
✅ "Implement vectorized force coefficient computation"

❌ "updates"
❌ "fixed stuff"
❌ "asdf"

---

*Keep this file updated as you learn new Git commands*