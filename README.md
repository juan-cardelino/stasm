STASM 4 build scripts
=====================

This is a set of scripts, mainly cmake ones, that can be used to compile the STASM library (version 4 and later).
* CMakeLists.txt: cmake build script to compile the STASM library and its examples
* STASMConfig.cmake.in: template to generate a STASMConfig.cmake which could be useful to use STASM as a library from another project
* *.cpp.diff: patches to correct some compilation errors in unix.

Changelog
=========

2013.05.09: 
* created CMakeLists.txt and tested on linux and mac
 
2014.01.14:       
* added comments of windows compilation
* added support for STASM 4.1.0
      
2014.08.03:       
* tested and added changes proposed by Yuji Ojamada:
  * added tasm support
  * added testing
  * added patches to correct compilation errors:
    * compile with newer unix compilers (gcc and clang) in appmisc.cpp
    * added #if directives for MS and Linux (shapefile.cpp)
  * removed some particular examples added by Juan Cardelino
* tested in newer platforms
* improved documentation


Instructions
============

Unix
----

* Download STASM source code from: http://www.milbo.users.sonic.net/stasm/ 
* uncompress it, for example to stasm4.1.0. I will refer to this directory as STASM_DIR
* unpack the provided files to STASM_DIR
* run cmake and generate a makefile: it is recommended to use a different build directory, in my case I will build into STASM_DIR/@build
* enter STASM_DIR/@build and compile with make or your favorite IDE (tested with make and netbeans)
* you will end up with the __minimal__ and __minimal2__ examples compiled and a static library __libstasm.a__


Tested in the following platforms (64bits if not specified):
* Linux:
  * Ubuntu 13.04, STASM 4.0.0, cmake 2.8.10.1, gcc 4.7.3, make 3.81, netbeans 7.3.1
  * Ubuntu 13.10, STASM 4.1.0, cmake 2.8.11.2, gcc 4.8.1, make 3.81, OpenCV 2.4.5
* Mac
  * OSX 10.8, STASM 4.0.0, cmake 2.8.9, gcc-clang 4.2, make XX, netbeans 7.2
  * OSX 10.9, STASM 4.0.0, cmake 2.8.12, clang 5.0, make 3.81, OpenCV 2.4.7
  * OSX 10.9, STASM 4.1.0, cmake 2.8.12, clang 5.0, make 3.81, OpenCV 2.4.7
  * OSX 10.9.4, STASM 4.1.0, cmake 2.8.12, clang 5.1, make 3.81, OpenCV 2.4.9
* Windows:
  * Windows 8 64bit, STASM 4.1.0, cmake 2.8.11, Visual Studio 10,  OpenCV 2.4.2. Built on 32bits

Using STASM as an external library
==================================
Once STASM is compiled, you will end up with a dynamic or static library. You can use the sample project provided in the external directory as an example of how to integrate STASM into another application

In the __external__ directory you will find and example about

ToDo
============
* In order to generate a proper windows dll (with exports) it is required to add some #defines
* Extend windows testing (64 bits, VS11)

