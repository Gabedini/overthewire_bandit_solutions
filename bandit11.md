[Bandit Level 10 → Level 11](https://overthewire.org/wargames/bandit/bandit10.html)

> The password for the next level is stored in the file data.txt, which contains base64 encoded data  

username: bandit10  
password: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s  

Solution below:  
———————————————————————————————————————  
`ssh bandit10@bandit.labs.overthewire.org -p2220`  
`ls` confirms the file is in the home directory again, catting out the file shows a bunch of silliness, but the hint mentions equals characters, so  


`exit`  