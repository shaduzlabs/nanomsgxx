
        ##########    Copyright (C) 2015 Vincenzo Pacella
        ##      ##    Distributed under MIT license, see file LICENSE
        ##      ##    or <http://opensource.org/licenses/MIT>
        ##      ##
##########      ############################################################# shaduzlabs.com #######

cmake_minimum_required (VERSION 2.8.0)

project (nanomsgxx)
set(NANOMSGXX_ROOT_DIR ${CMAKE_CURRENT_LIST_DIR})

if(${CMAKE_PROJECT_NAME} STREQUAL ${PROJECT_NAME})
  set(IS_NANOMSGXX ON)
else()
  set(IS_NANOMSGXX OFF)
endif()

if(IS_NANOMSGXX)
  list(APPEND CMAKE_MODULE_PATH "${NANOMSGXX_ROOT_DIR}/cmake")
  find_package(nanomsg REQUIRED)
endif()

set(LIBRARY_FILE_NAME     "nanomsgxx")
set(DEBUG_SUFFIX          "d")

set(
 inc_nanomsg_ext_SRCS
   inc/nanomsg/ext/nnxx_ext.h
)

set(
  inc_nnxx_SRCS
    inc/nnxx/bus.h
    inc/nnxx/chrono.h
    inc/nnxx/error.h
    inc/nnxx/inproc.h
    inc/nnxx/ipc.h
    inc/nnxx/message_control.h
    inc/nnxx/message_istream.h
    inc/nnxx/message_istream.hpp
    inc/nnxx/message_iterator.h
    inc/nnxx/message_ostream.h
    inc/nnxx/message_ostream.hpp
    inc/nnxx/message_streambuf.h
    inc/nnxx/message_streambuf.hpp
    inc/nnxx/message.h
    inc/nnxx/nn.h
    inc/nnxx/pair.h
    inc/nnxx/pipeline.h
    inc/nnxx/poll.h
    inc/nnxx/pubsub.h
    inc/nnxx/reqrep.h
    inc/nnxx/socket.h
    inc/nnxx/socket.hpp
    inc/nnxx/survey.h
    inc/nnxx/tcp.h
    inc/nnxx/timeout.h
)

source_group( "inc\\ext"     FILES ${inc_nanomsg_ext_SRCS} )
source_group( "inc\\nnxx"    FILES ${inc_nnxx_SRCS} )

set(
 nanomsgxx_INCLUDES
   ${inc_nanomsg_ext_SRCS}
   ${inc_nnxx_SRCS}
)

set(
 src_nanomsg_ext_SRCS
   src/nanomsg/ext/nnxx_ext.c
)

set(
 src_nnxx_SRCS
   src/nnxx/error.cpp
   src/nnxx/message_control.cpp
   src/nnxx/message_istream.cpp
   src/nnxx/message_iterator.cpp
   src/nnxx/message_ostream.cpp
   src/nnxx/message_streambuf.cpp
   src/nnxx/message.cpp
   src/nnxx/nn.cpp
   src/nnxx/poll.cpp
   src/nnxx/pubsub.cpp
   src/nnxx/reqrep.cpp
   src/nnxx/socket.cpp
   src/nnxx/survey.cpp
   src/nnxx/tcp.cpp
   src/nnxx/timeout.cpp
 )

 source_group( "src\\ext"     FILES ${src_nanomsg_ext_SRCS} )
 source_group( "src\\nnxx"    FILES ${src_nnxx_SRCS} )

 set(
  nanomsgxx_SRCS
    ${src_nanomsg_ext_SRCS}
    ${src_nnxx_SRCS}
)

set(
  nanomsg_ALL
    ${nanomsgxx_INCLUDES}
    ${nanomsgxx_SRCS}
)

add_library( nanomsgxx STATIC ${nanomsg_ALL} )
set_target_properties(
  ${PROJECT_NAME}
  PROPERTIES
    OUTPUT_NAME         "${LIBRARY_FILE_NAME}"
    OUTPUT_NAME_DEBUG   "${LIBRARY_FILE_NAME}${DEBUG_SUFFIX}"
)
target_compile_features(${PROJECT_NAME} PRIVATE cxx_noexcept)
target_include_directories( ${PROJECT_NAME} PUBLIC inc )
