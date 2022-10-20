[Bandit1](https://overthewire.org/wargames/bandit/bandit1.html)

> The password for the next level is stored in a file called - located in the home directory.

username: bandit1  
password: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL  

Solution below:  
———————————————————————————————————————  
`ssh bandit1@bandit.labs.overthewire.org -p2220`  

`ls` revels the mentioned file  
so let's just try to cat out the contents of the file? `cat -` or `cat *` seem to do nothing...  
What kind of file is that? I'm not sure, but `file -` also does not complete  
`./-` doesn't work, so it's not an executable file   
So it turns out - is standard input, so when we run that it's just waiting for us to give input, the same as if you ran `cat` with no file, that's while `file` also   doesn't work  
But, this is actually a file, if we define the full path commands seem to work  
So `file /home/bandit1/-` returns `./-: ASCII text./-: ASCII text`  
So we can just cat it out using that (the fancier way would be to refer to our current directory with ./ instead of the full path): `cat ./-`  
`exit`  