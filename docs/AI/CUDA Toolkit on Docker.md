# CUDA Toolkit on Docker

## Pre-requisites

- Docker
- Nvidia proprietary driver
- [Nvidia container toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)

On NixOS, adding the Nvidia container toolkit is simple

```nix
virtualisation.docker = {
  enable = true;
  enableNvidia = enableNvidia;
};
```

## Getting Container

- `docker run -it --rm -v $(realpath ~/notebooks):/tf/notebooks -p 8888:8888 tensorflow/tensorflow:latest-gpu-jupyter`
