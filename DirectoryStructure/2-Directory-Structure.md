# 2.0 Directory Structure

**Directory Structure**

The general directory layout for NuttX is very similar to the directory structure of the Linux kernel -- at least at the most superficial layers. At the top level is the main makefile and a series of sub-directories identified below and discussed in the following paragraphs:

**源码目录结构**

NuttX的源码目录结构和Linux内核的源码目录结构非常相似. 一级目录包含主makefile文件和若干下级目录.

# 2.5 nuttx/configs

The configs directory contains board specific configuration files. Each board must provide a subdirectory <board-name> under configs/ with the following characteristics:

<board-name>
|-- Kconfig
|-- include/
|   |-- board.h
|   `-- (board-specific header files)
|-- src/
|   |-- Makefile
|   `-- (board-specific source files)
|-- <config1-dir>
|   |-- Make.defs
|   `-- defconfig
|-- <config2-dir>
|   |-- Make.defs
|   `-- defconfig
|   ...
|-- scripts/
|   |-- (linker script files)
|   `-- Make.defs (optional
`-- (other board-specific configuration sub-directories)/


