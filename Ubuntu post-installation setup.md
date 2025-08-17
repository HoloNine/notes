# Ubuntu post-installation setup

## Update Ubuntu

```bash
sudo apt update
sudo apt upgrade -y
```

## Install JetBrains Fonts & JetBrains Mono Nerd Font

Install the latest fonts from [JetBrains](https://www.jetbrains.com/lp/mono/).

## Install curl

```bash
sudo apt install curl
```

## Install Starship

Install Starship custom prompt from [here](https://starship.rs/).

### Config Starship

Follow the [installation guide](https://starship.rs/guide/) to configure Starship.

## Install Git

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
```

## Install and configure Github CLI

### Installation

Install GitHub CLI from [here](https://cli.github.com/).

### Authentication

```bash
gh auth login
```

### Adding your SSH key to the ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Generate SSH Key (if not created during gh auth login)

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

### Adding your SSH key to Github

```bash
gh ssh-key add ~/.ssh/id_ed25519.pub
```

### Testing your SSH connection

```bash
ssh -T git@github.com
```

### Testing your SSH connection with Github CLI

```bash
gh auth status
```

## Install nodeJS

Install NodeJS from [NodeSource](https://nodejs.org/en/download).

## Install PHP, Composer and Laravel Installer

Install from [Laravel Docs](https://laravel.com/docs/)

## Install Docker

Install Docker from [Docker Docs](https://docs.docker.com/engine/install/ubuntu/).

## Install ddev

Follow the installation guide from [ddev Docs](https://ddev.com/get-started/).
