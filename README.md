# lua-cmake

Basic convenience CMakeLists.txt file to build lua.
Yes there are other similar projects out there, but I opted for implementing my own.

This custom version does the following:

- Vanilla lua downloaded from [https://www.lua.org/](https://www.lua.org/)
- It builds the static library, the standalone interpreter and standalone lua compiler.
- Build process is done with a C++11 compiler.
- Developed and tested on Windows with Visual Studio.

## How to build?

Clone this repository and go inside the repo root folder. Get the lua source source code
```
git submodule update --init
```
Then generate the build files with your prefered presets.
```
cmake --preset ninja-release
```
The build files are written to `..\build_cmake\ninja-release`, go there and execute `ninja`. You will get the binaries in the same folder.