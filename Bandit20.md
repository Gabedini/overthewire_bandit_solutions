[Bandit Level 19 → Level 20](https://overthewire.org/wargames/bandit/bandit20.html)

> To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.  

username: bandit19  
password: awhqfNnAbc1naukrpqDYcF95h7HoMTrC  

Solution below:  
———————————————————————————————————————  
`ssh bandit19@bandit.labs.overthewire.org -p2220`  
`man setuid` per hint  
So that didn't really help, and running just `setuid` acts like nothing is installed.  
Thinking that something is missing, I ran `ls -a` which showed a 'bandit20-do' file highlighted in red, so I think that is the setuid binary they're referring to, not as in a command line binary but a binary file. 
`file bandit20-do` returns some interesting info, so let's try `bandit20-do cat /etc/bandit_pass/bandit20` - that didn't work, it's trying to use that as a command. What about executing that with some parameters?  
`./bandit20-do cat /etc/bandit_pass/bandit20` and that gives a password so I guess that's what we were to do.  

`exit`  