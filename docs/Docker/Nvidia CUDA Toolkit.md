# Nvidia CUDA Toolkit

On Nixos, you can enable the `hardware.nvidia-container-toolkit.enable = true`
to install the nvidia container toolkit.

```bash
podman run --rm -it --device=nvidia.com/gpu=all ubuntu:latest nvidia-smi
```

```bash
docker run --rm -it --device=nvidia.com/gpu=all ubuntu:latest nvidia-smi
```

https://github.com/NixOS/nixpkgs/issues/337873#issuecomment-2320357105
