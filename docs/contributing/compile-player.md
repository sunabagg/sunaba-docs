# Compiling Sunaba Player

## Prerequisites

To compile, you will need the following:

- **[Haxe](https://haxe.org/)** v4.3.0+
- **[NodeJS](https://nodejs.org/en)**
- **[Godot](https://godotengine.org/)** v4.4.1+

## Getting the repository

```sh
$ git clone https://github.com/sunabagg/sunabaplayer.git
$ cd sunaba-player
```

## Installing haxe dependencies

```sh
$ haxelib git sunaba https://github.com/sunabagg/sunaba.git
$ haxelib git tsukuru https://github.com/sunabagg/tsukuru.git
$ haxelib install hxnodejs
```

## Getting the runtime libraries

You will need to obtain the necessary runtime libraries for you target platform either by [compiling them](compile-runtime.md) or obtaining pre-built ones from GitHub Actions

## Build & Run

Here's an example of how to build & run Sunaba Player from the command line

### Windows

```sh
./build run
```

### Unix-like systems ( macOS, Linux )

```sh
$ ./build.sh run
```

## Build & Export

Here's an example of how to build & export a release version

### Windows

```sh
./build export -release
```

### Unix-like systems ( macOS, Linux )

```sh
$ ./build.sh export -release
```