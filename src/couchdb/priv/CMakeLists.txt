SET(COUCH_PRIV_PREFIX ${COUCH_LIB_DIR}/priv)
SET(COUCH_PRIV_LIB_PREFIX ${COUCH_PRIV_PREFIX}/lib)

SET(COUCH_ICU_SRC icu_driver/couch_icu_driver.c)

ADD_LIBRARY(couch_icu_driver MODULE ${COUCH_ICU_SRC})

SET_TARGET_PROPERTIES(couch_icu_driver PROPERTIES COMPILE_FLAGS "-I. -I../.. -I${SNAPPY_INCLUDE_DIR} -I${V8_INCLUDE_DIR} -I/opt/local/include  -I/opt/local/include -I${CMAKE_INSTALL_PREFIX}/lib/erlang/usr/include ${ERLANG_INCLUDE_PATH} -DV8_POST_3_19_API -I${ICU_INCLUDE_DIR} -DXP_UNIX")

TARGET_LINK_LIBRARIES(couch_icu_driver "-Wl,-undefined -Wl,dynamic_lookup -lv8 -lsnappy -lm -L/usr/local/lib -L${ICU_LIB_DIR} -licuuc -licudata -licui18n")

SET(COUCH_EJSON_COMPARE_SRC couch_ejson_compare/couch_ejson_compare.c
                            couch_ejson_compare/couch_raw_json_compare.c
                            couch_ejson_compare/couch_ejson_compare_utils.c)

ADD_LIBRARY(couch_ejson_compare MODULE ${COUCH_EJSON_COMPARE_SRC})

SET_TARGET_PROPERTIES(couch_ejson_compare PROPERTIES COMPILE_FLAGS "-I. -I../.. -I${SNAPPY_INCLUDE_DIR} -I${V8_INCLUDE_DIR} -I/opt/local/include  -I/opt/local/include -I${CMAKE_INSTALL_PREFIX}/lib/erlang/usr/include ${ERLANG_INCLUDE_PATH} -DV8_POST_3_19_API -I${ICU_INCLUDE_DIR}")

TARGET_LINK_LIBRARIES(couch_ejson_compare "-Wl,-undefined -Wl,dynamic_lookup -lv8 -lsnappy -lm -L/usr/local/lib -L${ICU_LIB_DIR} -licuuc -licudata -licui18n")

INSTALL(TARGETS couch_icu_driver couch_ejson_compare
        DESTINATION ${COUCH_PRIV_LIB_PREFIX})
