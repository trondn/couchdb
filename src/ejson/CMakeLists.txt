FILE(GLOB SRC *.erl)
SET(EJSON_VERSION "0.1.0")
SET(EJSON_PREFIX ${CMAKE_ERL_LIB_INSTALL_PREFIX}/ejson-${EJSON_VERSION})
SET(EJSON_EBIN_PREFIX ${EJSON_PREFIX}/ebin)
SET(EJSON_PRIV_PREFIX ${EJSON_PREFIX}/priv)

SET(EJSON_SRC ejson.c
              decode.c
              encode.c
              yajl/yajl_alloc.c
              yajl/yajl_buf.c
              yajl/yajl.c
              yajl/yajl_encode.c
              yajl/yajl_gen.c
              yajl/yajl_lex.c
              yajl/yajl_parser.c)

INCLUDE_DIRECTORIES(BEFORE ${CMAKE_CURRENT_SOURCE_DIR}
                           ${CMAKE_CURRENT_SOURCE_DIR}/yajl
                           ${CMAKE_CURRENT_SOURCE_DIR}/../..
                           ${SNAPPY_INCLUDE_DIR}
                           ${V8_INCLUDE_DIR}
                           ${CMAKE_INSTALL_PREFIX}/lib/erlang/usr/include
                           ${ERLANG_INCLUDE_PATH})

ADD_LIBRARY(ejson MODULE ${EJSON_SRC})

TARGET_LINK_LIBRARIES(ejson ${V8_LIBRARIES} ${SNAPPY_LIBRARIES} ${COUCHBASE_MATH_LIBS})
ERL_BUILD("ejson_build" ${SRC})

INSTALL(TARGETS ejson
        DESTINATION ${EJSON_PRIV_PREFIX})
INSTALL(FILES ${outfiles}
        DESTINATION ${EJSON_EBIN_PREFIX})
