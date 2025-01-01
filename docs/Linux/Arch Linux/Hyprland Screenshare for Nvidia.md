# Issue

When `/usr/lib/xdg-desktop-portal-hyprland` is ran manually and use OBS to capture the  screen, the process fails.

Running:

```shell
killall xdg-desktop-portal-hyprland
killall xdg-desktop-portal
/usr/lib/xdg-desktop-portal-hyprland
```

Error:

```txt
❯ /usr/lib/xdg-desktop-portal-hyprland
warning: queue 0x565497b8a9d0 destroyed while proxies still attached:
  zwp_linux_dmabuf_feedback_v1@40 still attached
  zwp_linux_dmabuf_v1@41 still attached
2023/08/10 01:08:31 [ERROR] - xdg-desktop-portal-hyprland: unsupported wl_shm format 0x34324742
[1]    16041 IOT instruction (core dumped)  /usr/lib/xdg-desktop-portal-hyprland
```

# Solution

From [Screen sharing on Hyprland (Arch Linux)](https://gist.github.com/PowerBall253/2dea6ddf6974ba4e5d26c3139ffb7580#file-screen-sharing-hyprland-md)

Remove `hyprland` and install `hyprland-nvidia-git` package

```
yay -S hyprland-nvidia-git
```