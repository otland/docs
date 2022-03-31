# Compiling on Windows (vcpkg)

**1. Download/install the required software**

To compile on Windows, you will need to download and install:

* [Git](https://git-scm.com/download/win)
* [Visual Studio 2022 Community](https://visualstudio.microsoft.com/vs/) (compiler, make sure to install with the English language pack)
* [vcpkg](https://github.com/Microsoft/vcpkg) (package manager)

**2. Set up vcpkg**

Make sure to follow full installation of vcpkg, per [Official Quickstart](https://github.com/Microsoft/vcpkg#quick-start) execute the following in _cmd_ or _Powershell_:

To open Powershell navigate to your desired directory and choose `Open PowerShell window here` (shift + right click).

If you prefer `cmd` (command prompt) click on your `Start` windows button or just use the windows key on your keyboard and search for `cmd` then navigate to your desired directory using `cd` e.g. you want to have your vcpkg folder on root of your C drive:

```
cd C:\
```

then you can safely proceed with configuring vcpkg (may require administrator elevation)

```
git clone https://github.com/Microsoft/vcpkg && cd vcpkg && .\bootstrap-vcpkg.bat && .\vcpkg integrate install
```

**3. Download the source code**

```
git clone --recursive https://github.com/otland/forgottenserver.git
```

**4. Install libraries**

Choose one set of libraries, depending on the target platform and execute the following in _Git Bash_ or _Powershell_:

Note: **boost-filesystem** is not needed from [4b800b2](https://github.com/otland/forgottenserver/commit/4b800b20558f24344c5024fb3cb9a4974ebad90e) onwards

*   For 64-bit (x64) build:

    ```
    .\vcpkg install --triplet x64-windows boost-iostreams boost-asio boost-system boost-filesystem boost-variant boost-lockfree luajit libmariadb pugixml cryptopp fmt
    ```
*   For 32-bit (Win32) build:

    ```
    .\vcpkg install boost-iostreams boost-asio boost-system boost-filesystem boost-variant boost-lockfree luajit libmariadb pugixml cryptopp fmt
    ```

**5. Build**

1. **Open `vc17/theforgottenserver.vcxproj`**. This should launch Visual Studio.
2. Choose build configuration from the drop downs (Debug or Release and Win32 or x64). For best performance choose Release & x64.
3. To start compiling **press F7**.
