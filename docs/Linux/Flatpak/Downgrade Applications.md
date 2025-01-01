- Get the available versions of the application

```shell
flatpak remote-info --log flathub org.gnome.Boxes
```

- Downgrade to the commit of the version

```shell
flatpak update --commit=d46b5bf5a2a0e2493af730551b13d561d025a347e3592a6cc0a95047c8022bf4 org.gnome.Boxes
```