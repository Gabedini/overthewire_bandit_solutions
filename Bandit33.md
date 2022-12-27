[Bandit Level 32 → Level 33](https://overthewire.org/wargames/bandit/bandit33.html)

>After all this git stuff its time for another escape. Good luck!   

username: bandit32  
password: rmCBvG56y58BXzv98yZGdO7ATVL5dW8y  

Solution below:  
———————————————————————————————————————  
`ssh bandit32@bandit.labs.overthewire.org -p2220`  
Immediately upon logging in, we get prompted with something odd, it says "WELCOME TO THE UPPERCASE SHELL" and has >> as our line prompt...  
Immediately my thought is maybe just caps lock would work, but that seems to yield nothing. Just returns something like "sh: 1: LS: not found"  
It is actually converting everything to upper case, not needing upper case. So how do we make things lower case? Putting in quotes returns the same...  
After a little searching around, it looks like there is more than one way to do this, but mostly we're looking for a very simple trick. I was thinking that we needed to trick it to output something to maybe stderr or something like that, but it seems like if we have it return $0, then we can run commands easily enouugh. Specifically, if we return that and then check which user we are `whoami`, it appears this shell is using bandit33, and we then have permission to simply `cat /etc/bandit_pass/bandit33` and we have the password.  

So not very difficult, just need to try the proper trick.  

`exit`  