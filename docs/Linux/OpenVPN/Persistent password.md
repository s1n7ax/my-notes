- Add the username and password in a file

```
<username>
<password>
```

- Set permissions for the password file

```shell
chown root:root /etc/path/to/file.txt
chmod 000 /etc/path/to/file.txt
```

- Edit systemd service to check the file for username and password

```
# add --auth-user-pass /etc/path/to/file.txt
ExecStart=/usr/sbin/openvpn --daemon ovpn-%i --status /run/openvpn/%i.status 10 --cd /etc/openvpn --config /etc/openvpn/%i.ovpn --writepid /run/openvpn/% i.pid --auth-user-pass /etc/path/to/file.txt
```

- Reload the daemon

```shell
sudo systemctl daemon-reload
```

- Start the service

```
systemctl enable --now openvpn@server1
```
