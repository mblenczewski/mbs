# mbs
A minimal build system written in POSIX shell script. Templates a directory
structure for c and cpp projects, creates default build and clean scripts,
and includes a minimalist testing framework.

### Usage
To create a new mbs project, run the `mbs-init` shell script:
```sh
mbs-init <project-name>
cd <project-name>
```

To build an mbs project, run the `build` shell script or simply run `make debug`:
```sh
./build
## OR
make debug
## OR
make release
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

Alternatively, simply run `make` to build a debug version of the project and
run the built executable:
```sh
make
```

To clean an mbs project, run the `clean` shell script or run `make clean`:
```sh
./clean
## OR
make clean
```
