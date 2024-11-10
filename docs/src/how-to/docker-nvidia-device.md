# How to use NVIDIA GPU in Docker

WSL supports NVIDIA-based GPU acceleration, there are many use cases including
machine learning or general compute acceleration. Since Docker version 25, the
use of `virtualisation.docker.enableNvidia` has been deprecated in favour of a
more standard specification called Container Device Interface.

1. Enable the NVIDIA Container Toolkit and disable the mounting of executables,
   as this will cause an problem related to missing libraries.

```nix
hardware.nvidia-container-toolkit = {
  enable = true;
  mount-nvidia-executables = false;
};
```

2. As of Docker 25, the Docker daemon doesn't have the CDI feature enabled by
   default. by default, so we need to enable it.

```nix
virtualisation.docker = {
  enable = true;
  daemon.settings.features.cdi = true;
};
```
