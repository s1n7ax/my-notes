- Use the mac ID of the interface in NetworkManager to avoid sudden mac changes

- configure dhcpcd static ip for IP reservation
- iwd to set a static ip
- use iwd

```bash
sudo systemctl disable resolvconf.service
```

You can get DNS resolution details using following command if you are using `systemd-resolved`:

```bash
resolvectl status

```

```
# /etc/iwd/main.conf
[Network]
NameResolvingService=resolvconf
```

