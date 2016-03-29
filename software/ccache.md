[TOC]

# [Overview](https://ccache.samba.org/)
- [Arch Wiki](https://wiki.archlinux.org/index.php/Ccache)

**ccache** is a compiler cache. It speeds up recompilation by caching previous compilations and detecting when the same compilation is being done again. Supported languages are **C, C++, Objective-C and Objective-C++**.

The detection is done by hashing different kinds of information that should be unique for the compilation and then using the hash sum to identify the cached output.

If you are always compiling the same programs over and over again — such as trying out several kernel patches, or testing your own development — then ccache is perfect.

# [Performance](https://ccache.samba.org/performance.html)

# [Using](https://ccache.samba.org/manual.html)

# Misc
## Command Line Interface
- `ccache -s`: show a statistic summary
- `ccache -C`: clear the cache completely
