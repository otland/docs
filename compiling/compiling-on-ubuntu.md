# Compiling on Ubuntu

In order to compile The Forgotten Server under Ubuntu, you need Ubuntu 24.04 at least due to package requirements. Then follow the next steps:



**1. Install the required software**

The following command will install Git, CMake, a compiler and the libraries used by The Forgotten Server.

Git will be used to download the source code, and CMake will be used to generate the build files.

```
sudo apt install git cmake build-essential libluajit-5.1-dev libmysqlclient-dev libboost-system-dev libboost-iostreams-dev libpugixml-dev libcrypto++-dev libfmt-dev libboost-locale-dev libboost-json-dev liblua5.3-dev
```

**2. Download the source code**

```
git clone --recursive https://github.com/otland/forgottenserver.git
```

**3. Generate the build files**

```
cd forgottenserver
mkdir build && cd build
cmake ..
```

**4. Build**

```
make
```
