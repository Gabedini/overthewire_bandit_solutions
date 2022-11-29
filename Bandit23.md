[Bandit Level 22 → Level 23](https://overthewire.org/wargames/bandit/bandit23.html)

> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.  

> NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.  

username: bandit22  
password: WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff  

Solution below:  
———————————————————————————————————————  
`ssh bandit22@bandit.labs.overthewire.org -p2220`  
`ls -a /etc/cron.d/` looks like there is a "cronjob_bandit23" file, let's cat that out.  
`cat /etc/cron.d/cronjob_bandit23` which mentions a script, /usr/bin/cronjob_bandit22.sh, so
`cat /usr/bin/cronjob_bandit23.sh` which is below:  
———————————————————————————————————————
```#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
———————————————————————————————————————  
So per the hint above, it mentions running the script, which would make sense, since we don't know what the variable "$mytarget" is, I needed to cd in there to run it, so:  
`cd /usr/bin`  
`ls -a` reveals a lot, so `ls -a | grep cron` confirms it's there  
`./cronjob_bandit23.sh` gives us some output:   
> Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3...which doesn't help us since we're already logged in as that user, we need it for bandit23...it looks like per the script that it's MD5 hashing the username and that should be the same every time so we just needto MD5 hash the same thing to get hte proper filename to look in. So here are the commands I used:  
`mkdir /tmp/gabedini`  
`cd /tmp/gabedini`  
`touch script.sh`  
`nano script.sh` and then I pasted the above script in, but replaced the third line with "myname=bandit23"  
`chmod +x script.sh`  
`./script.sh` which outputted /tmp/8ca319486bfbbc3663ea0fbe81326349 and `cat /tmp/8ca319486bfbbc3663ea0fbe81326349` gives us a password  


`exit`  