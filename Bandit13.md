[Bandit Level 12 → Level 13](https://overthewire.org/wargames/bandit/bandit13.html)

> The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)  

username: bandit12  
password: JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv  

Solution below:  
———————————————————————————————————————  
`ssh bandit12@bandit.labs.overthewire.org -p2220`  
`ls` confirms the file is in the home directory again and we cat it and it looks like what we want but we can't read it, no surprise it's hex  
Per the recommendation, making a directory and copying the file over `mkdir /tmp/gabedini` then `cp data.txt /tmp/gabedini/` and hop in there to do stuff `cd /tmp/gabedini`  
So looking at the suggested binaries xxd looks promising, since we need to un-hexdump that first, `man xxd`  shows that yep you can reverse a hexdump wiht this... looks like -r or -revert should be our key so let's throw that in a file `xxd -r data.txt > newdata.txt` then catting that out, `cat newdata.txt` which looks different so I thinnk we made progress?  
Maybe this will show as a different file even with .txt, so `file newdata.txt` shows that yes, appears to have been a .bin file that was gzipped...soo `man gzip`  
Oh wait, we see at the top there's a `gunzip`, let's try `gunzip newdata.txt > newnewdata.txt` which throws an error...  
I think maybe it's because the file isn't a .gz? We can use mv to rename the file, `mv newdata.txt newdata.gz`  and then, I just ran gnuzip directly on that file wiht `gunzip newdata.gz` and it accepted it, I thought it would make me specify a new file, but it looks like it just made one anyway, which running `file newdata` (the new file with no extnsion) shows a bzip2 file format, so I think we made progress!?  
Per the man page it looks like there's an unzip for bzip2, bunzip2, so `bunzip2 newdata` and now ls reveals it has a .out file extension and file shows we're back to gzip  
`mv newdata.out newestdata.gz` and then `gunzip newdata.out` and we have no file extnsion again but it shows to be "POSIX tar archive" so `man tar`...but either I'm reading it wrong or that doesn't make sense to me..Googling revealed this command, which just mostly shows me that the og file is "data5.bin" `tar -tvf newestdata`. Oh, looks like this will extract a file `tar -xvf newestdata` See [this page](https://linuxhint.com/untar_files_linux/) for the desciption of those tags.  
Although that data5.bin just shows posix tar archive still, I can't cat it out, try again?..that produces data6.bin which is back to bzip2...  
`bunzip2 data6.bin`  produces data6.bin.out and back to tar  
`tar -xvf data6.bin.out`  produces data8.bin which is gz zipped, `mv data8.bin data8.gz` and then `gunzip data8.gz` produces data8 which we can cat out  

There is our password


`exit`  