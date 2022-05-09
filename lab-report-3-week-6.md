# Lab Report 3 (week 6 - 5/8/2022)

## Group Choice 1: Streamlining SSH

This wasn't difficult at all. I just opened the config file in /.ssh/ with notepad and unexpectedly found that the SSH plugin for VSCode had inserted a host for me:

![notepad screenshot](/images/hostssh.png)

So I copied and pasted that but shortened ieng6.ucsd.edu in the host line to just ieng6 because it's shorter:

![notepad screenshot 2](/images/hostssh2.png)

And it works just fine.

![terminal screenshot](/images/shortssh.png)

## Group Choice 2: Setting up Github access from ieng6

This task was very difficult and complicated and really not worth the effort.
I became extremely frustrated after spending over an hour trying:
- Uploading the key I already have to Github
- Generating a new key on ieng6, using SCP to copy it onto my computer, then uploading it to Github
- Doing all of the step above except with a new key that has the email I used to log in to Github (rmasserf@ucsd.edu)
- Setting up the ssh-agent on my local computer (this was really difficult for some reason!)
- Adding the rmasserf@ucsd.edu key to my local ssh-agent
- Setting up the ssh-agent on ieng6
- Adding the rmasserf@ucsd.edu key to ssh-agent on ieng6

And none of this showed any measure of success. Running `git push` from ieng6, it would just keep asking me for my password, then telling me that it no longer accepts passwords. 

Finally, I decided to ask my father who has used Linux and SSH before to help me. He noted that it was unusual that it kept asking for my username and password (something I could not have known) and found [this article](https://www.freecodecamp.org/news/how-to-fix-git-always-asking-for-user-credentials/) about it. It turned out the solution was to run this command:
```
git remote set-url origin git@github.com:(your username)/(name of repo).git
```
which was mentioned nowhere in the writeup or in the Github article. 

Then a new problem introduced itself: when I ran `git push origin` it was no longer asking for my username and password, which was good, but it told me that permission was denied because I had the wrong public key. This was because over the previous hour and a half I had made many RSA keys and the one that it decided to use had been deleted from my Github account. So I re-uploaded it, and then it finally worked.

![Success, but at what cost?](/images/itworks.png)

## Group Choice 3: Copy whole directories with scp -r

This one was pretty simple to get to work: 

![scp -r](/images/scpdashr.png)

However, I was not able to copy and compile MarkdownParse.java in the same line because it somehow, MarkdownParse.java had syntax errors when using the single-line SSH command. Using multiple commands, it no longer has any syntax errors:

![I have no idea.](/images/what.png)

I don't even know what can be done about this.
