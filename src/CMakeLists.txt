cmake_minimum_required(VERSION 3.5)
project(rastertoricohpjl)

set (CUPS_SRC_DIR ${SRC_DIR}/cups-2.1.1)
set (UNICODE_SRC_DIR ${SRC_DIR}/unicode)

find_program(CUPS_CONFIG NAMES cups-config REQUIRED)
function(cups_config_opt VAR OPT)
    execute_process(
        COMMAND "${CUPS_CONFIG}" ${OPT}
        OUTPUT_VARIABLE out
        OUTPUT_STRIP_TRAILING_WHITESPACE
    )
    set(${VAR} ${out} PARENT_SCOPE)
endfunction()

if(NOT CUPS_SERVER_BIN)
    cups_config_opt(CUPS_SERVER_BIN --serverbin)
endif()
if(NOT CUPS_DATA_DIR)
    cups_config_opt(CUPS_DATA_DIR --datadir)
endif()

find_library(CUPS_LIB cups)
find_library(CUPSIMAGE_LIB cupsimage)

include_directories(${CUPS_SRC_DIR})

set(SOURCES
	rastertoricohpjl.c
	libjbig/jbig.c
	libjbig/jbig_ar.c
)

add_executable(rastertoricohpjl ${SOURCES})
target_link_libraries(rastertoricohpjl ${CUPS_LIB} ${CUPSIMAGE_LIB})
# Install binary
install(TARGETS rastertoricohpjl DESTINATION "${CUPS_SERVER_BIN}/filter")
# Install PPD
install(FILES ../RICOH_Aficio_SP_100SU.ppd DESTINATION "${CUPS_DATA_DIR}/model")
