[Bandit2](https://overthewire.org/wargames/bandit/bandit2.html)

> The password for the next level is stored in a file called spaces in this filename located in the home directory.

username: bandit2  
password: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi  

Solution below:  
———————————————————————————————————————  
`ssh bandit2@bandit.labs.overthewire.org -p2220`  
`ls` reveals the file mentioned  
the idea is that `cat spaces in file name` won't work, we must either quote or delimit those spaces  
If we type `cat s` and then hit 'tab' it will fill out the whole thing with `cat spaces\ in\ this\ filename` and we have the password  
`cat "space in this filename"` will also work  
`exit`  