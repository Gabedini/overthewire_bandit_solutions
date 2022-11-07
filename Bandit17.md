[Bandit Level 16 → Level 17](https://overthewire.org/wargames/bandit/bandit17.html)

> The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.  



username: bandit16  
password: JQttfApK4SeyHwDlI9SXGR50qclOAil1  

Solution below:  
———————————————————————————————————————  
`ssh bandit16@bandit.labs.overthewire.org -p2220`  
If I remember right from when I was reading the nc man page it has an option to scan..
Well, so running `nc -zv localhost 31000-32000` outputs stuff but grepping for 'succeed' or any other variation doesn't seem to work even though I can see them in the output.. sooo  `man nmap` I suppose...this tool is so expansive i scrolled down to the examples and found `nmap -v scanme.nmap.org`  which I think we can use with the -p flag for `nmap -v localhost -p 31000-32000`  

Hey, that returns 5 ports that seem to have somethign on them? I'm not against brute forcing with only 5 options.  
`nc -N localhost 31960` yadda yadda, only the last three returned anything, but also I forgot about ssl... oops  

`openssl s_client -connect localhost:31790` returns a certificate so it looks like we're good! (don't forget to `chmod 400` that after saving as a .pem!)  


`exit`  