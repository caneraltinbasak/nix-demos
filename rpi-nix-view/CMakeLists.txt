cmake_minimum_required(VERSION 2.8)

find_package(PkgConfig)

pkg_check_modules(WebKitNix WebKitNix REQUIRED)
pkg_check_modules(GLIB glib-2.0 REQUIRED)
pkg_check_modules(CAIRO cairo REQUIRED)
#pkg_check_modules(LIBPROFILER libprofiler)

include_directories(Sample_INCLUDES
    /opt/vc/include
    /opt/vc/include/interface/vmcs_host
    /opt/vc/include/interface/vmcs_host/linux
    /opt/vc/include/interface/vcos/pthreads
    ${WebKitNix_INCLUDE_DIRS}
    ${GLIB_INCLUDE_DIRS}
    ${CAIRO_INCLUDE_DIRS}
)

link_directories(
    /opt/vc/lib
    ${WebKitNix_LIBRARY_DIRS}
    ${GLIB_LIBRARY_DIRS}
    ${CAIRO_LIBRARY_DIRS}
)

add_definitions("-Wall")

set(Sample_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})

set(Sample_INJECTEDBUNDLE_DIR ${CMAKE_BINARY_DIR}/InjectedBundle/)
add_definitions(-DSAMPLE_INJECTEDBUNDLE_DIR="${Sample_INJECTEDBUNDLE_DIR}")

add_executable(Sample main.cpp)
target_link_libraries(Sample
    ${GLIB_LIBRARIES}
    ${WebKitNix_LIBRARIES}
    GLESv2
    EGL
    bcm_host
    vcos
    vchiq_arm
#    ${LIBPROFILER_LIBRARIES}
)

add_subdirectory(InjectedBundle)
