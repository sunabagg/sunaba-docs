# Compiling the runtime

## Prerequisites

To compile, you will need the following:

- **[CMake](https://cmake.org/)** v3.22+
- C++ Compiler with at least **C++17** support (any recent compiler)
- Python 3.8+
- OpenSSL for luasec
- (optional) pkgconf for LuaJIT support
- vcpkg for installing OpenSSL and (optional) LuaJIT 
- (optional) **[ccache](https://ccache.dev/)** for faster rebuilds

## Getting the repository

```sh
$ git clone https://github.com/sunabagg/sunaba.git
$ cd sunaba
```

## Build & Install

Here's an example of how to build & install a release version (use the terminal to run the following commands in the parent directory of this repo):

### Not MSVC or Emscripten

```sh
$ cmake -B sunaba-build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=sunaba-install sunaba
$ cmake --build sunaba-build --parallel
$ cmake --install sunaba-build
```

### Emscripten

```sh
$ emcmake cmake -B sunaba-build-web -S . -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=sunaba-install-web -DCMAKE_CXX_FLAGS="-sSIDE_MODULE -fPIC -msimd128 -std=c++17 -sSUPPORT_LONGJMP=emscripten -o3 -pthread --target=wasm32-unknown-emscripten -sSHARED_MEMORY=1 -flto=thin" -DCMAKE_C_FLAGS="-sSIDE_MODULE -fPIC -msimd128 -sSUPPORT_LONGJMP=emscripten -o3 --target=wasm32-unknown-emscripten -sSHARED_MEMORY=1" -DCMAKE_EXE_LINKER_FLAGS="-sINITIAL_MEMORY=104857600 -sALLOW_MEMORY_GROWTH=1 -sSHARED_MEMORY=1"
$ cmake --build sunaba-build-web
$ cmake --install sunaba-build-web
```

### MSVC

```sh
cmake -B sunaba-build -G"Visual Studio 17 2022"  -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=sunaba-install sunaba
Copy-Item "lua51.lib" -Destination "sunaba-build\lua51.lib"
cmake --build sunaba-build --config Release
cmake --install sunaba-build
```

This tells CMake to use `Visual Studio 2022`. There is a list of Visual Studio generators [on the CMake site](https://cmake.org/cmake/help/latest/manual/cmake-generators.7.html#visual-studio-generators) - pick the one you are using.

### IOS

```sh
$ cmake -B sunaba-build-ios -G Xcode -DCMAKE_TOOLCHAIN_FILE="$(pwd)/cmake/ios.toolchain.cmake" -DPLATFORM=OS64 -DIPHONEOS_DEPLOYMENT_TARGET=18.5 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=sunaba-install-ios .
$ cmake --build sunaba-build-ios --config Release
$ cmake --install sunaba-build-ios
```

### IOS (Simulator)

```sh
$ cmake -B sunaba-build-ios-sim -G Xcode -DCMAKE_TOOLCHAIN_FILE="$(pwd)/cmake/ios.toolchain.cmake" -DPLATFORM=SIMULATORARM64 -DIPHONEOS_DEPLOYMENT_TARGET=18.5 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=sunaba-install-ios-sim .
$ cmake --build sunaba-build-ios-sim --config Release
$ cmake --install sunaba-build-ios-sim
```

### Android

```sh
$ cmake -B sunaba-android-build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=sunaba-android-install -DCMAKE_SYSTEM_NAME=Android -DCMAKE_ANDROID_NDK=/path/to/android/ndk -DCMAKE_ANDROID_ARCH_ABI=arm64-v8a
$ cmake --build sunaba-android-build --config Release
$ cmake --install sunaba-android-build
```