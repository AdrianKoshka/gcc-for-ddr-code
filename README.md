# Toolchain for Marvell DDR Code

This is meant to be a companion repo to [this blog post](https://blog.xn--adrianlucrcecleste-0vbx.page/posts/marvell-drr-code-and-gcc/) about my struggles with compiling Marvell's DDR code for the MACCHIATObin singleshot.

## What's here?

A specific source code archive of `gcc` and `binutils`, and instructions on how to build them on Debian 12.

## How do I build this?

I'll try to give you the cut down version, a bit modified from the blog post, after cloning the repository:

### Packages needed

```shell
$ sudo apt install build-essential acpica-tools device-tree-compiler uuid-dev libssl-dev gcc-aarch64-linux-gnu texinfo bison help2man --install-recommends -y
```

### GCC

```shell
$ cd toolchain-for-ddr-code
toolchain-for-ddr-code$ tar xvf gcc-11.4.0.tar.xz
toolchain-for-ddr-code$ mkdir objdir
toolchain-for-ddr-code$ cd gcc-11.4.0
toolchain-for-ddr-code/gcc-11.4.0$ ./contrib/download_prerequisites
toolchain-for-ddr-code/gcc-11.4.0$ cd ../objdir
toolchain-for-ddr-code/objdir$ $PWD/../gcc-11.4.0/configure --prefix=$HOME/buildroot/11.4.0 --enable-languages=c,c++,lto --enable-lto --disable-nls --disable-libquadmath --disable-libquadmath --enable-default-pie --disable-werror --enable-linker-build-id
toolchain-for-ddr-code/objdir$ make -j5
toolchain-for-ddr-code/objdir$ make install
```

### Binutils

```shell
$ cd toolchain-for-ddr-code
toolchain-for-ddr-code$ tar xvf binutils-2.40.tar.xz
toolchain-for-ddr-code$ cd binutils-2.40
toolchain-for-ddr-code/binutils-2.40$ ./configure --prefix=$HOME/buildroot/11.4.0/ ./configure --prefix=$HOME/buildroot/11.4.0/ --enable-lto --enable-year2038 --with-pic --enable-deterministic-archives
toolchain-for-ddr-code/binutils-2.40$ make -j5
toolchain-for-ddr-code/binutils-2.40$ make install
```