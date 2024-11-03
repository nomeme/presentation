
set(ENCODE_URL "https://github.com/nomeme/presentation")

add_custom_target(qrencode
    COMMAND qrencode -o ${CMAKE_CURRENT_BINARY_DIR}/qr.svg -t SVG ${ENCODE_URL}
    COMMENT "Encode url ${ENCODE_URL}."
)

add_dependencies(presentation
    qrencode
)
