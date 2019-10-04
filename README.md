# darknet_vendor

This is a CMake wrapper around [darknet](https://pjreddie.com/darknet), an open source neural network framework.

# Building

```
cd darknet_vendor/
mkdir build/
cd build/
cmake -DCMAKE_BUILD_TYPE=Release ..
make
```

The package offers two CMake options to control how it is built.

* `DARKNET_CUDA` (default: `On`) - Whether or not to build with CUDA support
* `DARKNET_OPENCV` (default: `On`) - Whether or not to build with OpenCV support

These can be disabled prior to compiling if you don't need either of those dependencies.

```
cmake -DDARKNET_CUDA=Off -DDARKNET_OPENCV=Off ..
```

# ROS 2 and Colcon

The package includes `package.xml` and should build fine using ROS 2 Dashing.

```
colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release --packages-select darknet_vendor
```

# Using darknet

If you are using `ament_cmake`, use `ament_target_dependencies()` as normal.

```CMake

find_package(darknet_vendor REQUIRED)

#...

ament_target_dependencies(my_library_or_executable_target
  darknet_vendor)
```

Otherwise, use the exported target `darknet_vendor::darknet_vendor`

```CMake
find_package(darknet_vendor REQUIRED)

#...

target_link_libraries(my_library_or_executable_target PUBLIC darknet_vendor::darknet_vendor)
```

Then include the `darknet.h` header in your project to make darknet functions available.

```C
#include <darknet.h>
```

Alternatively, include `darknet_vendor/darknet_vendor.h` to get preprocessor definitions with info about the installed `darknet_vendor` version.

```C
#include <darknet_vendor/darknet_vendor.h>
```
