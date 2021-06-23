# Ledger Nano X Application Builder

This container image contains all dependencies to compile an application for the Nano X.

## Build the container image

### Standard Build

Container can be build using standard tools:

```bash
# Docker
sudo docker build -t nanox-app-builder .
# Podman (from https://podman.io/)
podman build -t nanox-app-builder .
# Buildah (from https://buildah.io/)
buildah bud -t nanox-app-builder .
```

### App Scanner

Image can embed the [Coverity Scan](https://scan.coverity.com/) build tool. It is an excellent static analysis tool, and it can be very useful to find bugs in Nano apps.

The build tool must be downloaded before building the image. Archive can be downloaded from <https://scan.coverity.com/download>. Download is available to everyone, but it requires to create an account. After having registered, download Coverity Build Tool 2020.09 for Linux64 and place the downloaded archive in the `coverity` directory.

Then, build container with:

```bash
# Docker
sudo docker build -t nanox-app-scanner .
# Podman (from https://podman.io/)
podman build -t nanox-app-scanner .
# Buildah (from https://buildah.io/)
buildah bud -t nanox-app-scanner .
```

## Compile your app in the container

In the source folder of your Nano X application:

```bash
$ # docker can be replaced with podman or buildah without sudo
$ sudo docker run --rm -ti -v "$(realpath .):/app" nanox-app-builder
root@656be163fe84:/app# make
```

The Docker image includes the [Clang Static Analyzer](https://clang-analyzer.llvm.org/), which can be invoked with:

```bash
$ # docker can be replaced with podman or buildah without sudo
$ sudo docker run --rm -ti -v "$(realpath .):/app" nanox-app-builder
root@656be163fe84:/app# make scan-build
```
