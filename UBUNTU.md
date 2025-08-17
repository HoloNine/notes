# Update
```bash
sudo apt update
sudo apt upgrade -y
```

# Install curl
```bash
sudo apt install curl
```

# Install JetBrains Fonts

# Install starship

# Config Straship

# Install GitHub

. Git global configuration

git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main

4. Install and configure Github CLI
4.1 Installations

sudo dnf install gh

4.2 Authentication

gh auth login

4.3 Adding your SSH key to the ssh-agent

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

4.4 Generate SSH Key (if not created during gh auth login)

ssh-keygen -t ed25519 -C "your.email@example.com"

4.5 Adding your SSH key to Github

gh ssh-key add ~/.ssh/id_ed25519.pub

4.6 Testing your SSH connection

ssh -T git@github.com

4.7 Testing your SSH connection with Github CLI

gh auth status

# Install nodeJS
# Install PHP, Composer and Laravel Installer
