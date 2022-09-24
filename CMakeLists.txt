# Copyright (c) Microsoft Corporation
#
# All rights reserved.
#
# MIT License
#
# Permission is hereby granted, free of charge, to any person obtaining a copy of
# this software and associated documentation files (the "Software"), to deal in
# the Software without restriction, including without limitation the rights to
# use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
# of the Software, and to permit persons to whom the Software is furnished to do
# so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED *AS IS*, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

cmake_minimum_required(VERSION 3.11)

project(CoinUtils LANGUAGES C CXX VERSION 2.11.6)

set(CMAKE_CXX_STANDARD 14)

include(GNUInstallDirs)
set(INSTALL_INCLUDE_DIR ${CMAKE_INSTALL_INCLUDEDIR}/Coin)
set(INSTALL_CMAKE_DIR ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME})

if(MSVC)
  set(
    CMAKE_CXX_FLAGS
    "${CMAKE_CXX_FLAGS} /bigobj /MP /wd4996 /wd4819 /wd4251 /wd4267 /wd4244 /wd4275"
    )
endif()

if(APPLE)
  set(
    CMAKE_CXX_FLAGS
    "${CMAKE_CXX_FLAGS} -Wno-inconsistent-missing-override -Wno-unused-command-line-argument -Wno-unused-result -Wno-exceptions"
    )
  set(CMAKE_OSX_DEPLOYMENT_TARGET "10.9"
      CACHE STRING "Minimum OS X deployment version")
endif()

include(CheckIncludeFileCXX)
include(CheckIncludeFile)
check_include_file_cxx("cmath"    HAVE_CMATH)
check_include_file_cxx("cfloat"    HAVE_CFLOAT)
if(NOT HAVE_CMATH OR NOT HAVE_CFLOAT)
    message(FATAL_ERROR "Missing necessary include files, like cmath or cfloat")
endif()

set(UTILS_SOURCES
    src/CoinAdjacencyVector.cpp
    src/CoinAlloc.cpp
    src/CoinBronKerbosch.cpp
    src/CoinBuild.cpp
    src/CoinCliqueExtender.cpp
    src/CoinCliqueList.cpp
    src/CoinCliqueSet.cpp
    src/CoinConflictGraph.cpp
    src/CoinCutPool.cpp
    src/CoinDenseFactorization.cpp
    src/CoinDenseVector.cpp
    src/CoinDynamicConflictGraph.cpp
    src/CoinError.cpp
    src/CoinFactorization1.cpp
    src/CoinFactorization2.cpp
    src/CoinFactorization3.cpp
    src/CoinFactorization4.cpp
    src/CoinFileIO.cpp
    src/CoinFinite.cpp
    src/CoinIndexedVector.cpp
    src/CoinLpIO.cpp
    src/CoinMessage.cpp
    src/CoinMessageHandler.cpp
    src/CoinModel.cpp
    src/CoinModelUseful2.cpp
    src/CoinModelUseful.cpp
    src/CoinMpsIO.cpp
    src/CoinNodeHeap.cpp
    src/CoinOddWheelSeparator.cpp
    src/CoinOslFactorization2.cpp
    src/CoinOslFactorization3.cpp
    src/CoinOslFactorization.cpp
    src/CoinPackedMatrix.cpp
    src/CoinPackedVectorBase.cpp
    src/CoinPackedVector.cpp
    src/CoinParam.cpp
    src/CoinParamUtils.cpp
    src/CoinPostsolveMatrix.cpp
    src/CoinPrePostsolveMatrix.cpp
    src/CoinPresolveDoubleton.cpp
    src/CoinPresolveDual.cpp
    src/CoinPresolveDupcol.cpp
    src/CoinPresolveEmpty.cpp
    src/CoinPresolveFixed.cpp
    src/CoinPresolveForcing.cpp
    src/CoinPresolveHelperFunctions.cpp
    src/CoinPresolveImpliedFree.cpp
    src/CoinPresolveIsolated.cpp
    src/CoinPresolveMatrix.cpp
    src/CoinPresolveMonitor.cpp
    src/CoinPresolvePsdebug.cpp
    src/CoinPresolveSingleton.cpp
    src/CoinPresolveSubst.cpp
    src/CoinPresolveTighten.cpp
    src/CoinPresolveTripleton.cpp
    src/CoinPresolveUseless.cpp
    src/CoinPresolveZeros.cpp
    src/CoinRational.cpp
    src/CoinSearchTree.cpp
    src/CoinShallowPackedVector.cpp
    src/CoinShortestPath.cpp
    src/CoinSimpFactorization.cpp
    src/CoinSnapshot.cpp
    src/CoinStaticConflictGraph.cpp
    src/CoinStructuredModel.cpp
    src/CoinWarmStartBasis.cpp
    src/CoinWarmStartDual.cpp
    src/CoinWarmStartPrimalDual.cpp
    src/CoinWarmStartVector.cpp
)

