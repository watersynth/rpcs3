if (USE_SYSTEM_ZLIB)
	message(STATUS "RPCS3: Using system ZLIB")
	find_package(ZLIB QUIET)

	add_library(3rdparty_zlib INTERFACE)
	target_link_libraries(3rdparty_zlib INTERFACE ${ZLIB_LIBRARIES})
	target_include_directories(3rdparty_zlib INTERFACE ${ZLIB_INCLUDE_DIRS})
	target_compile_definitions(3rdparty_zlib INTERFACE -DZLIB_CONST=1)
else()
	message(STATUS "RPCS3: Using builtin ZLIB")
	set(SKIP_INSTALL_ALL ON)
	add_subdirectory(zlib EXCLUDE_FROM_ALL)

	add_library(3rdparty_zlib INTERFACE)
	target_link_libraries(3rdparty_zlib INTERFACE zlibstatic)
	target_include_directories(3rdparty_zlib INTERFACE zlib ${CMAKE_CURRENT_BINARY_DIR}/zlib)
	target_compile_definitions(3rdparty_zlib INTERFACE -DZLIB_CONST=1)
endif()
