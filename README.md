## containerd-nerdctl for gokrazy

This package contains the static build of https://github.com/containerd/containerd / https://github.com/opencontainers/runc / https://github.com/containerd/nerdctl

This is an alternative to [podman in gokrazy](https://gokrazy.org/packages/docker-containers/). It's larger but has less dependencies.

### Usage

```
gok add github.com/ascension-association/gk-containerd-nerdctl
gok update
```

The sections below assume you are logged into to your gokrazy device using
[breakglass](https://github.com/gokrazy/breakglass).


#### Run a container

```
mkdir -p /perm/cni/net.d
nerdctl pull docker.io/library/alpine:latest && nerdctl run --net host --cni-path /perm/cni --cni-netconfpath /perm/cni/net.d --rm -it docker.io/library/alpine:latest /bin/ash
```

#### Optional: tmpfs

By default, containers are stored on disk (`/var` is a symlink to `/perm/var` on
the permanent data partition). If you only want to try something out without
keeping the containers around across reboots, it is faster to work in RAM:

```
mount -t tmpfs tmpfs /var
```
