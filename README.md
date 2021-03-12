## Simple C template

Creates basic C99 compatible project in an idiomatic way for me.

- macOS
- OpenBSD
- Linux

### Make targets

- test: build and run the test_$projectname from the tests/ subdir
- valgrind_%: valgrind the relvant binary
- TAGS
- docs: run doxygen per Doxyfile

### Structure

- docs/
- include/
- src/
- tests/
