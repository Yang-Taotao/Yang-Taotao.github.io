---
title: "SSH and Signature"
author: "T. Yang"
date: "2026-01-12"
summary: "A simple reference guide on how to employ SSH"
description: ""
toc: true
readTime: true
autonumber: true
math: true
tags: ["ssh", "git", "guide"]
showTags: false
hideBackToTop: false
---

## Installation

We start by installing the necessary packages. 

1. `openssh`: SSH protocol
2. `sshfs`: FUSE client for SSH FTP
3. `keychain`: Front-end to ssh-agent

For example, on Arch, with some terminal of your choice:

```sh
$ sudo pacman -S openssh sshfs keychain
```

## SSH keys

The gist is that SSH connections are verified with key pairs. You should always keep your private key secure. Some popular tools include `keepassxc` and `bitwarden`.

### Keygen

We can generate these keys with:

```sh
$ ssh-keygen -t ed25519 -C "username@service.com" -f ~/.ssh/id_custom_key
```

This command generates some key pairs following `ed25519` algorithm with comment string `"username@service.com"` for human readability. The key pairs are saved as `~/.ssh/id_custom_key` and `~/.ssh/id_custom_key.pub`.

### Usage

What can we do with these keys then? Welp, let us assume that we have a remote server that is configured in `~/.ssh/config` as:

```sh
Host server
    HostName server.com
    User username
    IdentityFIle ~/.ssh/id_custom_key
```

We essentially specify the credentials and key to use for authenticating with the server. For example, with `github`, we can set:

```sh
Host github.com
    HostName github.com
    User git
    IdentityFIle ~/.ssh/id_custom_key
    IdentitiesOnly
```

Assuming the public keys for signing and authentication are added in your [settings](https://github.com/settings/keys), we can test for SSH connection via:

```sh
$ ssh -T github.com
```

Note, these `~/.ssh/config` files should have appropriate permissions set with:

```sh
$ chmod 700 ~/.ssh && chmod 600 ~/.ssh/config
```

### General case

And of course, this can be done for the example server that we set above with:

```sh
$ ssh-copy-id -i ~/.ssh/id_custom_key.pub username@server
```

We explicitly states the public key to upload to the `server` configured in `~/.ssh/config`. This will result in some entries being added to `$SERVER/~/.ssh/authorized_keys`. After which, we can simply connect to `server` via:

```sh
$ ssh server
```

## Agents

But entering the passwords for the ssh keys over and over is painful. We can mitigate this issue with `ssh-agent`. For example, with `bash`, add the following to `~/.bashrc`:

```sh
if [ -z "$SSH_AUTH_SOCK" ]; then
    eval "$(ssh-agent -s)"
fi
ssh-add ~/.ssh/id_custom_key 2>/dev/null
```

And if on `fish`:

```sh
if test -z "$SSH_AUTH_SOCK"
    and pgrep ssh-agent >/dev/null ^&1
    or test $status -ne 0
    eval (ssh-agent -c)
end
ssh-add ~/.ssh/id_custom_key 2>/dev/null
```

These setups allow for `ssh-agent` to run and persist for handling your `id_custom_key` for ssh authentication. Additionally, we can employ `keychain` for easier configurations. In `fish`:

```sh
keychain --quiet --eval id_custom_key | source
```

And of course, services like `bitwarden` and `keepassxc` can serve similar purpose, if not with more features loaded.

## Signature

What about signatures? Not only does it look nice when your commits show up as `verified`, it also signals that you are probably the person that did the commit because it has your signature. This can be done via `.gitconfigs`.

Simply set in your `~/.gitconfig`:

```sh
[user]
	name = YourName
    email = username@email.com
    signingkey = ~/.ssh/id_custom_key.pub

[commit]
    gpgsign = true

[gpg]
    format = ssh
```

We should now let `git` know that we are the allowed signers:

```sh
$ echo "username@email.com $(cat ~/.ssh/id_custom_key.pub)" > ~/.ssh/allowed_signers
```

Of course, we can also store this `allowed_signers` file in `~/.config/git` for consistency. Additionally, we should explicitly configure our `.gitconfig` to include:

```sh
[gpg "ssh"]
	allowedSignersFile = ~/.ssh/allowed_signers
```

What this does is to allow for `github` to recognize our signature that is already presnt in our commits. Assume that we are in a example project folder at `~/project`, we can do the following:

```sh
$ git init
$ touch test.md
$ git add .
$ git commit -m "add test"
```

Now, without `allowed_signers` declared, we inspect the commit with:

```sh
$ git cat-file -p HEAD
```

This should show something along the line of:

```sh
tree ...
parent ...
author ...
committer ...
gpgsig -----BEGIN SSH SIGNATURE-----
 ...
 -----END SSH SIGNATURE-----
 
some commit msg
```

After getting `allowed_signers` declared. We can inspect the signature status via:

```sh
$ git log --show-signature -1
```

This should show something like:

```sh
commit ...
Good "git" signature for ... with ED25519 key SHA256:...
Author: ... <email>
Date:   ...

    some commit msg
```

## Remarks

I wrote this after my wayland compositor plays terribly with nvidia cards and lead to repeated desktop environment crashes and having to redo all the configurations due to lost configs.
