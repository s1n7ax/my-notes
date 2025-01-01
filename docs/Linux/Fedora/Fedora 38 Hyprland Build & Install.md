# Installing Dependencies

```bash
sudo dnf install \
ninja-build \
cmake \
meson \
gcc-c++ \
libxcb-devel \
libX11-devel \
pixman-devel \
cairo-devel \
pango-devel \
libdrm-devel \
libudev-devel \
libdisplay-info-devel \
pixman-devel \
libseat-devel \
hwdata-devel \
libdisplay-info-devel \
libliftoff-devel \
vulkan-loader-devel \
glslang-devel \
libinput-devel \
xorg-x11-server-Xwayland-devel \
xcb-util-renderutil-devel \
'pkgconfig(xcb-ewmh)' \
'pkgconfig(gbm)' \
'pkgconfig(xkbcommon)' \
'pkgconfig(egl)' \
'pkgconfig(wayland-server)'
```

---

- wayland-protocols-devel is 1.31 in fedora >=1.32 is needed. so manually installing it

```bash
wget https://gitlab.freedesktop.org/wayland/wayland-protocols/-/releases/1.32/downloads/wayland-protocols-1.32.tar.xz
```

```bash
tar xf wayland-protocols-1.32.tar.xz
```

```bash
cd wayland-protocols-1.32 &&
mkdir build &&
cd    build &&
meson setup --prefix=/usr --buildtype=release &&
ninja
```

```bash
sudo ninja install
```

# Building & Installing Hyprland 

```bash
git clone --recursive https://github.com/hyprwm/Hyprland
cd Hyprland
meson --buildtype=release _build  
ninja -C _build
sudo ninja -C _build install
```