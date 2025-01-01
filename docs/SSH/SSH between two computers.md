- Generate the ssh key in the client
- Add the configuration to use the key for the server

```shell
Host 192.168.1.110
    HostName 192.168.1.110
    User orangepi
    IdentityFile /home/s1n7ax/.ssh/home_server
```

- Log into the server using SSH using password
- Create the `.ssh/authorized_keys` file and copy the content from `.ssh/key.pub`
- Restart the ssh agent `eval $(ssh-agent -s)`
- Now you can directly ssh without password

## Setting permissions for the SSH

[More info](https://superuser.com/a/1559867)

```bash
chown -R orangepi:orangepi .ssh/
chmod 700 .ssh
chmod 600 .ssh/authorized_keys
```

