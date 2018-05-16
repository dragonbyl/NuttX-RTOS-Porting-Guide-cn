# 3 Configuring and Building

# 3.1 Configuring NuttX

**Mannual Configuring**

Configuring NuttX requires only copying the board-specific configuration files into the top level directory which appears in the make files as the make variable, ${TOPDIR}. This could be done manually as follows:

- Copy configs/&lt;board-name&gt;/&lt;config-dir&gt;/Make.defs to ${TOPDIR}/Make.defs,
- Copy configs/&lt;board-name&gt;/&lt;config-dir&gt;/defconfig to ${TOPDIR}/.config

Where <board-name> is the name of one of the sub-directories of the NuttX configs/ directory. This sub-directory name corresponds to one of the supported boards identified above. <config-dir> is the optional, specific configuration directory for the board. And <app-dir> is the location of the optional application directory.

**Automated Configuring**

There is a script that automates these steps. The following steps will accomplish the same configuration:

 tools/configure.sh <board-name>[/<config-dir>]

There is an alternative Windows batch file, configure.bat, that can be used instead of configure.sh in the windows native environment like:

  tools\configure.bat <board-name>[\<config-dir>]

See tools/README.txt for more information about these scripts.

If your application directory is not in the standard location (../apps or ../apps-<version>), then you should also specify the location of the application directory on the command line like:

  tools/configure.sh -a <app-dir> <board-name>[/<config-dir>]


The .version file is also used during the build process to create a C header file at include/nuttx/version.h that contains the same version information. That version file may be used by your C applications for, as an example, reporting version information.

Additional Configuration Steps. The remainder of configuration steps will be performed by ${TOPDIR}/Makefile the first time the system is built as described below.

# 3.2 Building NuttX

**Building NuttX.** 

Once NuttX has been configured as described above, it may be built as follows:

cd ${TOPDIR}
make
The ${TOPDIR} directory holds:

The top level Makefile that controls the NuttX build.
That directory also holds:

The makefile fragment .config that describes the current configuration, and
The makefile fragment Make.defs that provides customized build targets.
Environment Variables. The specific environmental definitions are unique for each board but should include, as a minimum, updates to the PATH variable to include the full path to the architecture-specific toolchain identified in Make.defs.

First Time Make. Additional configuration actions will be taken the first time that system is built. These additional steps include:

- Auto-generating the file include/nuttx/config.h using the ${TOPDIR}/.config file.
- Auto-generating the file ${TOPDIR}/.version with version 0.0 if one does not exist.
- Auto-generating the file include/nuttx/version.h using the ${TOPDIR}/.version file.
- Creating a link to ${TOPDIR}/arch/<arch-name>/include at ${TOPDIR}/include/arch.
- Creating a link to ${TOPDIR}/configs/<board-name>/include at ${TOPDIR}/include/arch/board.
- Creating a link to ${TOPDIR}/configs/<board-name>/src at ${TOPDIR}/arch/<arch-name>/src/board
- Creating a link to ${APPDIR}/include at ${TOPDIR}/include/apps
- Creating make dependencies.


