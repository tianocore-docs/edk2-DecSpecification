<!--- @file
  3.9 [LibraryClasses] Sections

  Copyright (c) 2007-2019, Intel Corporation. All rights reserved.<BR>

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

## 3.9 [LibraryClasses] Sections

These sections are optional.

#### Summary

Defines the `[LibraryClasses]` tag in the DEC files.

The `[LibraryClasses]` section maps the location, relative to the DEC file, of
library ClassName to the header file for the library class specified by the
ClassName.

ClassName entries listed in architectural sections are not permitted to be
listed in the common architectural section.

The '`common`' architecture modifier in a section tag must not be combined with
other architecture type modifiers; doing so will result in a build break.

All paths must be relative to the directory that contains the DEC file. Use of
absolute paths, or `WORKSPACE` relative paths is prohibited.

It is permissible to use a `<MACROVAL>` entry in this section provided the
above rules are followed.

Each ClassName entry must be listed only once per section.

#### Prototype

```c
<LibraryClasses> ::= "[LibraryClasses" [<com_attribs>] "]" <EOL> <LcEntries>*
<com_attribs>    ::= {".common"} {<attribs>}
<attribs>        ::= <attrs> ["," <TS> "LibraryClasses" <attrs>]*
<attrs>          ::= "." <arch>
<LcEntries>      ::= {<LcEntry>} {<MacroDefinition>}
<LcEntry>        ::= [<LcDoxygenHelp>]
                     <TS> <ClassName> <FS> <Filename> {<CommentBlock>} {<EOL>}
<LcDoxygenHelp>  ::= <TS> "##" <TS> "@LibraryClasses" <TS> <AsciiString> <EOL>
<ClassName>      ::= <ToolWord>
                     # A User Defined Keyword consisting of
                     # alphanumeric characters. No special
                     # characters are permitted.
<Filename>       ::= <PATH> <File> ".h"
<CommentBlock>   ::= <TS> "##" <TS> <ModuleTypeList>
                     {<Comment>} {<EOL>}
```

#### Parameters

**_Filename_**

Path portion of the header file statements in this section must be relative to
the directory that contains the DEC file. Use of "..", "../" or "./" in the
directory path is prohibited.

#### Restrictions

It is NOT permissible to list a Library Class entry under common and under a
specific architecture. It is permissible to specify Library Class entries under
all architectures except `"common`" if different header filename values are
required for different architectures.

```ini
# Library Class Header section - list of Library Class header
# files that are provided by
# this package.
#
#######################################################################
[LibraryClasses.common]
  UefiRuntimeServicesTableLib |Include/Library/UefiRuntimeServicesTableLib.h
  UefiLib | Include/Library/UefiLib.h
  UefiDriverModelLib | Include/Library/UefiDriverModelLib.h
  UefiDriverEntryPoint | Include/Library/UefiDriverEntryPoint.h
  UefiDecompressLib | Include/Library/UefiDecompressLib.h
  UefiBootServicesTableLib | Include/Library/UefiBootServicesTableLib.h
  TimerLib|Include/Library/TimerLib.h
  SmbusLib|Include/Library/SmbusLib.h
  ResourcePublicationLib|Include/Library/ResourcePublicationLib.h
  PostCodeLib|Include/Library/PostCodeLib.h
  ReportStatusCodeLib|Include/Library/ReportStatusCodeLib.h
  PrintLib|Include/Library/PrintLib.h
  PerformanceLib|Include/Library/PerformanceLib.h
  PeiServicesTablePointerLib|Include/Library/PeiServicesTablePointerLib.h
  PeimEntryPoint|Include/Library/PeimEntryPoint.h
  PeiServicesLib|Include/Library/PeiServicesLib.h
  PeiCoreEntryPoint|Include/Library/PeiCoreEntryPoint.h
  PeCoffLib|Include/Library/PeCoffLib.h
  BaseLib|Include/Library/BaseLib.h

[LibraryClasses.IA32]
  UefiApplicationEntryPoint |Include/Library/UefiApplicationEntryPoint.h # UEFI_APPLICATION

[LibraryClasses.X64]
  UefiApplicationEntryPoint|Include/Library/UefiApplicationEntryPoint.h # UEFI_APPLICATION

[LibraryClasses.EBC]
  UefiApplicationEntryPoint|Include/Library/UefiApplicationEntryPoint.h # UEFI_APPLICATION
```
