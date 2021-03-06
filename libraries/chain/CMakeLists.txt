link_directories("${PROJECT_SOURCE_DIR}/libraries/chain/lib")

file(GLOB HEADERS "include/graphene/chain/*.hpp")
file(GLOB PROTOCOL_HEADERS "include/graphene/chain/protocol/*.hpp")

if(APPLE)
    file(GLOB GRAPHENE_CHAIN_LIB "lib/libgraphene_chain.dylib")
    FILE (COPY ${GRAPHENE_CHAIN_LIB} DESTINATION ${CMAKE_BINARY_DIR}/libraries/chain)
elseif(CMAKE_SYSTEM_NAME MATCHES "Linux")
    FILE (COPY lib/libgraphene_chain.tar.gz DESTINATION ${CMAKE_BINARY_DIR}/libraries/chain)
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar zxvf libgraphene_chain.tar.gz
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/libraries/chain
        )
endif()

INSTALL(FILES ${HEADERS} DESTINATION "include/graphene/chain")
INSTALL(FILES ${PROTOCOL_HEADERS} DESTINATION "include/graphene/chain/protocol")
