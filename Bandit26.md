[Bandit Level 25 → Level 26](https://overthewire.org/wargames/bandit/bandit26.html)

> Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.  

username: bandit25  
password: p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d  

Solution below:  
———————————————————————————————————————  
`ssh bandit25@bandit.labs.overthewire.org -p2220`  
an ls shows an sshkey for what I'm assuming is bandit26 as soon as we log in, so we can `ssh -i /home/bandit25/bandit26.sshkey bandit26@localhost -p2220` aaaand the connection is immediately closed.  

`ssh -i /home/bandit25/bandit26.sshkey -t bandit26@localhost -p2220 "cat /etc/bandit_pass/bandit26"`  

The below command should give us some info about the shell bandit26 is using. See [here](https://linuxconcept.com/understanding-the-etc-passwd-and-etc-shadow-files/) for more info:  
`cat /etc/passwd`  
> bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext  
I'm not sure if we can call that a shell per se, but it is more info!  
`cat /usr/bin/showtext`  
```
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```  
Now, I personally went down many a rabbit hole before the solution was made clear to this one. This used to be the final level, so it's a little extreme. Let's skip the commands I tried but the main thing that tricked me was that I found a variation of the SSH command that let me connect and just provided me with a blank cursor that I could type in and hit enter but nothing would happen. I tried many variations of commands to see if that would let me 'break out' of it but nothing worked.  

What is correct was my first gut feeling that I ignored and that is to look at the script above and see the 'more' command and then go to 'man more'  
In the 'more' binary there is an option to type `!command` and run commands, but I couldn't get anything to work with that. What there is, though, is 'v' which opens up a Vi editor which you can run commands inside.  
But the idea here is that 'more' let's you view text line by line, similar to how man pages work, when it doesn't all fit on the screen. Since that displays when you log in, and it calls that text.txt (doesn't really matter what it displays). So shrink your terminal window down to as few of lines as it will let you and execute your ssh command: `ssh -i /home/bandit25/bandit26.sshkey bandit26@localhost -p2220` and ensure that you see the 'more' ticker at the bottom.  

If you see the 'more' ticker, then you can type 'v' to execute the more command to open [Vi](https://www.thegeekdiary.com/basic-vi-commands-cheat-sheet/), then you can type ":r /etc/bandit_pass/bandit26." The colon indicates to Vi that you want to run a command and 'r' means read/import a file into the current one you're editingd. Once you have hit enter, you can make your terminal window larger again and you should see near the top by the bandit26 ascii art, the password!: c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1  

`exit`  