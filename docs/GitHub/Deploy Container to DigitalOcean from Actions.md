# Deploy Container to DigitalOcean from Github Actions

[Follow this](https://gist.github.com/danieltorscho/c104c23e97c840f09fd9a186ec092b28)
for more secure approach

- Create a new droplet
- Generate a new SSH key in the local machine

```bash
ssh-keygen
```

- Copy the public key and create a new SSH key in droplet using the public key

```bash
wl-copy < .ssh/digitalocean.pub
```

- Tell ssh to use `digitalocean` private key when connecting to droplet ip

```text
# ~/.ssh/config

Host xxx.xxx.xxx.xxx
  HostName xxx.xxx.xxx.xxx
  User root
  IdentityFile /home/s1n7ax/.ssh/digitalocean
```

- Test the connection

```bash
# following should ask to to add the key to the known hosts for the first time
# you should be able to log in to the droplet

ssh xxx.xxx.xxx.xxx
```

- Create a secret in GitHub for the SSH private key

```bash
wl-copy < .ssh/digitalocean.pub
```

- [Follow these instructions to](https://docs.docker.com/engine/install/ubuntu/)
  install docker inside the droplet
