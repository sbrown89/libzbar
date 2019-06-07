# libzbar
Complete Cross-Platform ZBar port
Uses CMake as the build system.

# Linux
mkdir build;
cd build;
cmake ..
make install

# Windows 10+ MSVC
Open VS 20xx Developer Command Prompt
mkdir build;
cd buil;
cmake -A x64 "-DCMAKE_INSTALL_PREFIX=C:/lib/libzbar" "-DCMAKE_BUILD_TYPE=Release" ..
msbuild.exe /p:Configuration=Release ALL_BUILD.vcxproj
msbuild.exe INSTALL.vcxproj

# LEGAL NOTE: 
On windows this will statically build and link the libiconv library. 
For non-opensource / proprietary code, by dynamically linking to the final lib (libzbar) then you will remain LGPL compliant as this, 
the original ZBar codebase and libiconv are released under the LGPL license.


