---
layout: single
title:  "Manage GitHub and Gitlab accounts on single machine"
date:   2022-07-31 18:20:15 +0500
categories: misc
tag: git
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Manage GitHub and Gitlab accounts on single machine with SSH keys on linux
For this example, We will use the same email address to produce two different SSH keys:

- for Github, and
- for Gitlab.

The logic also extends to different emails, and multiple Github, and Gitlab accounts.

## Generate new SSH keys

Check if you have any existing SSH keys `ls -al ~/.ssh` on your machine. You can also use the existing key pair if it is available, but I suggest that you don’t.

To create private and public SSH pairs for your personal, and work accounts, run:

```console
ssh-keygen -t rsa -C "personal@mail.com" -f ~/.ssh/id_rsa_github
ssh-keygen -t rsa -C "personal@mail.com" -f ~/.ssh/id_rsa_gitlib
```

The above commands will produce four different files namely as below:

```console
~/.ssh/id_rsa_github
~/.ssh/id_rsa_github.pub
~/.ssh/id_rsa_gitlab
~/.ssh/id_rsa_gitlab.pub
```

## Add SSH keys to Github, and Gitlab

### Github

Copy corresponding public key of your Gitlab account

```console
cat ~/.ssh/id_rsa_github.pub
```

Logon to your Github account. Then go to `Settings > SSH and GPG Keys > New SSH key`

Paste the public key on the Key, and edit the title.

![Adding SSH keys on GitHub](/assets/images/github.png)

### Gitlab

Copy corresponding public key of your Gitlab account

```console
cat ~/.ssh/id_rsa_gitlab.pub
```

Logon to your Gitlab account. Then go to `Settings > SSH Keys`

Paste the public key, and edit the title.

![Adding SSH keys on GitLab](/assets/images/gitlib.png)

### Register SSH Keys with the ssh-agent

Register all SSH keys on your local machine using the ssh-agent

```console
ssh-add ~/.ssh/id_rsa_github
ssh-add ~/.ssh/id_rsa_gitlab
```

## Editing Config File

Create a configuration file that will add the different SSH keys for all online repositories and emails that we created earlier.

```console
touch ~/.ssh/config
vim ~/.ssh/config
```

The config file should look like this

```console
# Personal account
Host github.com
   HostName github.com
   IdentityFile ~/.ssh/id_rsa_github# Personal gitlab account

# Work account
Host gitlab.com
   HostName gitlab.com
   IdentityFile ~/.ssh/id_rsa_gitlab
```

After following the above steps, you should be able clone, and edit both your GitHub, and GitLab repositories on your local machine.
