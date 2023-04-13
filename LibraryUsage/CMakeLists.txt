
# ********************************************************************************
# / <summary>
# / CMakeLists.txt
# / CMakeIntroduction
# / created by Mehrdad Soleimanimajd on 04.04.2019
# / </summary>
# / <created>ʆϒʅ, 04.04.2019</created>
# / <changed>ʆϒʅ, 13.04.2023</changed>
# ********************************************************************************

cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# option: link to the shared version
# set(LINK_SHARED_LIB ON)

set(TARGET_NAME LibraryUsage)
set(PROJECT_NAME ${TARGET_NAME})
project(${PROJECT_NAME}
  VERSION 0.1.0.0
  DESCRIPTION "CMake notes and examples"
  HOMEPAGE_URL "https://github.com/s-mehrdad/CMakeIntroduction"
  LANGUAGES CXX
)

# set(ROOT $ENV{UserProfile}/Source/Repos/CMakeIntroduction)
# set(ROOT ${CMAKE_CURRENT_SOURCE_DIR}/..)
# message(get_property(${ROOT}))
add_subdirectory(StaticAndSharedLibrary)

# link_directories(StaticAndSharedLibrary/build/debug)

# if(${LINK_SHARED_LIB} MATCHES ON)
# # dynamic library linkage
# link_directories(StaticAndSharedLibrary/build/debug)
# else()
# # static library linkage
# link_directories(StaticAndSharedLibrary/build)
# endif()

# include_directories(StaticAndSharedLibrary/source)

# Add source to this project's executable.
add_executable(${TARGET_NAME} "source/LibraryUsage.cpp")

if(${BUILD_SHARED_LIB} MATCHES ON)
  # pre and post build event
  # copy library into target directory
  # must follow a generation event
  add_custom_command(TARGET ${TARGET_NAME} PRE_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    ${CMAKE_CURRENT_BINARY_DIR_DIR}/StaticAndSharedLibrary/debug
    $<TARGET_FILE_DIR:${TARGET_NAME}>
  )
  # install(FILES ${CMAKE_CURRENT_BINARY_DIR_DIR}/StaticAndSharedLibrary/debug
  #   DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/debug
  # )
endif()

target_link_libraries(${TARGET_NAME}
  PUBLIC StaticAndSharedLibrary)
