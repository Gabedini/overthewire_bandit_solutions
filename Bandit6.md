[Bandit6](https://overthewire.org/wargames/bandit/bandit6.html)

> The password for the next level is stored somewhere on the server and has all of the following properties:
    owned by user bandit7  
    owned by group bandit6  
    33 bytes in size  


username: bandit6  
password: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU  

Solution below:  
———————————————————————————————————————  
`ssh bandit6@bandit.labs.overthewire.org -p2220`  
So my first idea when I hopped into this one was maybe I can just use `du` again, maybe du out like we did before from the / directory and then grep 33, but I was getting tons of stuff, so then I tried grepping "33 " to make sure it was only in the file name but I just got a bunch of permission denied messages  
I gave up on that and looked at the suggestions for this level and one of the commands is 'find', so   
`man find` - I saw the -L would do recursive, I see there was also -group and -user to check for users  
`find -L -group bandit6 -user bandit7` output way too much, removing the -L returnsn way too much info - it just keeps going and going  
removing the -L, though and we get a much smaller list, I can scroll up and see one that looks promising:  
./var/lib/dpkg/info/bandit7.password  
(However, it's lame to leave it like that) After trying to grep it out, that didn't work even with a -v to invert it and exclude 'permission denied' so I googled it, looks like we can use 2>/dev/null to indivate the message level and just send it elsewhere  
so `find -group bandit6 -user bandit7 2>/dev/null` works to output only the file we want  

`cat ./var/lib/dpkg/info/bandit7.password` and there's our password  

`exit`  