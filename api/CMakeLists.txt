# 添加 API 源文件
file(GLOB API_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/*.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/*.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/*.hpp"
)

add_library(quant1x-api STATIC ${API_SRC})

# 公共头文件目录
target_include_directories(quant1x-api PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include/quant1x/api>
)

# 依赖第三方库（如有）
target_link_libraries(quant1x-api PUBLIC quant1x-base)

# 可选：编译选项
# target_compile_options(quant1x_api PRIVATE ...)

# 安装 API 头文件到 std 的 include 目录
install(
    DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
    DESTINATION include/quant1x/api
    FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
)
