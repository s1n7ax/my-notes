# nix-env

- Installing hello to current user environment

```shell
# installs hello to /nix/store and link the output to user invironment
nix-env -i hello
```

- List installed derivations

```shell
# list just the names
nix-env -q

# list the names and the paths in the user environment
nix-env -q --out-path
```

- Rollback to last generation

```shell
# rollback to the last generation
nix-env --rollback

# rollback to nth generation
nix-env -G 3
```
