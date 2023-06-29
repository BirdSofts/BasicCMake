# ============================================================================
# / <summary>
# / CMakelists.txt
# / CMakeIntroduction
# / created by Mehrdad Soleimanimajd on 03.04.2019
# / </summary>
# / <created>ʆϒʅ, 03.04.2019</created>
# / <changed>ʆϒʅ, 29.06.2023</changed>
# ============================================================================

cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# option: build a shared version
set(BUILD_SHARED_LIB ON)

# project settings
set(TARGET_NAME StaticAndSharedLibrary)
set(PROJECT_NAME ${TARGET_NAME})
project(
  ${PROJECT_NAME}
  VERSION 1.0.1.0
  DESCRIPTION "CMake notes and examples"
  HOMEPAGE_URL "https://github.com/s-mehrdad/CMakeIntroduction"
  LANGUAGES CXX
)

set(VerCompanyName "BirdSofts")
set(VerFileDescription "CMake example: static/ dynamic library")
set(VerFileVersion "1,0,1,0")
set(VerInternalName ${TARGET_NAME})
set(VerLegalCopyright "Copyright (C) 2019-2023")
set(VerLegalTrademarks1 "BS")
set(VerLegalTrademarks2 "BSs")
set(VerOriginalFilename ${TARGET_NAME})
set(VerProductName ${TARGET_NAME})
set(VerProductVersion ${CMAKE_PROJECT_VERSION})

set(VerProjectType "VFT_DLL")

configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/../../CMakeIntroduction.rc.in CMakeIntroduction.rc @ONLY CRLF
)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

# TODO:
# how to include header files from here
# set(CMAKE_INCLUDE_DIRECTORIES_BEFORE ON)
# include_directories(source)
# target_include_directories(${TARGET_NAME} BEFORE
# PUBLIC source)
set(RESOURCE_FILES "CMakeIntroduction.rc")

# source files
list(
  APPEND
  HEADER_FILES
  source/StaticAndSharedLibrary.h
)
list(
  APPEND
  SOURCE_FILES
  source/StaticAndSharedLibrary.cpp
)

if(WIN32)
  list(
    APPEND
    SOURCE_FILES
    ${HEADER_FILES})
endif()

# generate the dynamic library
if(${BUILD_SHARED_LIB} MATCHES ON)
  add_library(
    ${TARGET_NAME}
    SHARED ${SOURCE_FILES}
    ${RESOURCE_FILES})

  # generate export header automatically
  include(GenerateExportHeader)
  generate_export_header(
    ${TARGET_NAME}
    BASE_NAME ${TARGET_NAME}
    EXPORT_MACRO_NAME ${TARGET_NAME}_EXPORTS
    EXPORT_FILE_NAME ${TARGET_NAME}_EXPORTS.h
    STATIC_DEFINE ${TARGET_NAME}_EXPORTS_BUILD_AS_STATIC
  )
else()
  add_library(
    ${TARGET_NAME}
    STATIC
    ${SOURCE_FILES}
    ${RESOURCE_FILES}
  )
endif()
