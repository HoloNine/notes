# Fedora 43 Post-Install Guide (Web Development)

Follow this in order on a fresh Fedora 43 install.

## 1) Full system update

```bash
sudo dnf upgrade --refresh -y
sudo reboot
```

After reboot:

```bash
sudo dnf check-update
```

If nothing important appears, your system is up to date.

---

## 2) Install Git + global config

Install Git:

```bash
sudo dnf install -y git
```

Set your global config:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global color.ui auto
```

Verify:

```bash
git config --global --list
```

---

## 3) Install GitHub CLI + SSH auth + link to GitHub

Install GitHub CLI:

```bash
sudo dnf install -y gh
```

Generate an SSH key (use your GitHub email):

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

Start agent and add key:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Upload key to GitHub:

```bash
gh ssh-key add ~/.ssh/id_ed25519.pub --title "fedora43-$(hostname)"
```

Authenticate GitHub CLI using SSH for git operations:

```bash
gh auth login --git-protocol ssh --web
```

Verify:

```bash
gh auth status
ssh -T git@github.com
```

---

## 4) Setup Bash + Starship

Install Starship:

```bash
sudo dnf install -y starship
```

Enable Starship in Bash:

```bash
grep -qxF 'eval "$(starship init bash)"' ~/.bashrc || echo 'eval "$(starship init bash)"' >> ~/.bashrc
source ~/.bashrc
```

Verify:

```bash
starship --version
```

---

## 5) Install Docker Engine only

Install Docker official repo and packages:

```bash
sudo dnf install -y dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Enable/start Docker service:

```bash
sudo systemctl enable --now docker
```

Allow your user to run Docker without sudo:

```bash
sudo usermod -aG docker "$USER"
newgrp docker
```

Verify:

```bash
docker --version
docker run --rm hello-world
```

---

## 6) Install DDEV

Install DDEV with the official installer:

```bash
curl -fsSL https://ddev.com/install.sh | bash
```

Verify:

```bash
ddev version
```

---

## 7) Install Node (with nvm)

Install nvm:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
source ~/.bashrc
```

Install latest LTS Node and set default:

```bash
nvm install --lts
nvm alias default 'lts/*'
nvm use default
```

Verify:

```bash
node -v
npm -v
```

---

## 8) Install HubSpot CLI

Install globally with npm:

```bash
npm install -g @hubspot/cli
```

Login and verify:

```bash
hs auth
hs --version
```

---

## 9) Install Laravel + PHP + Composer

Install all 3 with your chosen Laravel installer command:

```bash
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.4)"
```

Reload shell and verify:

```bash
source ~/.bashrc
php -v
composer --version
laravel --version
```

---

## 10) Apps to install for web development

### VS Code

Install Microsoft repo and VS Code:

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
printf "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc\n" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null
sudo dnf check-update
sudo dnf install -y code
```

Launch:

```bash
code
```

---

## Final quick check

Run this at the end:

```bash
git --version
gh --version
starship --version
docker --version
ddev version
node -v
npm -v
hs --version
php -v
composer --version
laravel --version
code --version
```
