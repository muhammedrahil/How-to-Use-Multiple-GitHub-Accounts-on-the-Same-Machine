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
