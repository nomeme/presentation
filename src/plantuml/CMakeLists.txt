##
# @file This file contains the targets required to
# create images from plantuml sources.
##

message(STATUS "Please make sure wget is installed.")
message(STATUS "This component needs a java runtime.")

set(PLANTUML_BINARY_SOURCE "https://github.com/plantuml/plantuml/releases/download/v1.2024.7/plantuml-1.2024.7.jar")

set(PLANTUML_EXECUTABLE "plantuml.jar")

##
# Collect all of the Plantuml files in this folder
##
file(GLOB PUML_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*puml)

add_custom_target(plantuml
    COMMENT "Create the plantuml files"
)

##
# Declaring the executable as source file here
# makes sure that we only download this when it is not
# available.
##
target_sources(plantuml
    PRIVATE
        ${CMAKE_CURRENT_BINARY_DIR}/${PLANTUML_EXECUTABLE}
)

foreach(file ${PUML_FILES})
    ##
    # We run plantuml for each *.puml file in this folder.
    # TODO: Change this to run only if the output file does not exist.
    ##
    add_custom_command(TARGET plantuml
        PRE_BUILD
        COMMAND java -jar ${PLANTUML_EXECUTABLE} ${file} -tsvg -o ${CMAKE_CURRENT_BINARY_DIR}
        COMMENT "Run plantuml for ${file}"
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
        DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/${PLANTUML_EXECUTABLE}
    )
endforeach(file IN PUML_FILES)


##
# Downloading plantuml executable.
# This downloads the GPL version of plantuml.
# Attention: This file is distributed under GPL license.
# Do not release or modify.
##
add_custom_command(
    COMMAND wget ${PLANTUML_BINARY_SOURCE} -O ${PLANTUML_EXECUTABLE}
    COMMENT "Download plantuml binaries."
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/${PLANTUML_EXECUTABLE}
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)

