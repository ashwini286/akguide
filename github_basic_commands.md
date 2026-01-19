
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

 ## Clean Remote Deleted Branches
 -- git remote prune origin

 ## Check Commit Log (One Line)
 git log --oneline

 ## Reset to a Specific Commit (Short Commit ID)
  git reset 19ebc4d