cmake_minimum_required(VERSION 3.0.0)
project(matplotlib-cpp VERSION 0.1.0)

include(CTest)
enable_testing()

add_executable(minimal examples/minimal.cpp)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

execute_process(COMMAND python -c "import numpy as np; print(np.get_include())," OUTPUT_VARIABLE NUMPY_INCLUDE_DIRS OUTPUT_STRIP_TRAILING_WHITESPACE)
message("numpy include dirs: " ${NUMPY_INCLUDE_DIRS})

find_package(PythonLibs 2.7)
target_include_directories(minimal PRIVATE 
    ${PYTHON_INCLUDE_DIRS}
    ${NUMPY_INCLUDE_DIRS}
    )
target_link_libraries(minimal ${PYTHON_LIBRARIES})
