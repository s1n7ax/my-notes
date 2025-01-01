- Install following dependencies

```shell
sudo dnf install mpv-devel
```

- Build and Install

```shell
git clone --single-branch https://github.com/GhostNaN/mpvpaper
cd mpvpaper
meson build --prefix=/usr/local --buildtype=release
ninja -C build
sudo ninja -C build install
```