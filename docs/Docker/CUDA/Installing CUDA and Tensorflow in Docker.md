# Installing CUDA in Docker

## Compose file

[docker-tensorflow-with-cuda](https://github.com/s1n7ax/docker-tensorflow-with-cuda)

## Steps

- Install the Nvidia driver in the host machine

- Run `nvidia-smi` you should see `CUDA Version: XX.X` in the output

```text
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 545.29.02              Driver Version: 545.29.02    CUDA Version: 12.3     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce GTX 1060 6GB    Off | 00000000:05:00.0  On |                  N/A |
|  0%   43C    P8              10W / 200W |    432MiB /  6144MiB |      0%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+
```

- Install `nvidia-container-toolkit` in the host machine using
  [following installation guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html).
  For NixOS, follow
  [this guide](../../Linux/Nix/Enable%20Nvidia%20Container%20Toolkit.md)

- Install docker
  [following the installation guide](https://docs.docker.com/engine/install/)

- Pull the Tensorflow container with GPU support

```bash
docker pull tensorflow/tensorflow:latest-gpu
```

- Test out the environment

```bash
# open bash in container
docker run --gpus all -it tensorflow/tensorflow:latest-gpu bash

# check if the GPU is detected
nvidia-smi

# if the GPU is detected, then the list should contain at least one GPU
python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"

# output
# [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```
