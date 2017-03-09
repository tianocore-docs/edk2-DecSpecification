<!--- @file
  2.4 [Defines] Usage

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

## 2.4 [Defines] Usage {#2-4-defines-usage}

This is a required section.

The `[Defines]` section is used to track the package's GUID and version, which
allows multiple copies of the same package with different versions to be
processed by tools. Architectural modifiers are not permitted in the
`[Defines]` section. If major changes to a package occur, the GUID value of the
package must also change.

The `DEC_SPECIFICATION` of existing DEC files does not need to be updated unless
content in the file has been updated to match new content specified by this
revision of the specification. Additionally, the package's version major number
may change. Minor changes require incrementing the package's version minor
number. The

`PACKAGE_UNI_FILE` entry points to a Unicode file containing localization
strings. The use of the #include statement in this file is prohibited. The file
path (if present) is relative to the directory containing the DEC file.

The parsing utilities process any local symbol assignments defined in this
section. Note that the sections are processed in the order listed in the DEC
file, and later assignments of these local symbols override previous
assignments.

This section will use only one section header:

`[Defines]`

The format for entries in this section is:

`Name = Value`

The following is an example of this section.

```ini
[Defines]
  DEC_SPECIFICATION = 0x00010019
  PACKAGE_NAME      = MdePkg
  PACKAGE_GUID      = 1E73767F-8F52-4603-AEB4-F29B510B6766
  PACKAGE_VERSION   = 1.02
  PACKAGE_UNI_FILE  = MdePkg.uni
```
