# System requirements

dentOS depends on the following software:
- [GNU Make](https://www.gnu.org/software/make)
- [Docker](https://docs.docker.com/get-docker)
- `binfmt support` package (required for ppc builds)
- `apt-transport-htpps` package

On Debian Linux system these packages can be installed using the `apt` package manager:
```
~ $ sudo apt install make docker binfmt-support apt-transport-https
```
Building all images will require about 40 GB of free disk space, and since compilation is a memory intensive process, it is recommended to build on a machine with at least 4 GB of RAM memory and 4 GB of swap memory. The build system also requires Docker to be installed and properly configured on the host system. 


For testing purposes Debian version 10 was used along with the following sotfware versions:
```
- GNU Make 4.3
- Docker 20.10.9
```
Testing was also performed on the Gentoo Linux and in general, any Linux distribution providing required packages should be able to build the dentOS images. Hardware testing was done on the arm64 device.
