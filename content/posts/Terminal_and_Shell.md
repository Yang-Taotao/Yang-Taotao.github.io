---
title: "Terminal and Shell"
author: "T. Yang"
date: "2025-10-30"
summary: "A simple guide on how to configure a personal terminal and shell"
description: ""
toc: true
readTime: true
autonumber: true
math: true
tags: ["terminal", "shell", "guide"]
showTags: false
hideBackToTop: false
---

## Prerequisite

Some **nerd font** of your choice. Find more via [Nerd Fonts](https://www.nerdfonts.com/).

## Choices

1. Some **terminal** of your choice, popular ones include

   1. [WezTerm](https://github.com/wezterm/wezterm)
   2. [Ghostty](https://github.com/wezterm/wezterm)
   3. [Alacritty](https://github.com/alacritty/alacritty)
   4. [kitty](https://github.com/kovidgoyal/kitty)

2. Some **shell** of your choice, popular ones include
   1. [zsh](https://github.com/zsh-users/zsh)
   2. [fish](https://github.com/fish-shell/fish-shell)
   3. [tcsh](https://github.com/tcsh-org/tcsh)
   4. [bash](https://tiswww.case.edu/php/chet/bash/bashtop.html#TOCAvailability)

## Installation - Terminal and Shell

Now we want to use some fancy terminals and shell just because we can. Let us install ```zsh``` and ```WezTerm``` in this guide.

### Shell

We will now install and configure ```zsh``` with ```oh-my-zsh```.

1. In command lines under ```Ubuntu```, we run:

    ```bash
    > apt install zsh
    ```

2. We can do a simple check to see if ```zsh``` is installed properly:

    ```bash
    > zsh --version
    ```

3. That is pretty much it, although we can now employ ```oh-my-zsh``` for ```zsh``` configuration. We can check for more information on its GitHub [page](https://github.com/ohmyzsh/ohmyzsh). We now install ```oh-my-zsh``` via terminal:

    ```bash
    > sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```

4. Further customization can be performed by editting ```~/.zshrc```. For example, let us default in entering our home directory at shell launch.

    ```bash
    > cd ~
    > echo "# Enter home dir" >> ~/.zshrc
    > echo "cd ~" >> ~/.zshrc
    ```

### Terminal

We will now install and configure ```WezTerm``` with ```starship```.

1. For a WSL setup, it is adviable to install our terminal under Windows file system. In terminal we run:

    ```bash
    > winget install wez.wezterm
    > winget upgrade wez.wezterm
    ```

2. And that's pretty much it, we can customize ```WezTerm``` and other terminal such as ```pwsh``` with ```starship```. To do this, with your terminal under Linux file system:

    ```bash
    > curl -sS https://starship.rs/install.sh | sh
    ```

3. Now that we have both our terminal and shell installed, we can get ```starship``` to customize our terminal via:

    ```bash
    > cd ~
    > echo "# Init starship for zsh" >> ~/.zshrc
    > echo 'eval "$(starship init zsh)"' >> ~/.zshrc
    ```

4. We can now apply some ```starship``` customization to our terminal by including a ```starship.toml``` file in ```~/.config```:

    ```bash
    > starship preset nerd-font-symbols -o ~/.config/starship.toml
    ```

### Remarks

There are many customizations that we can apply to these terminal and shells to improve our own efficiency, work habits, and the enjoyment of it.

One thing to take note for VSCode integration with ```zsh``` is that we should set for VSCode to also employ ```zsh``` over ```bash``` in its builtin terminal.
