# Setting up Github SSH Connections

If you are using a Mac or a Linux computer, then git will already be installed. If you are using a Windows machine, you must install git yourself by downloading this [file](https://github.com/git-for-windows/git/releases/download/v2.39.1.windows.1/Git-2.39.1-64-bit.exe) (you need Git Bash). 

Once git is installed, the next thing we want to do is setting up an ssh key to easily access all of the repositories that we have access to without needing to put your credentials in every time. 

[This official Github page](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) covers the setup in detail; we will just highlight some key steps you need to take here for your reference. We will assume that you have not used ssh before. Thus, we'll start from generating a ssh key, followed by registering it with Github.

## Generating a new SSH key
1. Open terminal (Unix) or Git Bash (Windows)
2. Paste the text below, substituting in your GitHub email address. (Note: don't copy the dollar sign!)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
```
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; When prompted to enter the file location and passphrase, simply press `Enter` (unless you want to set a passphrase; in this case, you'll have to enter the passphrase everytime you use a git command with the ssh key).

3. Ensure the ssh-agent is running by typing the following in to the terminal:
```
$ eval "$(ssh-agent -s)"
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; This will give you an output that looks like &nbsp;&nbsp;`> Agent pid 59566`.

4. Add your SSH private key to the ssh-agent.

```
$ ssh-add ~/.ssh/id_ed25519
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If you are a mac user and this doesn't work, refer to the Github tutorial linked above.

## Registering a new SSH key to your Github account
Once you have generated a new SSH key and saved it to your local machine, you need to register its public key to your Github account. 

1. Copy the SSH public key to your clipboard.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If you type `ls ~/.ssh/` on your terminal, you will see `id_ed25519` and `id_ed25519.pub`. The former is the private key and the other one is the public key. Never reveal your private key in any case. Instead, you will need to register the public key.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; To do so, type `cat ~/.ssh/id_ed25519.pub` on your terminal. Copy the output to your clipboard, which looks something like below:

```
ssh-ed25519 the-public-ssh-key-here your_email@example.com
```

2. Go to *github.com*. In the upper-right corner of any page, click your profile photo, then click **Settings**.

3. In the **"Access"** section of the sidebar, click **SSH and GPG keys**.

4. Click **New SSH key** or **Add SSH key**.

5. In the **"Title"** field, add a descriptive label for the new key. For example, if you're using a personal laptop, you might call this key "Personal laptop".

6. Paste your key into the **"Key"** field and click **Add SSH key**.

Voilà, that's it! You can now clone, pull, and push to your private repos without having to provide your credentials each time :) To begin by cloning your repo, type `git clone {ssh repo link}` where {ssh repo link} is the link you get when you go to a repository, click on the green code button and select the ssh tab.
