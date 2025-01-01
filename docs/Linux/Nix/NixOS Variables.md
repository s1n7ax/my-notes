# NixOS Variables

## How to check variables

Example: looking up `config.boot.kernelPackages.nvidiaPackages.stable` variable

`config.boot.kernelPackages` is an alias to `pkgs.linuxPackages` so the variable
can be found at `pkgs.linuxPackages.nvidiaPackages.stable`

- Spin up a repl `nix repl`
- Load nix packages `:l <nixpkgs>`
- access `pkgs.linuxPackages.nvidiaPackages.stable` to find the package
