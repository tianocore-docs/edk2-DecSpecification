<!--- @file
  3.8 [PPIs] Sections

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

## 3.8 [PPIs] Sections

These sections are optional.

#### Summary

Defines the optional `[Ppis]` section tag. This is a list of the global PPI C
Names that are referenced in the EDK II package's module C code.

PPI entries listed in architectural sections are not permitted to be listed in
the common architectural section.

The '`common`' architecture modifier in a section tag must not be combined with
other architecture type modifiers; doing so will result in a build break.

The use of a `<MACROVAL>` element in this section is prohibited.

Each PPI entry must be listed only once per section.

#### Prototype

```c
<Ppis>          ::= "[Ppis" [<com_attribs>] "]" <EOL> <PpiEntries>*
<com_attribs>   ::= {".common"} {<attribs>}
<attribs>       ::= <attrs> ["," <TS> "Ppis" <attrs>]*
<attrs>         ::= "." <arch>
<PpiEntries>    ::= [<PpiComment>]
                    <TS> <CName> <Eq> <CFormatGUID> {<CommentBlock>} {<EOL>}
<PpiComment>    ::= [<Description>]
                    <TS> "##" <TS> <PpiHeaderFile> <EOL>
<Description>   ::= <TS> "##" <TS> <AsciiString> <EOL>
                    [<TS> "#" <TS> <AsciiString> <EOL>]*
<PpiHeaderFile> ::= <PATH> <Word> ".h"
<CommentBlock>  ::= [<TS> "##" <TS> <ModuleTypeList>]
                    {<Comment>} {<EOL>}
```

#### Parameters

**_PpiHeaderFile_**

Path to the PPI header file statement listed in comments in this section must
be relative to the directory that contains the DEC file. Use of "..", "../" or
"./" in the directory path is prohibited.

#### Restrictions

It is NOT permissible to list a PPI entry under common and under a specific
architecture. It is permissible to specify PPI entries under all architectures
except `"common`" if different Guid values may be required for different
architectures.

```ini
# Global Ppis Definition section - list of Global Ppis C Name
# Data Structures that are provided by
# this package.
#
#######################################################################
[Ppis.common]
gPeiNtThunkPpiGuid    = { 0x98C281E5, 0xF906, 0x43DD,{ 0xA9, 0x2B, 0xB0, 0x03, 0xBF, 0x27, 0x65, 0xDA }}
gNtPeiLoadFilePpiGuid = { 0xFD0C65EB, 0x0405, 0x4CD2,{ 0x8A, 0xEE, 0xF4, 0x00, 0xEF, 0x13, 0xBA, 0xC2 }}
gNtFwhPpiGuid         = { 0x4E76928F, 0x50AD, 0x4334,{ 0xB0, 0x6B, 0xA8, 0x42, 0x13, 0x10, 0x8A, 0x57 }}
gPeiNtAutoScanPpiGuid = { 0x0DCE384D, 0x007C, 0x4BA5,{ 0x94, 0xBD, 0x0F, 0x6E, 0xB6, 0x4D, 0x2A, 0xA9 }}
```
