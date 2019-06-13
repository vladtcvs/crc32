project(crc32 C)
cmake_minimum_required(VERSION 3.13)

set(DEST_DIR "${CMAKE_INSTALL_PREFIX}")


foreach(LIB ${COMMA_SEAPARATED_LIST})
  set(PRIVATE_LIBS "${PRIVATE_LIBS} -l${LIB}")
endforeach()
CONFIGURE_FILE("crc32.pc.in" "crc32.pc" @ONLY)

add_library(crc32 STATIC src/crc32.c)
target_include_directories(crc32 PUBLIC include)

install(TARGETS crc32 ARCHIVE DESTINATION lib)
install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/
	DESTINATION include/crc
	FILES_MATCHING PATTERN "*.h")

install(FILES ${CMAKE_BINARY_DIR}/crc32.pc
	DESTINATION lib/pkgconfig)
