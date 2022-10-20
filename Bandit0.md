[Bandit0](https://overthewire.org/wargames/bandit/bandit0.html)

> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

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