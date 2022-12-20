[Bandit Level 27 → Level 28](https://overthewire.org/wargames/bandit/bandit28.html)

>There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo. The password for the user bandit27-git is the same as for the user bandit27.  

>Clone the repository and find the password for the next level.  

username: bandit27  
password: YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS  

Solution below:  
———————————————————————————————————————  
`ssh bandit27@bandit.labs.overthewire.org -p2220`  
We'll need somehwere to put that repo on the server, so `mkdir /tmp/gabedini5` then `cd /tmp/gabedini5`  
It mentions 'git' in the recommended binarys, `man git` will give us the info we need, we simply needs clone the repo into our directory:  
`git clone ssh://bandit27-git@localhost/home/bandit27-git/repo` complains about the port, which defaults to 22, we need to use 2220 for this server just like for our ssh connections: `git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo`  
It should prompt us for the password as if we are logging in to the server with that 'bandit27-git' user, so go ahead and paste the password. Then we can run `ls` and should se a 'repo' in our directory. `file repo` reveals it is a directory (that's how all repos will appear) so we can cd into it, 'cd repo' says the file doesn't exist but we can see that it does, so `cd /tmp/gabedini5/repo` takes us there.

Another `ls` reveals a README, `cat README` then reveals the password!

`exit`  