[Bandit Level 0 → Level 1]](https://overthewire.org/wargames/bandit/bandit1.html)  

(bandit level 0)  
> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.  
(bandit level 0 -> 1)  
> The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.  

username: bandit0  
password: bandit0  

Solution below:  
———————————————————————————————————————  
`ssh bandit0@bandit.labs.overthewire.org -p2220`  
(enter password)  
Note: I had to delete my hosts file after verifying that all the hosts in it were fine before this would let me in  
`nano ~/.ssh/known_hosts` to verify we're gucci  
then `sudo rm` that bad boi  
`ls -a` reveals a readme on the server  
`cat readme` aaaaand we have a password  
`exit`  