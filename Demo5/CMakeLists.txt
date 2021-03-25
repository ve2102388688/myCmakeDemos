cmake_minimum_required(VERSION 2.8)

# 工程名
project(Demo4)

######################### 写一个宏名USE_MATH来启用使用MathFunctions
# 设置编译宏名USE_MYMATH，注解，默认值ON（不管main是否使用MathFunctions，我都编译它），注意此代码必须在前！！！
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

# # 安装(make isntall)
# # Installing Targets
# install(TARGETS Demo DESTINATION bin)
# # Installing Files
# install(FILES "${PROJECT_BINARY_DIR}/config.h" DESTINATION include)


# 测试(make test)--相同的测试案例会自动忽略
# 使能测试
enable_testing()

# 1号测试
add_test(test_run Demo 5 2)

# 2号测试--帮助信息
add_test(test_usage Demo)
set_tests_properties(test_usage PROPERTIES PASS_REGULAR_EXPRESSION "Usage: .*base exponent")

# 3号测试，结果是25，其他都会失败
add_test(test_5_2 Demo 5 2)
set_tests_properties(test_5_2 PROPERTIES PASS_REGULAR_EXPRESSION "is 25")

# 3号测试，结果是25，其他都会失败
add_test(test_2_10 Demo 2 10)
set_tests_properties(test_2_10 PROPERTIES PASS_REGULAR_EXPRESSION "is 1024")


# 大量测试--定义一个宏，简化测试工作
macro(do_test arg1 arg2 result)
    add_test(test_${arg1}_${arg2} Demo ${arg1} ${arg2})
    set_tests_properties(test_${arg1}_${arg2} PROPERTIES PASS_REGULAR_EXPRESSION ${result}) 
endmacro(do_test)

do_test(5 3 "is 125")
do_test(2 9 "is 512")
do_test(10 5 "is 100000")