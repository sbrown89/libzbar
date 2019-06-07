# libzbar
Complete Cross-Platform ZBar port <br />
Uses CMake as the build system <br />
<br />
I have removed/moved files that don’t directly contribute to the locating and decoding of barcodes/qrcodes. They are located in the directory notused. If you would like their functionality .. then add them to the compilation yourself. :wink:

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
## Suggested use, NOT ACTUAL  LEGAL ADVICE
On windows this will statically build and link the libiconv library.
For non-opensource / proprietary code, by dynamically linking to the final lib (libzbar), you will remain LGPL compliant. This, the original ZBar codebase and libiconv are released under the LGPL license.<br />
<br />
You should review the LGPL legal doc if unsure of use.


## Original Sources
[zbar.sourceforge.net](http://zbar.sourceforge.net/)<br />
[libiconv](https://www.gnu.org/software/libiconv/)
