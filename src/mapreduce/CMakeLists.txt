FILE(GLOB SRC *.erl)
SET(MR_VERSION "1.0")
SET(MR_PREFIX ${CMAKE_ERL_LIB_INSTALL_PREFIX}/mapreduce-${MR_VERSION})
SET(MR_EBIN_PREFIX ${MR_PREFIX}/ebin)
SET(MR_PRIV_PREFIX ${MR_PREFIX}/priv)

SET(COUCH_VIEW_MR_SRC mapreduce_nif.cc
                      mapreduce.cc)

INCLUDE_DIRECTORIES(BEFORE ${CMAKE_CURRENT_SOURCE_DIR}/../..
                           ${SNAPPY_INCLUDE_DIR}
                           ${V8_INCLUDE_DIR}
                           ${CMAKE_INSTALL_PREFIX}/lib/erlang/usr/include
                           ${ERLANG_INCLUDE_PATH})

ADD_LIBRARY(mapreduce_nif MODULE ${COUCH_VIEW_MR_SRC})

TARGET_LINK_LIBRARIES(mapreduce_nif ${V8_LIBRARIES} ${SNAPPY_LIBRARIES} ${COUCHBASE_MATH_LIBS})

ERL_BUILD("mapreduce" ${SRC})

INSTALL(TARGETS mapreduce_nif
    DESTINATION ${MR_PRIV_PREFIX})
INSTALL(FILES ${outfiles}
        DESTINATION ${MR_EBIN_PREFIX})
