# Sources

This folder contains the input files for the `pandoc` task.

We use the `Presentation.md` input file in *Markdown* format to generate a `*.pdf` file for a presentation.
All neccessary files are copied to the build directory before triggering pandoc.
This makes sure that we can use relative paths in the input *Markdown* file.
