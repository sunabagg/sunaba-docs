# Compiling the runtime

## Prerequisites

To compile, you will need the following:

- **[Haxe](https://haxe.org/)** v4.3.0+
- **[NodeJS](https://nodejs.org/en)**

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

## Build & Run

Here's an example of how to build & run Sunaba Player from the command line

```sh
$ haxe buildsys.hxml
$ node build run
```

## Build & Export

Here's an example of how to build & export a release version

```sh
$ haxe buildsys.hxml
$ node build export -release
```