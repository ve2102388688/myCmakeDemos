# 将math下的所有源文件都编译成静态库
aux_source_directory(. MATH_DIR_SRC)

add_library(mathfun ${MATH_DIR_SRC})

# # 指定库的安装路径
# # Installing Targets
# install(TARGETS mathfun DESTINATION bin)
# # Installing Files
# install(FILES MathFunctions.h DESTINATION include)
