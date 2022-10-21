[Bandit Level 4 → Level 5](https://overthewire.org/wargames/bandit/bandit5.html)

> The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

username: bandit4  
password: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe  

Solution below:  
———————————————————————————————————————  
`ssh bandit4@bandit.labs.overthewire.org -p2220`  
`ls` reveals 'inhere' is in the same spot as last time so `cd inhere` gets us there  
Then we see with `ls` that there are 10 files in this directory, but we don't know which one is the 'human readable one'  
`file *` for checking all of them with the asterisk wildcard returns something goofy:  
file: Cannot open `ile00' (No such file or directory)  
file: Cannot open `ile01' (No such file or directory)  
file: Cannot open `ile02' (No such file or directory)  
file: Cannot open `ile03' (No such file or directory)  
file: Cannot open `ile04' (No such file or directory)  
file: Cannot open `ile05' (No such file or directory)  
file: Cannot open `ile06' (No such file or directory)  
file: Cannot open `ile07' (No such file or directory)  
file: Cannot open `ile08' (No such file or directory)  
file: Cannot open `ile09' (No such file or directory)  

The names aren't printing right - but oh wait, the file names start with "-" again, it seems like the shell is interpreting the '-f' as a command of some sort?  
Not sure but it looks like the earlier level where if we call the full filepath it might work: file /home/bandit4/inhere/*  
Which it does, we see that only "/home/bandit4/inhere/-file07: ASCII text" is the human readable and is the one we want:  
`cat /home/bandit4/inhere/-file07` gives us the password.  
  
`exit`  