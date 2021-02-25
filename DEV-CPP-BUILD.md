# Building rhminer with Dev-C++ and TDM-GCC 9.2.0

## Toolchain
* Embarcadero Dev-C++ 6.3   https://github.com/Embarcadero/Dev-Cpp/releases/tag/v6.3
* TDM-GCC 9.2.0             https://jmeubank.github.io/tdm-gcc/articles/2020-03/9.2.0-release

## Build steps
* Download and unzip Boost 1.74.0 (1.75.0 has build system broken and fails to produce a version compatible with TDM-GCC)
  https://dl.bintray.com/boostorg/release/1.74.0/source/boost_1_74_0.zip

* Build Boost thread library with TDM-GCC
  * Add TDM-GCC bin folder to PATH. This is the folder where _gcc.exe_ and _g++.exe_ reside, for me it is folder is _C:\Program Files (x86)\Embarcadero\Dev-Cpp\TDM-GCC-64\bin_
  * Check that the right version of gcc will be used, since you may have several of them installed. Go to boost root folder (the one that contains _bootstrap.bat_ )  and execute _gcc.exe --version_
    Expected output:
> gcc.exe (tdm64-1) 9.2.0
> Copyright (C) 2019 Free Software Foundation, Inc.
> This is free software; see the source for copying conditions.  There is NO 
> warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.     

  * Bootstrap Boost build system with  the following command: _bootstrap.bat gcc_

  * Build the library with _b2 toolset=gcc link=static --with-thread_
    This command only builds thread library which is required to build rhminer further on. 
    There is no problem to have other Boost libaries built at the same system before or after this step and for whatever reasons.

  * Check that the file _boost_1_74_0\stage\lib\libboost_thread-mgw9-mt-x64-1_74.a_  exists
    Note that it is OK if there are other files at the same location or other instances of the same file at other folders

* Build jsoncpp library with Dev-C++\TDM-GCC
  (the project file is at rhminer\jsoncpp-1.8.0\makefiles\Dev-CPP\jsoncpp.dev) 

* Open either release or debug versions of rhminer projects
  (rhminer\rhminer.dev or rhminer\rhminer-debug.dev)

* Select "Project\Project Option" menu item, follow to "Parameters" tab and check "Linker" area. 
  Three items there should provide correct paths to the libraries required. If your configuration is different please fix it as required.

* Compile and enjoy. There should be single warning during build regarding a call strncat to at Global.cpp. If you see more something went wrong.  

## Release notes
* rhminer.dev is configured to support CPU mining only.  CUDA and OpenCL mining will work, but it requires porting of respective libraries to Dev-CPP\TDM-GCC environment.
  
