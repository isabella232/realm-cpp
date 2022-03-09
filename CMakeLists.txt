cmake_minimum_required(VERSION 3.15)

project(realmcpp)

# Project-wide build flags
set(CMAKE_CXX_STANDARD 20)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)
#set(CMAKE_CXX_EXTENSIONS OFF)
#set(CMAKE_CXX20_STANDARD_COMPILE_OPTION "-std=c++2a")

option(REALM_DOTNET_BUILD_CORE_FROM_SOURCE "Build Realm Core from source, as opposed to downloading prebuilt binaries" ON)
if(REALM_DOTNET_BUILD_CORE_FROM_SOURCE)
    set(REALM_BUILD_LIB_ONLY ON)

    add_subdirectory(realm-core EXCLUDE_FROM_ALL)
else()
    # TODO: implement downloading realm-core builds from the CDN
    message(FATAL_ERROR "Using prebuilt realm-core is not implemented")
endif()

include_directories(src)
add_subdirectory(src)
add_subdirectory(tests)