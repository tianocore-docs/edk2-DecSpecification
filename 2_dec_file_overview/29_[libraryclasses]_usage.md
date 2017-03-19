<!--- @file
  2.9 [LibraryClasses] Usage

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

## 2.9 [LibraryClasses] Usage

This is an optional section.

This section is used to define the headers associated with the new EDK II
library classes. A library class is declared and its associated header file
specified in this section. The module library instances that satisfy a Library
Class must use the Library Class Header file, without modification.

Refer to the `[LibraryClasses]` definition later in this document for a
complete description of this section and its contents.

This section uses one of the following section definitions:

```ini
[LibraryClasses.common]

[LibraryClasses.IA32]

[LibraryClasses.X64]

[LibraryClasses.IPF]

[LibraryClasses.EBC]

[LibraryClasses]
```

Format for the entries in this section is two fields, with a pipe "|"
character as the field separator, as shown below.

`LibraryClassName | Relative/path/and/header_filename.h`

The relative path is relative to the directory the DEC file is in. Use of "..",
"../" or "./" in the directory path is prohibited.
