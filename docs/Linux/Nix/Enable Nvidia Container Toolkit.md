# Enable Nvidia Container Toolkit

- Add the following to the NixOS configuration

```nix
virtualisation = {
  docker = {
    enable = true;
    enableNvidia = true;
  };
};
```
