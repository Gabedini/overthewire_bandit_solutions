[Bandit Level 10 → Level 11](https://overthewire.org/wargames/bandit/bandit11.html)

> The password for the next level is stored in the file data.txt, which contains base64 encoded data  

username: bandit10  
password: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s  

Solution below:  
———————————————————————————————————————  
`ssh bandit10@bandit.labs.overthewire.org -p2220`  
`ls` confirms the file is in the home directory again, catting out the file shows something that almost looks like the passwords we've used but it's too long, assuming that's what base64 should look like per the hint. Also per the hint: man base64  

Looks like there's a -d option for decode  
`base64 -d data.txt`  and there's our password again  


`exit`  