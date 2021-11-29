# Building Reproducible Environments
This document outlines the steps that are required to build my dev environment on any fresh linux install.
These steps will later get automated using an automation tool, such as [Ansible](https://docs.ansible.com/ansible/latest/index.html), [puppet](https://forge.puppet.com/)
or chezmoi's run once scripts.

> **NOTE:** For now this is only build for Ubuntu. some packages might not be available or have a different names on other distros.

## Required software
| Software                                                      | Install command                                                                                 |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [git](https://git-scm.com/)                                   | `sudo apt install git`                                                                          |
| [chezmoi](https://www.chezmoi.io/)                            | `snap install chezmoi --classic`                                                                |
| [nvm](https://github.com/nvm-sh/nvm#installing-and-updating)  | See linked section of the docs                                                                  |

> **NOTE:** After installing zsh and oh-my-zsh you need to log out and back in if you changed it to be your default shell.

## Generating an SSH key
To authenticate with GitHub and access the dotfiles repository, generate a new SSH key if none is already on the machine.

```sh
ssh-keygen -t ed25519 -C "$USER@$(hostname)"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Output the key and copy it to GitHub to add it as an SSH key
cat ~/.ssh/id_ed25519.pub
# Or if xclip is installed
xclip -sel clip ~/.ssh/id_ed25519.pub
```

## Downloading dotfiles
If [chezmoi](https://www.chezmoi.io/) is installed, then downloading all configuration, aka dotfiles is
as simple as running one command:

```sh
chezmoi init --apply git@github.com:C-574/dotfiles.git
```

## Installing Cascadia Code
I use the awesome [Cascadia Code](https://github.com/microsoft/cascadia-code) font in VS Code.
To install it, download the latest release from the releases page, unzip it and either copy the ttf font files into
the local `~/.local/share/fonts/` folder or globally into `/usr/local/share/fonts/`. See [this](https://askubuntu.com/a/3706) for more info. Don't forget to update the font cache after installing the font with `fc-cache -f -v`.
