# Compiling on CentOS

### CentOS 8

**Enable PowerTools to install lua-devel**

```
$ sudo sed -i 's/enabled=0/enabled=1/g' /etc/yum.repos.d/CentOS-PowerTools.repo
```

**Install this package to get pugixml-devel**

```
$ sudo dnf install epel-release  # for luajit pugixml-devel cryptopp-devel
$ sudo dnf install git boost-devel make cmake3 cryptopp-devel gcc-c++ gmp-devel lua-devel luajit mariadb-devel pugixml-devel fmt
```

**2. Download the source code**

```
$ git clone https://github.com/otland/forgottenserver.git
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

Note: If you're getting an error with text "had text segment at different address", try running the following command and repeat steps 3 & 4 again:

> sed -i "s/-Werror//g" ../CMakeLists.txt

### CentOS 7

**1. Install the required software**

The following command will install Git, CMake, a compiler and the libraries used by The Forgotten Server.

Git will be used to download the source code, and CMake will be used to generate the build files.

```
$ sudo yum install epel-release  # for cmake3 luajit pugixml-devel
$ sudo yum install git boost-devel cmake3 cryptopp-devel gcc-c++ gmp-devel lua-devel luajit mariadb-devel pugixml-devel
```

**2. Download the source code**

```
$ git clone https://github.com/otland/forgottenserver.git
```

**3. Generate the build files**

```
$ cd forgottenserver
$ mkdir build && cd build
$ cmake3 ..
```

**4. Build**

```
$ make
```
