# Tunneling to Homelab using Wireguard and Docker

> [!IMPORTANT] The generated peer1.conf file does not work as it is. You need to change the `Address` field to add the subnet
> Before `Address = 10.0.0.2`
> After `Address = 10.0.0.2/32`

## Hub and Spoke Topology

[More info](https://www.procustodibus.com/blog/2020/11/wireguard-hub-and-spoke-config)

## Setup hub

- Go to vps and create a compose for the wireguard hub

```yaml
services:
  wireguard:
    image: lscr.io/linuxserver/wireguard:latest
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE #optional
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - SERVERURL=64.xxx.xxx.xxx # UPDATE THE HUB IP ADDRESS
      - SERVERPORT=51820
      - PEERS=2
      - INTERNAL_SUBNET=10.0.0.0
      - ALLOWEDIPS=10.0.0.0/24
      - LOG_CONFS=true
    volumes:
      - ./data:/config/
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```

- Run the compose file. In the first run, compose file will generate the peer details and generate and log QR code to scan with the phone app.
- Go to the container and copy the content of `/config/peer1/peer1.conf` to homelab
- Get the log of the container to see the QR code for the 2nd peer and add the VPN to the phone app.
