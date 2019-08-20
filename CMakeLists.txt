cmake_minimum_required(VERSION 3.8)
project(slv)

set(CMAKE_CXX_STANDARD 17)

SET(OPTIMIZE_FLAGS "-O2")
# SET(GCC_COVERAGE_COMPILE_FLAGS "-fprofile-arcs -ftest-coverage")
# SET(GCC_COVERAGE_LINK_FLAGS    "-lgcov")

SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} ${OPTIMIZE_FLAGS}")
SET(CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS} -L /usr/local/lib/")


set(Boost_USE_STATIC_LIBS OFF)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)
find_package(Boost 1.65.1 COMPONENTS thread)
if(Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
endif()


add_executable(sah SemiAnalyticHeston.cpp)
target_link_libraries(sah ${Boost_LIBRARIES} QuantLib)

add_executable(mc MC.cpp)
target_link_libraries(mc ${Boost_LIBRARIES} QuantLib)

add_executable(fd FD.cpp)
target_link_libraries(fd ${Boost_LIBRARIES} QuantLib)