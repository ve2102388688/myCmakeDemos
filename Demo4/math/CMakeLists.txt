# 将math下的所有源文件都编译成静态库
aux_source_directory(. MATH_DIR_SRC)

add_library(mathfun ${MATH_DIR_SRC})