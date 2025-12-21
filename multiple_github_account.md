
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

    ssh -V

---

## SSH Key Generation

    ssh-keygen -t ed25519 -C "personal-email@example.com"
    ~/.ssh/id_ed25519_personal

    ssh-keygen -t ed25519 -C "work-email@company.com"
    ~/.ssh/id_ed25519_work

---

## SSH Agent

    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_ed25519_personal
    ssh-add ~/.ssh/id_ed25519_work

---

## Public Keys

    cat ~/.ssh/id_ed25519_personal.pub
    cat ~/.ssh/id_ed25519_work.pub

GitHub → Settings → SSH and GPG Keys → New SSH Key

---

## SSH Configuration

    nano ~/.ssh/config

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

    git clone git@github-personal:username/repository.git
    git clone git@github-work:organization/repository.git

---

## Git Remote Commands

    git remote -v
    git remote add origin git@github-work:organization/repository.git
    git remote set-url origin git@github-work:organization/repository.git
    git remote remove origin

---

## Branch Push

    git push -u origin branch-name

---

## SSH Test

    ssh -T git@github-work
    ssh -T git@github-personal

---

## Git Identity (Per Repository)

    git config user.name "Your Name"
    git config user.email "your-email@example.com"

---

## Notes

- Always use SSH aliases from ~/.ssh/config
- Never use github.com-work
- Each repository can have its own Git identity
