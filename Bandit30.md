[Bandit Level 29 → Level 30](https://overthewire.org/wargames/bandit/bandit30.html)

>There is a git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo. The password for the user bandit29-git is the same as for the user bandit29.  

>Clone the repository and find the password for the next level.  

username: bandit29  
password: tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S  

Solution below:  
———————————————————————————————————————  
`ssh bandit29@bandit.labs.overthewire.org -p2220`  
We need a directory to clone into, again, so `mkdir /tmp/gabedini7` and `cd /tmp/gabedini7`  
Clone our repo: `git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo`  
`ls` reveals the new repo, we need to cd with the full path again, `cd /tmp/gabedini7/repo`  
`ls` shows a README.md again,catting that out shows the following:
```# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```  
This makes me think that there might be a non-prod branch.. `git branch` shows what doesn't appear to be another option, just master... after a quick search there is a '-a' flag to `git branch -a` and that shows 4 different branches so I bet one of them has our password, based on the readme it would make sense for dev to have it. We can know from the `git --help` command that there is a 'git diff' option, I think we can run this: `git diff  remotes/origin/HEAD remotes/origin/dev` and boom there is a password in our output.

`exit`  