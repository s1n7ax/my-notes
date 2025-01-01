```shell
sudo cat /var/lib/iwd/s1n7ax.psk
[IPv4]
DNS=192.168.1.1
Address=192.168.1.110
Netmask=255.255.255.0
Gateway=192.168.1.1
```

```shell
[General]
# iwd is capable of performing network configuration on its own, including
# DHCPv4 based address configuration.  By default this behavior is
# disabled, and an external service such as NetworkManager, systemd-network
# or dhcpclient is required.  Uncomment the following line if you want iwd
# to manage network interface configuration.
#
EnableNetworkConfiguration=true

[Network]
# If EnableNetworkConfiguration=true is set, iwd forwards DNS information to
# the system resolving service.  The currently supported services are:
# - systemd-resolved ["systemd"]
# - openresolv / resolvconf ["resolvconf"]
#
# If not set, the value "systemd" is used by default.  Uncomment the value
# below if you are using openresolv:
#
NameResolvingService=systemd
```