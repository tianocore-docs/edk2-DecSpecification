<!--- @file
  3.6 [Guids] Sections

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

## 3.6 [Guids] Sections

These sections are optional.

#### Summary

Defines the `[Guids]` section tag of the DEC files.

GUID entries listed in architectural sections are not permitted to be listed in
the common architectural section.

The '`common`' architecture modifier in a section tag must not be combined with
other architecture type modifiers; doing so will result in a build break.

The use of a `<MACROVAL>` element in this section is prohibited.

Each GUID entry must be listed only once per section.

#### Prototype

```c
<Guids>          ::= "[Guids" [<com_attribs>] "]" <EOL> <GuidEntries>*
<com_attribs>    ::= {".common"} {<attribs>}
<attribs>        ::= <attrs> ["," <TS> "Guids" <attrs>]*
<attrs>          ::= "." <arch>
<GuidEntries>    ::= [<GuidComment>]
                     <TS> <CName> <Eq> <CFormatGUID> {<CommentBlock>} {<EOL>}
<GuidComment>    ::= [<Description>]
                     <TS> "##" <TS> <GuidHeaderFile> <EOL>
<GuidValue>      ::= <CFormatGUID>
<GuidHeaderFile> ::= <PATH> <Word> ".h"
<Description>    ::= <TS> "##" <TS> <AsciiString> <EOL>
                     [<TS> "#" <TS> <AsciiString> <EOL>]*
<CommentBlock>   ::= <TS> "##" <TS> <ModuleTypeList>
                     {<Comment>} {<EOL>}
```

#### Parameters

**_GuidHeaderFile_**

Path to the GUID header file statement listed in comments in this section must
be relative to the directory that contains the DEC file. Use of "..", "../" or
"./" in the directory path is prohibited.

#### Restrictions

It is not permissible to list a GUID entry under common and under a specific
architecture. It is permissible to specify GUID entries under all architectures
except `"common`" if different GUID values may be required for different
architectures.

```ini
# Global Guid Definition section - list of Global Guid C Name
# Data Structures that are provided by
# this package.
#
#######################################################################
[Guids.common]
gPcdHobGuid                  = { 0x582E7CA1, 0x68CD, 0x4D44,{ 0xB4, 0x3B, 0xF2, 0x98, 0xED, 0x58, 0x7B, 0xA6 }}
gEfiWinNtPassThroughGuid     = { 0xCC664EB8, 0x3C24, 0x4086,{ 0xB6, 0xF6, 0x34, 0xE8, 0x56, 0xBC, 0xE3, 0x6E }}
gEfiWinNtCPUSpeedGuid        = { 0xD4F29055, 0xE1FB, 0x11D4,{ 0xBD, 0x0D, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtCPUModelGuid        = { 0xBEE9B6CE, 0x2F8A, 0x11D4,{ 0xBD, 0x0D, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtMemoryGuid          = { 0x99042912, 0x122A, 0x11D4,{ 0xBD, 0x0D, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtConsoleGuid         = { 0xBA73672C, 0xA5D3, 0x11D4,{ 0xBD, 0x00, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtUgaGuid             = { 0xAB248E99, 0xABE1, 0x11D4,{ 0xBD, 0x0D, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtGopGuid             = { 0x4e11e955, 0xccca, 0x11d4,{ 0xbd, 0x0d, 0x00, 0x80, 0xc7, 0x3c, 0x88, 0x81 }}
gEfiWinNtSerialPortGuid      = { 0x0C95A93D, 0xA006, 0x11D4,{ 0xBC, 0xFA, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtFileSystemGuid      = { 0x0C95A935, 0xA006, 0x11D4,{ 0xBC, 0xFA, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtPhysicalDisksGuid   = { 0x0C95A92F, 0xA006, 0x11D4,{ 0xBC, 0xFA, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtVirtualDisksGuid    = { 0x0C95A928, 0xA006, 0x11D4,{ 0xBC, 0xFA, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiEdkNt32PkgTokenSpaceGuid = { 0x0D79A645, 0x1D91, 0x40a6,{ 0xA8, 0x1F, 0x61, 0xE6, 0x98, 0x2B, 0x32, 0xB4 }}
```
