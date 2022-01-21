# Building dentOS

This section will explain how to build dentOS from source.

# Structure
The build system repository structure is as follows:
- `builds/` - contains architecture-specific configuration files
- `docker/` - contains Docker configurations for all available builds (e.g. Debian 8, Debian 9 builds)
- `docs/` - contains documentation
- `make/` - contains make rules
- `packages/` - contain package configuration, custom patches, etc.
- `tools/` - contains scripts which drive the build system

DentOS binaries can be obtaining by downloading pre-built binaries, which are available at https://nexus.dent.dev/content/repositories/releases/org/dent/1.0 or by manually compiling from source.
Compilation from source, being more time and resource demanding, has some advantages, such as that it enables us to include additional package [1] or drop others from the default configuration. We can also change various environment variables, such as compilation flags to optimize the built binaries for a selected architecture while on the other hand pre-built binaries and images are built generically and can't be customized in detail.

dentOS uses the Docker environment inside which the build process is executed.
As already mentioned, compilation is a resource intensive process.
Officially supported platform for building images is the Debian Linux distribution (versions 8-10), although generic compilation inside a Docker container should work on any Linux Distribution (assuming Docker is setup properly). Detailed instructions on how to install and configure Docker engine on Debian Linux can be found [here](https://docs.docker.com/engine/install/debian).
dentOS uses Dockerized Buildroot-like Makefiles where integration is based on the direct Makefile inclusion.
Many custom Python scripts are used to drive the build in the `./tools` directory. Before executing a target, the top-level Makefile include `./make/config.mk` file.
Entrypoint to the build system is a python script in `./tools/docker/onlbuilder`. This build system is capable of building a ONIE-compatible installer.
Currently supported architectures are: 
- `amd64`
- `arm` (`armel` and `armhf`)
- `arm64`
- `ppc`

 To start the build process is it enough to invoke the `make` command inside a local copy of the repository.
 ```
 ~ $ git clone clone https://github.com/dentproject/dentOS.git
 ~ $ cd dentOS
 ~ $ make docker
 ```
 This will by default build a Debian 9 based image. In order to build an image which is based on the different Debian version we can specify the `VERSION` variable in the `make` command,:
 ```
 # build a Debian 8 based image
 ~ $ make docker VERSION=8
 ```
 
Note that when setting up the Docker engine, it is often necessary to add your user to the “docker” group. This will enable using docker for non-privileged users.


[1] https://packages.debian.org/stable/
