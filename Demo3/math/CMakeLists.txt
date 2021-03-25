# 将本目录下的所有文件全部编译成静态库
aux_source_directory(. MATH_DIR_SRC)

add_library(mathfun ${MATH_DIR_SRC})