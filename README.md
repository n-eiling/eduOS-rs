# eduOS-rs - A teaching operating system written in Rust

## Status

|   | Build & Test |
|---|:-----:|
|**all OS'**|[![Build & Test](https://dev.azure.com/RWTH-OS/eduOS-rs/_apis/build/status/RWTH-OS.eduOS-rs)](https://dev.azure.com/RWTH-OS/eduOS-rs/_build?definitionId=1)|
|**Linux only**|[![Build & Test](https://git.rwth-aachen.de/os/eduOS-rs/badges/master/pipeline.svg)](https://git.rwth-aachen.de/os/eduOS-rs/pipelines)|

## Introduction

<p align="center"><img src="/img/demo.gif?raw=true"/></p>

eduOS-rs is a Unix-like operating system based on a monolithic architecture for educational purposes.
It is developed for the course [Operating Systems][acsos] at RWTH Aachen University and includes a modified hypervisor that simplifies the boot process to increase the intelligibility of the OS.
eduOS-rs is derived from following tutorials and software distributions:

1. Philipp Oppermann's [excellent series of blog posts][opp].
2. Erik Kidd's [toyos-rs][kidd], which is an extension of Philipp Opermann's kernel.
3. The original version of [eduOS][stlankes], which was the old teaching kernel written in C.

[opp]: http://blog.phil-opp.com/
[kidd]: http://www.randomhacks.net/bare-metal-rust/
[stlankes]: http://rwth-os.github.io/eduOS/
[rust-barebones-kernel]: https://github.com/thepowersgang/rust-barebones-kernel
[acsos]: http://www.os.rwth-aachen.de/

## Requirements to build eduOS-rs
eduOS-rs is tested under Linux, macOS, and Windows.

### macOS
Apple's *Command Line Tools* must be installed.
The Command Line Tool package gives macOS terminal users many commonly used tools and compilers, that are usually found in default Linux installations.
The following terminal command installs these tools without Apple's IDE Xcode:

```sh
$ xcode-select --install
```

### Windows
To build eduOS-rs on Windows you have to install a linker, [make](http://gnuwin32.sourceforge.net/packages/make.htm) and a [git client](https://git-scm.com/downloads).
We tested eduOS-rs with the linker from Visual Studio.
Consequently, we suggest installing Visual Studio in addition to [make](http://gnuwin32.sourceforge.net/packages/make.htm) and [git](https://git-scm.com/downloads).

### Linux
Linux users should install common developer tools.
For instance, on Ubuntu 18.04 the following command installs the required tools:

```sh
$ apt-get install -y curl wget nasm make autotools-dev gcc g++ build-essential
```

### Common for macOS, Windows and Linux
It is required to install the Rust toolchain.
Please visit the [Rust website](https://www.rust-lang.org/) and follow the installation instructions for your operating system.
It is important that the *nightly channel* is used to install the toolchain.
This is queried during installation and should be answered appropriately.

Building the kernel also requries the installation of *cargo-xbuild* and the source code of Rust runtime:

```sh
$ cargo install cargo-xbuild
$ rustup component add rust-src
```

eduOS-rs is able to run within [ehyve](https://github.com/RWTH-OS/ehyve), a specialized hypervisor for eduOS-rs.
[ehyve](https://github.com/RWTH-OS/ehyve) may be installed using cargo:

```sh
$ cargo install --git https://github.com/RWTH-OS/ehyve.git
```

Please check if your system fullfills ehyve's [system requirements](https://github.com/RWTH-OS/ehyve).

## Building
As a final step, create a copy of the repository and build the kernel:

```sh
$ # Get our source code.
$ git clone https://github.com/RWTH-OS/eduOS-rs.git
$ cd eduOS-rs

$ # Build kernel
$ make
```

The kernel can now be run the kernel in ehyve:

```sh
$ make run
```

## Overview of all branches

Step by step (here branch by branch) the operating system design is introduced.
This tutorial shows the steps of operating system development from a minimal kernel up to a Unix-like computer operating system.
Currently, the following stages of development are available:

0. stage0 - Smallest HelloWorld in the World

   Description of loading a minimal 64bit kernel

1. stage1 - Cooperative/non-preemptive multitasking

   Introduction into a simple form of multitasking, where no interrupts are required.

2. stage2 - Priority-based cooperative/non-preemptive multitasking

   Introduction into a simple form of priority-based multitasking, where no interrupts are required.

3. stage3 - Synchronization primitives

   Introduce basic synchronization primitives

4. stage 4 - Preemptive multitasking

   Introduction into preemptive multitasking and interrupt handling

5. stage 5 - Support of user-level tasks

   Add support of user-level tasks with an small interface for basic system calls

6. stage 6 - Support of paging

   Add support for paging and a simple demo of process creation

7. stage 7 - Integration of an in-memory file system

   Introduce a virtual file system with an in-memory file system as example file system.

8. stage8 - Run Linux application as common process

   Start a simple Linux application (_HelloWorld_) on top of eduOS-rs. The application is a _position-independent executable_ (PIE) and use [musl-libc](http://www.musl-libc.org) as standard C library.

## Useful Links

1. [http://www.gnu.org/software/grub/manual/multiboot/](http://www.gnu.org/software/grub/manual/multiboot/)
2. [http://www.osdever.net/tutorials/view/brans-kernel-development-tutorial](http://www.osdever.net/tutorials/view/brans-kernel-development-tutorial)
3. [http://www.jamesmolloy.co.uk/tutorial_html/index.html](http://www.jamesmolloy.co.uk/tutorial_html/index.html)
4. [http://techblog.lankes.org/tutorials/](http://techblog.lankes.org/tutorials/)
5. [http://www.os.rwth-aachen.de](http://www.os.rwth-aachen.de)
6. [http://www.noteblok.net/2014/06/14/bachelor](http://www.noteblok.net/2014/06/14/bachelor)
7. [https://sourceware.org/newlib/](https://sourceware.org/newlib/)
8. [http://rwth-os.github.io/eduOS/](http://rwth-os.github.io/eduOS/)
9. [https://intermezzos.github.io](https://intermezzos.github.io)

## License

Licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.
