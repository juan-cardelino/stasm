project(STASM)

#**************************************************************************************************
# General cMake settings
#**************************************************************************************************
cmake_minimum_required(VERSION 2.8)



#**************************************************************************************************
# Search for dependencies (Stasm, OpenCV)
#**************************************************************************************************
find_package(OpenCV REQUIRED)
if(OpenCV_FOUND)
  include_directories(${OpenCV_INCLUDE_DIRS})
endif()

find_package(STASM REQUIRED)
if(STASM_FOUND)
  include_directories(${STASM_INCLUDE_DIRS})
endif()

LINK_DIRECTORIES( ${OpenCV_LIB_DIR} ${STASM_LINK_DIRS} )

SET(LIBS ${STASM_LIBRARIES} ${OpenCV_LIBS}  )


SET(EXECUTABLES minimal)
FOREACH(var ${EXECUTABLES})
add_executable(${var} ../apps/${var}.cpp)
target_link_libraries(${var} ${LIBS})
ENDFOREACH(var)
