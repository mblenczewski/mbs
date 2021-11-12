# mbs
A minimal build system written in POSIX shell script. Templates a directory
structure for c and cpp projects, creates default build and clean scripts,
and includes a minimalist testing framework.

## mbs-init
### Directory Structure
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
f     mbs_prelude.h
f     example-proj.h
d   /lib
d   /obj
d   /out
d   /src
f     mbs_prelude.c
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

### mbs\_prelude
The `mbs_prelude.{c,h}` files contain global definitions for integral types,
string types, common functions, and their implementations. They also contain
common headers to be included.

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
directories. It will additionally ignore any vim swapfiles.

### Usage
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
about the steps its taking, as well as the `REGIME={DBG,REL}` flag to select
the compilation regime (and include the appropriate toolchain flags):
```sh
VERBOSE=1 REGIME=DBG ./build

REGIME=REL ./build

# NOTE: you can provide a custom regime, but will need to add the regime flag
#       variables (MY_REGIME_CXXFLAGS, MY_REGIME_LDDFLAGS, etc) to ./build
#       and optionally to ./common.sh
REGIME=MY_REGIME ./build
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
