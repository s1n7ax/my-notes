# Remove unwanted `xdg-desktop-portal` implementations

- List all installed `xdg-desktop-portal` implementations

```shell
dnf list installed | grep 'xdg-desktop-portal-'
```

- Remove all `xdg-desktop-portal` implementations
- Install dependencies

```shell
sudo dnf install \
'pkgconfig(libpipewire-0.3)'
inih-devel \
libuuid-devel \
qt6-qtbase-devel \
qt6-qtwayland 
```

- Build and install `xdg-desktop-portal-hyprland`

```shell
git clone https://github.com/hyprwm/xdg-desktop-portal-hyprland.git
cd xdg-desktop-portal-hyprland
meson build --prefix=/usr --buildtype=release
ninja -C build
cd hyprland-share-picker && make all && cd ..
ninja -C build install
sudo cp ./hyprland-share-picker/build/hyprland-share-picker /usr/bin
reboot
```