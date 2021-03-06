cmake_minimum_required(VERSION 3.1)
project(SoftRobots_test VERSION 1.0)

find_package(SofaFramework REQUIRED)
find_package(SofaCommon REQUIRED)
find_package(SofaTest REQUIRED)
find_package(SofaGTestMain REQUIRED)

set(HEADER_FILES)
set(SOURCE_FILES
    component/constraint/SurfacePressureConstraintTest.cpp
    component/constraint/UnilateralPlaneConstraintTest.cpp
    
    component/controller/AnimationEditorTest.cpp
    component/controller/DataVariationLimiterTest.cpp
    component/controller/SerialPortBridgeGenericTest.cpp
    
    component/engine/VolumeFromTrianglesTest.cpp
    component/engine/VolumeFromTetrahedronsTest.cpp
    )

add_executable(${PROJECT_NAME} ${SOURCE_FILES} ${RC_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC "${SoftRobots_INCLUDE_DIRS}")

target_link_libraries(${PROJECT_NAME} SofaTest SofaGTestMain SoftRobots SofaCore SofaConstraint SofaBaseMechanics SofaUserInteraction SofaComponentCommon)
add_definitions("-DSOFTROBOTS_TEST_DIR=\"${CMAKE_CURRENT_SOURCE_DIR}/\"")

add_test(NAME ${PROJECT_NAME} COMMAND ${PROJECT_NAME})

