# mbs
A minimal build system written in POSIX shell script. Templates a directory
structure for c and cpp projects, creates default build and clean scripts,
and includes a minimalist testing framework.

## Usage
To create a new mbs project, simply invoke the `mbs` script with a project
name. Preferrably the name has no spaces, otherwise all blankspace characters
will be replaced with `-`. Once in the project directory, simply use the
available shell scripts (`clean.sh`, `build.sh`, and `test.sh`) or the
Makefile wrapper to build your desired projects.

The build system recognises the following environment variables:
```text
TOOLCHAIN=[host|<my-toolchain>] :
- uses the defined toolchain-<my-toolchain>.sh file to set the default
  toolchain flags

REGIME=[DEBUG|RELEASE|<my-regime>] :
- sets the additional compilation-regime-specific toolchain flags to add to
  the build flags. if a custom regime is specified, it has to be added to the
  toolchain preset files

VERBOSE[=1] :
- if defined, will print out all executed commands to stderr

DRYRUN[=1] :
- if defined, will print out all commands that would be executed to stderr,
  without actually executing the commands
```

## Example
```sh
$ mbs testproj
$ cd testproj
$ REGIME=DEBUG ./build.sh all
$ VERBOSE=1 make testproj
$ make clean
$ cd ..
```
