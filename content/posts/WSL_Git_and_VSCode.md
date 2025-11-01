---
title: "WSL, Git, and VSCode"
author: "T. Yang"
date: "2025-10-30"
summary: "A simple guide on how to install and configure WSL, Git, and VSCode"
description: ""
toc: true
readTime: true
autonumber: true
math: true
tags: ["wsl", "git", "guide"]
showTags: false
hideBackToTop: false
---

## Installation - WSL, VSCode, and Git

In this seciton, we will install WSL and VSCode.

### WSL

Consequently, we could simply follow along the [documentation](https://learn.microsoft.com/en-us/windows/wsl/install) provided to have ```WSL``` working on our windows device.

1. We will get the default Ubuntu distribution. In ```pwsh```:

    ```bash
    > wsl --install
    ```

2. Set up your ```username``` and ```password``` for your Linux distribution according to the guide. Now we should open our WSL Ubuntu on windows.

    ```bash
    > wsl.exe
    ```

3. We can now enter the ```/home/{username}``` directory:

    ```bash
    > cd ~
    ```

4. Now a quick update and upgrade to get everything up to the latest:

    ```bash
    > sudo apt update && sudo apt upgrade
    ```

### VSCode

We now follow the [documentation](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode) for VSCode usage with WSL.

1. Use installer to install if you havn't got VSCode on machine. For Windows usage with WSL, install VSCode natively under Windows file system.

2. Follow the guide to setup ```Remote - SSH``` extension. There are a number of different extensions available that improves quality of life, but we will come back to that at a later point.

3. In terminal, we can create a folder for our coding projects, let us call it ```repo```:

    ```bash
    > cd ~
    > mkdir repo
    > cd repo
    ```

4. We have now created a new folder under ```/home/{username}``` and changed our directory to ```~/repo```. How can we make changes to files with VSCode from this point onwards? It is simply with:

    ```bash
    > code .
    ```

5. By running ```> code .``` in terminal, we open VSCode under the current directory ```.```. Consequently, we can also open files with VSCode just like ```> vi {filename}```:

    ```bash
    > code {filename}
    ```

### Git

Once again, there are additional [documentation](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git) that we can follow.

1. Check if Git is istalled. In your Linux shell, run:

    ```bash
    > git --version
    ```

2. Install Git if you don't have it:

    ```bash
    > sudo apt-get install git
    ```

3. Run Git configs:

    ```bash
    > git config --global user.name "Your Name"
    > git config --global user.email "youremail@domain.com"
    ```

4. We can now double check our ```.gitconfig``` by checking:

    ```bash
    > cd ~
    > ls -a
    > cat .gitconfig
    ```

### Remarks

These steps pretty much concludes the initial setting up of the tools mentioned. Additional steps should be performed for tracking and syncing changes with Git and GitHub.
