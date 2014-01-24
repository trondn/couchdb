FILE(GLOB SRC src/*.erl)
INCLUDE_ERDIR(${CMAKE_CURRENT_SOURCE_DIR}/../../src)
INCLUDE_ERDIR(${CMAKE_CURRENT_SOURCE_DIR}/../../src/couchdb)

ERL_BUILD("couch_index_merger" ${SRC})
SET(COUCH_INDEX_MERGER_PREFIX ${CMAKE_ERL_LIB_INSTALL_PREFIX}/couch_index_merger-1.0.0)

SET(COUCH_INDEX_MERGER_INCLUDE_FILES include/couch_index_merger.hrl
                                     include/couch_view_merger.hrl)

INSTALL(FILES ${COUCH_INDEX_MERGER_INCLUDE_FILES}
       DESTINATION ${COUCH_INDEX_MERGER_PREFIX}/include)

INSTALL(FILES ${outfiles}
    DESTINATION ${COUCH_INDEX_MERGER_PREFIX}/ebin)
