# libzbar
Complete Cross-Platform ZBar port <br />
Uses CMake as the build system <br />

# Linux
mkdir build; <br />
cd build; <br />
cmake .. <br />
make install <br />

# Windows 10+ MSVC
Open VS 20xx Developer Command Prompt <br />
mkdir build; <br />
cd buil; <br />
cmake -A x64 "-DCMAKE_INSTALL_PREFIX=C:/lib/libzbar" "-DCMAKE_BUILD_TYPE=Release" .. <br />
msbuild.exe /p:Configuration=Release ALL_BUILD.vcxproj <br />
msbuild.exe INSTALL.vcxproj <br />

# LEGAL NOTE: 
On windows this will statically build and link the libiconv library.
For non-opensource / proprietary code, by dynamically linking to the final lib (libzbar), you will then remain LGPL compliant. This, the original ZBar codebase and libiconv are released under the LGPL license.<br />


