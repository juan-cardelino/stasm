STASM build scripts
===================

This is a set of scripts, mainly cmake ones, that can be used to compile the STASM library.

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
* compile with make or your favorite IDE (tested with make and netbeans)


Tested in:
* Ubuntu 13.04, STASM 4.0.0, cmake 2.8.10.1, gcc 4.7.3, make 3.81, netbeans 7.3.1
