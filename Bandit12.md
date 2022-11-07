[Bandit Level 11 → Level 12](https://overthewire.org/wargames/bandit/bandit12.html)

> The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions  

username: bandit11  
password: 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM  

Solution below:  
———————————————————————————————————————  
`ssh bandit11@bandit.labs.overthewire.org -p2220`  
`ls` confirms the file is in the home directory again and we cat it and it looks like what we want but we can't read it
I think strings has an option to shift? `man strings`....mmm not seeing that..I don't think grep or uniq will help, sort didn't have much when we used that earlier, base64 naw and I doubt gzip or bzip2 either, so `man tr`, tr means translate, so that sounds promising, but there are not any usage examples...  
So I searched and found echo `'linuxize' | tr 'l-n' 'w-z'` as an example, but when I tried something like this: `cat data.txt | tr 'm-k' 'a-z'` it complained about m-k being out of order... then I found [this](https://unix.stackexchange.com/questions/19772/how-does-tr-a-z-n-za-m-work) and that showed the format we are looking for, I just piped it twice, once for upper and one for lower case:  
`cat data.txt | tr 'a-z' 'n-za-m' | tr 'A-Z' 'N-ZA-M'`

and there's our answer  

`exit`  