[Bandit Level 30 → Level 31](https://overthewire.org/wargames/bandit/bandit31.html)

>There is a git repository at ssh://bandit30-git@localhost/home/bandit30-git/repo. The password for the user bandit30-git is the same as for the user bandit30.  

>Clone the repository and find the password for the next level.  

username: bandit30  
password: xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS  

Solution below:  
———————————————————————————————————————  
`ssh bandit30@bandit.labs.overthewire.org -p2220`  
We need a directory to clone into, again, so `mkdir /tmp/gabedini8` and `cd /tmp/gabedini8`  
Clone our repo: `git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo` 
`ls` reveals the new repo, we need to cd with the full path again, `cd /tmp/gabedini8/repo`  
Still have our README, however now it just gloats that it's 'just an empty file' let's see what else we can find  
`ls -a` reveals some interesting stuff, including what appears to be a directory called '.git' (we need to call the full filepath to get in there still, `cd /tmp/gabedini8/repo/.git`, catting and CDing some stuff in here then and we see when we `cat packged-refs` the below:  
```
# pack-refs with: peeled fully-peeled sorted 
0019ee8c6d6fd1dba2d73666b9e6339ad3314ddb refs/remotes/origin/master
831aac2e2341f009e40e46392a4f5dd318483019 refs/tags/secret
```  
Sooo I think that might be something? Looks like maybe a change/file hash referencing the original commit to the 'blank' file above and then another one. So we can see what that is with `git show 831aac2e2341f009e40e46392a4f5dd318483019` aaaand that shows what I think is a password?  

After testing it out, looks like we can log in!  

`exit`  