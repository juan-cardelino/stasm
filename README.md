STASM 4 build scripts
=====================

This is a set of scripts, mainly cmake ones, that can be used to compile the STASM library (version 4 and later).
* CMakeLists.txt: cmake build script to compile the STASM library and its examples
* STASMConfig.cmake.in: template to generate a STASMConfig.cmake which could be useful to use STASM in a library from another project

Changelog
=========
05.2013: created CMakeLists.txt and tested on linux and mac

Instructions
============

Unix
----

* Download STASM source code from: http://www.milbo.users.sonic.net/stasm/ 
* uncompress it, for example to stasm4.0.0
* copy the provided files (CMakeLists.txt and STASMConfig.cmake.in)
* run cmake and generate a makefile
* it is recommended to use a different build directory, in my case I will build into stasm4.0.0/@build
* enter stasm4.0.0/@build and compile with make or your favorite IDE (tested with make and netbeans)
* you will end up with the __minimal__ and __minimal2__ examples compiled and a static library __libstasm.a__


Tested in:
* Ubuntu 13.04, STASM 4.0.0, cmake 2.8.10.1, gcc 4.7.3, make 3.81, netbeans 7.3.1
* OSX 10.8, STASM 4.0.0, cmake 2.8.9, gcc-clang 4.2, make XX, netbeans 7.2

ToDo
============
* To generate a proper windows dll (with exports) it is required to add some #defines
* Properly test it on windows
* Add example of using stasm as an external library
