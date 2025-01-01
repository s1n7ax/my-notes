# Update system

```shell
sudo dnf update --refresh
sudo dnf install git
reboot
```

# SSH config

From github ssh
```shell
ssh-keygen -t ed25519 -C "srineshnisala@gmail.com"
```

# Setting up dothome

```shell
git init
git switch -c main
git remote add origin https://github.com/s1n7ax/dothome.git
git pull origin main
```

# Installing Hyprland

- Follow the instructions in [[Fedora 38 Hyprland Build & Install]]

# Nvidia Propitiatory Driver

- Installing RPMFusion free/non-free repositories from [rpmfusion](https://rpmfusion.org/Configuration/)

```shell
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

- From [Howto/NVIDIA](https://rpmfusion.org/Howto/NVIDIA#Current_GeForce.2FQuadro.2FTesla)

```shell
sudo dnf update -y
sudo dnf install akmod-nvidia
sudo dnf install xorg-x11-drv-nvidia-cuda #optional for cuda/nvdec/nvenc support
```

- Add following environment variable to `/etc/environment`

```shell
WLR_NO_HARDWARE_CURSORS=1
```

# System Dependencies

```bash
sudo dnf install \
git \
flathub \
alacritty \
wofi \
zsh \
pass \
yt-dlp \
go \
```

# Flathub remote for Flatpak

From [flatpakrepo-files](https://docs.flatpak.org/en/latest/hosting-a-repository.html#flatpakrepo-files)

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

# Flatpak Apps

```bash
flatpak install flathub \
md.obsidian.Obsidian \
org.mozilla.firefox \
com.github.tchx84.Flatseal \
com.obsproject.Studio \
fr.handbrake.ghb \
org.videolan.VLC \
org.kde.digikam \
org.gimp.GIMP \
org.kde.kdenlive \
org.gnome.baobab \
io.missioncenter.MissionCenter \
com.github.micahflee.torbrowser-launcher \
```

# Cargo Setup

- From [rustup.rs](https://rustup.rs/)
```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

# Oh-My-ZSH Setup

- From [oh-my-zsh/#install](https://ohmyz.sh/#install)

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

- Reference global environment variables by appending following to `~/.zprofile`

```shell
. ~/.s1n7ax/init_global_env
```

- Reference local environment variables & aliases by appending following to `~/.zshrc`

```shell
. ~/.s1n7ax/init_alias
. ~/.s1n7ax/init_local_env
```

# Setup Home Profile

```
mkdir ~/.profiles
touch ~/.profiles/home
touch ~/.profiles/common
```

# Install Cargo packages

```shell
cargo install \
exa \
bob-nvim \
fd-find \
ripgrep \
starship \
skim \
```

# Install Go Packages

```shell
# from https://github.com/jesseduffield/lazygit#go
go install github.com/jesseduffield/lazygit@latest
```

# Install Node

```shell
wget https://nodejs.org/dist/v18.17.0/node-v18.17.0-linux-x64.tar.xz
tar xf node-v18.17.0-linux-x64.tar.xz
mv node-v18.17.0-linux-x64 ~/.node
rm node-v18.17.0-linux-x64.tar.xz
```

# Install neovim config

```shell
git clone --depth 1 https://github.com/AstroNvim/AstroNvim ~/.config/nvim

git clone https://github.com/s1n7ax/colemak_astronvim_config.git ~/.config/astronvim
```