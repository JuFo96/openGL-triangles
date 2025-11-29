# Introduction to graphics programming with openGL
The purpose of this repo is primarily for me to learn graphics programming concepts and initially the openGL framework.

# Installation

I have included the source code for GLAD an open source library that handles openGL drivers in the `external` folder. 

GLFW should automatically be downloaded and built via CMake.

The project uses CMake to build the binaries.

On Linux
```bash
mkdir build
cd build
cmake ..
make
./binaryName
```

Or use an appropriate cmake compliant IDE.