# Android Note

[TOC]



## Android with C++

#### 1. Project setup

- New Project -> include C++ / Native C++, 
  it will generate  `src/main/cpp` with `CMakeList.txt` and `native-lib.cpp` inside.

Folder structure looks like this:


 > src
 > |-main
 > |--**cpp**
 > |---**CMakeList.txt**
 > |---**native-lib.cpp**

#### 2. Linking C++ library : cmake & JNI setting

Install library files :

- Create a folder under your project to store the `.so` lib files, e.g: `app/scr/main/jniLibs`

- For example using opencv: copy all folders under `Opencv/android/sdk/native/libs` to the folder just created

Include files : 

- Create folder `app/scr/main/cpp/include`
- For example using opencv: Copy all include from your library `Opencv/android/sdk/native/jni/include`

Config setup :

- `CMakeList.txt`

  ```
  cmake_minimum_required(VERSION 3.4.1)
  
  find_library(  # find lib inside ndk: ..\android-ndk-r16\sysroot\usr\include
  		log-lib  # Sets the name of the path variable.
  		log  # Specifies the name of the NDK library that
  )
  
  include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
  add_library( lib_opencv STATIC IMPORTED )
  set_target_properties(
  		lib_opencv PROPERTIES IMPORTED_LOCATION
          ${CMAKE_CURRENT_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/libopencv_java3.so
  )
  
  add_library( # Sets the name of the library.
               native-lib
               SHARED   # Sets the library as a shared library.
  			${CMAKE_CURRENT_SOURCE_DIR}/native-lib.cpp  # Provides a relative path to your source file(s).
  		)
  
  include_directories(${CMAKE_CURRENT_SOURCE_DIR})
  add_library(
  		cpp-tool-lib
  		SHARED
  		${CMAKE_CURRENT_SOURCE_DIR}/CaptureHintScanner.h
  		${CMAKE_CURRENT_SOURCE_DIR}/CaptureHintScanner.cpp
  )
  
  target_link_libraries( # Specifies the target library.
  		cpp-tool-lib
  		${log-lib}
  		lib_opencv
  )
    
  target_link_libraries( # Specifies the target library.  
  	  	native-lib
  	  	${log-lib}
  	  	lib_opencv
  	  	jnigraphics
  		cpp-tool-lib
  )
  ```

- `app/build.gradle`

  ```
  android {
  	...
  	defaultConfig {
  		...
  		ndk{  
  		    abiFilters 'armeabi-v7a', 'x86', 'x86_64', 'arm64-v8a' // <- check your Libs support
  		}
  	}
  }
  ```

#### 3. Implement c++ function






## Troubleshooting

#### Environment Setting

###### Error: lambda expressions are not supported at language level '7

> File > Project Structure > Modules > app > Properties > Source Compatibility > select "1.8 (Java 8 )" 



###### Build error : library missing build rule

`...x86_64/libnative-libso', missing and no known rule to make it...`

Because the path of lib is not correct, to fix make the .so name match in `CMakeList.txt`: `set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/<libopencv_java3.so>) <-- same as your .so name`



###### CMake error : format string is not a string literal

 `error: format string is not a string literal (potentially insecure) [-Werror,-Wformat-security] __android_log_print(ANDROID_LOG_DEBUG, LOG_TGA, sc);`

这个由于我们是用CMake开发，不存在mk文件，所以只需要在`CMakeLists.txt`里加上这样一句话就可以 `set(CMAKE_C_FLAGS "-Wno-error=format-security")`



## Reference

- [Official: CMake](<https://developer.android.com/ndk/guides/cmake>)
- [Android NDK 原生 API](<https://developer.android.com/ndk/guides/stable_apis.html?hl=zh-CN>)

- [安卓开发学习之初识ndk开发](https://www.codetd.com/article/931844)

- [使用CMake来进行Android NDK开发](<https://blog.csdn.net/qq_34902522/article/details/78104610>)
- [CMake 入門/加入編譯選項](<https://zh.wikibooks.org/zh-hk/CMake_%E5%85%A5%E9%96%80/%E5%8A%A0%E5%85%A5%E7%B7%A8%E8%AD%AF%E9%81%B8%E9%A0%85>)

- [[转] Android JNI 作用及其详解](<https://www.jianshu.com/p/5f5d7f132c53?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation>)

- [Android使用Opencv图片处理 Mat与Bitmap互转](<https://www.jianshu.com/p/08dcc910b088>)
- [Android studio使用JAVA與JNI調用OpenCV](<https://www.twblogs.net/a/5c8addd1bd9eee35fc14baed>)
- [void 指標的實際用途](<http://www.programmer-club.com.tw/ShowSameTitleN/c/14171.html>)
- [使用 Android NDK 重用现有的 C 代码](<https://www.ibm.com/developerworks/cn/opensource/tutorials/os-androidndk/index.html>)
- [Android NDK 开发实践之路](<https://github.com/glumes/AndroidDevWithCpp>)
- [Android JNI 之 Bitmap 操作](<https://juejin.im/post/5b5810a56fb9a04f8c5ee296>)
- 

