SolveSpack
==========

This repository contains the source code of [SolveSpace][] for [KMOLab][].

[solvespace]: http://solvespace.com
[KMOLab]: http://kmolab.github.io
[MSYS2]: http://www.msys2.org/
[CMake]: https://cmake.org/files/v3.10/cmake-3.10.1-win64-x64.zip
[d3dcompiler_43.dll]: https://blogs.msdn.microsoft.com/chuckw/2012/05/07/hlsl-fxc-and-d3dcompile/
[zlib]: https://www.zlib.net/

Installation
------------

### Windows 10 64-bit

Building using [MSYS2][]
-----------------

You will need the [MSYS2], [CMake] and [zlib] for Windows 10 64-bit:

From https://www.zlib.net/zlib-1.2.11.tar.gz download zlib source codes, use

cmake .. -G "MinGW Makefiles"

and

mingw32-make 

to create libzlibstatic.a, libzlib.dll.a and libzlib.dll, and put them into mingw64\lib directory (for example, y:\msys64\mingw64\lib)

Before building, check out the project and the necessary submodules:

    git clone https://github.com/solvespace/solvespace.git solvespack
    cd solvespack
    git submodule update --init

After that, modify extlib/angle/CMakeLists.txt as following:

    #[[
        list(APPEND ANGLE_DEFINITIONS
            "-DANGLE_PRELOADED_D3DCOMPILER_MODULE_NAMES={ \"d3dcompiler_47.dll\", \"d3dcompiler_46.dll\", \"d3dcompiler_43.dll\" }")
    ]]

Under solvespack directory, use

    mkdir build
    cd build
    cmake .. -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Release
    mingw32-make
    
to get solvespace.exe under build/bin, executed with

mingw64\bin\libwinpthread-1.dll (for example, y:\msys64\mingw64\bin\libwinpthread-1.dll) and [d3dcompiler_43.dll].

