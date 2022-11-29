[Bandit Level 21 → Level 22](https://overthewire.org/wargames/bandit/bandit22.html)

> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.  

username: bandit21  
password: NvEJF7oVjkddltPSrdKEFOllh9V1IBcq  

Solution below:  
———————————————————————————————————————  
`ssh bandit21@bandit.labs.overthewire.org -p2220`  
`ls -a /etc/cron.d/` looks like there is a "cronjob_bandit22" file, let's cat that out.  
`cat /etc/cron.d/cronjob_bandit22` which mentions a script, /usr/bin/cronjob_bandit22.sh, so
`cat /usr/bin/cronjob_bandit22.sh` which is below:
> #!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

So we should be able to just cat that other file out, assuming we have permissions? `cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`  

aaaand yeah we do so there we go

`exit`  