# cmake语法关键字--大/小写无关
# cmake的最低版本号，注意VERSION需要大写
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

# 设置一个工程名字
project(Demo1)

# 目标可执行程序Demo， 需要编译main.cc
add_executable(Demo main.cc)