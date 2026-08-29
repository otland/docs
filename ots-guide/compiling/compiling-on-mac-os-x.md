# Compiling on Mac OS X

**1. Install the required software**

**1.1. Installing Homebrew**

Homebrew is a package manager for Mac OS X. It uses formulae scripts to compile the software on your system. If you already have Homebrew installed, you can skip this step.

Open a Terminal window and run:

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**1.2. Installing software and libraries**

The following command will install Git, CMake and the libraries used by The Forgotten Server.

Git will be used to download the source code, and CMake will be used to generate the build files.

```
$ brew install git cmake gmp mysql-connector-c luajit boost pugixml pkg-config fmt
```

Install [cryptopp](https://github.com/weidai11/cryptopp) manually (it is no longer available via brew). Make sure to use latest version, in case it is 8.5.0, you can try this:

```
wget https://github.com/weidai11/cryptopp/archive/refs/tags/CRYPTOPP_8_5_0.zip
unzip CRYPTOPP_8_5_0.zip && cd cryptopp-CRYPTOPP_8_5_0
make shared all
make install
```

**2. Download the source code**

```
$ git clone --recursive https://github.com/otland/forgottenserver.git
```

**3. Generate the build files**

```
$ cd forgottenserver
$ mkdir build; cd build
$ cmake ..
```

**4. Build**

```
$ make
```
