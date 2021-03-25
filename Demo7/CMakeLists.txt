cmake_minimum_required(VERSION 2.8)

# 工程名
project(Demo4)

# 测试系统是否包含相关函数，若没有使用自己函数
# CMAKE_ROOT: /usr/share/cmake-3.10
# 1. 先添加CheckFunctionExists.cmake
include(${CMAKE_ROOT}/Modules/CheckFunctionExists.cmake)
# 2. check_function_exists测试链接器是否可以找到pow，宏名HAVE_POW需要在config.h.in定义
check_function_exists(pow HAVE_POW)


######################### 写一个宏名USE_MATH来启用使用MathFunctions
# 设置编译宏名USE_MYMATH，注解，默认值ON（不管main是否使用MathFunctions，我都编译它）
# 如果设置OFF，在config.h.in不管怎么改，都不会调用
option(USE_MYMATH "use provided math implementation" ON)

# 加入一个配置头文件config.h.in，用于编译选项的设置，注意这个文件必须用户提前建立，否则编译错误--找不到该文件
configure_file(
    "${PROJECT_SOURCE_DIR}/config.h.in"
    "${PROJECT_BINARY_DIR}/config.h"
)
# 是否加入mathfun
if (USE_MYMATH)
    # include_directories("${PROJECT_SOURCE_DIR}/math")
    add_subdirectory(math)                              # 编译其他文件夹的源代码
    set(EXTRA_LIBS mathfun)
endif(USE_MYMATH)


# 编译当前目录下的源文件
aux_source_directory(. DIR_SRC)
add_executable(Demo ${DIR_SRC})

# 链接其他文件夹下的动态、静态库
target_link_libraries(Demo ${EXTRA_LIBS})