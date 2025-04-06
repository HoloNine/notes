## 1. System Update

```bash
sudo dnf update
```
## 2. Update grub resolutin
```bash
sudo nano /etc/default/grub
# Add the lines
GRUB_CMDLINE_LINUX_DEFAULT="quiet"
GRUB_TERMINAL_OUTPUT="gfxterm"
GRUB_GFXMODE=1920x1080x32
```
Update grub
```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

## 2. ZSH installation and configuration

### 2.1 Install zsh

```bash
sudo dnf install zsh
```

### 2.2 Set zsh as your default shell

```bash
chsh -s $(which zsh)
```

Log out and back in to apply changes.

### 2.3 Check what shell you are using

```bash
echo $SHELL
```

### 2.4 Backup your current .zshrc file

```bash
cp $HOME/.zshrc $HOME/.zshrc.bak
```

### 2.5 Configure Path in .zshrc

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> $HOME/.zshrc
```

### 2.6 Install Starship

### 2.7 Add saved `.zshrc` file
### 2.8 Restart terminal
```bash
source ~/.zshrc
```

## 3. Git global configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
```

## 4. Install and configure Github CLI

### 4.1 Installations

```bash
sudo dnf install gh
```

### 4.2 Authentication

```bash
gh auth login
```

### 4.3 Adding your SSH key to the ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 4.4 Generate SSH Key (if not created during gh auth login)

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

### 4.5 Adding your SSH key to Github

```bash
gh ssh-key add ~/.ssh/id_ed25519.pub
```

### 4.6 Testing your SSH connection

```bash
ssh -T git@github.com
```

### 4.7 Testing your SSH connection with Github CLI

```bash
gh auth status
```

### 4.8 Install netcat

```bash
sudo dnf install nmap-ncat
```

## 5. Install Node.js

### 5.1 Installations

Install Node.js using the official command with node package manager (npm):

### 5.2 Verification

```bash
node -v
npm -v
```

## 6. Installing PHP and the Laravel Installer

```bash
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.4)"
```

Restart the terminal

```bash
composer global require laravel/installer
```

### 6.1 Add the Laravel installer to your PATH

```bash
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> $HOME/.zshrc
```

## 7. Configure `podman`

### 7.1 Install podman and podman-compose

```bash
sudo dnf install -y podman podman-compose podman-docker
```

### 7.2 Enable and start the Podman Docker socket

```bash
systemctl --user enable podman.socket
systemctl --user start podman.socket
```

### 7.3 Set the Docker host environment variable (is already in `.zshrc`)

```bash
echo 'export DOCKER_HOST=unix:///run/user/$UID/podman/podman.sock' >> $HOME/.zshrc
```

### 7.4 Install `lazydocker`

### 7.3 Take ownership of the project folders (dev env only)

```bash
sudo chcon -Rt svirt_sandbox_file_t ./public
sudo chown -R $USER:$USER ./public
chmod -R u+rw ./public
```
change user inside container
```bash
podman exec -it wordpress bash
chown -R www-data:www-data /var/www/html
exit
```
### 7.4 Add to `wp-config.php`
```bash
define('FS_METHOD', 'direct');
```
