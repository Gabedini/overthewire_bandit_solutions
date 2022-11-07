[Bandit Level 14 → Level 15](https://overthewire.org/wargames/bandit/bandit15.html)

> The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on  

username: bandit14  
password: fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq  

Solution below:  
———————————————————————————————————————  
`ssh bandit14@bandit.labs.overthewire.org -p2220`  
`ls` reveals that there is a sshkey.private in the `/home/bandit13` directory  



`exit`  