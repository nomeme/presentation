# Presentation

This repository contains the source code to create a presentation using pandoc with latex beamer template.

## Requirements

This project has following requirements.

* Java runtime for [Plantuml](https://plantuml.com/)
* Pandoc packages installed (`pacman -Su pandoc`)
* Cmake packages installed (`pacman -Su cmake`)
* Wget package installed (`pacman -Su wget`)

## Building

Building the presentation follows the default `cmake` rules.

``` bash
mkdir build
cd build
cmake ..
make presentation
```

The cmake configure step will download the plantuml executable (`jar`) into the build folder.
This is then used to generate the `*.svg` files under the target `plantuml`.
The `*svg` files can be removed for re-build using the target `plantuml_clean`.

The pdf for the presentation can be found under `build/Presentation.pdf`

