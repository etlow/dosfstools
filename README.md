## Plus/minus testing code

This code only tests the difference between plus and minus for multiple device sizes as stated in GitHub issue <https://github.com/dosfstools/dosfstools/issues/125>. It should not actually format any file.

It can be built normally with the instructions below up to `make` and then `src/mkfs.fat -C file.img 1` run as normal. The range of sizes tested can be updated by modifying the for loop near the bottom of `mkfs.fat.c`.

## dosfstools readme

dosfstools consists of the programs mkfs.fat, fsck.fat and fatlabel to create,
check and label file systems of the FAT family.  The dosfstools are licensed
under the GNU GPL version 3 or later. See the file `COPYING` for details.


### Build Requirements

The test suite requires the tool `xxd` (available as part of the `vim`
distribution).


### Installing

dosfstools are built using an autoconf/automake system, so the standard method
applies:

```
./configure
make
make install
```

You need to have superuser privileges in order to install into the standard
system wide locations.

The `./configure` script has an option `--enable-compat-symlinks` that will
configure the build to symlink older names of the tools to the current ones on
installation. These are `dosfsck`, `fsck.msdos` and `fsck.vfat` for `fsck.fat`,
`mkdosfs`, `mkfs.msdos` and `mkfs.vfat` for `mkfs.fat` and `dosfslabel` for
`fatlabel`.


### Running the test suite

The test suite can be run with `make check` after configuring. Note that if
`xxd` isn't available, all tests will be skipped and nothing actually tested.

During the tests temporary files of multiple GB in size will be created, but the
actual data content is not more than a few MB. The operating system and the
filesystem the tests are executed on should support sparse files, otherwise the
tests will be resource intensive.


### Building from the VCS repository

If you are working directly from a git clone of the official dosfstools
repository, you will find that you can not run `./configure` straight away
because it, like other autogenerated files for the build system, is not included
in the repository.

First, autoconf, automake and gettext have to be installed.  Then you can run
`./autogen.sh` to generate all the required files.
