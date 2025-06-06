
To include libraries with CMake, we need a **CMake Configuration File** :
	`CMakeLists.txt`

You need to create manually a project like so : 
```
Project
|——— CMakeLists.txt
|
|————————— assets/             (optional)
|————————— src/
|  |————————— main.cpp
|————————— include/
|  |—————————main.hpp
```


```
if (APPLE)

	cmake_minimum_required(VERSION 3.15)
	project(Test VERSION 1.0 LANGUAGES CXX)

	set(CMAKE_CXX_STANDARD 20)
	set(CMAKE_CXX_STANDARD_REQUIRED True)

	include_directories(include)
	file(GLOB_RECURSE SOURCE "src/*.cpp")
	file(GLOB_RECURSE INCLUDE "include/*.hpp")

	add_executable(Test MACOSX_BUNDLE ${SOURCE} ${INCLUDE})

	find_package(SDL3 REQUIRED CONFIG)
	target_link_libraries(Test PRIVATE SDL3::SDL3)

	set(ASSETS_SOURCE_DIR ${CMAKE_SOURCE_DIR}/assets)
	set(ASSETS_DEST_DIR ${CMAKE_BINARY_DIR}/Test.app/Contents/Resources)
	file(COPY ${ASSETS_SOURCE_DIR} DESTINATION ${ASSETS_DEST_DIR})

elseif(WIN32)

	cmake_minimum_required(VERSION 3.15)
	project(Test VERSION 1.0 LANGUAGES CXX)

	set(CMAKE_CXX_STANDARD 20)
	set(CMAKE_CXX_STANDARD_REQUIRED True)

	include_directories(include)
	file(GLOB_RECURSE SOURCE "src/*.cpp")
	file(GLOB_RECURSE INCLUDE "include/*.hpp")

	# Create a normal Windows executable (no bundle)
	add_executable(Test ${SOURCE} ${INCLUDE})

	# Find SDL3 (make sure SDL3 is installed and discoverable on Windows)
	find_package(SDL3 REQUIRED CONFIG)
	target_link_libraries(Test PRIVATE SDL3::SDL3)

	# Copy assets folder next to the executable after build
	set(ASSETS_SOURCE_DIR ${CMAKE_SOURCE_DIR}/assets)
	set(ASSETS_DEST_DIR ${CMAKE_BINARY_DIR}/assets)
	file(COPY ${ASSETS_SOURCE_DIR} DESTINATION ${ASSETS_DEST_DIR})

endif()
```


*CMakeLists.txt* :
```
cmake_minimum_required(VERSION 3.15)
project(Test VERSION 1.0 LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Source and headers
include_directories(include)
file(GLOB_RECURSE SOURCE "src/*.cpp")
file(GLOB_RECURSE INCLUDE "include/*.hpp")

# Create executable
add_executable(Test MACOSX_BUNDLE ${SOURCE} ${INCLUDE})

# Try to find SDL3 lib
find_package(SDL3 REQUIRED CONFIG)
target_link_libraries(Test PRIVATE SDL3::SDL3)

# Optional: copy assets if you have any
set(ASSETS_SOURCE_DIR ${CMAKE_SOURCE_DIR}/assets)
set(ASSETS_DEST_DIR ${CMAKE_BINARY_DIR}/MyProject.app/Content/Resources)
file(COPY ${ASSETS_SOURCE_DIR} DESTINATION ${ASSETS_DEST_DIR})

set_target_properties(MyProject PROPERTIES
    MACOSX_BUNDLE TRUE
    MACOSX_BUNDLE_INFO_PLIST "${CMAKE_SOURCE_DIR}/Info.plist.in"
)
```

Then add an `Info.plist.in` to the project root :
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
   "http://www.apple.com/DTDs/PropertyList-1.0.dtd">

<plist version="1.0">
	<dict>
	    <key>CFBundleName</key>
	    <string>MyProject</string>
	    <key>CFBundleExecutable</key>
	    <string>MyProject</string>
	    <key>CFBundleIdentifier</key>
	    <string>com.example.myproject</string>
	    <key>CFBundleVersion</key>
	    <string>1.0</string>
	    <key>CFBundlePackageType</key>
	    <string>APPL</string>
	</dict>
</plist>
```


then you can create your Xcode project to go with the config like so :
```
cmake -S . -B build -G Xcode
open build/MyProject.xcodeproj
```

this will read the `CMakeLists.txt` file and create a project for it

to add files, just add them and run : `cmake --build build` and if it doesn't work, recreate the project with the previous commands