project(CalcLib)

set(HEADER_FILES test_mod.h)

set(SOURCE_FILES test_mod.cpp)

add_library(CalcLib STATIC ${SOURCE_FILES} ${HEADER_FILES})
