1. Open a shell with following dependencies

```shell
nix shell flake:nixpkgs#cmake flake:nixpkgs#gettext
```

1. Make changes to Neovim
1. Build and test using `make build`
1. Run `make doc` to update documentation
1. Commit and push
