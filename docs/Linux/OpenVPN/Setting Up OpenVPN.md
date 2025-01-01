- Install OpenVPN
- Download the OpenVPN configurations from the VPN provider
- Place all the configurations in `/etc/openvpn` directory
- Pick two TCP and UDP server configurations and if the files contains `.ovpn` extension, make them `.conf` extension

```shell
sudo mv /etc/openvpn/server1.ovpn /etc/openvpn/server1.conf
```

- Start the systemd services to connect to the server

```shell
sudo systemctl enable --now openvpn@server1
```

- Systemd will prompt to get the username. Enter the username from the VPN provider
- Run following in another terminal and enter the password 

```shell
sudo systemd-tty-ask-password-agent
```

- Now the service should be running