# Setting up your GitHub repo
*Since it's important for us to have a base level understanding of git and how that works this will be some simple setup instructions for getting things working.*

1) Set up and log into your GitHub
2) Create an empty repo, optionally check to create a readme 
3) Hop into your directory of choice, mine is ~/Programs (I create this and treat it like downs or downloads on all my computers): cd ~/Programs
4) Make a directory of your naming choice, this will become the repo: mkdir learningwilldelete
5) Hop into that directory: cd learningwilldelete
6) Initialize: git init
7) Add your username to the repo (note: global option allows it to be for all repos on your machine, leave that off for just this repo): git config user.name Gabedinlos
8) Same for email: git config user.email nunya@bidness.com
9) Add a remote origin for your repo that corresponds to step (2), note added .git to the end: git remote add origin https://github.com/Gabedinlos/learningwilldelete.git
10) Create a file in the repo: echo "hello" > hello.txt
11) Check the status of the repo: git status (note it shows a file, hello.txt, in there not added to the repo)
12) Add hello.txt to the repo: git add hello.txt
13) Check the status again to see it's now added and is awaint commit.
14) Now we can commit the changes (with a message so it doesn't prompt and we remeber what changed): git commit -m "first test"
15) Ok that worked, but oh no, it's not in the github repo! That's because we have only committed it locally, we need to push it to the repo for this to show up on GitHub.
16) Push the repo: git push (it will propmt for your password): git push https://github.com/Gabedinlos/learningwilldelete.git
17) Ope! We got an error. That's because it's not considered safe anymore to use username/password authentication. So we need to use a Personal Access Token to do it, see [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) to generate a PAT and configure it's access (we need repo and that should be it).
18) Now you can use that in place of your password with the same command: git push https://github.com/Gabedinlos/learningwilldelete.git
19) Great now it worked and things pushed! But wait, something looks off. So yeah, we screwed up but I kept it in there because that's how you learn. Basically, we're operating on the master branch. but GitHub has a branch called 'main' - so we gotta fix that:
20) We can run this to grab the stuff GitHub has that we don't: git pull --allow-unrelated-histories https://github.com/Gabedinlos/learningwilldelete
21) We can see that we have the readme now when checking status: git status
22) Now that we have our readme file, we need to commit it to our local repo: git commit -m "yepp"
23) We can then push the changes and we have both hello.txt and the readme.md in the same branch: git push https://github.com/Gabedinlos/learningwilldelete.git
24) But wait, we still have two branches and don't really need those, we can fix that by merging the two branches: git branch -m master main 
25) Then pushing the update: git push -u origin main
Basically, now it looks correct on GitHub and locally we're running on the main branch (git branch to check). We could delete that branch if we wanted to, but it doesn't hurt anything so we'll leave it for now.
### *Basically half of those steps could have been avoided if we had simply cloned the repo into ~/Programs instead of inititalizing a repository and horsing around that way, but then we wouldn't have learned as much!*