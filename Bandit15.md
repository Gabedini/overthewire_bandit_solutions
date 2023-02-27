[Bandit Level 14 → Level 15](https://overthewire.org/wargames/bandit/bandit15.html)

> The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.  

username: bandit14  
password: fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq  

Solution below:  
———————————————————————————————————————  
`ssh bandit14@bandit.labs.overthewire.org -p2220`  
I don't think ssh or telnet is useful based on the prompt above, but nc sounds promising  
`man nc` and that says "It can open TCP connections, send UDP packets" which sounds double promising  
In that man page I got down to the 'client/server model' and then read it incorrectly and tried the -l flag. After reading again I realized that we don't need to listen but to connect to a process already listening. So we need the -N flag: `nc -N localhost 30000`  
That opens up a connection and when we paste password in there, per the man pages instructions, we get a reply back with our password for the next level!


`exit`  