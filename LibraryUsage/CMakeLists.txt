# ============================================================================
# / <summary>
# / CMakeLists.txt
# / CMakeIntroduction
# / created by Mehrdad Soleimanimajd on 04.04.2019
# / </summary>
# / <created>ʆϒʅ, 04.04.2019</created>
# / <changed>ʆϒʅ, 29.06.2023</changed>
# ============================================================================

cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# option: link to the shared version
set(LINK_SHARED_LIB ON)
set(TARGET_NAME LibraryUsage)
set(PROJECT_NAME ${TARGET_NAME})
project(
  ${PROJECT_NAME}
  VERSION 1.0.1.0
  DESCRIPTION "CMake notes and examples"
  HOMEPAGE_URL "https://github.com/s-mehrdad/CMakeIntroduction"
  LANGUAGES CXX
)

set(VerCompanyName "BirdSofts")
set(VerFileDescription "CMake example: static/ dynamic library usage")
set(VerFileVersion "1,0,1,0")
set(VerInternalName ${TARGET_NAME})
set(VerLegalCopyright "Copyright (C) 2019-2023")
set(VerLegalTrademarks1 "BS")
set(VerLegalTrademarks2 "BSs")
set(VerOriginalFilename ${TARGET_NAME})
set(VerProductName ${TARGET_NAME})
set(VerProductVersion ${CMAKE_PROJECT_VERSION})

set(VerProjectType "VFT_APP")

configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/../CMakeIntroduction.rc.in CMakeIntroduction.rc @ONLY CRLF
)

add_subdirectory(StaticAndSharedLibrary)

# if(${LINK_SHARED_LIB} MATCHES ON)
# # dynamic library linkage
# link_directories(StaticAndSharedLibrary/build/Debug)
# else()
# # static library linkage
# link_directories(StaticAndSharedLibrary/build)
# endif()
set(RESOURCE_FILES "CMakeIntroduction.rc")

# Add source to this project's executable.
add_executable(
  ${TARGET_NAME}
  "source/LibraryUsage.cpp"
  ${RESOURCE_FILES}
)

if(${LINK_SHARED_LIB} MATCHES ON)
  # pre and post build event
  # copy library into target directory
  # must follow a generation event
  add_custom_command(
    TARGET ${TARGET_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    ${CMAKE_CURRENT_BINARY_DIR_DIR}/StaticAndSharedLibrary/Debug/StaticAndSharedLibrary.dll
    ${CMAKE_CURRENT_BINARY_DIR}/Debug

    # $<TARGET_FILE_DIR:${TARGET_NAME}>
  )

  # install
  # (
  # FILES ${CMAKE_CURRENT_BINARY_DIR_DIR}/StaticAndSharedLibrary/Debug/StaticAndSharedLibrary.dll
  # RUNTIME
  # TYPE LIB
  # CONFIGURATIONS Debug
  # DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/Debug
  # )
endif()

target_link_libraries(
  ${TARGET_NAME}
  PUBLIC StaticAndSharedLibrary
)
