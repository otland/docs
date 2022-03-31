# Compiling on FreeBSD

**1. Install the required software**

The following command will install Git, CMake and the libraries used by The Forgotten Server.

Git will be used to download the source code, and CMake will be used to generate the build files.

```
# pkg install git cmake luajit boost-libs gmp mysql-connector-c pugixml
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
