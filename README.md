# mbs
A minimal build system written using GNU Make. Templates a monorepo directory
structure for c and cpp projects and includes a minimalist testing framework.

## Usage
To create a new mbs project, simply invoke the `mbs` script with a project
name. Preferrably the name has no spaces, otherwise all blankspace characters
will be replaced with `-`. Once in the project directory, simply use the
Makefile to build the project.

The Makefile recognises the following environment variables.
```text
REGIME=[DEBUG|RELEASE|<my-regime>] :
- sets the additional compilation-regime-specific toolchain flags to add to
  the build flags. if a custom regime is specified, it has to be added to the
  config.mk preset file
```
