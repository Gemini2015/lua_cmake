cmake_minimum_required(VERSION 3.20)

project(lua_cmake)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# request c++11 without gnu extension for the whole project and enable more warnings
if (CXXOPTS_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD ${CXXOPTS_CXX_STANDARD})
else()
  set(CMAKE_CXX_STANDARD 11)
endif()

set(CMAKE_CXX_EXTENSIONS OFF)

if(MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W2")
elseif(CMAKE_CXX_COMPILER_ID MATCHES "[Cc]lang" OR CMAKE_CXX_COMPILER_ID MATCHES "GNU")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
endif()
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -s")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -s")


# set output directory
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/lib")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/bin")


include_directories(${CMAKE_SOURCE_DIR}/src)
link_directories(${PROJECT_BINARY_DIR}/lib)

set(SRC_LIST
    src/lapi.c
    src/lauxlib.c
    src/lbaselib.c
    src/lcode.c
    src/lcorolib.c
    src/lctype.c
    src/ldblib.c
    src/ldebug.c
    src/ldo.c
    src/ldump.c
    src/lfunc.c
    src/lgc.c
    src/linit.c
    src/liolib.c
    src/llex.c
    src/lmathlib.c
    src/lmem.c
    src/loadlib.c
    src/lobject.c
    src/lopcodes.c
    src/loslib.c
    src/lparser.c
    src/lstate.c
    src/lstring.c
    src/lstrlib.c
    src/ltable.c
    src/ltablib.c
    src/ltests.c
    src/ltm.c
    src/lundump.c
    src/lutf8lib.c
    src/lvm.c
    src/lzio.c
    )

set(SRC_BIN_LIST
    src/lua.c
    )

set(INC_LIST
    src/lapi.h
    src/lauxlib.h
    src/lcode.h
    src/lctype.h
    src/ldebug.h
    src/ldo.h
    src/lfunc.h
    src/lgc.h
    src/ljumptab.h
    src/llex.h
    src/llimits.h
    src/lmem.h
    src/lobject.h
    src/lopcodes.h
    src/lopnames.h
    src/lparser.h
    src/lprefix.h
    src/lstate.h
    src/lstring.h
    src/ltable.h
    src/ltests.h
    src/ltm.h
    src/lua.h
    src/luaconf.h
    src/lualib.h
    src/lundump.h
    src/lvm.h
    src/lzio.h
    )

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${SRC_LIST})
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${INC_LIST})

add_definitions(-DLUA_USE_APICHECK)

add_executable(lua ${SRC_BIN_LIST} ${SRC_LIST} ${INC_LIST})
# add_library(lua STATIC ${SRC_LIST} ${INC_LIST})
