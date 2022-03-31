# Compile on Arch

**1. Install the required software**

The following command will install Git, CMake, a compiler and the libraries used by The Forgotten Server.

Git will be used to download the source code, and CMake will be used to generate the build files.

```
$ sudo pacman -Syu
$ sudo pacman -S base-devel git cmake luajit boost boost-libs libmariadbclient pugixml crypto++ fmt
```

**2. Download the source code**

```
$ git clone https://github.com/otland/forgottenserver.git
```

**3. Generate the build files**

```
$ cd forgottenserver
$ cmake . -B build
```

**4. Build**

```
$ make -C build
```

The executable will be located in `./build/tfs`
