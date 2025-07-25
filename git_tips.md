# **Git Usage Guide: Comprehensive Documentation**  
*Based on our discussions about Git, branches, versioning, and troubleshooting*  

---

## **Table of Contents**  
1. [Basic Git Commands](#1-basic-git-commands)  
2. [Branch Management](#2-branch-management)  
3. [Version Control & Tags](#3-version-control--tags)  
4. [Reverting to Previous Versions](#4-reverting-to-previous-versions)  
5. [Pushing & Pulling Changes](#5-pushing--pulling-changes)  
6. [Troubleshooting](#6-troubleshooting)  
7. [Picom & Kvantum Fixes (Bonus)](#7-picom--kvantum-fixes-bonus)  

---

## **1. Basic Git Commands**  
### **Initialize a Repository**  
```sh
git init
```
### **Clone a Repository**  
```sh
git clone <repository-url>
```
### **Check Status**  
```sh
git status
```
### **Stage Changes**  
```sh
git add <file>       # Add specific file
git add .            # Add all changes
```
### **Commit Changes**  
```sh
git commit -m "Your commit message"
```
### **View Commit History**  
```sh
git log --oneline    # Compact view
git log -p           # Detailed changes
```

---

## **2. Branch Management**  
### **List Branches**  
```sh
git branch           # Local branches
git branch -a        # All branches (local + remote)
```
### **Create & Switch to a New Branch**  
```sh
git checkout -b <branch-name>      # Old syntax
git switch -c <branch-name>        # New (Git ≥ 2.23)
```
### **Switch to an Existing Branch**  
```sh
git checkout <branch-name>
git switch <branch-name>
```
### **Delete a Branch**  
```sh
git branch -d <branch-name>        # Safe delete (checks merges)
git branch -D <branch-name>        # Force delete (unmerged changes)
```
### **Push a Branch to Remote**  
```sh
git push -u origin <branch-name>   # First push (sets upstream)
git push                           # Subsequent pushes
```

---

## **3. Version Control & Tags**  
### **List Tags**  
```sh
git tag -l
```
### **Create a Tag**  
```sh
git tag v1.0.0 -m "Release version 1.0.0"
```
### **Push Tags to Remote**  
```sh
git push origin --tags
```
### **Checkout a Tag (Read-Only)**  
```sh
git checkout v1.0.0
```
### **Create a Branch from a Tag**  
```sh
git checkout -b <new-branch> v1.0.0
```

---

## **4. Reverting to Previous Versions**  
### **Find Old Commits**  
```sh
git log --oneline    # Copy the commit hash (e.g., `a1b2c3d`)
```
### **Revert to a Specific Commit**  
#### **Method 1: Soft Reset (Keeps Changes)**  
```sh
git reset --soft a1b2c3d
```
#### **Method 2: Hard Reset (Discards Changes)**  
```sh
git reset --hard a1b2c3d   # ⚠️ Destructive! Use carefully.
```
#### **Method 3: Revert (Safe for Shared Branches)**  
```sh
git revert a1b2c3d         # Creates a new undo commit
```
### **Rollback to a Tag**  
```sh
git checkout -b rollback-branch v0.7.1
```

---

## **5. Pushing & Pulling Changes**  
### **Push Changes to Remote**  
```sh
git push origin <branch-name>
```
### **Force Push (Overwrites Remote History)**  
```sh
git push --force origin <branch-name>   # ⚠️ Use with caution!
```
### **Pull Latest Changes**  
```sh
git pull origin <branch-name>
```
### **Fetch Remote Branches**  
```sh
git fetch origin
```

---

## **6. Troubleshooting**  
### **Recover Lost Commits**  
```sh
git reflog                   # Find lost commits
git checkout HEAD@{1}        # Restore
```
### **Fix Merge Conflicts**  
1. Open conflicted files and resolve manually.  
2. Mark as resolved:  
```sh
git add <file>
git commit
```
### **Undo Last Commit**  
```sh
git reset --soft HEAD~1      # Keeps changes staged
git reset --hard HEAD~1      # Discards changes
```

## **Final Notes**  
- **Always** check `git status` before making changes.  
- **Avoid `--force` on shared branches** unless necessary.  
- **Tags are immutable**—use them for releases.  

For advanced Git workflows, explore:  
- `git stash` (temporarily save changes)  
- `git rebase` (rewrite commit history)  
- `git cherry-pick` (copy specific commits)  

Let me know if you need further clarifications! 🚀
