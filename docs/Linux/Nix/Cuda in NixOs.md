# CUDA in NixOS

- Add CUDA binary cache to speed up the process

```bash
# this will add cachix and cachix.nix to the /etc/nixos path
nix-shell -p cachix
sudo cachix use cuda-maintainers
```

- Import the `cachix.nix` to the configuration to use cuda-maintainers cache

```nix
  imports = [
    ./cachix.nix
    ./hardware-configuration.nix
  ];
```

- Rebuild to enable the changes

```bash
sudo nixos-rebuild switch
```
