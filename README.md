# VS2017RC1-Crash

The VS project has include directories to boost headers and a "version" header set up. The `server/libs/boost` directory contains some Boost 1.62 header files.

The `version/version.h` file is an emptye Unicode encoded file (it only contains a little-endian BOM (FF FE)).

Before opening the `server/main/main.sln` solution, ensure that the `.vs` directory does not exist in the same directory. When the solution is opened, the include files are parsed and Visual Studio 2017 crashes.

Removing the BOM from the `version.h` file or adding some content (e.g. a newline) to it prevents the crash. However, there is some strange interplay with the Boost config headers and the `version.h` file with just the BOM. Renaming the `server/libs/boost` directory (to prevent the contained include files from being parsed) also allows the project to load successfully.