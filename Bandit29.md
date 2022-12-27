[Bandit Level 28 → Level 29](https://overthewire.org/wargames/bandit/bandit29.html)

>There is a git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo. The password for the user bandit28-git is the same as for the user bandit28.  

>Clone the repository and find the password for the next level.  

username: bandit28  
password: AVanL161y9rsbcJIsFHuw35rjaOM19nR  

Solution below:  
———————————————————————————————————————  
`ssh bandit28@bandit.labs.overthewire.org -p2220`  
We need a directory to clone into, again, so `mkdir /tmp/gabedini6` and `cd /tmp/gabedini6`  
This is the same as the last one too, with updated numbers: `git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo`  
`ls` reveals the new repo, we need to cd with the full path again, `cd /tmp/gabedini6/repo`  

`ls` shows a README.md again,catting that out shows the following:
```
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```  
So we see that there is a file in here, that had (has?) the password in it. So what can we do with that? Well `git --help` has some useful info, if you've entered any incorrect commands so far you know that exists.  
In there we see a few things, on that might be of use is `git branch` which just confirms we're on the master branch, ok. `git log` though is intererting. When running that, it shows 3 differet edits like the below:
```
commit 5f45cfaca938393c7706fec16ab1ca627e947f64 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Sat Dec 3 08:14:06 2022 +0000

    fix info leak

commit f08ee321c5f564b2da90789fac14b5ae2e55c56c
Author: Morla Porla <morla@overthewire.org>
Date:   Sat Dec 3 08:14:06 2022 +0000

    add missing data

commit 6968b2ffdcc317a1aeb2ebfb54259f860a390354
Author: Ben Dover <noone@overthewire.org>
Date:   Sat Dec 3 08:14:06 2022 +0000

    initial commit of README.md
```  
So those different commits sound promising, perhaps the first one has the password unhidden? Or Maybet he second one? We can see by 'going back in time' but running `git checkout 6968b2ffdcc317a1aeb2ebfb54259f860a390354`  to see the first one. `ls` shows we still only have the README in there.  Catting it out shows that the password is there but hasn't been set yet.  
`git checkout f08ee321c5f564b2da90789fac14b5ae2e55c56c` reveals the same, but when we cat out the readme, the password is there, and it's in plaintext!  


`exit`  