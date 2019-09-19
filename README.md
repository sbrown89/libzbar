# libzbar
Complete CMake Cross-Platform ZBar port <br />
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
<br />
mkdir build; <br />
cd build; <br />
cmake -A x64 "-DCMAKE_INSTALL_PREFIX=C:/lib/libzbar" "-DCMAKE_BUILD_TYPE=Release" .. <br />
cmake --build . --config Release --target INSTALL <br />

# Android
## Linux:
./android.sh

## Windows 10+ MSVC
Open VS 20xx Developer Command Prompt. For the most part the same arguments can be used to compile against the Android NDK on Linux. You will need to adapt for your environment. Im using the Ninja generator provided with the NDK.<br />
<br />
cmake -G Ninja "-DANDROID_ABI=x86" "-DCMAKE_INSTALL_PREFIX=C:/lib/libzbar-android-api-26" "-DCMAKE_BUILD_TYPE=Release" "-DANDROID_NDK=C:\Users\brown\AppData\Local\Android\Sdk\ndk-bundle" "-DCMAKE_TOOLCHAIN_FILE=C:\Users\brown\AppData\Local\Android\Sdk\ndk-bundle\build\cmake\android.toolchain.cmake" "-DANDROID_NATIVE_API_LEVEL=android-26" "-DBUILD_SHARED_LIBS=ON" .. <br />

cmake --build . --config Release -- -j4 <br />
OR <br />
ninja build <br />
ninja install <br />

# macOS
mkdir build; <br />
cd buil; <br />
cmake .. <br />
make install <br />

# iOS
You should have xcode and command line tools installed. Do it the "Apple" way and don't use homebrew stuff ... make your life much easier. <br />
<br />
cmake -G Xcode "-DCMAKE_INSTALL_PREFIX=~/lib/libzbar-ios" "-DCMAKE_BUILD_TYPE=Release" "-DIOS_ARCH=arm64" "-DIPHONEOS_DEPLOYMENT_TARGET=12.4" "-DCMAKE_TOOLCHAIN_FILE=/bldsrc/libzbar/platforms/ios/cmake/Toolchains/Toolchain-iPhoneOS_Xcode.cmake" .. <br />

xcodebuild -list -project libzbar.xcodeproj /* Optional to show info about the build*/ <br />
xcodebuild -configuration Release -scheme install <br />
Or <br />
Open project file in xcode to make additional changes <br />

## LEGAL: 
On Windows, Android, Apple, and iOS this will statically build and link the libiconv library.
For non-opensource / proprietary code, by dynamically linking to the final lib (libzbar), you will remain LGPL compliant. This, the original ZBar codebase and libiconv are released under the LGPL license.<br />
<br />
You should review the LGPL legal doc to ensure proper use.


## Original Sources
[zbar.sourceforge.net](http://zbar.sourceforge.net/)<br />
[libiconv](https://www.gnu.org/software/libiconv/)<br />
[iOS Toolchain](https://github.com/opencv/opencv)
