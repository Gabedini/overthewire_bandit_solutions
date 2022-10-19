[Bandit5](https://overthewire.org/wargames/bandit/bandit5.html)

> The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
    human-readable
    1033 bytes in size
    not executable


username: bandit5
password: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

Solution below:
———————————————————————————————————————
`ssh bandit5@bandit.labs.overthewire.org -p2220`
`ls` reveals the inhere, `cd inhere` gets us there.
ls reveals a whole bunch of 'maybe here' that are purple in my terminal, file * shows they're all directories.
`cd maybehere00` and then `ls` shows that there are several files in each, some with spaces, some starting with -, so we probbaly have at least 100 files
I cat-ed out the first one just to see and it looks like a super long string, file says 'ASCII text, with very long lines (1038)'

So, checking the list of commands supplied for this level: ls , cd , cat , file , du , find
We already have used cat, ls, cd, and file - while file will help us know if it's human readable I'm not sure how much it'll do, ls, lists stuff and we can could do that but that might be a headache, but du shows us the size of files per `man du` - I see there is a -a flag per the man page so when I ran just 'du -a' from /inhere it listed the files recursively through all the subdirectories so that is nice
Turns out there is also a -b flag which I noticed in the man pages, so we can use and that will display the sizes in bytes, which is helpful since we know 1033 bytes
I do see a file in there but that's kind of lame since it's just everything and to just manually check it hurts my brain so just bringing in some previous knowledge we can use grep to look for 1033.
Grep basically takes an argument and searches for it in every line of an output and then lists every line containing that argument: `du -ab --apparent-size | grep 1033`
returns one file: 1033	./maybehere07/.file2
cating out that file revels what appears to be a password! (and a bunch of white space, but we can ignore that because we got our answer)

`exit`