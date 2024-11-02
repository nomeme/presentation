add_subdirectory(plantuml)
add_subdirectory(images)

##
# Main target to build the presentation.
##
add_custom_target(presentation)

##
# This runs during configure step to set up
# the build environment.
# Copies the main markdown file to the build
# directory.
##
# TODO: get date from system and set it.
configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/Presentation.md
    ${CMAKE_CURRENT_BINARY_DIR}/Presentation.md
    @ONLY
)

configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/header.tex
    ${CMAKE_CURRENT_BINARY_DIR}/header.tex
    COPYONLY
)

##
# Create the pdf presentation from markdown using the beamer template.
##
add_custom_target(pandoc
    COMMAND pandoc -t beamer Presentation.md -o ${CMAKE_BINARY_DIR}/Presentation.pdf -H ${CMAKE_CURRENT_BINARY_DIR}/header.tex
    COMMENT "Run pandoc to create a pdf from markdown."
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    SOURCES ${CMAKE_CURRENT_BINARY_DIR}/Presentation.md
    BYPRODUCTS ${CMAKE_BINARY_DIR}/Presentation.pdf
)

message(STATUS "Pandoc command required, did you install pandoc?")
message(STATUS "pacman -Su pandoc")

##
# Add the pandoc target as dependency to the main
# presentation target.
##
add_dependencies(presentation
    pandoc
)

##
# Add the plantuml target as dependency of pandoc.
# We need the images before we can run pandoc.
##
add_dependencies(pandoc
    plantuml
)

