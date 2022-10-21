[Bandit Level 9 → Level 10](https://overthewire.org/wargames/bandit/bandit10.html)

> The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.  

username: bandit9  
password: EN632PlfYiZbn3PhVK3XOGSlNInNE00t  

Solution below:  
———————————————————————————————————————  
`ssh bandit9@bandit.labs.overthewire.org -p2220`  
`ls` confirms the file is in the home directory again, catting out the file shows a bunch of silliness, but the hint mentions equals characters, so  
`cat data.txt | grep =`  returns "grep: (standard input): binary file matches" so I'm not sure if that's feasible?  

`file data.txt` returns "data.txt: data" - so I'm not sure if that changes anything? Let's try strings since that's suggested in the hints
`man strings` displays:  
For each file given, GNU strings prints the printable character sequences that are at least 4 characters
       long (or the number given with the options below) and are followed by an unprintable character.  

Ok, so that might be helpeful, `strings data.txt` returns a bunch of short lines of characters and we do see the password as well, I added `grep ==` and that outputs some "the password is" and the password at the end, so there we go!   
`strings data.txt | grep ==`

`exit`  