[Bandit Level 8 → Level 9](https://overthewire.org/wargames/bandit/bandit9.html)

> The password for the next level is stored in the file data.txt and is the only line of text that occurs only once  

username: bandit8  
password: TESKZC0XvTetK0S9xNwm25STk5iWrBvP  

Solution below:  
———————————————————————————————————————  
`ssh bandit8@bandit.labs.overthewire.org -p2220`  
`ls` confirms the file is in the home directory again
I'm just gonna cat it out to see what's in this file, `cat data.txt`  
So it's a bunch of passwords, apparently only one is unique then  
I see uniq is a binary according to the hints, `man uniq` the first flag for uniq is "-c, --count: prefix lines by the number of occurrences", so I think we could do that and see what it does: `uniq -c data.txt`...well that did'nt work it just added a 1 before every line  
Well, I tried several variants of uniq with -u, -z, and -c and they all just printed the whole file it seems (well, I suppose probs 1 occurance of each password?)   

I tried `sort data.txt` since that's another recommended binary, which does allow me to manually find the binary, it looks like all the other passwords occur 10 times🤔  
Ooook, so if I do `sort` then pipe to `uniq -c` it outputs proper counts, so then I should be able to grep for 1 and we'll be gucci  
`sort data.txt | uniq -c | grep "1 "` - note a space is necessary, since the others occur 10 times, but we did get our password, so nice!  
Korbyn's more clean solutions: `sort data.txt | uniq -u`

`exit`  