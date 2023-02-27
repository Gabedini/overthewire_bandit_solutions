[Bandit Level 15 → Level 16](https://overthewire.org/wargames/bandit/bandit16.html)

> The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.  
`Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…`  


username: bandit15  
password: jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt  

Solution below:  
———————————————————————————————————————  
`ssh bandit15@bandit.labs.overthewire.org -p2220`  
Doesn't look like there are any ssl mentions in the man page for nc...  
While I was trying to verify that I came across this example instead: `openssl s_client -connect <someserver>:`, so let's try that since it seems to be in the recommended list anyway  
`openssl s_client -connect localhost:30001` spits out a bunch of stuff but if we ignore than and just send over the password it gives us another password back so we got it!  

`exit`  