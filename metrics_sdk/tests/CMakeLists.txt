include_directories(${METRICS_SDK_TOP_DIR}/src)

add_library(metrics_sdk_testing STATIC
        ${METRICS_SDK_SOURCE})

file(GLOB_RECURSE METRICS_SDK_TEST_SRC_FILES ${CMAKE_CURRENT_SOURCE_DIR} *.cpp)

set(METRICS_SDK_TESTS_DEPENDENT_LIBS
        pthread
        CACHE INTERNAL "Dependeent libraries")


foreach(_test_file ${METRICS_SDK_TEST_SRC_FILES})
    get_filename_component(_test_name ${_test_file} NAME_WE)
    add_executable(${_test_name} ${_test_file})
    target_link_libraries(${_test_name} metrics_sdk_testing ${METRICS_SDK_TESTS_DEPENDENT_LIBS})
    add_test(${_test_name} ${_test_name})
    set_tests_properties(${_test_name} PROPERTIES TIMEOUT 5)
endforeach()
