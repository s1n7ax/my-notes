# Disable swap file in Orange PI

```bash
sudo swapoff -a
sudo rm -f /swapfile
sudo systemctl disable swapfile.swap
```
