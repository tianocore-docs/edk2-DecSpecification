<!--- @file
  3.4 [Defines] Section

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

## 3.4 [Defines] Section

This section is required.

#### Summary

This describes the `[Defines]` section, which is required in all DEC files.
This file is created during installation of a UEFI distribution package or by
the developer and is an input to the EDK II build tool parsing utilities.
Elements may appear in any order within this section.

The code for this specification is `"0001001A`" and new versions of this
specification must increment the minor (001A) portion of the specification
code. This value may also be specified as a decimal value, 1.26.

Existing DEC files are not required to update the `DEC_SPECIFICATION` version
value. This value may be used by tools to identify any new functionality
introduced by this specification version.

Tools are allowed to use the `PACKAGE_GUID` and `PACKAGE_VERSION` values for
testing dependencies. This is particularly import for creating UEFI
Distribution Packages, as they are required fields in the distribution package
description file.

Note that comments may be appended to define statements as well as located
anywhere within the `[Defines]` section.

#### Prototype

```c
<defines>    ::= "[Defines]" <EOL>
                 <TS> "DEC_SPECIFICATION" <Eq> <SpecVer> <EOL>
                 <TS> "PACKAGE_NAME" <Eq> <UiNameType> <EOL>
                 <TS> "PACKAGE_GUID" <Eq> <RegistryFormatGUID> <EOL>
                 <TS> "PACKAGE_VERSION" <Eq> <DecimalVersion> <EOL> [<TS>
                 "PACKAGE_UNI_FILE" <Eq> <Filename> <EOL>]
                 <MacroDefinition>*
<UiNameType> ::= <Word>
<SpecVer>    ::= {<HexVersion>} {(0-9))+ "." (0-9)+}
```

#### Parameters

**_UiNameType_**

The `PACKAGE_NAME` value may be used for creating directories.

**_DecimalVersion_**

This is a decimal number, and if not specified is assumed to be 0 Alpha
characters are not permitted.

**_SpecVer_**

For new DEC files, the version value must be set to 0x0001001A Tools that
process this version of the DEC file can successfully process earlier versions
of the DEC file (this is a backward compatible update). There is no requirement
to change the value in existing DEC files if no other content changes. This may
also be specified as decimal value, 1.26.

**_Filename_**

Filenames listed in the `[Defines]` section must be relative to the directory
the DEC file is in. Use of "..", "." and "../" in the directory path is not
permitted. Use of an absolute path is not permitted. The file name specified in
the `PACKAGE_UNI_FILE` entry must be a Unicode file with an extension of .uni, .UNI
or .Uni.

#### Example 1

```ini
[DEFINES]
  DEC_SPECIFICATION = 0x0001001A
  PACKAGE_NAME      = MdePkg
  PACKAGE_GUID      = 1E73767F-8F52-4603-AEB4-F29B510B6766
  PACKAGE_VERSION   = 1.06
  PACKAGE_UNI_FILE  = MdePkg.uni
```

#### Example 2

```ini
[DEFINES]
  DEC_SPECIFICATION = 1.26
  PACKAGE_NAME      = IntelFspPkg
  PACKAGE_GUID      = 444C6CDF-55BD-4744-8F74-AE98B003B955
  PACKAGE_VERSION   = 0.1
```
