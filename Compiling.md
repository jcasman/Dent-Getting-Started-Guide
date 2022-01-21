# Compiling applications

This section will explain how to add new package to the dentOS build system.

The `builds/any/rootfs/$version/common` directory [1] contains per-architecture configurations for default packages that are indluded in the build process, where `$version` represents the targedet Debian version.
Currently available options are:
- `buster` - Debian 10 based configuration
- `jessie` - Debian 8 based configuration
- `stretch` - Debian 9 based configuration
- `wheezy` - Debian 7 based configuration

`all-base-packages.yml` contains base set of packages that are included in all targets, while additional files define architecture specific packages. 

[1] - https://github.com/dentproject/dentOS/tree/main/builds/any/rootfs/stretch/common
