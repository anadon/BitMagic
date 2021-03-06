cmake_minimum_required(VERSION 2.8)

project(bm)


set( CMAKE_VERBOSE_MAKEFILE on )

# SET(BMOPTFLAGS "BMSSE42OPT" CACHE STRING "User-specified optimization flag")

set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build/bin)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

include_directories("${PROJECT_SOURCE_DIR}/src")

set (CMAKE_CXX_STANDARD 11)

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU" OR
    "${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")

    if ("${BMOPTFLAGS}" STREQUAL "BMSSE42OPT")
	    set(bmoptf "-march=nehalem -O2 -msse4.2 -DBMSSE42OPT")
    elseif("${BMOPTFLAGS}" STREQUAL "BMAVX2OPT")
        set(bmoptf "-march=skylake -mavx2 -O2 -DBMAVX2OPT")
    else()
        set(bmoptf "-march=core2")
    endif()

    set(flags "-Wall -Wextra -Wno-ignored-qualifiers -march=core2 -fPIC")
    set(optflags -g0 -O3)
    SET( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} -Wl,-stack_size,0x100000000")

elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Intel")
    set(flags, "-tpp7 -march=core2 -restrict -DBM_HASRESTRICT -fno-fnalias -Wall")
    set(optflags, "-g0 -O3 -opt_report_fileopt.txt -opt_report_levelmax")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")

    if ("${BMOPTFLAGS}" STREQUAL "BMSSE42OPT")
	set(bmoptf "-DBMSSE42OPT")
    elseif("${BMOPTFLAGS}" STREQUAL "BMAVX2OPT")
        set(bmoptf "-DBMAVX2OPT") 
    endif()

    set(flags "/W4 /EHsc /F 5000000 ")
    set(optflags "-O2")
    SET( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} /STACK:\"10000000\"")
endif()

set(CMAKE_C_FLAGS   "${CMAKE_C_FLAGS} ${flags} ${bmoptf}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${flags} ${bmoptf}")

add_executable(bmsvutil ${PROJECT_SOURCE_DIR}/utils/svutil/svutil.cpp)

add_executable(bmtest ${PROJECT_SOURCE_DIR}/tests/stress/t.cpp)
add_executable(bmtest64 ${PROJECT_SOURCE_DIR}/tests/stress64/t64.cpp)
add_executable(bmperf ${PROJECT_SOURCE_DIR}/tests/perf/perf.cpp)
add_executable(bmperf64 ${PROJECT_SOURCE_DIR}/tests/perf64/perf64.cpp)
add_executable(bmlnkutil ${PROJECT_SOURCE_DIR}/utils/lnkutil/lnkutil.cpp)
add_executable(bminv ${PROJECT_SOURCE_DIR}/utils/inv_list/inv_list.cpp)

add_executable(bvsample01 ${PROJECT_SOURCE_DIR}/samples/bvsample01/sample1.cpp)
add_executable(bvsample02 ${PROJECT_SOURCE_DIR}/samples/bvsample02/sample2.cpp)
add_executable(bvsample03 ${PROJECT_SOURCE_DIR}/samples/bvsample03/sample3.cpp)
add_executable(bvsample04 ${PROJECT_SOURCE_DIR}/samples/bvsample04/sample4.cpp)
add_executable(bvsample05 ${PROJECT_SOURCE_DIR}/samples/bvsample05/sample5.cpp)
add_executable(bvsample06 ${PROJECT_SOURCE_DIR}/samples/bvsample06/sample6.cpp)
add_executable(bvsample07 ${PROJECT_SOURCE_DIR}/samples/bvsample07/sample7.cpp)
add_executable(bvsample08 ${PROJECT_SOURCE_DIR}/samples/bvsample08/sample8.cpp)
add_executable(bvsample09 ${PROJECT_SOURCE_DIR}/samples/bvsample09/sample9.cpp)
add_executable(bvsample10 ${PROJECT_SOURCE_DIR}/samples/bvsample10/sample10.cpp)
add_executable(bvsample11 ${PROJECT_SOURCE_DIR}/samples/bvsample11/sample11.cpp)
add_executable(bvsample12 ${PROJECT_SOURCE_DIR}/samples/bvsample12/sample12.cpp)
add_executable(bvsample14 ${PROJECT_SOURCE_DIR}/samples/bvsample14/sample14.cpp)
add_executable(bvsample15 ${PROJECT_SOURCE_DIR}/samples/bvsample15/sample15.cpp)
add_executable(bvsample16 ${PROJECT_SOURCE_DIR}/samples/bvsample16/sample16.cpp)
add_executable(bvsample17 ${PROJECT_SOURCE_DIR}/samples/bvsample17/sample17.cpp)
add_executable(bvsample18 ${PROJECT_SOURCE_DIR}/samples/bvsample18/sample18.cpp)
add_executable(bvsample19 ${PROJECT_SOURCE_DIR}/samples/bvsample19/sample19.cpp)
add_executable(bvsample20 ${PROJECT_SOURCE_DIR}/samples/bvsample20/sample20.cpp)
add_executable(bvsample21 ${PROJECT_SOURCE_DIR}/samples/bvsample21/sample21.cpp)

