# CDT (Contract Development Toolkit)
## Version : 3.0.0

⚠️ This repository contains an archive of the CDT which is a C/C++ toolchain targeting WebAssembly and a set of tools to facilitate development of smart contracts written in C/C++ that are meant to be deployed to an EOSIO blockchain. The repository is no longer maintained and users of CDT are instead directed to use the code in [AntelopeIO/cdt](https://github.com/AntelopeIO/cdt) which is a continuation of this product. That version of CDT in the [AntelopeIO](https://github.com/AntelopeIO) GitHub organization is updated to support contract development on blockchains following newer versions of the Antelope protocol, which is an evolution of the EOSIO protocol.

## Binary Releases
CDT currently supports Linux x86_64 Debian packages.
### Debian Package Install
```sh
wget https://github.com/eosnetworkfoundation/mandel.cdt/releases/download/v3.0.0-rc1/cdt_3.0.0-rc1_amd64.deb
sudo apt install ./cdt_3.0.0-rc1_amd64.deb
```
### Debian Package Uninstall
```sh
sudo apt remove cdt
```

## Building

### Ubuntu 20.04 dependencies
```sh
apt-get update && apt-get install   \
        build-essential             \
        clang                       \
        cmake                       \
        git                         \
        libxml2-dev                 \
        opam ocaml-interp           \
        python3                     \
        python3-pip                 \
        time
```
```sh
python3 -m pip install pygments
```

If issues persist with ccache
```sh
export CCACHE_DISABLE=1
```

### Building Integration Tests

Integration tests require access to a mandel build.  Instructions below provide additional steps for using a mandel built from source.  For development purposes it is generally advised to use mandel built from source.

#### For building integration tests with mandel built from source

Set an environment variable to tell CDT where to find the Mandel build directory:

```sh
export eosio_DIR=/path/to/mandel/build/lib/cmake/eosio
```

### Guided Installation or Building from Scratch
```sh
git clone --recursive https://github.com/eosnetworkfoundation/mandel.cdt
cd mandel.cdt
mkdir build
cd build
cmake ..
make -j8
```

From here onward you can build your contracts code by simply exporting the `build` directory to your path, so you don't have to install globally (makes things cleaner).
Or you can install globally by running this command:

```sh
sudo make install
```

### Running Tests

#### Unit Tests
```sh
cd build

ctest
```

#### Running Integration Tests (if built)
```sh
cd build/tests/integration

ctest
```

### Uninstall after manual installation

```sh
sudo rm -fr /usr/local/cdt
sudo rm -fr /usr/local/lib/cmake/cdt
sudo rm /usr/local/bin/eosio-*
sudo rm /usr/local/bin/cdt-*
```

## Installed Tools
---
* cdt-cpp
* cdt-cc
* cdt-ld
* cdt-init
* cdt-abidiff
* cdt-wasm2wast
* cdt-wast2wasm
* cdt-ranlib
* cdt-ar
* cdt-objdump
* cdt-readelf

## License

[MIT](./LICENSE)