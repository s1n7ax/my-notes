- Add static IP to `/etc/dhcpcd.conf` and replace the interface

```shell
interface eth0
static ip_address=192.168.1.110/24	
static routers=192.168.1.1
static domain_name_servers=192.168.1.1
```