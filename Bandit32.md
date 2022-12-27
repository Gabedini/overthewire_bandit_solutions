[Bandit Level 31 → Level 32](https://overthewire.org/wargames/bandit/bandit32.html)

>There is a git repository at ssh://bandit31-git@localhost/home/bandit31-git/repo. The password for the user bandit31-git is the same as for the user bandit31.  

>Clone the repository and find the password for the next level.  

username: bandit31  
password: OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt  

Solution below:  
———————————————————————————————————————  
`ssh bandit31@bandit.labs.overthewire.org -p2220`  
We need a directory to clone into, again, so `mkdir /tmp/gabedini9` and `cd /tmp/gabedini9`  
This is the same as the last one too, with updated numbers: `git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo` 
`ls` reveals the new repo, we need to cd with the full path again, `cd /tmp/gabedini9/repo`  
Still have our README, but this time it gives us instructions:
```
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```  
Well, I guess let's make that file, `nano key.txt` then paste in that sentence. "ls" to make sure it saved right.  
So, since we went over adding/pushing files in the setup for this series, we know roughly how this goes. `git branch` confirms we're on master - `git add *` (could specify by name but this is easier) to add the new file...except that gives an error, we need to add -f flag to that command, `git add -f * `. 'git status' shows the file added, we commit with `git commit -m "does this work?"` which seems to succeed. Now we just need to push it to the remote repo, which should be the same as our clone command but with push: `git push ssh://bandit31-git@localhost:2220/home/bandit31-git/repo`  and boom, there it outputs in the push confirmation our next password!  

`exit`  