add_executable(bvsetalgebra ${PROJECT_SOURCE_DIR}/samples/bvsetalgebra/bvsetalgebra.cpp)

add_executable(bvsample01_64 ${PROJECT_SOURCE_DIR}/samples/bvsample01_64/bvsample01_64.cpp)


add_executable(xsample01 ${PROJECT_SOURCE_DIR}/samples/xsample01/xsample01.cpp)
add_executable(xsample02 ${PROJECT_SOURCE_DIR}/samples/xsample02/xsample02.cpp)
add_executable(xsample03 ${PROJECT_SOURCE_DIR}/samples/xsample03/xsample03.cpp)
add_executable(xsample04 ${PROJECT_SOURCE_DIR}/samples/xsample04/xsample04.cpp)
add_executable(xsample04a ${PROJECT_SOURCE_DIR}/samples/xsample04a/xsample04a.cpp)
add_executable(xsample05 ${PROJECT_SOURCE_DIR}/samples/xsample05/xsample05.cpp)
add_executable(xsample06 ${PROJECT_SOURCE_DIR}/samples/xsample06/xsample06.cpp)

add_executable(svsample01 ${PROJECT_SOURCE_DIR}/samples/svsample01/svsample01.cpp)
add_executable(svsample02 ${PROJECT_SOURCE_DIR}/samples/svsample02/svsample02.cpp)
add_executable(svsample03 ${PROJECT_SOURCE_DIR}/samples/svsample03/svsample03.cpp)
add_executable(svsample04 ${PROJECT_SOURCE_DIR}/samples/svsample04/svsample04.cpp)
add_executable(svsample05 ${PROJECT_SOURCE_DIR}/samples/svsample05/svsample05.cpp)
add_executable(svsample06 ${PROJECT_SOURCE_DIR}/samples/svsample06/svsample06.cpp)
add_executable(svsample07 ${PROJECT_SOURCE_DIR}/samples/svsample07/svsample07.cpp)
add_executable(svsample08 ${PROJECT_SOURCE_DIR}/samples/svsample08/svsample08.cpp)
add_executable(svsample09 ${PROJECT_SOURCE_DIR}/samples/svsample09/svsample09.cpp)

add_executable(rscsample01 ${PROJECT_SOURCE_DIR}/samples/rscsample01/rscsample01.cpp)
add_executable(rscsample02 ${PROJECT_SOURCE_DIR}/samples/rscsample02/rscsample02.cpp)

add_executable(strsvsample01 ${PROJECT_SOURCE_DIR}/samples/strsvsample01/strsvsample01.cpp)
add_executable(strsvsample02 ${PROJECT_SOURCE_DIR}/samples/strsvsample02/strsvsample02.cpp)
add_executable(strsvsample03 ${PROJECT_SOURCE_DIR}/samples/strsvsample03/strsvsample03.cpp)
add_executable(strsvsample04 ${PROJECT_SOURCE_DIR}/samples/strsvsample04/strsvsample04.cpp)
add_executable(strsvsample05 ${PROJECT_SOURCE_DIR}/samples/strsvsample05/strsvsample05.cpp)


