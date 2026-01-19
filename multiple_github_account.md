
# GitHub Multiple Accounts (Work + Personal) on Windows using SSH

This file documents the complete setup for using multiple GitHub accounts on a single Windows machine with SSH.

---

## Goal

- Windows operating system
- Two GitHub accounts (Work and Personal)
- SSH-based authentication
- Separate Git identity per repository

---

## SSH Availability

    ssh -V  # Check if SSH is installed and show version

---

## SSH Key Generation

    ssh-keygen -t ed25519 -C "personal-email@example.com"  # Generate SSH key for personal account with email as comment
    ~/.ssh/id_ed25519_personal  # Save personal key to this file path

    ssh-keygen -t ed25519 -C "work-email@company.com"  # Generate SSH key for work account with email as comment
    ~/.ssh/id_ed25519_work  # Save work key to this file path

---

## SSH Agent

    eval "$(ssh-agent -s)"  # Start SSH agent in background and set environment variables
    ssh-add ~/.ssh/id_ed25519_personal  # Add personal SSH key to agent for authentication
    ssh-add ~/.ssh/id_ed25519_work  # Add work SSH key to agent for authentication

---

## Public Keys

    cat ~/.ssh/id_ed25519_personal.pub  # Display personal SSH public key to copy to GitHub
    cat ~/.ssh/id_ed25519_work.pub  # Display work SSH public key to copy to GitHub

GitHub → Settings → SSH and GPG Keys → New SSH Key

---

## SSH Configuration

    nano ~/.ssh/config  # Open SSH config file in nano editor to add host aliases

    Host github-personal
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_ed25519_personal

    Host github-work
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_ed25519_work

---

## SSH Alias Rules

    github-personal  
    github-work     

---

## Repository Cloning

    git clone git@github-personal:username/repository.git  # Clone repository using personal SSH alias
    git clone git@github-work:organization/repository.git  # Clone repository using work SSH alias

---

## Git Remote Commands

    git remote -v  # List all remote repositories and their URLs
    git remote add origin git@github-work:organization/repository.git  # Add remote origin using work SSH alias
    git remote set-url origin git@github-work:organization/repository.git  # Change existing remote origin URL
    git remote remove origin  # Remove the remote origin repository

---

## Branch Push

    git push -u origin branch-name  # Push branch and set upstream tracking

---

## SSH Test

    ssh -T git@github-work  # Test SSH connection to GitHub using work account
    ssh -T git@github-personal  # Test SSH connection to GitHub using personal account

---

## Git Identity (Per Repository)

    git config user.name "Your Name"  # Set Git username for commits in this repository
    git config user.email "your-email@example.com"  # Set Git email for commits in this repository

---

## Notes

- Always use SSH aliases from ~/.ssh/config
- Never use github.com-work
- Each repository can have its own Git identity

## Github Basic changes

## Check Current Global Username & Email
git config --global user.name
git config --global user.email

## change the Global Username & Email
-- git config --global user.name "Ashwini kumari"
-- git config --global user.email "abc@gmail.com"

## Delete branch in local 
-- git branch -D ""branch name
-- git branch -D bpsc_pyd

## Delete branch form github
 git push origin --delete branch name
 git push origin --delete bpsc_pyd

 ## what the use of this command
 -- git remote prune origin