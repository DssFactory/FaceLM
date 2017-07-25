# ----------------------------------------------------------------------------
#  Root CMake file for FaceLM
#
#    From the off-tree build directory, invoke:
#      $ cmake <PATH_TO_FACELM_ROOT>
#
# ----------------------------------------------------------------------------

include(cmake/FaceLMMinDepVersions.cmake)

if(CMAKE_GENERATOR MATCHES Xcode AND XCODE_VERSION VERSION_GREATER 4.3)
  cmake_minimum_required(VERSION 2.8.8 FATAL_ERROR)
elseif(CMAKE_SYSTEM_NAME MATCHES WindowsPhone OR CMAKE_SYSTEM_NAME MATCHES WindowsStore)
  cmake_minimum_required(VERSION 3.1 FATAL_ERROR)

  #Required to resolve linker error issues due to incompatibility with CMake v3.0+ policies.
  #CMake fails to find _fseeko() which leads to subsequent linker error.
  #See details here: http://www.cmake.org/Wiki/CMake/Policies
  cmake_policy(VERSION 2.8)
else()
  cmake_minimum_required(VERSION "${MIN_VER_CMAKE}" FATAL_ERROR)
endif()



# Recurse into the "FaceLM" subdirectories. This does not actually
# cause another cmake executable to run. The same process will walk through
# the project's entire directory structure.
add_subdirectory(FaceLM)
