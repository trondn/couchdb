FILE(GLOB LHTTP_SRC *.erl)
ERL_BUILD("erlang_oauth" ${LHTTP_SRC})
INSTALL(FILES ${outfiles}
    DESTINATION ${CMAKE_ERL_LIB_INSTALL_PREFIX}/erlang-oauth/ebin)

