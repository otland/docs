# Compiling on Debian GNU Linux

The Forgotten Server requires at least gcc 5.0, which is available in Debian 9.

**1. Install the required software**

The following command will install Git, CMake, a compiler and the libraries used by The Forgotten Server.

Git will be used to download the source code, and CMake will be used to generate the build files.

```
# apt-get install git cmake build-essential libluajit-5.1-dev libmariadb-dev-compat libboost-date-time-dev libboost-filesystem-dev libboost-system-dev libboost-iostreams-dev libpugixml-dev libcrypto++-dev libfmt-dev
```

Replace `libmariadb-dev-compat` with `libmysqlclient-dev` on Debian 8 and below.

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
