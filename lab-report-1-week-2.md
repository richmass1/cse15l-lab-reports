Yo look at this sick picture of a cat

![Image](images/cat.png)

This was to make sure the pictures were working but I'm gonna leave it here

Anyways hello youtube, today I will be teaching you how to access a remote server.
# Step 1: getting your class-specific username, and setting a password
Go to [this website](https://sdacs.ucsd.edu/~icc/index.php) and type in your info and it will give you your class-specific username.

Click the button with your new username and click "change your password". Then use the password reset tool which is kind of a quagmire, good luck.
# Step 2: Opening a command prompt
## Option 1: Using the Windows command prompt
ok so what you want to do is hit the windows key + R and this thing will show up

![Image](/images/windowsrun.JPG)

and you should type cmd and hit enter.
Then this thing appears

![Image](/images/cmd.JPG)

but instead of Richard it will say your name. 

## Option 2: Using VS Code
This is the one recommended by the class instructor. But both ways work. To do this go to [the VS Code website](https://code.visualstudio.com/) and download the installer and run it. It will look something like this:

![Image](/images/vscode1.JPG)

Click Terminal and then click New Terminal.

![Image](/images/vscode2.JPG)

And this will show up and you'll be typing into this.

![Image](/images/vscode3.JPG)

# Step 3: using SSH
Type `ssh <username>@ieng6.ucsd.edu` and it should prompt you for a password. You won't be able to see your password as you type it but that's fine. Make sure you didn't type "cse15l" as the username because for some reason it's actually "cs15l". 

After you type in your password a bunch of stuff will come up. This is what it should look like. 

![Image](/images/helloagt.JPG)

And now you're in, you're connected to the remote server. Good job. Now you can do stuff with the remote server. You're typing the commands on your computer, but they're getting executed on the server computer.

Since you're accessing it via the command line, you'll have to use Unix-like commands. Here are some lists of such commands: 
* [list 1](http://mally.stanford.edu/~sr/computing/basic-unix.html) 
* [list 2](https://stats.oarc.ucla.edu/other/mult-pkg/faq/fileman/unix_cmds/)

If you don't want to have to use these commands, download MobaXterm and connect via remote desktop. But that's outside the scope of this post.

# Step 4: using SCP
SCP stands for secure copy. What's it for? Well since you're interacting with this server via SSH you clearly won't be able to use any beautiful IDEs with nice graphics, so you're gonna want to write your code on your own machine. But then you have to send it to the server somehow if you want to have it be able to run on the server. So that's what SCP is for. 

In order to use SCP you have to run it on your machine-- you can't be inside SSH when you're doing it. You can type "exit" to log out of SSH. SCP is pretty simple: you just type `scp <path of local file> <username>@ieng6.ucsd.edu:~/<server path>`. If you're putting it in the home directory on the server then don't type anything for the server path. It will prompt you for a password.
  
Here's an example of the SCP command; I'm copying a file called WhereAmI.java from the working directory to the home directory of the server.
  
![Image](/images/scp.JPG)
  
# Step 5: using SSH keys
So if you don't feel like typing in your password every time you want to do anything you can get an SSH key. Go into your terminal and make your working directory one that is specific to your current purposes and type ssh-keygen. A bunch of stuff will show up. I can't post a screenshot because I've already done it and I don't know whether doing it again will cause problems. Sorry. Anyways, press enter three times; there's no need to change the path or add a passphrase. 

Now do windows + R and type in powershell but instead of hitting enter hit Ctrl+Shift+Enter. This will open powershell in administrator mode. Then type in these 4 commands:
  
1. `Get-Service ssh-agent | Set-Service -StartupType Manual`
2. `Start-Service ssh-agent`
3. `Get-Service ssh-agent` (this one should tell you that it's running)
4. `ssh-add <path of your private key, that's the one that doesn't have .pub>`
  
Now you have to send it to the server. Access the server via SSH and make a directory called .ssh. You should know how to do this, I shouldn't have to tell you. Then logout and copy your public key (that's the one with the .pub!) to this directory under the name "authorized_keys". This should be easy but I'll spell it out anyways:
  
`scp <path of public key> <username>@ieng6.ucsd.edu:~/.ssh/authorized_keys`

and that should have it working.

# Step 6: optimizing

There are a bunch of ways to optimize but here are the ones that worked for me the best:
* using the up arrow to recall the last command that you executed
* using `ssh <username>@ieng6.ucsd.edu "<your command here>"` to execute a command on the server without having to log in to it
* stringing together multiple commands with semicolons, like `scp WhereAmI.java cs15lsp22agt@ieng.ucsd.edu:~/ ; ssh cs15lsp22agt@ieng.ucsd.edu "javac WhereAmI.java" ; ssh cs15lsp22agt@ieng.ucsd.edu "java WhereAmI"`. This single command copies my WhereAmI.java onto the server, compiles it, then runs it. And if I want to execute the command again, all I have to do is press up and then enter.
