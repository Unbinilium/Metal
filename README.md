## Metal

It's the original Metal-cpp which has a low-overhead C++ interface for Metal, written by Apple. Here I wrapped the Metal-cpp into a CMake portable library.

## Usege

Please clone this repository first, then add the code below to you `CMakeLists.txt` of your project:

```
add_subdirectory(<Path to the Metal library>)
target_link_libraries(${PROJECT_NAME} PUBLIC Metal)
```
