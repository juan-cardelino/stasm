project(STASM)

#**************************************************************************************************
# General cMake settings
#**************************************************************************************************
cmake_minimum_required(VERSION 2.8)

#**************************************************************************************************
# Preprocessor definitions
#**************************************************************************************************
if (CMAKE_CL_64)
 add_definitions(-DWIN64)
 set(PLATFORM x64)
else (CMAKE_CL_64)
 set(PLATFORM x86)
endif (CMAKE_CL_64)

if(WIN32)
  ADD_DEFINITIONS(-DIGTB_EXPORTS)
  ADD_DEFINITIONS(-D_WIN32_WINNT=0x0501)
endif(WIN32)

enable_testing()

#**************************************************************************************************
# Search for OpenCV
#**************************************************************************************************
find_package(OpenCV REQUIRED)
if(OpenCV_FOUND)
  include_directories(${OpenCV_INCLUDE_DIRS})
endif()

LINK_DIRECTORIES(
  ${OpenCV_LIB_DIR}
)

SET(STASM_BASE_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
SET(STASM_APP_SHAPEFILE_DIR "${STASM_BASE_DIR}/apps/shapefile")

SET(OBJ_STASM
${STASM_BASE_DIR}/stasm/asm.cpp
${STASM_BASE_DIR}/stasm/classicdesc.cpp
${STASM_BASE_DIR}/stasm/convshape.cpp
${STASM_BASE_DIR}/stasm/err.cpp
${STASM_BASE_DIR}/stasm/eyedet.cpp
${STASM_BASE_DIR}/stasm/eyedist.cpp
${STASM_BASE_DIR}/stasm/faceroi.cpp
${STASM_BASE_DIR}/stasm/hat.cpp
${STASM_BASE_DIR}/stasm/hatdesc.cpp
${STASM_BASE_DIR}/stasm/landmarks.cpp
${STASM_BASE_DIR}/stasm/misc.cpp
${STASM_BASE_DIR}/stasm/pinstart.cpp
${STASM_BASE_DIR}/stasm/print.cpp
${STASM_BASE_DIR}/stasm/shape17.cpp
${STASM_BASE_DIR}/stasm/shapehacks.cpp
${STASM_BASE_DIR}/stasm/shapemod.cpp
${STASM_BASE_DIR}/stasm/startshape.cpp
${STASM_BASE_DIR}/stasm/stasm.cpp
${STASM_BASE_DIR}/stasm/stasm_lib.cpp
)

SET(OBJ_MOD1
${STASM_BASE_DIR}/stasm/MOD_1/facedet.cpp
${STASM_BASE_DIR}/stasm/MOD_1/initasm.cpp
)

SET(OBJ_STASM_MAIN
${STASM_BASE_DIR}/apps/stasm_main.cpp
${STASM_BASE_DIR}/apps/appmisc.cpp
)

SET(OBJ_SWAS
${STASM_BASE_DIR}/apps/swas/swas.cpp
${STASM_BASE_DIR}/apps/appmisc.cpp
${STASM_BASE_DIR}/apps/shapefile/shapefile.cpp
${STASM_BASE_DIR}/apps/shapefile/stasm_regex.cpp
${STASM_BASE_DIR}/apps/swas/fitmeas.cpp
${STASM_BASE_DIR}/apps/swas/fm29.cpp
)

#SET(OBJ_MIRROR
#${STASM_BASE_DIR}/apps/appmisc.cpp
#${STASM_BASE_DIR}/apps/shapefile/stasm_regex.cpp
#${STASM_APP_SHAPEFILE_DIR}/shapefile.cpp
#${STASM_APP_SHAPEFILE_DIR}/shapemirror.cpp
#)

SET(OBJ_TASM
${STASM_BASE_DIR}/apps/appmisc.cpp
${STASM_BASE_DIR}/apps/shapefile/shapefile.cpp
${STASM_BASE_DIR}/apps/shapefile/stasm_regex.cpp
${STASM_BASE_DIR}/apps/swas/fitmeas.cpp
${STASM_BASE_DIR}/apps/swas/fm29.cpp
${STASM_BASE_DIR}/apps/appmem.cpp
${STASM_BASE_DIR}/apps/linsolve.cpp
${STASM_BASE_DIR}/tasm/src/tasm.cpp
${STASM_BASE_DIR}/tasm/src/tasmalignshapes.cpp
${STASM_BASE_DIR}/tasm/src/tasmclassic.cpp
${STASM_BASE_DIR}/tasm/src/tasmconf.cpp
${STASM_BASE_DIR}/tasm/src/tasmdescmod.cpp
${STASM_BASE_DIR}/tasm/src/tasmdraw.cpp
${STASM_BASE_DIR}/tasm/src/tasmhat.cpp
${STASM_BASE_DIR}/tasm/src/tasmimpute.cpp
${STASM_BASE_DIR}/tasm/src/tasmlandtab.cpp
${STASM_BASE_DIR}/tasm/src/tasmmeanshape.cpp
${STASM_BASE_DIR}/tasm/src/tasmshapemod.cpp
)

#SET(OBJ_MDIFF
#${STASM_BASE_DIR}/apps/mdiff/mdiff.cpp
#)

include_directories(${STASM_BASE_DIR}/stasm)
include_directories(${STASM_BASE_DIR}/stasm/MOD_1)
include_directories(${STASM_APP_SHAPEFILE_DIR})

SET(STASM_INCLUDE_DIRS
${STASM_BASE_DIR}/stasm
${STASM_BASE_DIR}/stasm/MOD_1
)

SET(LIBS ${OpenCV_LIBS})

set(STASM_LIB stasm)
add_library(${STASM_LIB} ${OBJ_MOD1} ${OBJ_STASM})
target_link_libraries(${STASM_LIB} ${LIBS})

SET(EXECUTABLES minimal minimal2)
FOREACH(var ${EXECUTABLES})
add_executable(${var} apps/${var}.cpp)
target_link_libraries(${var} ${STASM_LIB} ${LIBS})
ENDFOREACH(var)

set(STASM_EXE stasmMain)
add_executable(${STASM_EXE} ${OBJ_STASM_MAIN})
target_link_libraries(${STASM_EXE} ${STASM_LIB} ${LIBS})

set(SWAS_EXE swas)
add_executable(${SWAS_EXE} ${OBJ_SWAS})
target_link_libraries(${SWAS_EXE} ${STASM_LIB} ${LIBS})

#set(TASM_MIRROR shapemirror)
#add_executable(${TASM_MIRROR} ${OBJ_MIRROR})
#target_link_libraries(${TASM_MIRROR} ${STASM_LIB} ${LIBS})

set(TASM_EXE tasm)
add_executable(${TASM_EXE} ${OBJ_TASM})
target_link_libraries(${TASM_EXE} ${STASM_LIB} ${LIBS})

#set(MDIFF_EXE mdiff)
#add_executable(${MDIFF_EXE} ${OBJ_MDIFF})
#target_link_libraries(${MDIFF_EXE} )


#**************************************************************************************************
# Test
#**************************************************************************************************

add_test(TestMinimal ./minimal)
add_test(TestMinimal2 ./minimal2)
add_test(TestStasm ./stasmMain ../data/testface.jpg)
add_test(TestStasmMulti ./stasmMain -m ../tests/data/testmulti.jpg)
add_test(TestStasmMulti2 ./stasmMain -d -m -s -c ../tests/data/testmulti.jpg)
add_test(TestStasm68 ./stasmMain -i -n 68 ../data/testface.jpg)
add_test(TestSwas ./swas -f ../tests/data/testface.shape)
add_test(TestTasm ./tasm -d test_tasmout -w ../tasm/shapes/muct77_short.shape)

#**************************************************************************************************
# Generate batch files for examples
#**************************************************************************************************
#setup Config.cmake
configure_file(STASMConfig.cmake.in
  "${PROJECT_BINARY_DIR}/STASMConfig.cmake" @ONLY)

INSTALL(
FILES ${PROJECT_BINARY_DIR}/STASMConfig.cmake
DESTINATION ${CMAKE_INSTALL_PREFIX}/share/cmake/
COMPONENT dev)
