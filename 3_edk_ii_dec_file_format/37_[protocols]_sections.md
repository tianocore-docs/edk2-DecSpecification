<!--- @file
  3.7 [Protocols] Sections

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

## 3.7 [Protocols] Sections

These sections are optional.

#### Summary

Defines the `[Protocols]` section tag. This is a list of the global PROTOCOL C
Names and their C Guid values that are declared in the EDK II package (.DEC)
file. Protocol entries listed in architectural sections are not permitted to be
listed in the common architectural section.

The '`common`' architecture modifier in a section tag must not be combined with
other architecture type modifiers; doing so will result in a build break.

The use of a `<MACROVAL>` element in this section is prohibited.

Each Protocol entry must be listed only once per section.

#### Prototype

```c
<Protocols>       ::= "[Protocols" [<com_attribs>] "]" <EOL> <ProtocolEntries>*
<com_attribs>     ::= {<Public>} {<Hidden>}
<Public>          ::= {".common"} {<attribs>}
<Hidden>          ::= {".common.Private"} {<hattribs>}
<attribs>         ::= <attrs> ["," <TS> "Protocols" <attrs>]8
<attrs>           ::= "." <arch>
<hattribs>        ::= <hattrs> ["," <TS> "Protocols" <hattrs>]*
<hattrs>          ::= "." <arch> ".Private"
<ProtocolEntries> ::= [<ProtocolComment>]
                      <TS> <CName> <Eq> <CFormatGUID> {<CommentBlock>} {<EOL>}
<ProtocolComment> ::= [<Description>]
                      <ProtoHdrFile>
<ProtoHdrFile>    ::= <TS> "##" <TS> <PATH> <Word> ".h"
<Description>     ::= <TS> "##" <TS> <AsciiString> <EOL>
                      [<TS> "#" <TS> <AsciiString> <EOL>]*
<CommentBlock>    ::= [<TS> "##" <TS> <ModuleTypeList>]
                      {<Comment>} {<EOL>}
```

#### Parameters

**_ProtocolHeaderFile_**

Path to the Protocol header file statement listed in comments in this section
must be relative to the directory that contains the DEC file. Use of "..",
"../" or "./" in the directory path is prohibited.

#### Restrictions

It is NOT permissible to list a Protocol entry under common and under a
specific architecture. It is permissible to specify Protocol entries under all
architectures except `"common`" if different Guid values may be required for
different architectures.

It is NOT permissible to mix section tags without the `Private` modifier with
section tags with the `Private` modifier. If this condition is detected, the
build tools must terminate with an error message.

For example, `[Protocols.common, Protocols.IA32.Private]` is prohibited.

It is NOT permissible for the same protocol to be listed in section tags with
and without the `Private` modifier. If this condition is detected, the build
tools must terminate with an error message.

For example, the following is prohibited because the protocol named
`MyPrivateProtocol` is listed in a tag with and without a `Private` modifier.

```
[Protocols]
  MyPrivateProtocol = { 0xc7c4a20f, 0xd1d1, 0x427a, { 0xb0, 0x82, 0xa8, 0xb6, 0x24, 0xf7, 0x69, 0x4f }}

[Protocols.common.Private]
  MyPrivateProtocol = { 0xc7c4a20f, 0xd1d1, 0x427a, { 0xb0, 0x82, 0xa8, 0xb6, 0x24, 0xf7, 0x69, 0x4f }}
```

#### Example

```ini
# Global Protocols Definition section - list of Global Protocols C Name
# Data Structures that are provided by
# this package.
#
#######################################################################
[Protocols.common]
gEfiWinNtThunkProtocolGuid = { 0x58C518B1, 0x76F3, 0x11D4,{ 0xBC, 0xEA, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
gEfiWinNtIoProtocolGuid    = { 0x96EB4AD6, 0xA32A, 0x11D4,{ 0xBC, 0xFD, 0x00, 0x80, 0xC7, 0x3C, 0x88, 0x81 }}
```
