# NixOS Secret Management with Sops

We can use,

- gpg
- age

## Generate a GPG key

```bash
gpg --full-generate-key
```

## Generate an age key

```bash
mkdir -p ~/.config/sops/age/
age-keygen -o ~/.config/sops/age/keys.txt
```
