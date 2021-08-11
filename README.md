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
d   /include
f     main.h
d   /lib
d   /out
d   /src
f     main.c
d   /test
f     test.h
f     test_example.c
x   build
x   clean
f   common.sh
f   .gitignore
```

### common.sh

This file contains the project settings, such as global compiler, preprocessor,
and linker flags, the different directories, the toolchain in use (compiler, 
linker, archiver), and the implementation of the minimal build system.

### build

This shell script defines the project sources, performs an out-of-source build,
and runs all tests.

### clean

This shell script cleans out the `/out` directory.

### .gitignore

The default `.gitignore` will ignore all files under the `/out` directory.

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

