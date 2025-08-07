# Noxcoin

Copyright (c) 2025, The Noxcoin

## Table of Contents

  - [Development resources](#development-resources)
  - [Vulnerability response](#vulnerability-response)
  - [Research](#research)
  - [Announcements](#announcements)
  - [Translations](#translations)
  - [Coverage](#coverage)
  - [Introduction](#introduction)
  - [About this project](#about-this-project)
  - [Supporting the project](#supporting-the-project)
  - [License](#license)
  - [Contributing](#contributing)
  - [Scheduled software upgrades](#scheduled-software-upgrades)
  - [Release staging schedule and protocol](#release-staging-schedule-and-protocol)
  - [Compiling Noxcoin from source](#compiling-noxcoin-from-source)
    - [Dependencies](#dependencies)
    - [Guix builds](#guix-builds)
  - [Internationalization](#Internationalization)
  - [Using Tor](#using-tor)
  - [Pruning](#Pruning)
  - [Debugging](#Debugging)
  - [Known issues](#known-issues)

## Development resources

- Web: [noxcoin.org](https://noxcoin.org)
- GitHub: [https://github.com/noxcoin-project/noxcoin](https://github.com/noxcoin-project/noxcoin)
- It is HIGHLY recommended that you join the #noxcoin-dev IRC channel if you are developing software that uses Noxcoin. Due to the nature of this open source software project, joining this channel and idling is the best way to stay updated on best practices and new developments in the Noxcoin ecosystem. All you need to do is join the IRC channel and idle to stay updated with the latest in Noxcoin development. If you do not, you risk wasting resources on developing integrations that are not compatible with the Noxcoin network. The Noxcoin core team and community continuously make efforts to communicate updates, developments, and documentation via other platforms – but for the best information, you need to talk to other Noxcoin developers, and they are on IRC. #noxcoin-dev is about Noxcoin development, not getting help about using Noxcoin, or help about development of other software, including yours, unless it also pertains to Noxcoin code itself. For these cases, checkout #noxcoin.

## Vulnerability response

- Our [Vulnerability Response Process](https://github.com/noxcoin-project/meta/blob/master/VULNERABILITY_RESPONSE_PROCESS.md) encourages responsible disclosure
- We are also available via [HackerOne](https://hackerone.com/noxcoin)

## Research

The [Noxcoin Research Lab](https://src.noxcoin.org/resources/research-lab/) is an open forum where the community coordinates research into Noxcoin cryptography, protocols, fungibility, analysis, and more. We welcome collaboration and contributions from outside researchers! Because not all Lab work and publications are distributed as traditional preprints or articles, they may be easy to miss if you are conducting literature reviews for your own Noxcoin research. You are encouraged to get in touch with the Noxcoin research community if you have questions, wish to collaborate, or would like guidance to help avoid unnecessarily duplicating earlier or known work.

The Noxcoin research community is available on IRC in [#noxcoin-research-lab on Libera](https://web.libera.chat/#noxcoin-research-lab), which is also accessible via Matrix.

## Announcements

## Translations
The CLI wallet is available in different languages. If you want to help translate it, see our self-hosted localization platform, Weblate, on [translate.noxcoin.org]( https://translate.noxcoin.org/projects/noxcoin/cli-wallet/). Every translation *must* be uploaded on the platform, pull requests directly editing the code in this repository will be closed. If you need help with Weblate, you can find a guide with screenshots [here](https://github.com/noxcoin-ecosystem/noxcoin-translations/blob/master/weblate.md).
&nbsp;

If you need help/support/info about translations, contact the localization workgroup. You can find the complete list of contacts on the repository of the workgroup: [noxcoin-translations](https://github.com/noxcoin-ecosystem/noxcoin-translations#contacts).

## Coverage

| Type      | Status |
|-----------|--------|
| Coverity  | [![Coverity Status](https://scan.coverity.com/projects/9657/badge.svg)](https://scan.coverity.com/projects/9657/)
| OSS Fuzz  | [![Fuzzing Status](https://oss-fuzz-build-logs.storage.googleapis.com/badges/noxcoin.svg)](https://bugs.chromium.org/p/oss-fuzz/issues/list?sort=-opened&can=1&q=proj:noxcoin)
| Coveralls | [![Coveralls Status](https://coveralls.io/repos/github/noxcoin-project/noxcoin/badge.svg?branch=master)](https://coveralls.io/github/noxcoin-project/noxcoin?branch=master)
| License   | [![License](https://img.shields.io/badge/license-BSD3-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)

## Introduction

Noxcoin is a private, secure, untraceable, decentralised digital currency. You are your bank, you control your funds, and nobody can trace your transfers unless you allow them to do so.

**Based on Monero Core:** Ring Signatures, Stealth Addresses, RingCT, and Bulletproofs+ — same privacy foundation.

**New Emission Schedule:** 21 million NOX total supply instead of Monero’s infinite tail emission.

**Faster Blocks:** 120-second block time with no penalty mechanics.

**Low Fees:** Base fee: 0.0000005 NOX/kB — up to 6× cheaper than Monero.

## About this project

Noxcoin is built for people who believe in the right to private money — without surveillance, censorship, or central control. Whether you're a miner, a developer, a privacy advocate, or a curious newcomer, this is your home.

## License

See [LICENSE](LICENSE).

## Contributing

If you want to help out, see [CONTRIBUTING](docs/CONTRIBUTING.md) for a set of guidelines.


## Compiling Noxcoin from source

### Dependencies

The following table summarizes the tools and libraries required to build. A
few of the libraries are also included in this repository (marked as
"Vendored"). By default, the build uses the library installed on the system
and ignores the vendored sources. However, if no library is found installed on
the system, then the vendored source will be built and used. The vendored
sources are also used for statically-linked builds because distribution
packages often include only shared library binaries (`.so`) but not static
library archives (`.a`).

| Dep          | Min. version  | Vendored | Debian/Ubuntu pkg    | Arch pkg     | Void pkg           | Fedora pkg          | Optional | Purpose         |
| ------------ | ------------- | -------- | -------------------- | ------------ | ------------------ | ------------------- | -------- | --------------- |
| GCC          | 7             | NO       | `build-essential`    | `base-devel` | `base-devel`       | `gcc`               | NO       |                 |
| CMake        | 3.5           | NO       | `cmake`              | `cmake`      | `cmake`            | `cmake`             | NO       |                 |
| pkg-config   | any           | NO       | `pkg-config`         | `base-devel` | `base-devel`       | `pkgconf`           | NO       |                 |
| Boost        | 1.66          | NO       | `libboost-all-dev`   | `boost`      | `boost-devel`      | `boost-devel`       | NO       | C++ libraries   |
| OpenSSL      | basically any | NO       | `libssl-dev`         | `openssl`    | `openssl-devel`    | `openssl-devel`     | NO       | sha256 sum      |
| libzmq       | 4.2.0         | NO       | `libzmq3-dev`        | `zeromq`     | `zeromq-devel`     | `zeromq-devel`      | NO       | ZeroMQ library  |
| libunbound   | 1.4.16        | NO       | `libunbound-dev`     | `unbound`    | `unbound-devel`    | `unbound-devel`     | NO       | DNS resolver    |
| libsodium    | ?             | NO       | `libsodium-dev`      | `libsodium`  | `libsodium-devel`  | `libsodium-devel`   | NO       | cryptography    |
| libunwind    | any           | NO       | `libunwind8-dev`     | `libunwind`  | `libunwind-devel`  | `libunwind-devel`   | YES      | Stack traces    |
| liblzma      | any           | NO       | `liblzma-dev`        | `xz`         | `liblzma-devel`    | `xz-devel`          | YES      | For libunwind   |
| libreadline  | 6.3.0         | NO       | `libreadline6-dev`   | `readline`   | `readline-devel`   | `readline-devel`    | YES      | Input editing   |
| expat        | 1.1           | NO       | `libexpat1-dev`      | `expat`      | `expat-devel`      | `expat-devel`       | YES      | XML parsing     |
| GTest        | 1.5           | YES      | `libgtest-dev`       | `gtest`      | `gtest-devel`      | `gtest-devel`       | YES      | Test suite      |
| ccache       | any           | NO       | `ccache`             | `ccache`     | `ccache`           | `ccache`            | YES      | Compil. cache   |
| Doxygen      | any           | NO       | `doxygen`            | `doxygen`    | `doxygen`          | `doxygen`           | YES      | Documentation   |
| Graphviz     | any           | NO       | `graphviz`           | `graphviz`   | `graphviz`         | `graphviz`          | YES      | Documentation   |
| lrelease     | ?             | NO       | `qttools5-dev-tools` | `qt5-tools`  | `qt5-tools`        | `qt5-linguist`      | YES      | Translations    |
| libhidapi    | ?             | NO       | `libhidapi-dev`      | `hidapi`     | `hidapi-devel`     | `hidapi-devel`      | YES      | Hardware wallet |
| libusb       | ?             | NO       | `libusb-1.0-0-dev`   | `libusb`     | `libusb-devel`     | `libusbx-devel`     | YES      | Hardware wallet |
| libprotobuf  | ?             | NO       | `libprotobuf-dev`    | `protobuf`   | `protobuf-devel`   | `protobuf-devel`    | YES      | Hardware wallet |
| protoc       | ?             | NO       | `protobuf-compiler`  | `protobuf`   | `protobuf`         | `protobuf-compiler` | YES      | Hardware wallet |
| libudev      | ?             | NO       | `libudev-dev`        | `systemd`    | `eudev-libudev-devel` | `systemd-devel`  | YES      | Hardware wallet |

Install all dependencies at once on Debian/Ubuntu:

```
sudo apt update && sudo apt install build-essential cmake pkg-config libssl-dev libzmq3-dev libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline6-dev libexpat1-dev qttools5-dev-tools libhidapi-dev libusb-1.0-0-dev libprotobuf-dev protobuf-compiler libudev-dev libboost-chrono-dev libboost-date-time-dev libboost-filesystem-dev libboost-locale-dev libboost-program-options-dev libboost-regex-dev libboost-serialization-dev libboost-system-dev libboost-thread-dev python3 ccache doxygen graphviz git curl autoconf libtool gperf
```

Install all dependencies at once on Arch:
```
sudo pacman -Syu --needed base-devel cmake boost openssl zeromq unbound libsodium libunwind xz readline expat python3 ccache doxygen graphviz qt5-tools hidapi libusb protobuf systemd
```

Install all dependencies at once on Fedora:
```
sudo dnf install gcc gcc-c++ cmake pkgconf boost-devel openssl-devel zeromq-devel unbound-devel libsodium-devel libunwind-devel xz-devel readline-devel expat-devel ccache doxygen graphviz qt5-linguist hidapi-devel libusbx-devel protobuf-devel protobuf-compiler systemd-devel
```

Install all dependencies at once on openSUSE:

```
sudo zypper ref && sudo zypper in cppzmq-devel libboost_chrono-devel libboost_date_time-devel libboost_filesystem-devel libboost_locale-devel libboost_program_options-devel libboost_regex-devel libboost_serialization-devel libboost_system-devel libboost_thread-devel libexpat-devel libminiupnpc-devel libsodium-devel libunwind-devel unbound-devel cmake doxygen ccache fdupes gcc-c++ libevent-devel libopenssl-devel pkgconf-pkg-config readline-devel xz-devel libqt5-qttools-devel patterns-devel-C-C++-devel_C_C++
```

Install all dependencies at once on macOS with the provided Brewfile:

```
brew update && brew bundle --file=contrib/brew/Brewfile
```

FreeBSD 12.1 one-liner required to build dependencies:

```
pkg install git gmake cmake pkgconf boost-libs libzmq4 libsodium unbound
```

### Cloning the repository

Clone recursively to pull-in needed submodule(s):

```
git clone --recursive https://github.com/noxcoin-project/noxcoin
```

If you already have a repo cloned, initialize and update:

```
cd noxcoin && git submodule init && git submodule update
```

*Note*: If there are submodule differences between branches, you may need 
to use `git submodule sync && git submodule update` after changing branches
to build successfully.

### Build instructions

Noxcoin uses the CMake build system and a top-level [Makefile](Makefile) that
invokes cmake commands as needed.

#### On Linux and macOS

* Install the dependencies
* Change to the root of the source code directory, change to the most recent release branch, and build:

    ```bash
    cd noxcoin
    git checkout release-v0.18
    make
    ```

    *Optional*: If your machine has several cores and enough memory, enable
    parallel build by running `make -j<number of threads>` instead of `make`. For
    this to be worthwhile, the machine should have one core and about 2GB of RAM
    available per thread.

    *Note*: The instructions above will compile the most stable release of the
    Noxcoin software. If you would like to use and test the most recent software,
    use `git checkout master`. The master branch may contain updates that are
    both unstable and incompatible with release software, though testing is always
    encouraged.

* The resulting executables can be found in `build/release/bin`

* Add `PATH="$PATH:$HOME/noxcoin/build/release/bin"` to `.profile`

* Run Noxcoin with `noxcoind --detach`

* **Optional**: build and run the test suite to verify the binaries:

    ```bash
    make release-test
    ```

    *NOTE*: `core_tests` test may take a few hours to complete.

* **Optional**: to build binaries suitable for debugging:

    ```bash
    make debug
    ```

* **Optional**: build documentation in `doc/html` (omit `HAVE_DOT=YES` if `graphviz` is not installed):

    ```bash
    HAVE_DOT=YES doxygen Doxyfile
    ```

* **Optional**: use ccache not to rebuild translation units, that haven't really changed. Noxcoin's CMakeLists.txt file automatically handles it

    ```bash
    sudo apt install ccache
    ```

#### On the Raspberry Pi

Tested on a Raspberry Pi 5B with a clean installation of Raspberry Pi OS (64-bit) with Debian 12 from https://www.raspberrypi.com/software/operating-systems/.

* `apt-get update && apt-get upgrade` to install the latest software

* Install the dependencies for Noxcoin from the 'Debian' column in the table above.

* **Optional**: increase the system swap size:

    ```bash
    sudo /etc/init.d/dphys-swapfile stop  
    sudo nano /etc/dphys-swapfile  
    CONF_SWAPSIZE=2048
    sudo /etc/init.d/dphys-swapfile start
    ```

* If using an external hard disk without an external power supply, ensure it gets enough power to avoid hardware issues when syncing, by adding the line "max_usb_current=1" to /boot/config.txt

* Clone Noxcoin and checkout the most recent release version:

    ```bash
    git clone --recursive https://github.com/noxcoin-project/noxcoin.git
    cd noxcoin
    git checkout v0.18.4.1
    ```

* Build:

    ```bash
    USE_SINGLE_BUILDDIR=1 make release
    ```

* Wait a few hours

* The resulting executables can be found in `build/release/bin`

* Add `export PATH="$PATH:$HOME/noxcoin/build/release/bin"` to `$HOME/.profile`

* Run `source $HOME/.profile`

* Run Noxcoin with `noxcoind --detach`

* You may wish to reduce the size of the swap file after the build has finished, and delete the boost directory from your home directory

#### On Windows:

Binaries for Windows can be built on Windows using the MinGW toolchain within
[MSYS2 environment](https://www.msys2.org). The MSYS2 environment emulates a
POSIX system. The toolchain runs within the environment and *cross-compiles*
binaries that can run outside of the environment as a regular Windows
application.

**Preparing the build environment**

* Download and install the [MSYS2 installer](https://www.msys2.org). Installing MSYS2 requires 64-bit Windows 10 or newer.
* Open the MSYS shell via the `MSYS2 MSYS` shortcut
* Update packages using pacman:

    ```bash
    pacman -Syu
    ```

* Install dependencies:

    ```bash
    pacman -S mingw-w64-x86_64-toolchain make mingw-w64-x86_64-cmake mingw-w64-x86_64-boost mingw-w64-x86_64-openssl mingw-w64-x86_64-zeromq mingw-w64-x86_64-libsodium mingw-w64-x86_64-hidapi mingw-w64-x86_64-unbound
    ```

* Open the MingW shell via `MSYS2 MINGW64` shortcut.

**Cloning**

* To git clone, run:

    ```bash
    git clone --recursive https://github.com/noxcoin-project/noxcoin.git
    ```

**Building**

* Change to the cloned directory, run:

    ```bash
    cd noxcoin
    ```

* If you would like a specific [version/tag](https://github.com/noxcoin-project/noxcoin/tags), do a git checkout for that version. eg. 'v0.18.4.1'. If you don't care about the version and just want binaries from master, skip this step:

    ```bash
    git checkout v0.18.4.1
    ```

* To build Noxcoin, run:

    ```bash
    make release-static -j $(nproc)
    ```

   The resulting executables can be found in `build/release/bin`


* **Optional**: to build Windows binaries suitable for debugging, run:

    ```bash
    make debug -j $(nproc)
    ```

   The resulting executables can be found in `build/debug/bin`

### On FreeBSD:

The project can be built from scratch by following instructions for Linux above(but use `gmake` instead of `make`). 
If you are running Noxcoin in a jail, you need to add `sysvsem="new"` to your jail configuration, otherwise lmdb will throw the error message: `Failed to open lmdb environment: Function not implemented`.

Noxcoin is also available as a port or package as `noxcoin-cli`.

### On OpenBSD:

You will need to add a few packages to your system. `pkg_add cmake gmake zeromq libiconv boost libunbound`.

The `doxygen` and `graphviz` packages are optional and require the xbase set.
Running the test suite also requires `py3-requests` package.

Build noxcoin: `gmake`

Note: you may encounter the following error when compiling the latest version of Noxcoin as a normal user:

```
LLVM ERROR: out of memory
c++: error: unable to execute command: Abort trap (core dumped)
```

Then you need to increase the data ulimit size to 2GB and try again: `ulimit -d 2000000`

### On NetBSD:

Check that the dependencies are present: `pkg_info -c libexecinfo boost-headers boost-libs protobuf readline libusb1 zeromq git-base pkgconf gmake cmake | more`, and install any that are reported missing, using `pkg_add` or from your pkgsrc tree.  Readline is optional but worth having.

Third-party dependencies are usually under `/usr/pkg/`, but if you have a custom setup, adjust the "/usr/pkg" (below) accordingly.

Clone the noxcoin repository recursively and checkout the most recent release as described above. Then build noxcoin: `gmake BOOST_ROOT=/usr/pkg LDFLAGS="-Wl,-R/usr/pkg/lib" release`.  The resulting executables can be found in `build/NetBSD/[Release version]/Release/bin/`.

### On Solaris:

The default Solaris linker can't be used, you have to install GNU ld, then run cmake manually with the path to your copy of GNU ld:

```bash
mkdir -p build/release
cd build/release
cmake -DCMAKE_LINKER=/path/to/ld -D CMAKE_BUILD_TYPE=Release ../..
cd ../..
```

Then you can run make as usual.

### Cross Compiling

You can also cross-compile static binaries on Linux for Windows and macOS with the `depends` system.

* ```make depends target=x86_64-linux-gnu``` for 64-bit linux binaries.
* ```make depends target=x86_64-w64-mingw32``` for 64-bit windows binaries.
  * Requires: `g++-mingw-w64-x86-64`
  * You also need to run:
    ```shell
    update-alternatives --set x86_64-w64-mingw32-g++ $(which x86_64-w64-mingw32-g++-posix) && \
    update-alternatives --set x86_64-w64-mingw32-gcc $(which x86_64-w64-mingw32-gcc-posix)
    ```
* ```make depends target=x86_64-apple-darwin``` for Intel macOS binaries.
  * Requires: `clang`
* ```make depends target=arm64-apple-darwin``` for Apple Silicon macOS binaries.
  * Requires: `clang`
* ```make depends target=i686-linux-gnu``` for 32-bit linux binaries.
  * Requires: `g++-multilib bc`
* ```make depends target=i686-w64-mingw32``` for 32-bit windows binaries.
  * Requires: `python3 g++-mingw-w64-i686`
* ```make depends target=arm-linux-gnueabihf``` for armv7 binaries.
  * Requires: `g++-arm-linux-gnueabihf`
* ```make depends target=aarch64-linux-gnu``` for armv8 binaries.
  * Requires: `g++-aarch64-linux-gnu`
* ```make depends target=riscv64-linux-gnu``` for RISC V 64 bit binaries.
  * Requires: `g++-riscv64-linux-gnu`
* ```make depends target=x86_64-unknown-freebsd``` for freebsd binaries.
  * Requires: `clang-8`
* ```make depends target=arm-linux-android``` for 32bit android binaries
* ```make depends target=aarch64-linux-android``` for 64bit android binaries


The required packages are the names for each toolchain on apt. Depending on your distro, they may have different names. The `depends` system has been tested on Ubuntu 18.04 and 20.04.

Using `depends` might also be easier to compile Noxcoin on Windows than using MSYS. Activate Windows Subsystem for Linux (WSL) with a distro (for example Ubuntu), install the apt build-essentials and follow the `depends` steps as depicted above.

The produced binaries still link libc dynamically. If the binary is compiled on a current distribution, it might not run on an older distribution with an older installation of libc.

### Trezor hardware wallet support

If you have an issue with building Noxcoin with Trezor support, you can disable it by setting `USE_DEVICE_TREZOR=OFF`, e.g., 

```bash
USE_DEVICE_TREZOR=OFF make release
```

For more information, please check out Trezor [src/device_trezor/README.md](src/device_trezor/README.md).

### Guix builds

See [contrib/guix/README.md](contrib/guix/README.md).

## Installing Noxcoin from a package

**DISCLAIMER: These packages are not part of this repository or maintained by this project's contributors, and as such, do not go through the same review process to ensure their trustworthiness and security.**

Packages are available for

* Debian Buster

    See the [instructions in the whonix/noxcoin-gui repository](https://gitlab.com/whonix/noxcoin-gui#how-to-install-noxcoin-using-apt-get)

* Debian Bullseye and Sid

    ```bash
    sudo apt install noxcoin
    ```
More info and versions in the [Debian package tracker](https://tracker.debian.org/pkg/noxcoin).

* Arch Linux [(via Community packages)](https://www.archlinux.org/packages/community/x86_64/noxcoin/):

    ```bash
    sudo pacman -S noxcoin
    ```

* NixOS:

    ```bash
    nix-shell -p noxcoin-cli
    ```

* GuixSD

    ```bash
    guix package -i noxcoin
    ```

* Gentoo [Noxcoin overlay](https://github.com/gentoo-noxcoin/gentoo-noxcoin)

    ```bash
    emerge --noreplace eselect-repository
    eselect repository enable noxcoin
    emaint sync -r noxcoin
    echo '*/*::noxcoin ~amd64' >> /etc/portage/package.accept_keywords
    emerge net-p2p/noxcoin
    ```

* Alpine Linux:

    ```bash
    apk add noxcoin
    ```

* macOS [(homebrew)](https://brew.sh/)
    ```bash
    brew install noxcoin
    ```

* Docker

    ```bash
    # Build using all available cores
    docker build -t noxcoin .

    # or build using a specific number of cores (reduce RAM requirement)
    docker build --build-arg NPROC=1 -t noxcoin .

    # either run in foreground
    docker run -it -v /noxcoin/chain:/home/noxcoin/.bitnoxcoin -v /noxcoin/wallet:/wallet -p 19888:19888 noxcoin

    # or in background
    docker run -it -d -v /noxcoin/chain:/home/noxcoin/.bitnoxcoin -v /noxcoin/wallet:/wallet -p 19888:19888 noxcoin
    ```

* The build needs 3 GB space.
* Wait one hour or more

Packaging for your favorite distribution would be a welcome contribution!

## Running noxcoind

The build places the binary in `bin/` sub-directory within the build directory
from which cmake was invoked (repository root by default). To run in the
foreground:

```bash
./bin/noxcoind
```

To list all available options, run `./bin/noxcoind --help`.  Options can be
specified either on the command line or in a configuration file passed by the
`--config-file` argument.  To specify an option in the configuration file, add
a line with the syntax `argumentname=value`, where `argumentname` is the name
of the argument without the leading dashes, for example, `log-level=1`.

To run in background:

```bash
./bin/noxcoind --log-file noxcoind.log --detach
```

To run as a systemd service, copy
[noxcoind.service](utils/systemd/noxcoind.service) to `/etc/systemd/system/` and
[noxcoind.conf](utils/conf/noxcoind.conf) to `/etc/`. The [example
service](utils/systemd/noxcoind.service) assumes that the user `noxcoin` exists
and its home is the data directory specified in the [example
config](utils/conf/noxcoind.conf).

If you're on Mac, you may need to add the `--max-concurrency 1` option to
noxcoin-wallet-cli, and possibly noxcoind, if you get crashes refreshing.

## Internationalization

See [README.i18n.md](docs/README.i18n.md).

## Using Tor

> There is a new, still experimental, [integration with Tor](docs/ANONYMITY_NETWORKS.md). The
> feature allows connecting over IPv4 and Tor simultaneously - IPv4 is used for
> relaying blocks and relaying transactions received by peers whereas Tor is
> used solely for relaying transactions received over local RPC. This provides
> privacy and better protection against surrounding node (sybil) attacks.

While Noxcoin isn't made to integrate with Tor, it can be used wrapped with torsocks, by
setting the following configuration parameters and environment variables:

* `--p2p-bind-ip 127.0.0.1` on the command line or `p2p-bind-ip=127.0.0.1` in
  noxcoind.conf to disable listening for connections on external interfaces.
* `--no-igd` on the command line or `no-igd=1` in noxcoind.conf to disable IGD
  (UPnP port forwarding negotiation), which is pointless with Tor.
* `DNS_PUBLIC=tcp` or `DNS_PUBLIC=tcp://x.x.x.x` where x.x.x.x is the IP of the
  desired DNS server, for DNS requests to go over TCP, so that they are routed
  through Tor. When IP is not specified, noxcoind uses the default list of
  servers defined in [src/common/dns_utils.cpp](src/common/dns_utils.cpp).
* `TORSOCKS_ALLOW_INBOUND=1` to tell torsocks to allow noxcoind to bind to interfaces
   to accept connections from the wallet. On some Linux systems, torsocks
   allows binding to localhost by default, so setting this variable is only
   necessary to allow binding to local LAN/VPN interfaces to allow wallets to
   connect from remote hosts. On other systems, it may be needed for local wallets
   as well.
* Do NOT pass `--detach` when running through torsocks with systemd, (see
  [utils/systemd/noxcoind.service](utils/systemd/noxcoind.service) for details).
* If you use the wallet with a Tor daemon via the loopback IP (eg, 127.0.0.1:9050),
  then use `--untrusted-daemon` unless it is your own hidden service.

Example command line to start noxcoind through Tor:

```bash
DNS_PUBLIC=tcp torsocks noxcoind --p2p-bind-ip 127.0.0.1 --no-igd
```

A helper script is in contrib/tor/noxcoin-over-tor.sh. It assumes Tor is installed
already, and runs Tor and Noxcoin with the right configuration.

### Using Tor on Tails

TAILS ships with a very restrictive set of firewall rules. Therefore, you need
to add a rule to allow this connection too, in addition to telling torsocks to
allow inbound connections. Full example:

```bash
sudo iptables -I OUTPUT 2 -p tcp -d 127.0.0.1 -m tcp --dport 19889 -j ACCEPT
DNS_PUBLIC=tcp torsocks ./noxcoind --p2p-bind-ip 127.0.0.1 --no-igd --rpc-bind-ip 127.0.0.1 \
    --data-dir /home/amnesia/Persistent/your/directory/to/the/blockchain
```

## Pruning

As of April 2022, the full Noxcoin blockchain file is about 130 GB. One can store a pruned blockchain, which is about 45 GB.
A pruned blockchain can only serve part of the historical chain data to other peers, but is otherwise identical in
functionality to the full blockchain.
To use a pruned blockchain, it is best to start the initial sync with `--prune-blockchain`. However, it is also possible
to prune an existing blockchain using the `noxcoin-blockchain-prune` tool or using the `--prune-blockchain` `noxcoind` option
with an existing chain. If an existing chain exists, pruning will temporarily require disk space to store both the full
and pruned blockchains.

For more detailed information see the ['Pruning' entry in the Noxcoinpedia](https://www.noxcoin.org/resources/noxcoinpedia/pruning.html)

## Debugging

This section contains general instructions for debugging failed installs or problems encountered with Noxcoin. First, ensure you are running the latest version built from the GitHub repo.

### Obtaining stack traces and core dumps on Unix systems

We generally use the tool `gdb` (GNU debugger) to provide stack trace functionality, and `ulimit` to provide core dumps in builds which crash or segfault.

* To use `gdb` in order to obtain a stack trace for a build that has stalled:

Run the build.

Once it stalls, enter the following command:

```bash
gdb /path/to/noxcoind `pidof noxcoind`
```

Type `thread apply all bt` within gdb in order to obtain the stack trace

* If however the core dumps or segfaults:

Enter `ulimit -c unlimited` on the command line to enable unlimited filesizes for core dumps

Enter `echo core | sudo tee /proc/sys/kernel/core_pattern` to stop cores from being hijacked by other tools

Run the build.

When it terminates with an output along the lines of "Segmentation fault (core dumped)", there should be a core dump file in the same directory as noxcoind. It may be named just `core`, or `core.xxxx` with numbers appended.

You can now analyse this core dump with `gdb` as follows:

```bash
gdb /path/to/noxcoind /path/to/dumpfile`
```

Print the stack trace with `bt`

 * If a program crashed and cores are managed by systemd, the following can also get a stack trace for that crash:

```bash
coredumpctl -1 gdb
```

#### To run Noxcoin within gdb:

Type `gdb /path/to/noxcoind`

Pass command-line options with `--args` followed by the relevant arguments

Type `run` to run noxcoind

### Analysing memory corruption

There are two tools available:

#### ASAN

Configure Noxcoin with the -D SANITIZE=ON cmake flag, eg:

```bash
cd build/debug && cmake -D SANITIZE=ON -D CMAKE_BUILD_TYPE=Debug ../..
```

You can then run the noxcoin tools normally. Performance will typically halve.

#### valgrind

Install valgrind and run as `valgrind /path/to/noxcoind`. It will be very slow.

### LMDB

Instructions for debugging suspected blockchain corruption as per @HYC

There is an `mdb_stat` command in the LMDB source that can print statistics about the database but it's not routinely built. This can be built with the following command:

```bash
cd ~/noxcoin/external/db_drivers/liblmdb && make
```

The output of `mdb_stat -ea <path to blockchain dir>` will indicate inconsistencies in the blocks, block_heights and block_info table.

The output of `mdb_dump -s blocks <path to blockchain dir>` and `mdb_dump -s block_info <path to blockchain dir>` is useful for indicating whether blocks and block_info contain the same keys.

These records are dumped as hex data, where the first line is the key and the second line is the data.

# Known Issues

## Protocols

### Socket-based

Because of the nature of the socket-based protocols that drive noxcoin, certain protocol weaknesses are somewhat unavoidable at this time. While these weaknesses can theoretically be fully mitigated, the effort required (the means) may not justify the ends. As such, please consider taking the following precautions if you are a noxcoin node operator:

- Run `noxcoind` on a "secured" machine. If operational security is not your forte, at a very minimum, have a dedicated a computer running `noxcoind` and **do not** browse the web, use email clients, or use any other potentially harmful apps on your `noxcoind` machine. **Do not click links or load URL/MUA content on the same machine**. Doing so may potentially exploit weaknesses in commands which accept "localhost" and "127.0.0.1".
- If you plan on hosting a public "remote" node, start `noxcoind` with `--restricted-rpc`. This is a must.

### Blockchain-based

Certain blockchain "features" can be considered "bugs" if misused correctly. Consequently, please consider the following:

- When receiving noxcoin, be aware that it may be locked for an arbitrary time if the sender elected to, preventing you from spending that noxcoin until the lock time expires. You may want to hold off acting upon such a transaction until the unlock time lapses. To get a sense of that time, you can consider the remaining blocktime until unlock as seen in the `show_transfers` command.
