# mulle-objc-developer

[![Build Status](https://travis-ci.org/mulle-objc/mulle-objc-developer.svg)](https://travis-ci.org/mulle-objc/mulle-objc-developer)
![GitHub tag](https://img.shields.io/github/tag/mulle-objc/mulle-objc-developer.svg)
![GitHub release](https://img.shields.io/github/release/mulle-objc/mulle-objc-developer.svg)


This project packages all items together into a single homebrew formula. This is also the goto project for issues, that don't match any of the other projects or its unclear where they belong.

You install **mulle-objc-developer** with [brew](//brew.sh):

```
brew install mulle-objc/software/mulle-objc-developer
```

This will install the necessary **mulle-objc** packages to write
Objective-C code and the [mulle-clang](//github.com/codeon-gmbh/mulle-clang)
compiler.

> See [mulle-objc Community](//mulle-objc.github.io) for more information.


## Xcode integration

### Xcode 8
 For *Xcode 7* we can use [`mulle-clang-add-to-xcode.sh`](mulle-clang-add-to-xcode.sh)  to integrate **mulle-clang** with project anyhow this doesn't work for *Xcode 8* since [Xcode 8 uses library validation.](https://github.com/alcatraz/Alcatraz/issues/475)

**Xcode 8 integration for mulle-clang with CMake**

 ```bash
cd <pathToProjectDir>/MulleObjC
```

```bash
mkdir build-xcode.d ; cd build-xcode.d ; cmake -G "Xcode" .. ; open *.xcodeproj
```

### Xcode 7

You can get *Xcode 7* integration for **mulle-clang**. mulle-clang will appear as
an available compiler in Xcode in the "Build Settings":

![Screeny](pix/xcode-integration.png)


<br>
Run [`mulle-clang-add-to-xcode.sh`](mulle-clang-add-to-xcode.sh) to integrate
the **mulle-clang** compiler into Xcode. This will install a plugin in
`~/Volumes/Users/nat/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins`:

```
mulle-clang-add-to-xcode.sh
```

The `.xcconfig` string for the compiler is:

```
GCC_VERSION = de.codeon.compilers.mulle-clang
```


## Developing mulle-objc itself

If you want to hack on `mulle-objc` it is easiest to use the supplied
script [`mulle-objc-clone.sh`](mulle-objc-clone.sh) to setup things on
your machine.


This needs [mulle-build](//mulle-nat/mulle-build) as a pre-requisite.

```
brew install mulle-kybernetik/software/mulle-build
```

Now run `mulle-objc-clone.sh` in a directory, where you want the repositories to reside
in. Then you can just compile and test any project conveniently with **mulle-build**:

```
mulle-objc-clone.sh
#
cd MulleObjC
mulle-build -y
mulle-test
```

You can use the supplied **Xcode** project files to edit and build the projects, but in order for them
to work you must run `mulle-build -y` (or `mulle-bootstrap -y`) once.
