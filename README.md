## Metal

It's the original Metal-cpp which has a low-overhead C++ interface for Metal, written by Apple. Here I wrapped the Metal-cpp into a CMake portable library.

## Usege

Please clone this repository first, then add the code below to you `CMakeLists.txt` of your project:

```cmake
add_subdirectory(<Path to the Metal library>)
target_link_libraries(${PROJECT_NAME} PUBLIC Metal)
```

Or you can also use CMake's `FetchContent` to automatically add Metal-cpp library to your project:

```cmake
include(FetchContent)
FetchContent_Declare(Metal GIT_REPOSITORY https://github.com/Unbinilium/Metal.git GIT_SHALLOW 1)
FetchContent_GetProperties(Metal)
if (NOT Metal_POPULATED)
    FetchContent_MakeAvailable(Metal)
endif()
target_link_libraries(${PROJECT_NAME} PUBLIC Metal)
```

## Example

For minimal Metal-cpp library testing, you can try this program:

```cpp
// main.cpp

#include <cstdio>

#include <Foundation/Foundation.hpp>
#include <Metal/Metal.hpp>

int main() {
    MTL::Device* device = MTL::CreateSystemDefaultDevice();
    std::printf("%s", device->description()->cString(NS::UTF8StringEncoding));
    device->release();
}
```

**Note: there is no need to add other #define(s) for the header file*

```cmake
# CMakeLists.txt

cmake_minimum_required(VERSION 3.12.0)
project(minimal-test VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 17)

add_compile_options(-Wall -Wextra)
add_executable(${PROJECT_NAME} main.cpp)

include(FetchContent)
FetchContent_Declare(Metal GIT_REPOSITORY https://github.com/Unbinilium/Metal.git GIT_SHALLOW 1)
FetchContent_GetProperties(Metal)
if (NOT Metal_POPULATED)
    FetchContent_MakeAvailable(Metal)
endif()
target_link_libraries(${PROJECT_NAME} PUBLIC Metal)
```

If the test passed successfully, you cloud consider a further learning on [Apple Metal Sample Code](https://developer.apple.com/metal/sample-code/).
