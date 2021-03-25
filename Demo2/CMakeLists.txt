cmake_minimum_required(VERSION 2.8)

# 工程名
project(Demo2)

# method 1
# 使用aux_source_directory将指定路径下的源文件全部绑定到DIR_SRC，这样编译直接用这个宏就好啦
aux_source_directory(. DIR_SRC)
add_executable(Demo ${DIR_SRC})

# method 2
# 将所有的源文件依次列出来
# add_executable(Demo main.cc MathFunctions.cc)