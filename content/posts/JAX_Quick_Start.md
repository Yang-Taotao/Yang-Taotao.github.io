---
title: "JAX Quick Start"
date: 2024-08-21
Editted: 2024-08-21
draft: false
---

## JAX Quick Start

We will cover a quick start for doing stuff with jax on Windows.

### Step 1: Prepare Linux environment

#### 1.1 Get WSL for Linux

We follow: <https://learn.microsoft.com/en-us/windows/wsl/install>.

1. We will get the default Ubuntu distribution. In PowerShell:

    ```shell
    wsl --install
    ```

1. Set up your username and password for your Linux distribution according to the guide.
1. Now a quick update and upgrade to get everything up to the latest:

    ```shell
    sudo apt update && sudo apt upgrade
    ```

#### 1.2 Get VSCode for WSL

We follow: <https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode>.

1. Use installer to install if you havn't got vscode on machine.
1. Navigate to your project folder and open your Linux shell. This can be done from Windows explorer with 'Shift + RMB'.
1. With Linux shell open, run:

    ```shell
    code .
    ```

1. We now have the project opened within VSCode running on stock WSL.

#### 1.3 Get Git

We follow: <https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git>.

1. Check if Git is istalled. In your Linux shell, run:

    ```shell
    git --version
    ```

1. Install Git if you don't have it:

    ```shell
    sudo apt-get install git
    ```

1. Run Git configs:

    ```shell
    git config --global user.name "Your Name"
    git config --global user.email "youremail@domain.com"
    ```

### Step 2: Python development set up and Git

#### 2.1 Virtual environment setup

We set up a venv for better package control and compatibility.

1. Say we want a project called ```JAXTest``` on py3.12, we should first navigate to the project directory. It looks like ```C:\MyProjects\JAXTest```.
1. We can now get this py distribution with:

    ```shell
    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt update
    sudo apt install python3.12-full
    ```

1. Now we can create and activate a virtual environment with:

    ```shell
    python3.12 -m venv .venv
    source .venv/bin/activate
    ```

1. We now see ```\.venv``` folder within our project. We should have Git ignore it. Simply create a ```.gitignore``` file in root folder.

#### 2.2 Sync with GitHub

We now set GitHub up for remote repository.

1. Create a GitHub repository online. Follow: <https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories>.
1. We want to initialize Git to this project directory. In Linux shell, run:

    ```shell
    git init
    ```

1. We actually want to rename this branch to ```main```:

    ```shell
    git branch -m main
    ```

1. We can now link local repo with remote:

    ```shell
    git remote add origin'https://github.com/Your_Username/JAXTest.git'
    ```

1. We now make a sample ```README.md``` file with some messages written within.
1. Now we add both ```.gitignore``` and ```README.md``` to staging for commit. Remember to use good commit practices.
1. Push/pull to sync up changes.

    ```bash
    git push
    ```

### Step 3: JAX related setup

#### 3.1: JAX install

We have two options: GPU or CPU version of JAX. Use at your own discretion. We follow: <https://jax.readthedocs.io/en/latest/installation.html>.

1. Let us start with getting pip up to date. In Linux shell, run:

    ```shell
    pip install --upgrade pip
    ```

1. We install the GPU version of JAX for our NVIDIA GPU:

    ```shell
    pip install pip install --upgrade "jax[cuda12]"
    ```

#### 3.2 Reading time

Read up and continue to reference on the common gotchas of JAX in <https://jax.readthedocs.io/en/latest/notebooks/Common_Gotchas_in_JAX.html>.
