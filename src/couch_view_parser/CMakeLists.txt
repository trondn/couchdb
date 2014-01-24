FILE(GLOB SRC *.erl)
SET(COUCH_VIEW_PARSER_VERSION "1.0")
SET(COUCH_VIEW_PARSER_PREFIX ${CMAKE_ERL_LIB_INSTALL_PREFIX}/couch_view_parser-${COUCH_VIEW_PARSER_VERSION})
SET(COUCH_VIEW_PARSER_EBIN_PREFIX ${COUCH_VIEW_PARSER_PREFIX}/ebin)
SET(COUCH_VIEW_PARSER_PRIV_PREFIX ${COUCH_VIEW_PARSER_PREFIX}/priv)

SET(COUCH_VIEW_YAJL_SRC couch_view_parser.cc
    couch_view_parser_nif.cc
    yajl/yajl.c
    yajl/yajl_alloc.c
    yajl/yajl_buf.c
    yajl/yajl_encode.c
    yajl/yajl_gen.c
    yajl/yajl_lex.c
    yajl/yajl_parser.c
    yajl/yajl_tree.c
    yajl/yajl_version.c)

INCLUDE_DIRECTORIES(BEFORE ${CMAKE_CURRENT_SOURCE_DIR}
                           ${CMAKE_CURRENT_SOURCE_DIR}/yajl
                           ${CMAKE_CURRENT_SOURCE_DIR}/../..
                           ${SNAPPY_INCLUDE_DIR}
                           ${V8_INCLUDE_DIR}
                           ${CMAKE_INSTALL_PREFIX}/lib/erlang/usr/include
                           ${ERLANG_INCLUDE_PATH})



ADD_LIBRARY(couch_view_parser_nif MODULE ${COUCH_VIEW_YAJL_SRC})

TARGET_LINK_LIBRARIES(couch_view_parser_nif ${V8_LIBRARIES} ${SNAPPY_LIBRARIES} ${COUCHBASE_MATH_LIBS})
ERL_BUILD("couch_view_parser" ${SRC})

INSTALL(TARGETS couch_view_parser_nif
        DESTINATION ${COUCH_VIEW_PARSER_PRIV_PREFIX})
INSTALL(FILES ${outfiles}
        DESTINATION ${COUCH_VIEW_PARSER_EBIN_PREFIX})
