# nix-store

- List direct runtime dependencies of a derivation

```shell
# only the direct runtime dependencies
nix-store -q --references `which hello`

# list the closure
# this includes every dependency recursivly to run the hello
# command
nix-store -qR `which hello`

# list the closure but in a tree structure
nix-store -q --tree `which hello`
```

- List derivations depending on the given derivation

```shell
nix-store -q --referrers `which hello`
```
