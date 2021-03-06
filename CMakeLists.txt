cmake_minimum_required (VERSION 2.6)
project (BoostTutorial)
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall")
file (GLOB inputfiles relative ${CMAKE_SOURCE_DIR}/*.cpp)

find_package (Boost COMPONENTS system filesystem program_options REQUIRED)
if (NOT Boost_FOUND)
    message (FATAL_ERROR "Boost not found")
endif()

find_package (Threads REQUIRED)

set (Boost_USE_MULTITHREAD ON)

foreach (filename ${inputfiles})
    string (REPLACE ".cpp" "" outputfile ${filename})
    string (REPLACE "${CMAKE_SOURCE_DIR}/" "" outputfile ${outputfile})
    add_executable ("${outputfile}" "${filename}")
    target_link_libraries ("${outputfile}" ${Boost_LIBRARIES})
    target_link_libraries ("${outputfile}" Threads::Threads)
endforeach(filename ${inputfiles})

