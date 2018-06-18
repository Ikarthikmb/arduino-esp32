file(GLOB core_srcs
  libraries/*/src/*.c
  libraries/*/src/*.cpp
  cores/esp32/*.c
  cores/esp32/*.cpp
  cores/esp32/libb64/*.c
  )

# Note: we set COMPONENT_SRCS not COMPONENT_SRCDIRS here because
# not all of libraries/*/src contain source files, some are
# header-only...
set(COMPONENT_SRCS cores/esp32/ cores/esp32/libb64 ${core_srcs})

file(GLOB core_lib_dirs LIST_DIRECTORIES true
  libraries/*/src/)

set(COMPONENT_ADD_INCLUDEDIRS cores/esp32 variants/esp32 ${core_lib_dirs})
set(COMPONENT_PRIV_INCLUDEDIRS cores/esp32/libb64)

set(COMPONENT_REQUIRES spi_flash mbedtls mdns ethernet)
set(COMPONENT_PRIV_REQUIRES fatfs nvs_flash app_update spiffs bootloader_support)

register_component()

