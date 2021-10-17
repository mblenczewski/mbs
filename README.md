# mbs

A minimal build system written in POSIX shell script. Templates a directory
structure for c and cpp projects, creates default build and clean scripts,
and includes a minimalist testing framework.

## Directory Structure

mbs creates the following directory structure:
```text
# usage: mbs-init <project-name>
$ mbs-init example-proj

# creates the following directory structure
# Key:
#   d - directory   x - executable shell script   f - file
d /example-proj
d   /.git
d   /include
f     example-proj.h
d   /lib
d   /obj
d   /out
d   /src
f     main.c
d   /test
f     test.h
f     test_example.c
f   .gitignore
x   build
x   clean
f   common.sh
f   Makefile
f   README.md
```

### common.sh

This file contains the project settings, such as global compiler, preprocessor,
and linker flags, the different directories, the toolchain in use (compiler, 
linker, archiver), and the implementation of the minimal build system.

### build

This shell script defines the project sources, performs an out-of-source build,
and runs all tests.

### clean

This shell script cleans all the generated files.

### .gitignore

The default `.gitignore` will ignore all files under the `/obj` and `/out`
directories.

## Usage

To create a new mbs project, run the `mbs-init` shell script:
```sh
mbs-init <project-name>
cd <project-name>
```

To build an mbs project, run the `build` shell script:
```sh
./build
```

The `build` shell script recognises a `VERBOSE=1` flag to show more information
about the steps its taking, as well as the `DBG=1` and `REL=1` flags to select
the compilation regime (and include the appropriate toolchain flags):
```sh
VERBOSE=1 DBG=1 ./build

REL=1 ./build

# NOTE: this will cause both the debug and release flags to be included,
#       which might not be what you want
DBG=1 REL=1 ./build
```

The `build` shell script does not run any built executables. It exits with a
non-zero exit code if any tests fail, and should be chained with running the
executable as follows:
```sh
build && ./out/<executable-name>
```

To clean an mbs project, run the `clean` shell script:
```sh
./clean
```

### Makefile
Additionally, a very simple Makefile wrapper around the build and clean scripts
is generated, so instead of running `./build` or `./clean` you can simply call
`make` with the appropriate target.
