enable_testing()

add_executable(cpprealm-tests 
    tests.cpp 
    str_tests.cpp 
    list_tests.cpp 
    query_tests.cpp 
    test_utils.hpp
    test_objects.hpp
    test_utils.cpp
)

target_link_libraries(cpprealm-tests cpprealm)
add_test(NAME Tests COMMAND cpprealm-tests)
