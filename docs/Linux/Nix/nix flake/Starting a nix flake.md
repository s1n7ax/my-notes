- Create a new directory for flakes

```shell
mkdir nix-flakes
cd nix-flakes
```

- Initialize nix flake

```shell
nix flake init
```

- Initialize a git repository

```shell
git init
```

- Add the flake.nix file

```shell
git add .
```

- Run nix build to build the flake

```shell
# -L for build logs
nix build -L .
```
