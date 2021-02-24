# Building rhminer with Dev-C++ and TDM-GCC 9.2.0

## Toolchain
* Embarcadero Dev-C++ 6.3   https://github.com/Embarcadero/Dev-Cpp/releases/tag/v6.3
* TDM-GCC 9.2.0             https://jmeubank.github.io/tdm-gcc/articles/2020-03/9.2.0-release

## Build steps
* Download and unzip Boost 1.74.0 (1.75.0 has build system broken and fails to produce a version compatible with TDM-GCC)
  https://dl.bintray.com/boostorg/release/1.74.0/source/boost_1_74_0.zip

* Build Boost thread library with TDM-GCC
  (steps can be explained if necessary)

* Build jsoncpp library with Dev-C++\TDM-GCC
  (the project file is at rhminer\jsoncpp-1.8.0\makefiles\Dev-CPP\jsoncpp.dev) 

* Open either release or debug versions of rhminer projects
  (rhminer\rhminer.dev or rhminer\rhminer-debug.dev)

* Select "Project\Project Option" menu item, follow to "Parameters" tab and check "Linker" area. 
  Three items there should provide correct paths to the libraries required. If your configuration is different please fix it as required.

* Compile and enjoy. There should ber single warning during build regarding a call strncat to at Global.cpp. If you see more something went wrong.  