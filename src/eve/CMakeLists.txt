include(GenerateExportHeader)
add_library(eve STATIC Eve2_81x.c ST7789V.c)
add_library(evedll SHARED Eve2_81x.c ST7789V.c)
set_target_properties(eve PROPERTIES OUTPUT_NAME "eve_static")
set_target_properties(evedll PROPERTIES OUTPUT_NAME "eve")
target_compile_options(eve PUBLIC -DEVE_STATIC_DEFINE )
target_compile_options(evedll PUBLIC -DEVE_MO_INTERNAL_BUILD )
target_include_directories(eve PUBLIC "${CMAKE_SOURCE_DIR}/Include/eve")
target_include_directories(evedll PUBLIC "${CMAKE_SOURCE_DIR}/Include/eve")
target_link_libraries(eve PUBLIC usb_bridge)
target_link_libraries(evedll PUBLIC usb_bridge)
target_include_directories(eve PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
target_include_directories(evedll PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
generate_export_header(evedll BASE_NAME EVE NO_DEPRECATED_MACRO_NAME )
install(FILES Eve2_81x.c DESTINATION ./EVE2-Library)
install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/eve/ DESTINATION ./EVE2-Library FILES_MATCHING PATTERN "*.h")
install(TARGETS evedll DESTINATION ./bin)