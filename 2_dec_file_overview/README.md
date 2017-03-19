<!--- @file
  2 DEC File Overview

  Copyright (c) 2007-2017, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->

# 2 DEC File Overview

This document describes the format of EDK II package declaration (DEC) files.
The DEC files are used by the EDK II utilities that parse EDK II DSC and EDK II
INF files to generate AutoGen.c and AutoGen.h files for the EDK II build
infrastructure.

There are no new features or format introduced in this specification.

This version of the specification reflects changes to the EDK II reference
build system that has been updated to support builds using EDK II Packages that
are located in directories outside of the directory specified by the system
environment variable, WORKSPACE. Refer to the TianoCore.org web-site for more
information on the EDK II build system.

An EDK II Package (directory) is a directory that contains an EDK II package
declaration (DEC) file. Only one DEC file is permitted per directory. EDK II
Packages cannot be nested within other EDK II Packages.

A DEC file describes content for a collection of 'like' modules located in a
directory tree. Each collection of modules must be in a unique directory tree
in the `WORKSPACE`, and must contain only one DEC file.

EDK II modules are located in subdirectories below the directory containing
this file. If a module is a Library, the module directory must be created in
the "Library" subdirectory. An "Include" subdirectory is also required, with
the header file for the Library class placed in the sub-directory
Include/Library/, and be called LibraryClassName.h. Additional content for the
Include directory may include header files and potentially another Industry
Standard directory.

**********
**Note:** Path and Filename elements within the DEC are case-sensitive in order
to support building on UNIX style operating systems. Names that are used in C
code are case sensitive as well as MACRO names used as short-cuts within the
DEC file. Use of "..", "./" and "../" in path and filename elements is
prohibited.
**********
**Note:** GUID values are used during runtime to uniquely map the C names of
PROTOCOLS, PPIS, PCDS and other variable names.
**********
**Note:** The examples in this document use a backslash "\" character when the
example line does not fit in between the margins. This character is not
permitted in the actual DEC file, as all valid entries must appear on the same
line.
**********
**Note:** The total path and file name length is limited by the operating
system and third party tools. It is recommended that for EDK II builds that the
WORKSPACE (or directories listed in the PACKAGESPATH system environment
variable) directory be either a directory under a subst drive in Windows
(s:/build as an example) or be located in either the /opt directory or in the
user's / home/username directory for Linux and OS/X._
**********
