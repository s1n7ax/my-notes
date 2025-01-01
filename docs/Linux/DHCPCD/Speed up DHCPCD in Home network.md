Add following to `/etc/dhcpcd.conf` 

```
noarp
```

DHCP standard to verify via ARP if the assigned IP is not used by something else. This disables it