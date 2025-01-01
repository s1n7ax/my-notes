# Neovim in Devcontainer

## What is Devcontainer?

- Development container is a container configured for development
- [Devcontainer Specification](https://containers.dev/implementors/spec/)
- [Devcontainer CLI](https://github.com/devcontainers/cli)

---

## Disclaimer

- You don't need Devcontainer to do development using Neovim inside a container

---

## Why Devcontainers?

- Reproducible development environment
- Easy to add features
- Managing containers are easy
- Environment could be as simple as the base image or as complex as a compose file with multiple services
- ~~Support editor integration~~

---

## Can I use Neovim?

- Is there a terminal? Then yes
- Remote access to Neovim is also possible but you need to handle the port mapping by yourself

```shell
# Server:
nvim --listen 0.0.0.0:8888 --headless
```

```shell
# Client:
nvim --server localhost:8888 --remote-ui
```

---

## How to use Neovim

- Create the devcontainer spec inside the project `.devcontainer/devcontainer.json`

```json
{
  "name": "spring boot container",
  "image": "ubuntu:latest",
  "features": {
    "ghcr.io/s1n7ax/devcontainer-features/jdk21:0": {},
    "ghcr.io/s1n7ax/devcontainer-features/neovim-essentials:0": {},
    "ghcr.io/s1n7ax/devcontainer-features/neovim:0": {},
    "ghcr.io/s1n7ax/devcontainer-features/astronvim:0": {}
  }
}
```

- Start the container

```shell
devcontainer up --workspace-folder .
```

- Start up Neovim

```shell
devcontainer exec --workspace-folder . nvim
```

---

## Other Useful Devcontainer Options

- `--remove-existing-container` - to rebuilds the image

```shell
devcontainer up --workspace-folder . --remove-existing-container
```

- `--mount` - to mount neovim user config

```shell
devcontainer up --workspace-folder . --mount 'type=bind,source=/home/s1n7ax/.config/astronvim,target=/root/.config/astronvim'
```

- `--additional-features` - if you don't want to edit the `devcontainer.json` but want to use Neovim, use this flag to add additional features

```shell
devcontainer up --workspace-folder . --additional-features '{ "ghcr.io/s1n7ax/devcontainer-features/lookatme:0": {}" }'
```

- `--dotfiles-repository` - personalize the container with your dotfiles

```shell
devcontainer up --workspace-folder . --dotfiles-repository "https://github.com/s1n7ax/dothome.git"
```

---

## Challenges of Creating features

- Dependency of features?

  - `installsAfter` to mark dependencies of a feature but these will be ignored if `devcontainer.json` does not use theme

    ```json
    # this is a part of the astronvim feature
    # devcontainer-feature.json
    "installsAfter": [
        "ghcr.io/s1n7ax/devcontainer-features/neovim-essentials:0",
        "ghcr.io/s1n7ax/devcontainer-features/neovim:0"
    ]
    ```

    ```json
    # devcontainer.json
    {
      "name": "Ubuntu image just for demo",
      "image": "ubuntu:latest",
      "features": {
        "ghcr.io/s1n7ax/devcontainer-features/jdk21:0": {},
        "ghcr.io/s1n7ax/devcontainer-features/neovim-essentials:0": {},
        "ghcr.io/s1n7ax/devcontainer-features/neovim:0": {},
        "ghcr.io/s1n7ax/devcontainer-features/astronvim:0": {}
      }
    }
    ```

    - It appears devcontainer supposed to be self contained?

- Features works only on the targeted base images
- No build logs on test success

---

## Disadvantages

- Containers does not completely resolve package conflicts
- While it's fun to plug in features, not so much to create them
- Containers are not 100% reproducible
