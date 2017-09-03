

SET(CMAKE_BUILD_TYPE "Debug") 

SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
add_executable(testlib main.c)
add_library(hello SHARED IMPORTED)
set_target_properties(hello PROPERTIES IMPORTED_LOCATION  
                    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/libhello.so)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../inc)
target_link_libraries(testlib hello)

#首先在CMakeLists.txt下加入
#设置为调试模式
#SET(CMAKE_BUILD_TYPE "Debug") 
#在下面加入：
#SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
#SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
#原因是CMake 中有一个变量 CMAKE_BUILD_TYPE ,可以的取值是 Debug Release RelWithDebInfo >和 MinSizeRel。
#当这个变量值为 Debug 的时候,CMake 会使用变量 CMAKE_CXX_FLAGS_DEBUG 和 CMAKE_C_FLAGS_DEBUG 中的字符串作为编译选项生成 Makefile;
#cmake  -DCMAKE_BUILD_TYPE=Debug    (源文件路径) 设置为调试模式
