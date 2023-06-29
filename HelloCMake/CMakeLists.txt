# ============================================================================
# / <summary>
# / CMakeLists.txt
# / CMakeIntroduction
# / created by Mehrdad Soleimanimajd on 03.04.2019
# / </summary>
# / <created>ʆϒʅ, 03.04.2019</created>
# / <changed>ʆϒʅ, 29.06.2023</changed>
# ============================================================================

cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# project settings
set(TARGET_NAME "HelloCMake")
set(PROJECT_NAME ${TARGET_NAME})
project(
  ${PROJECT_NAME}
  VERSION 1.0.1.0
  DESCRIPTION "CMake simple example"
  HOMEPAGE_URL "https://github.com/s-mehrdad/CMakeIntroduction"
  LANGUAGES CXX
)

set(VerCompanyName "BirdSofts")
set(VerFileDescription "CMake example: HelloCMake")
set(VerFileVersion "1,0,1,0")
set(VerInternalName ${TARGET_NAME})
set(VerLegalCopyright "Copyright (C) 2019-2023")
set(VerLegalTrademarks1 "BS")
set(VerLegalTrademarks2 "BSs")
set(VerOriginalFilename ${TARGET_NAME})
set(VerProductName ${TARGET_NAME})
set(VerProductVersion "1.0.1.0")

set(VerProjectType "VFT_APP")

configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/../CMakeIntroduction.rc.in CMakeIntroduction.rc @ONLY CRLF
)

set(RESOURCE_FILES "CMakeIntroduction.rc")

# project source files
set(
  SOURCE_FILES
  "source/HelloCMake.cpp"
  "source/HelloCMake.h"
)

# Add source to this project's executable.
add_executable(
  ${PROJECT_NAME}
  ${SOURCE_FILES}
  ${RESOURCE_FILES}
)
