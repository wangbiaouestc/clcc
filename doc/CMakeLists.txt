##########################################################################
#  Copyright (c) 2009-2011 Organic Vectory B.V.
#  Written by George van Venrooij
#
#  Contributions by:   
#      Ian Cullinan    (https://sourceforge.net/users/cibyr/)
#
#  Distributed under the Boost Software License, Version 1.0.
#  (See accompanying file license.txt)
##########################################################################

set(DOXYGEN_SKIP_DOT false)
find_package(Doxygen)

#   (cat clcc.doxygen \; echo DOT_PATH=${DOXYGEN_DOT_EXECUTABLE} )
#   Handle dot tool (perhaps add to path at build-time?)

if (DOXYGEN_FOUND)
    message("${DOXYGEN_EXECUTABLE}" "${PROJECT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}")
    configure_file(clcc.doxygen.cfg ${CMAKE_CURRENT_BINARY_DIR}/clcc.doxygen)
    add_custom_target(clcc_doc "${DOXYGEN_EXECUTABLE}" ${CMAKE_CURRENT_BINARY_DIR}/clcc.doxygen WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR} VERBATIM SOURCES clcc.doxygen.cfg ${CMAKE_CURRENT_BINARY_DIR}/clcc.doxygen)
endif()

#	Installation instructions
install	(	DIRECTORY	${CMAKE_CURRENT_BINARY_DIR}/html	
			DESTINATION	doc
			COMPONENT	documentation
		)
