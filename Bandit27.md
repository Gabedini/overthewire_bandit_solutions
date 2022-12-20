[Bandit Level 26 → Level 27](https://overthewire.org/wargames/bandit/bandit27.html)

> Good job getting a shell! Now hurry and grab the password for bandit27!

username: bandit26  
password: c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1  

Solution below:  
———————————————————————————————————————  
This is one of those levels that is just necessary to know an annoying trick.  
So we know we were able to run a read command on the last level but that wasn't really a shell.  
I didn't see this in any of the Vi cheatsheets I read, but we can execute a command then specify a shell of our choice to then operate out of.  
Then we can run that shell from Vi with the `:shell` command and we're off to the races, we can explore the files instead of just reading ones that we know are existing already.  

So, if you haven't already, log back into bandit25 `ssh bandit25@bandit.labs.overthewire.org -p2220`  
Just like before, make you window really small and connect to bandit26 with the ssh command: `ssh -i /home/bandit25/bandit26.sshkey bandit26@localhost -p2220`  
Then type v to take us into Vi. Now we can set the shell with `:set-shell=/bin/bash` which will configure the shell we want to use, then we can use it by executing `:shell` and boom, we're in a normal shell.  

Now, when we simply run `ls` on bandit26's home directory we see the bandit26 text.txt that was being printed out as well as a setuid binary for bandit27 and we already know how to use those.  
So, simply `./bandit27-do cat /etc/bandit_pass/bandit27` gets us the password for the next level.  

`exit`  