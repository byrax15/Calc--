project(test)

add_executable(test test.cpp)

target_link_libraries(test CalcLib)

target_link_libraries(test gtest gtest_main)