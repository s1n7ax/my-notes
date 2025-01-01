# Enable polkit debug logs

- Create a polkit rule at `/etc/polkit-1/rules.d/00-log-access.rules`

```
polkit.addRule(function(action, subject) {
    polkit.log("action=" + action);
    polkit.log("subject=" + subject);
});
```

- Enable logging in `systemd` service by removing `--no-debug` flag in 
`/usr/lib/systemd/system/polkit.service` 

```
[Unit]
Description=Authorization Manager
Documentation=man:polkit(8)

[Service]
Type=dbus
BusName=org.freedesktop.PolicyKit1
ExecStart=/usr/lib/polkit-1/polkitd
```

- Restart the service

```shell
sudo systemctl daemon-reload
sudo systemctl restart polkit
```