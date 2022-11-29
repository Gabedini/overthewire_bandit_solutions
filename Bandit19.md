[Bandit Level 18 → Level 19](https://overthewire.org/wargames/bandit/bandit19.html)

> The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.  

username: bandit18  
password: hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg  

Solution below:  
———————————————————————————————————————  
`ssh bandit18@bandit.labs.overthewire.org -p2220`  
Aaaaand look at that it just said byebyebye and ends the connection  
maybe we can send the command through quicklike and just append it on the end? `ssh bandit18@bandit.labs.overthewire.org -p2220 | cat readme`  
That appears to try to run that on my machine in the directory I'm in before the ssh....  
`man ssh` this unfortunately didn't yield a whole lot other than the below which confirms it can be done but I'm not sure how based on the man page:    
> If a command is specified, it will be executed on the remote host instead of a
     login shell.  A complete command line may be specified as command, or it may
     have additional arguments.  If supplied, the arguments will be appended to the
     command, separated by spaces, before it is sent to the server to be executed.
Upon some searching, [this](https://stackoverflow.com/questions/9816769/how-to-ssh-into-a-remote-host-and-execute-a-command-immediately) page was found, which mentions the `-t` flag with a command in quotes, I think that's what  need  
`ssh -t bandit18@bandit.labs.overthewire.org -p2220 "cat readme"`
After entering our password, it logs us out... but it has a password, too!

`exit`  