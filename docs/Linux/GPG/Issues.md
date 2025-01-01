# Fix-error: unsafe permissions on homedir

```shell
chown -R $(whoami) ~/.gnupg/
chmod 600 ~/.gnupg/*
chmod 700 ~/.gnupg
```

# Fix-error: There is no assurance this key belongs to the named user

```shell
gpg --edit-key <KEY_ID>
gpg> trust

1 = I don't know or won't say
2 = I do NOT trust
3 = I trust marginally
4 = I trust fully
5 = I trust ultimately
m = back to the main menu

Your decision? 5
Do you really want to set this key to ultimate trust? (y/N) y

gpg> quit
```