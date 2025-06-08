# WireGuard Hub and Spoke Configuration Guide

## Overview

This guide covers setting up a WireGuard VPN in a Hub and Spoke topology with three hosts:

- **Endpoint A**: Client workstation (10.0.0.1)
- **Endpoint B**: Server with HTTP service (10.0.0.2)
- **Host C**: Hub/router (10.0.0.3)

The hub allows two endpoints behind NAT/firewalls to communicate through a central relay point.

## Step 1: Install WireGuard

Install WireGuard on all three hosts following the [official installation instructions](https://www.wireguard.com/install/).

Verify installation:

```bash
wg help
```

## Step 2: Generate WireGuard Keys

Generate key pairs for each host. Run these commands on each respective host for security:

**For Endpoint A:**

```bash
wg genkey > endpoint-a.key
wg pubkey < endpoint-a.key > endpoint-a.pub
```

**For Endpoint B:**

```bash
wg genkey > endpoint-b.key
wg pubkey < endpoint-b.key > endpoint-b.pub
```

**For Host C (Hub):**

```bash
wg genkey > host-c.key
wg pubkey < host-c.key > host-c.pub
```

This creates 6 files total:

- `*.key` files contain private keys (keep secret)
- `*.pub` files contain public keys (shared with peers)

## Step 3: Configure Host C (Hub)

Create `/etc/wireguard/wg0.conf` on Host C:

```ini
# /etc/wireguard/wg0.conf
# local settings for Host C
[Interface]
PrivateKey = [HOST_C_PRIVATE_KEY]
Address = 10.0.0.3/32
ListenPort = 51823

# remote settings for Endpoint A
[Peer]
PublicKey = [ENDPOINT_A_PUBLIC_KEY]
AllowedIPs = 10.0.0.1/32

# remote settings for Endpoint B
[Peer]
PublicKey = [ENDPOINT_B_PUBLIC_KEY]
AllowedIPs = 10.0.0.2/32
```

Set proper permissions:

```bash
sudo chown root:root /etc/wireguard/wg0.conf
sudo chmod 600 /etc/wireguard/wg0.conf
```

## Step 4: Configure Routing on Host C

Enable IP forwarding by adding this line to the Hub's config:

```ini
[Interface]
PrivateKey = [HOST_C_PRIVATE_KEY]
Address = 10.0.0.3/32
ListenPort = 51823
PreUp = sysctl -w net.ipv4.ip_forward=1
```

For IPv6, use:

```ini
PreUp = sysctl -w net.ipv6.conf.all.forwarding=1
```

## Step 5: Configure Endpoint A (Client Spoke)

Create `/etc/wireguard/wg0.conf` on Endpoint A:

```ini
# /etc/wireguard/wg0.conf
# local settings for Endpoint A
[Interface]
PrivateKey = [ENDPOINT_A_PRIVATE_KEY]
Address = 10.0.0.1/32
ListenPort = 51821

# remote settings for Host C
[Peer]
PublicKey = [HOST_C_PUBLIC_KEY]
Endpoint = [HOST_C_PUBLIC_IP]:51823
AllowedIPs = 10.0.0.0/24
```

Set proper permissions:

```bash
sudo chown root:root /etc/wireguard/wg0.conf
sudo chmod 600 /etc/wireguard/wg0.conf
```

## Step 6: Configure Endpoint B (Server Spoke)

Create `/etc/wireguard/wg0.conf` on Endpoint B:

```ini
# /etc/wireguard/wg0.conf
# local settings for Endpoint B
[Interface]
PrivateKey = [ENDPOINT_B_PRIVATE_KEY]
Address = 10.0.0.2/32
ListenPort = 51822

# remote settings for Host C
[Peer]
PublicKey = [HOST_C_PUBLIC_KEY]
Endpoint = [HOST_C_PUBLIC_IP]:51823
AllowedIPs = 10.0.0.0/24
PersistentKeepalive = 25
```

**Note:** `PersistentKeepalive = 25` keeps the connection open through NAT/firewalls.

Set proper permissions:

```bash
sudo chown root:root /etc/wireguard/wg0.conf
sudo chmod 600 /etc/wireguard/wg0.conf
```

## Step 7: Start WireGuard

On all three hosts, start the WireGuard service:

**With systemd:**

```bash
sudo systemctl enable wg-quick@wg0.service
sudo systemctl start wg-quick@wg0.service
```

**Without systemd:**

```bash
sudo wg-quick up /etc/wireguard/wg0.conf
```

## Step 8: Test the Connection

**On Endpoint B**, start a test web server:

```bash
# As root for port 80
sudo python3 -m http.server 80

# Or as regular user for port 8080
python3 -m http.server 8080
```

**On Endpoint A**, test connectivity:

```bash
curl 10.0.0.2
# or for port 8080:
curl 10.0.0.2:8080
```

If you see HTML output, the tunnels are working!

## Step 9: Basic Troubleshooting

### Check IP Forwarding

On Host C:

```bash
sudo sysctl net.ipv4.ip_forward
# Should return: net.ipv4.ip_forward = 1
```

### Check WireGuard Status

On all hosts:

```bash
sudo wg
```

Look for:

- **Interface is up**: Shows public key, listening port
- **Successful handshake**: Shows "latest handshake" field
- **Data transfer**: Shows bytes sent/received

### Common Issues

- **Connection refused**: Check IP forwarding on Hub
- **Hangs**: Check firewall rules allowing UDP traffic
- **No handshake**: Verify public/private key pairs match in configs

## Optional: Configure Firewall on Host C

Add iptables rules to secure the hub:

```ini
[Interface]
PrivateKey = [HOST_C_PRIVATE_KEY]
Address = 10.0.0.3/32
ListenPort = 51823
PreUp = sysctl -w net.ipv4.ip_forward=1
PreUp = iptables -A INPUT -i wg0 -m state --state ESTABLISHED,RELATED -j ACCEPT
PreUp = iptables -A INPUT -i wg0 -j REJECT
PreUp = iptables -A FORWARD -i wg0 -m state --state ESTABLISHED,RELATED -j ACCEPT
PreUp = iptables -A FORWARD -i wg0 -m state --state NEW -d 10.0.0.2 -p tcp --dport 80 -j ACCEPT
PreUp = iptables -A FORWARD -i wg0 -j REJECT
PostDown = iptables -D INPUT -i wg0 -m state --state ESTABLISHED,RELATED -j ACCEPT
PostDown = iptables -D INPUT -i wg0 -j REJECT
PostDown = iptables -D FORWARD -i wg0 -m state --state ESTABLISHED,RELATED -j ACCEPT
PostDown = iptables -D FORWARD -i wg0 -m state --state NEW -d 10.0.0.2 -p tcp --dport 80 -j ACCEPT
PostDown = iptables -D FORWARD -i wg0 -j REJECT
```

## Key Configuration Notes

### IP Address Planning

- Use private IP ranges (10.0.0.0/8, 192.168.0.0/16, 172.16.0.0/12)
- Hub needs IP forwarding enabled
- AllowedIPs on spokes should include the full VPN subnet
- AllowedIPs on hub should specify individual spoke IPs

### Port Configuration

- Hub must accept incoming UDP on its WireGuard port
- Spokes can use any available port (or let WireGuard choose)
- NAT/firewall must forward hub's WireGuard port

### Security Best Practices

- Generate keys on each host individually
- Set config files to 600 permissions (root only)
- Use PersistentKeepalive for spokes behind strict NAT
- Consider firewall rules to restrict forwarded traffic

## Quick Reference

| Host       | VPN IP   | Role         | Incoming Port | Config File |
| ---------- | -------- | ------------ | ------------- | ----------- |
| Endpoint A | 10.0.0.1 | Client Spoke | 51821         | wg0.conf    |
| Endpoint B | 10.0.0.2 | Server Spoke | 51822         | wg0.conf    |
| Host C     | 10.0.0.3 | Hub/Router   | 51823         | wg0.conf    |
