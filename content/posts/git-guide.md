---
title: "Mastering Git and GitHub on AWS Linux"
date: 2025-07-17
draft: false
---

# Mastering Git and GitHub on AWS Linux
A complete guide to setting up Git on an AWS Linux instance, managing repositories, and mastering essential Git commands.

## **1. Introduction**
Version control systems like **Git** are essential for collaborative development. GitHub and GitLab are popular platforms that host Git repositories, making it easy to manage and share code.

In this blog, you’ll learn:
- How to install **Git** on an AWS Linux instance
- How to create and push a repository to GitHub
- How to work with multiple servers and branches
- Useful Git commands for developers

---

## **2. Prerequisites**
- AWS Free Tier Account
- Basic Linux Command Line knowledge
- GitHub Account
- Git Personal Access Token (PAT)

---

## **3. Setting Up AWS Linux Instance**
1. Create an AWS account and log in to the **AWS Management Console**.
2. Launch a new **EC2 Linux instance** (choose Amazon Linux 2 AMI).
3. Select the nearest region (e.g., Mumbai).
4. Download the **.pem key** file after creating the instance.
5. Copy the public IP of the instance.

---

## **4. Connecting to AWS Linux via SSH**
Open your terminal and run:

```bash
# Set read-only permissions for the private key
chmod 400 key_name.pem

# Connect to the EC2 instance
ssh -i key_name.pem ec2-user@public-ip

```

## **5. Installing Git on AWS Linux**

Once connected, switch to root and install Git:

```
sudo su
yum update -y
yum install git -y
which git
git --version

```
## **6. Configure Git**

```
git config --global user.name "your-name"
git config --global user.email "your-email@example.com"
git config --list

```
## **7. Local Repository Setup**

On Local Server 1:

```
mkdir mumbaigit
cd mumbaigit
git init

```
Create a file:

```
cat > file1
This is our first file
# Press Ctrl+D to save

```
Add and commit:
```
git add .
git commit -m "First commit"
```
## **8. Push to GitHub**

1. Create a new repository on GitHub (e.g., centralgit).
2. Copy the repository URL.

Add remote and push:

```
git remote add origin https://github.com/username/centralgit.git
git push -u origin master

```
You’ll be asked for credentials. Use Personal Access Token as the password.

## **9. Clone Repository on Another Server**

On Local Server 2:

```
mkdir singaporegit
cd singaporegit
git init
git remote add origin https://github.com/username/centralgit.git
git pull origin master

```
## **10. Working with Branches**

```
git branch            # List branches
git branch branch1    # Create branch
git checkout branch1  # Switch to branch

```
Add a file, commit changes, and merge:

```
git merge branch1
```
## **11. Useful Git Commands**
    
 1. Stash changes
```
git stash
```
## What it does:
Temporarily saves your uncommitted changes (both staged and unstaged) so you can work on a clean working directory without committing those changes.
Useful when:

  i) You need to quickly switch branches but don't want to commit your current work.

  ii) You want to pull updates without committing local changes.

Retrieve stashed changes:

```
git stash pop
```
 2. Reset changes
```
git reset <file>      # Unstage a file (keeps changes in working directory)
git reset --hard      # Reset everything to last commit (WARNING: deletes changes)
```
What it does:

git reset <file> → Moves the file from staging area back to working directory.

git reset --hard → Discards all uncommitted changes (both staged and working directory).
Use with caution because this cannot be undone easily.

 3. Revert commit
```
git revert <commit-id>
```
What it does:
Creates a new commit that undoes the changes introduced by the specified commit.

    Safe for public branches because it does not rewrite history.

    Preferred over reset when collaborating.

 4. Remove untracked files
```
git clean -fd
```
What it does:
Deletes untracked files and directories from the working directory.

 -f → Force deletion (Git will not delete files unless you confirm with -f).

 -d → Remove directories as well.

 -x → Also removes files ignored by .gitignore.

Dry run (preview before deleting):
```
git clean -n
```
 5. Tag a version

git tag -a v1.0 -m "Version 1.0" <commit-id>

What it does:
Tags a specific commit with a human-readable name (like v1.0). Useful for marking release versions in your code history.

 -a → Annotated tag (includes metadata like author, date, message).

 -m → Message describing the tag.

List all tags:
```
git tag

Show details of a tag:

git show v1.0
```
## **12. Creating Multiple Files**

```
touch file1 file2 file3 file4
```

What it does:
Creates multiple empty files at once. Useful when setting up a new project or creating placeholders.

 All files (file1, file2, file3, file4) will appear in your working directory.




