[Bandit Level 20 → Level 21](https://overthewire.org/wargames/bandit/bandit21.html)

> There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).  

username: bandit20  
password: VxCazJaVykI6W36BkBU0mJTCM8rR95XT  

Solution below:  
———————————————————————————————————————  
`ssh bandit20@bandit.labs.overthewire.org -p2220`  
`ls` confirms the file's presence.  

The description for this levels sounds similar to when we had to send data in earlier levels to specific ports, so maybe we can do the same? I guess the only question is does it matter which port?  
`./suconnect 30000` opens a connection but if I paste in the password for this level it doesn't seemt to do anything? I also tried this but not matter how I format it, I get an incorrect password error: `./suconnect 22 VxCazJaVykI6W36BkBU0mJTCM8rR95XT`  
`cat suconnect` does reveal this, though: 
> This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.  

So I think we need to set up a listening item and then try to connect to that, which IIRC I think we can do with netcat?
`man nc` reveals that I think we can just do `nc -l 1234`  to listen and I suppose from another window run the suconnect?  
Close - so what I did was run the netcat command above, then open a second ssh connection and ran `./suconnect 1234` which appeared to then be listening as well. I pasted in the password into this window, which didn't do anything, but when I pasted it in the terminal running the netcat command then it updated on the suconnect side and output the below:

Read: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
Password matches, sending next password

and on the netcat window it returned the password!

`exit`  