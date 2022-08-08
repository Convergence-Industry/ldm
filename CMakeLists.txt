cmake_minimum_required(VERSION 3.19)
project(ldm)

find_package(PkgConfig REQUIRED)
pkg_check_modules(LibUdev REQUIRED IMPORTED_TARGET libudev)
pkg_check_modules(Mount REQUIRED IMPORTED_TARGET mount)
pkg_check_modules(Glib REQUIRED IMPORTED_TARGET glib-2.0)

add_executable(ldm ldm.c ipc.c ipc.h)
target_link_libraries(ldm PUBLIC
        PkgConfig::LibUdev
        PkgConfig::Mount
        PkgConfig::Glib)

add_executable(ldmc ldmc.c ipc.c ipc.h)

set(ldm_compile_defs VERSION_STR="v0.7" _GNU_SOURCE)

target_compile_definitions(ldm PRIVATE ${ldm_compile_defs})
target_compile_definitions(ldmc PRIVATE ${ldm_compile_defs})
