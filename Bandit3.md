[Bandit3](https://overthewire.org/wargames/bandit/bandit3.html)

> The password for the next level is stored in a hidden file in the inhere directory.  

username: bandit3  
password: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG  

Solution below:  
———————————————————————————————————————  
`ssh bandit3@bandit.labs.overthewire.org -p2220`  
After getting logged in it looks like that 'inhere' was right in the home directory: `ls`  
Hope in that bad boy: `cd inhere`  
`ls` reveals a .hidden file, I wasn't sure if we could 'cat' that out directly, but `file .hidden` returned:  
".hidden: ASCII text"  
Which, the earlier '-' file returned that too when we checked the full filepath so we should be able to cat it  
`cat .hidden` and that reveals the password  


`exit`  