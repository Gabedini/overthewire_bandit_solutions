[Bandit Level 13 → Level 14](https://overthewire.org/wargames/bandit/bandit14.html)

> The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on  

username: bandit13  
password: wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw  

Solution below:  
———————————————————————————————————————  
`ssh bandit13@bandit.labs.overthewire.org -p2220`  
`ls` reveals that there is a sshkey.private in the `/home/bandit13` directory  
`cat sshkey.private` outputs what appears to be a certificate, makes sense I  
So what I did was copy that output and saved it to my machine as a .pem file, similar to how we log into VSS servers  
If you run `man ssh` we see that the -i flag allows us to use an 'identity file' so let's try this:  
`ssh -i /path/to/.pem bandit14@@bandit.labs.overthewire.org -p2220`  
And that complains about permissions (0644), saying they're too open and then prompts for a password...  
A quick search reveals that 400 is what we want for permissions `chmod 400 /path/to/.pem`  
But even after trying that it's still asking for a password... I guess after re-reading the prompt above that maybe we need both?  
`cd /etc/bandit_pass` and then `file bandit14` shows we indeed can't read that file, I also tried just executing the file which didn't work  
Re-reading the prompt again makes me realize it mentions localhost, so I think we're supposed to log in via level 13  
Addmittedly I hosed this up and spent 30 minutes trying other solutions, but as long as you format the command right it's ezpz  
`ssh -i /home/bandit13/sshkey.private bandit14@localhost -p2220` logs you right in, so you can then cat out bandit14:  
`cat /etc/bandit_pass/bandit14`  

(really once you've used the key to log in you've won this level but we're snagging the password because we need it for the next level's task)


`exit`  