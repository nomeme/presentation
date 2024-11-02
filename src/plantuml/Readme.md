# Plantuml

This folder contains the plantuml input files.

During the `cmake` configure step a `plantuml` binary is downloaded which is used by the *custom target* `plantuml` to generate the `*.svg` files used by the presentation.
The additional target `plantuml_clean` serves to clean all of the generated `*.svg` files if the auto-update on file-change does not work properly.

> This can happen as we currently do not track file changes of imported files.
