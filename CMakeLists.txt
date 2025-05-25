set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
cmake_minimum_required(VERSION 3.4)
project(lab6)
include_directories("formatter_lib/" "formatter_ex_lib/" "solver_lib/")
add_subdirectory(formatter_ex_lib)
add_subdirectory(formatter_lib)
add_subdirectory(solver_lib)
add_subdirectory(solver_application)
add_subdirectory(hello_world_application)
install(TARGETS solva
    DESTINATION bin
    COMPONENT bin
)
install(DIRECTORY "formatter_lib"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "formatter_ex_lib"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "formatter_ex_lib"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "hello_world_application"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "formatter_ex_lib"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "solver_application"
    DESTINATION sources
    COMPONENT sources
)
install(DIRECTORY "solver_lib"
    DESTINATION sources
    COMPONENT sources
)




set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Your name")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "libc6 (>=2.28), zlib1g")
add_custom_target(packageSources
  COMMAND cpack 
    -D CPACK_GENERATOR="ZIP"
    -D CPACK_COMPONENTS_ALL=sources
  COMMAND cpack
    -D CPACK_GENERATOR="TGZ"
    -D CPACK_COMPONENTS_ALL=sources
  COMMENT "Building archives for Component A (ZIP/TGZ)"
)

add_custom_target(packageBin
  COMMAND cpack 
    -D CPACK_GENERATOR="DEB"
    -D CPACK_COMPONENTS_ALL=bin
  COMMENT "Building packages for Component B (DEB/RPM)"
)

add_custom_target(package_all
  DEPENDS
    packageSources
    packageBin
  COMMENT "Building all packages"
)

set(CPACK_SOURCE_GENERATOR "ZIP")
set(CPACK_DEB_COMPONENT_INSTALL ON)
set(CPACK_COMPONENTS_ALL bin sources)
set(CPACK_ARCHIVE_COMPONENT_INSTALL ON)
include(CPack)
