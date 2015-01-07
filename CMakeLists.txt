##########################################################################
#  Copyright (c) 2009-2012 Organic Vectory B.V.
#  Written by George van Venrooij
#
#  Contributions by:   
#      Fredrik Orderud (https://sourceforge.net/users/fredrior/)
#      Ian Cullinan    (https://sourceforge.net/users/cibyr/)
#
#  Distributed under the Boost Software License, Version 1.0.
#  (See accompanying file license.txt)
##########################################################################

cmake_minimum_required(VERSION 2.8)

project(clcc)

set(CLCC_VERSION_MAJOR	0)
set(CLCC_VERSION_MINOR	3)
set(CLCC_VERSION_PATCH	0)
set(CLCC_VERSION_BUILD	0)	#	Undetermined, set by subversion (if present)

find_package(Subversion)

if (Subversion_FOUND)
	Subversion_WC_INFO(${PROJECT_SOURCE_DIR} clcc)
	set(CLCC_VERSION_BUILD	${clcc_WC_REVISION})
endif()

if (WIN32)
	set(CLCC_PLATFORM	win32)    
endif()

if (APPLE)
	set(CLCC_PLATFORM	macosx)    
endif()

if (UNIX)
	if (NOT CLCC_PLATFORM)
		set(CLCC_PLATFORM	unix)
	endif()
endif()

enable_testing()

add_subdirectory(src)
add_subdirectory(doc)

#	Packaging instructions
set (CPACK_GENERATOR ZIP TGZ TBZ2)
set (CPACK_PACKAGE_VERSION_MAJOR "${CLCC_VERSION_MAJOR}")
set (CPACK_PACKAGE_VERSION_MINOR "${CLCC_VERSION_MINOR}")
set (CPACK_PACKAGE_VERSION_PATCH "${CLCC_VERSION_PATCH}")
set (CPACK_INCLUDE_TOPLEVEL_DIRECTORY 0)
set	(CPACK_COMPONENTS_ALL runtime documentation)

set (CPACK_PACKAGE_FILE_NAME ${CMAKE_PROJECT_NAME}-${CLCC_VERSION_MAJOR}.${CLCC_VERSION_MINOR}.${CLCC_VERSION_PATCH}-${CLCC_VERSION_BUILD}-${CLCC_PLATFORM})

include (CPack)