set(UTILS_HEADERS
    src/CoinAdjacencyVector.hpp
    src/CoinAlloc.hpp
    src/CoinBronKerbosch.hpp
    src/CoinBuild.hpp
    src/CoinCliqueExtender.hpp
    src/CoinCliqueList.hpp
    src/CoinCliqueSet.hpp
    src/CoinConflictGraph.hpp
    src/CoinCutPool.hpp
    src/CoinDenseFactorization.hpp
    src/CoinDenseVector.hpp
    src/CoinDistance.hpp
    src/CoinDynamicConflictGraph.hpp
    src/CoinError.hpp
    src/CoinFactorization.hpp
    src/CoinFileIO.hpp
    src/CoinFinite.hpp
    src/CoinFloatEqual.hpp
    src/CoinHelperFunctions.hpp
    src/CoinIndexedVector.hpp
    src/CoinLpIO.hpp
    src/CoinMessageHandler.hpp
    src/CoinMessage.hpp
    src/CoinModel.hpp
    src/CoinModelUseful.hpp
    src/CoinMpsIO.hpp
    src/CoinNodeHeap.hpp
    src/CoinOddWheelSeparator.hpp
    src/CoinOslC.h
    src/CoinOslFactorization.hpp
    src/CoinPackedMatrix.hpp
    src/CoinPackedVectorBase.hpp
    src/CoinPackedVector.hpp
    src/CoinParam.hpp
    src/CoinPragma.hpp
    src/CoinPresolveDoubleton.hpp
    src/CoinPresolveDual.hpp
    src/CoinPresolveDupcol.hpp
    src/CoinPresolveEmpty.hpp
    src/CoinPresolveFixed.hpp
    src/CoinPresolveForcing.hpp
    src/CoinPresolveImpliedFree.hpp
    src/CoinPresolveIsolated.hpp
    src/CoinPresolveMatrix.hpp
    src/CoinPresolveMonitor.hpp
    src/CoinPresolvePsdebug.hpp
    src/CoinPresolveSingleton.hpp
    src/CoinPresolveSubst.hpp
    src/CoinPresolveTighten.hpp
    src/CoinPresolveTripleton.hpp
    src/CoinPresolveUseless.hpp
    src/CoinPresolveZeros.hpp
    src/CoinRational.hpp
    src/CoinSearchTree.hpp
    src/CoinShallowPackedVector.hpp
    src/CoinShortestPath.hpp
    src/CoinSignal.hpp
    src/CoinSimpFactorization.hpp
    src/CoinSmartPtr.hpp
    src/CoinSnapshot.hpp
    src/CoinSort.hpp
    src/CoinStaticConflictGraph.hpp
    src/CoinStructuredModel.hpp
    src/CoinTime.hpp
    src/CoinTypes.h
    src/CoinUtility.hpp
    src/CoinUtilsConfig.h
    src/CoinWarmStartBasis.hpp
    src/CoinWarmStartDual.hpp
    src/CoinWarmStart.hpp
    src/CoinWarmStartPrimalDual.hpp
    src/CoinWarmStartVector.hpp
    # Note that the following 3 files are excluded from installable headers on Osi and Clp because
    # all 3 projects install to the same include directory and we want CoinUtils versions of the
    # headers to take precedence
    src/configall_system.h
    src/configall_system_msc.h
    src/config_default.h

    src/config_coinutils_default.h
)

add_library(${PROJECT_NAME} ${UTILS_SOURCES})

target_include_directories(${PROJECT_NAME} PUBLIC $<INSTALL_INTERFACE:${INSTALL_INCLUDE_DIR}> $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>)

if(MSVC)
  target_compile_definitions(${PROJECT_NAME} PRIVATE _CRT_SECURE_NO_WARNINGS)
endif()
target_compile_definitions(${PROJECT_NAME} PRIVATE HAVE_CMATH HAVE_CFLOAT)

install(FILES ${UTILS_HEADERS} DESTINATION ${INSTALL_INCLUDE_DIR})

install(TARGETS ${PROJECT_NAME}
        EXPORT "${PROJECT_NAME}Targets"
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin)

include(CMakePackageConfigHelpers)

set(version_config "${CMAKE_CURRENT_BINARY_DIR}/temp/${PROJECT_NAME}ConfigVersion.cmake")
set(project_config "${CMAKE_CURRENT_BINARY_DIR}/temp/${PROJECT_NAME}Config.cmake")
set(namespace "Coin::")

write_basic_package_version_file("${version_config}"
                                 COMPATIBILITY SameMajorVersion)

configure_package_config_file("Config.cmake.in"
                              "${project_config}"
                              INSTALL_DESTINATION
                              "${INSTALL_CMAKE_DIR}")

install(FILES "${project_config}" "${version_config}"
        DESTINATION "${INSTALL_CMAKE_DIR}")

install(EXPORT "${PROJECT_NAME}Targets"
        NAMESPACE "${namespace}"
        DESTINATION "${INSTALL_CMAKE_DIR}")
