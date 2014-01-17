STASM 4 build scripts
=====================

This is a set of scripts, mainly cmake ones, that can be used to compile the STASM library (version 4 and later).
* CMakeLists.txt: cmake build script to compile the STASM library and its examples
* STASMConfig.cmake.in: template to generate a STASMConfig.cmake which could be useful to use STASM in a library from another project

Changelog
=========

2013.05.09: 
* created CMakeLists.txt and tested on linux and mac
 
2014.01.14:       
* added comments of windows compilation
* added support for STASM 4.1.0
          
Instructions
============

Unix
----

* Download STASM source code from: http://www.milbo.users.sonic.net/stasm/ 
* uncompress it, for example to stasm4.1.0. I will refer to this directory as STASM_DIR
* copy the provided files (CMakeLists.txt and STASMConfig.cmake.in) to STASM_DIR
* run cmake and generate a makefile
* it is recommended to use a different build directory, in my case I will build into STASM_DIR/@build
* enter STASM_DIR/@build and compile with make or your favorite IDE (tested with make and netbeans)
* you will end up with the __minimal__ and __minimal2__ examples compiled and a static library __libstasm.a__


Tested in:
* Ubuntu 13.04, STASM 4.0.0, cmake 2.8.10.1, gcc 4.7.3, make 3.81, netbeans 7.3.1
* OSX 10.8, STASM 4.0.0, cmake 2.8.9, gcc-clang 4.2, make XX, netbeans 7.2
* OSX 10.9, STASM 4.0.0, cmake 2.8.12, clang 5.0, make 3.81, OpenCV 2.4.7
* OSX 10.9, STASM 4.1.0, cmake 2.8.12, clang 5.0, make 3.81, OpenCV 2.4.7
* Windows 8 64bit, STASM 4.1.0, cmake 2.8.11, Visual Studio 10,  OpenCV 2.4.2. Built on 32bits


ToDo
============
* In order to generate a proper windows dll (with exports) it is required to add some #defines
* Extend windows testing (64 bits, VS11)
* Add example of using stasm as an external library
