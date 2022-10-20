[Bandit7](https://overthewire.org/wargames/bandit/bandit7.html)

> The password for the next level is stored somewhere on the server and has all of the following properties:  
    owned by user bandit7  
    owned by group bandit6  
    33 bytes in size  


username: bandit7  
password: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S  

Solution below:  
———————————————————————————————————————  
`ssh bandit7@bandit.labs.overthewire.org -p2220`  
The password for the next level is stored in the file data.txt next to the word millionth

`exit`  