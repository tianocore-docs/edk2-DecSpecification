<!--- @file
  2.5 [Includes] Usage

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

## 2.5 [Includes] Usage

This is an optional section.

The `[Includes]` section is used to identify the "standard" location "include
directories" provide by this EDK II package. The `[Includes]` contains a list
of package relative directory names. These directories contain sub-directories
or header files. If the Package directory contains the directories, and the
`Include`, `Include/Ppis`, `Include/Protocol` and `Include/Guid`, and header
files exist in each of these directories, then all four directories will be
listed in this section.

This list of directories is used by the build tools to create the list of
standard directory locations required by compilers.

Also included in this section are the directories containing headers that may
be required for individual EDK II module types. Refer to Appendix, "EDK II
Module Types", for a list of the valid types.

Refer to the `[Includes]` definition later in this document for a complete
description of this section and its contents.

The `[Includes]` section uses one of the following section definitions:

```ini
[Includes.common]

[Includes.IA32]

[Includes.X64]

[Includes.IPF]

[includes.EBC]

[Includes]
```

The format for entries in this section is one field, with an optional comment
"`#`" field as shown below:

`Package_Relative/path # Comment such as Keyword List`

The relative path is relative to the directory the DEC file is in. Use of "..",
"./" and "../" in the directory path is not permitted.

**********
**Caution:** Do not list individual files in the `[Includes]` section.
**********
