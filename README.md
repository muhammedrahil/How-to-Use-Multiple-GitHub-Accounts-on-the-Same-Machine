# How to Use Multiple GitHub Accounts on the Same Machine

Working with multiple GitHub accounts on the same machine can be challenging, especially when it comes to managing separate SSH keys and repositories. In this article, we will guide you through the process of setting up and using multiple GitHub accounts on your computer, making your development workflow more efficient and organized.

## Step 1: Generate SSH Keys for Each GitHub Account

To generate a new SSH key for each GitHub account, open your terminal and run the following command, replacing "your_email@example.com" with the email address associated with the GitHub account:

```bash
ssh-keygen -t ed25519 -C "work_email@example.com"
```

```bash
ssh-keygen -t ed25519 -C "personal_email@example.com"
```

When prompted for a file in which to save the key, choose a unique name and location, such as `~/.ssh/any_name_enter_here`.

### Example

```bash
$ ssh-keygen -t ed25519 -C "work_email@example.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/MyPc/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
```

If you want to change the file name, enter a new path:

```bash
$ ssh-keygen -t ed25519 -C "work_email@example.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/MyPc/.ssh/id_ed25519): /c/Users/MyPc/.ssh/any_name_enter_here
Enter passphrase (empty for no passphrase):
```


## Step 2: Add the SSH Key to the SSH Agent

To add the newly generated SSH key to the SSH agent, run these commands in your terminal:

```bash
eval "$(ssh-agent -s)"
```

Then add your keys:

```bash
ssh-add ~/.ssh/personal
ssh-add ~/.ssh/work
```

Example:

```bash
MyPc@DESKTOP ~
$ cd .ssh/

MyPc@DESKTOP ~/.ssh
$ ls
config  id_rsa.pub   known_hosts.old  personal.pub  work.pub
id_rsa  known_hosts  personal         work
```

## Step 3: Configuring GitHub Accounts

To configure your GitHub accounts, create a new file called `config` in the `~/.ssh` directory:

```bash
MyPc@DESKTOP ~/.ssh
$ cat config
Host github.com-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/work

Host github.com-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/personal
```

## Step 4: Test the Configuration

To test your configuration, run the following command for each account, replacing "github.com-work" or "github.com-personal" with the correct Host value from your config file:

```bash
MyPc@DESKTOP ~/.ssh
$ ssh -T git@github.com-work
git@github.com: Permission denied (publickey).
```

If you encounter this issue, check if the public key is added to the appropriate GitHub account.

### Add Your Public Key to GitHub

To add your public key, print the content of the `.pub` file and copy it:

```bash
MyPc@DESKTOP ~/.ssh
$ cat personal.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDYjVY0dPurupQoAHBbT4Lef4XgSN+GWCvd//T61mSyD personal_email@example.com
```

- Go to GitHub settings under SSH keys.
- Create a new SSH key.
- Paste the content of the `.pub` file (as shown above).


### Test Again

After adding the key, test again:

```bash
MyPc@DESKTOP ~/.ssh
$ ssh -T git@github.com-personal
Hi yourname! You've successfully authenticated, but GitHub does not provide shell access.
```

## Step 5: Managing Multiple Repositories

### Cloning a Repository

To clone a repository from one of your GitHub accounts, use the following command, replacing `github.com-personal` with the appropriate Host value and `your_username` and `your_repository` with the correct information:

```bash
git clone git@github.com-personal:your_username/your_repository.git
```

Next, configure Git:

```bash
git config user.email personal_email@example.com
git config user.name your_username
```

### Pushing Changes to a Repository

To push changes to a repository, navigate to the local repository folder and execute the following commands:

```bash
git add .
git commit -m "Your commit message"
git push
```

### Push Files into a New Repository

To push files into your new repository:

```bash
git config user.email personal_email@example.com
git config user.name your_username
```

```bash
git init
git add .
git commit -m "Your commit message"
git branch -M main
git remote add personal git@github.com-personal:your_username/your_repository.git
git push personal main
```

That's it! Now you're all set to manage multiple GitHub accounts on the same machine.

