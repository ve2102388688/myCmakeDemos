# cmake的最低版本号，注意VERSION需要大写
cmake_minimum_required(VERSION 2.8)

# 工程名
project(Demo3)

# 编译其他目录下的文件，如math
add_subdirectory(math)

# 编译当前目录下的文件
add_executable(Demo main.cc)

# 把其他目录下的静态、动态库链接进来
target_link_libraries(Demo mathfun)