# Clean up the generations

```bash
nix-env --list-generations

nix-collect-garbage  --delete-old

# this does not work
nix-collect-garbage  --delete-generations 1 2 3

# recommended to sometimes run as sudo to collect additional garbage
sudo nix-collect-garbage -d

# As a separation of concerns - you will need to run this command to clean out boot
sudo /run/current-system/bin/switch-to-configuration boot
```

## Upgrading

```bash
nixos-rebuild switch --upgrade
# above is equivalent to following two commands
# nix-channel --update nixos && nixos-rebuild switch
```
