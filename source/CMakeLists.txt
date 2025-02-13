################################################################
cmake_minimum_required(VERSION 3.25)
################################################################
set(LIBRARY_NAME "base64")
set(LIBRARY_DESC "Library with Base64 encoder/decoder")

project(libict-${LIBRARY_NAME})

set(CMAKE_CXX_STANDARD 17)
find_package(Threads)

include(../libict-dev-tools/libs-include.cmake)
include(../libict-dev-tools/info-include.cmake)
include(../libict-dev-tools/test-include.cmake)
include(../libict-dev-tools/git-include.cmake)

file(GLOB CMAKE_HEADER_LIST . *.hpp)

set(CMAKE_SOURCE_FILES 
  info.cpp
  robot.cpp
  get.cpp
)

add_library(ict-static-${LIBRARY_NAME} STATIC ${CMAKE_SOURCE_FILES})
target_link_libraries(ict-static-${LIBRARY_NAME} ${CMAKE_THREAD_LIBS_INIT})
target_link_libraries(ict-static-${LIBRARY_NAME} ${CMAKE_LINK_LIBS})
set_target_properties(ict-static-${LIBRARY_NAME}  PROPERTIES OUTPUT_NAME ict-${LIBRARY_NAME})

add_library(ict-shared-${LIBRARY_NAME} SHARED ${CMAKE_SOURCE_FILES})
target_link_libraries(ict-shared-${LIBRARY_NAME} ${CMAKE_THREAD_LIBS_INIT})
target_link_libraries(ict-shared-${LIBRARY_NAME} ${CMAKE_LINK_LIBS})
set_target_properties(ict-shared-${LIBRARY_NAME}  PROPERTIES OUTPUT_NAME ict-${LIBRARY_NAME})

add_executable(${PROJECT_NAME}-test test.cpp ${CMAKE_SOURCE_FILES})
target_link_libraries(${PROJECT_NAME}-test ${CMAKE_THREAD_LIBS_INIT})
target_link_libraries(${PROJECT_NAME}-test ${CMAKE_LINK_LIBS})
target_compile_definitions(${PROJECT_NAME}-test PUBLIC -DENABLE_TESTING)

################################################################
install(TARGETS ict-static-${LIBRARY_NAME} ict-shared-${LIBRARY_NAME} DESTINATION lib COMPONENT libraries)
install(
  FILES ${HEADER_LIST}
  DESTINATION include/libict/${LIBRARY_NAME} COMPONENT headers
)
################################################################
enable_testing()

add_test(NAME ict-base64-tc1 COMMAND ${PROJECT_NAME}-test ict base64 tc1)
add_test(NAME ict-base64-tc2 COMMAND ${PROJECT_NAME}-test ict base64 tc2)
add_test(NAME ict-base64-tc3 COMMAND ${PROJECT_NAME}-test ict base64 tc3)
add_test(NAME ict-base64-tc4 COMMAND ${PROJECT_NAME}-test ict base64 tc4)
add_test(NAME ict-base64-tc5 COMMAND ${PROJECT_NAME}-test ict base64 tc5)
add_test(NAME ict-base64-tc6 COMMAND ${PROJECT_NAME}-test ict base64 tc6)
add_test(NAME ict-base64-tc7 COMMAND ${PROJECT_NAME}-test ict base64 tc7)
add_test(NAME ict-base64-tc8 COMMAND ${PROJECT_NAME}-test ict base64 tc8)
add_test(NAME ict-base64-tc9 COMMAND ${PROJECT_NAME}-test ict base64 tc9)
add_test(NAME ict-base64-tc10 COMMAND ${PROJECT_NAME}-test ict base64 tc10)
add_test(NAME ict-base64-tc11 COMMAND ${PROJECT_NAME}-test ict base64 tc11)
add_test(NAME ict-base64-tc12 COMMAND ${PROJECT_NAME}-test ict base64 tc12)

################################################################
include(../libict-dev-tools/cpack-include.cmake)
################################################################