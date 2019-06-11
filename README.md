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

# Android
Open VS 20xx Developer Command Prompt. For the most part the same arguments can be used to compile against the Android NDK on Linux. You will need to adapt for your environment. Im using the Ninja generator provided with the NDK.<br />
<br />
cmake -G Ninja "-DANDROID_ABI=x86" "-DCMAKE_INSTALL_PREFIX=C:/lib/libzbar-android-api-26" "-DCMAKE_BUILD_TYPE=Release" "-DANDROID_NDK=C:\Users\brown\AppData\Local\Android\Sdk\ndk-bundle" "-DCMAKE_TOOLCHAIN_FILE=C:\Users\brown\AppData\Local\Android\Sdk\ndk-bundle\build\cmake\android.toolchain.cmake" "-DANDROID_NATIVE_API_LEVEL=android-26" "-DBUILD_SHARED_LIBS=ON" .. <br />

cmake --build . --config Release -- -j4 <br />
OR
ninja build <br />
ninja install <br />

# LEGAL NOTE: 
## Suggested use, NOT ACTUAL  LEGAL ADVICE
On Windows and Android this will statically build and link the libiconv library.
For non-opensource / proprietary code, by dynamically linking to the final lib (libzbar), you will remain LGPL compliant. This, the original ZBar codebase and libiconv are released under the LGPL license.<br />
<br />
You should review the LGPL legal doc if unsure of use.


## Original Sources
[zbar.sourceforge.net](http://zbar.sourceforge.net/)<br />
[libiconv](https://www.gnu.org/software/libiconv/)
