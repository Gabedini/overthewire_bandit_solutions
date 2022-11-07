[Bandit Level 17 → Level 18](https://overthewire.org/wargames/bandit/bandit18.html)

> There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new  

> NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19.    

username: bandit17  
password: use .pem file  

Solution below:  
———————————————————————————————————————  
`ssh -i /path/to/.pem bandit17@bandit.labs.overthewire.org -p2220`  
`ls` confirms the files mentioned are there, let's cat them out, `cat passwords.old` `cat passwords.new` - appears to be a bunch of passwords, seems like at least 50 or so, too much to fit into terminal  

Per the recommended commands, 'diff' is a thing, lets' just try inputting the two files into that: `diff passwords.old passwords.new` and that does indeed return just one password so that must be it!  

`exit`  