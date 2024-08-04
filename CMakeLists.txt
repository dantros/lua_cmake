cmake_minimum_required(VERSION 3.20)

# Do note we are building Lua as C++ code
project(lua_project CXX)

set(LUA_SRC_DIR "lua-5.4.7/src")

set(LUA_SRC_FILES
    "${LUA_SRC_DIR}/lapi.c"
    "${LUA_SRC_DIR}/lauxlib.c"
    "${LUA_SRC_DIR}/lbaselib.c"
    "${LUA_SRC_DIR}/lcode.c"
    "${LUA_SRC_DIR}/lcorolib.c"
    "${LUA_SRC_DIR}/lctype.c"
    "${LUA_SRC_DIR}/ldblib.c"
    "${LUA_SRC_DIR}/ldebug.c"
    "${LUA_SRC_DIR}/ldo.c"
    "${LUA_SRC_DIR}/ldump.c"
    "${LUA_SRC_DIR}/lfunc.c"
    "${LUA_SRC_DIR}/lgc.c"
    "${LUA_SRC_DIR}/linit.c"
    "${LUA_SRC_DIR}/liolib.c"
    "${LUA_SRC_DIR}/llex.c"
    "${LUA_SRC_DIR}/lmathlib.c"
    "${LUA_SRC_DIR}/lmem.c"
    "${LUA_SRC_DIR}/loadlib.c"
    "${LUA_SRC_DIR}/lobject.c"
    "${LUA_SRC_DIR}/lopcodes.c"
    "${LUA_SRC_DIR}/loslib.c"
    "${LUA_SRC_DIR}/lparser.c"
    "${LUA_SRC_DIR}/lstate.c"
    "${LUA_SRC_DIR}/lstring.c"
    "${LUA_SRC_DIR}/lstrlib.c"
    "${LUA_SRC_DIR}/ltable.c"
    "${LUA_SRC_DIR}/ltablib.c"
    "${LUA_SRC_DIR}/ltm.c"
    "${LUA_SRC_DIR}/lundump.c"
    "${LUA_SRC_DIR}/lutf8lib.c"
    "${LUA_SRC_DIR}/lvm.c"
    "${LUA_SRC_DIR}/lzio.c"
)

# We need to tell CMake that the source .c files should be interpreted as C++ files
set_source_files_properties(${LUA_SRC_FILES} "${LUA_SRC_DIR}/lua.c" "${LUA_SRC_DIR}/luac.c" PROPERTIES LANGUAGE CXX )

# We need to tell CMake that the we will use the C++ linker, check the target property LINKER_LANGUAGE bellow.

add_library(lua_static STATIC ${LUA_SRC_FILES})
set_property(TARGET lua_static PROPERTY CXX_STANDARD 11)
set_target_properties(lua_static PROPERTIES LINKER_LANGUAGE CXX)
#target_compile_definitions(lua_static PRIVATE LUA_USE_WINDOWS)
target_include_directories(lua_static PRIVATE "${LUA_SRC_DIR}")

add_executable(lua "${LUA_SRC_DIR}/lua.c")
set_property(TARGET lua PROPERTY CXX_STANDARD 11)
set_target_properties(lua PROPERTIES LINKER_LANGUAGE CXX)
target_include_directories(lua PRIVATE "${LUA_SRC_DIR}")
target_link_libraries(lua PRIVATE lua_static)

add_executable(luac "${LUA_SRC_DIR}/luac.c")
set_property(TARGET luac PROPERTY CXX_STANDARD 11)
set_target_properties(luac PROPERTIES LINKER_LANGUAGE CXX)
target_include_directories(luac PRIVATE "${LUA_SRC_DIR}")
target_link_libraries(luac PRIVATE lua_static)
