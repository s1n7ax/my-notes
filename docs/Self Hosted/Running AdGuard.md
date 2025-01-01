# Running AdGuard

Following is the compose file to run AdGuard Home on a server.

```yaml
adguardhome:
  image: adguard/adguardhome
  container_name: adguardhome
  volumes:
    - ./data/adguardhome/workdir:/opt/adguardhome/work
    - ./data/adguardhome/confdir:/opt/adguardhome/conf
  ports:
    - 53:53/tcp
    - 53:53/udp
    - 67:67/udp
    - 68:68/udp
    - 80:80/tcp
    - 443:443/tcp
    - 443:443/udp
    - 3000:3000/tcp
    - 853:853/tcp
    - 784:784/udp
    - 853:853/udp
    - 8853:8853/udp
    - 5443:5443/tcp
    - 5443:5443/udp
```

When running the `docker compose up`, AdGuard failed due to a process already using port 53. The solution was to stop the process using the port.

To resolve that, dns resolver should be stopped first.

On OragnePi, the command to stop the dns resolver is:

```bash
sudo systemctl stop dnsmasq.service
sudo systemctl disable dnsmasq.service
```

AdGuard Home can be accessed at `http://<server-ip>:3000` after the service is up and running.
