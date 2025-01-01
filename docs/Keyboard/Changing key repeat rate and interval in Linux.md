# xinitrc to run X11

pass `-ardelay` and `arinterval` flags to `X11` using `~/.xserverrc`

```sh
exec /usr/bin/X -ardelay 200 -arinterval 100 -nolisten tcp "$@"
```

# Lightdm