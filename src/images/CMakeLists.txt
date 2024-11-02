file(GLOB IMAGE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.jpg)

foreach(file ${IMAGE_FILES})
    get_filename_component(file_name ${file} NAME)
    set(out_file ${CMAKE_CURRENT_BINARY_DIR}/${file_name})
    configure_file(
        ${file}
        ${out_file}
        COPYONLY
    )
endforeach(file ${IMAGE_FILES})
