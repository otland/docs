# Compiling on Fedora

**1. Install the required software**

The following command will install Git, CMake, a compiler and the libraries used by The Forgotten Server.

Git will be used to download the source code, and CMake will be used to generate the build files.

```
$ sudo dnf install git cmake gcc-c++ boost-devel community-mysql-devel lua-devel pugixml-devel cryptopp-devel make fmt-devel
```

**2. Download the source code**

```
$ git clone --recursive https://github.com/otland/forgottenserver.git
```

**3. Generate the build files**

```
$ cd forgottenserver
$ mkdir build && cd build
$ cmake ..
```

**4. Build**

```
$ make
```
