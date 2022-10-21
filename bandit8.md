[Bandit Level 7 → Level 8](https://overthewire.org/wargames/bandit/bandit8.html)

> The password for the next level is stored in the file data.txt next to the word millionth  


username: bandit7  
password: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S  

Solution below:  
———————————————————————————————————————  
`ssh bandit7@bandit.labs.overthewire.org -p2220`  
`ls` confirms it's in our home directory already, don't have to search for it  
based on the clue for this level, I'm guessing millionth only occurs once, either the millionth character or line, classic spot to use grep and snag the whole line that's on  
`cat data.txt | grep millionth` and wow there it be, we could clean that up some more but meh, it is already pretty clean  

`exit`  