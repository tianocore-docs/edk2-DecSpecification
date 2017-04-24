<!--- @file
  3.5 [Includes] Sections

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

## 3.5 [Includes] Sections

These sections are optional.

#### Summary

Defines the `[Includes]` section tag in the DEC files. This section lists the
"standard" include locations, not file names, provided in the package. Each
include `<PATH>` entry listed in a section must be unique to the section
(duplicate entries within a section are not permitted).

A path entry listed in an architectural section must not be listed in the
common section.

The included path must not end with the `<FileSep>` character.

All paths must be relative to the directory that contains the DEC file. Use of
absolute paths, or `WORKSPACE` relative paths is prohibited.

It is permissible to use a `<MACROVAL>` entry in this section provided the
above rules are followed.

The '`common`' architecture modifier in a section tag must not be combined with
other architecture type modifiers; doing so will result in a build break.

#### Prototype

```c
<Include>      ::= "[Includes" [<com_attribs>] "]" <EOL> <IncEntries>*
<com_attribs>  ::= {<Public>} {<Hidden>}
<Public>       ::= {".common"} {<attribs>}
<Hidden>       ::= {".common.Private"} {<hattribs>}
<attribs>      ::= <attrs> ["," <TS> "Includes" <attrs>]*
<attrs>        ::= "." <arch>
<hattribs>     ::= <hattrs> ["," <TS> "includes" <hattrs>]*
<hattrs>       ::= "." <arch> ".Private"
<IncEntries>   ::= {<MacroDefinition>} {<HdrFile>}
<HdrFile>      ::= <CommentBlock>*
                   <TS> <PATH>
                   {<CommentBlock>} {<EOL>}
<CommentBlock> ::= <TS> "##" <TS> <ModuleTypeList> <CmtOrEol>
<CmtOrEol>     ::= {<Comment>} {<EOL>}
```

#### Parameters

**_PATH_**

Path statements listed in this section must be relative to the directory that
contains the DEC file. Use of "..", "../" or "./" in the directory path is
prohibited.

#### Restrictions

It is NOT permissible to list an include directory under common and under a
specific architecture. It is permissible to specify include directory entries
under all architectures except `"common`" if different include directories are
required for different architectures.

It is NOT permissible to mix section tags without the `Private` modifier with
section tags with the `Private` modifier. If this condition is detected, the
build tools must terminate with an error message.

For example, `[Includes.common, Includes.IA32.Private]` is prohibited.

#### Example

```ini
# Include section - list of Include Paths relative to the DEC file that
# are provided by this package.
# Comments are used for Keywords and Module Types.
#
#######################################################################
[Includes.common]
  Include # Includes for all processor architectures

[Includes.IA32]
  Include/Ia32 # Includes specific to IA32

[Includes.X64]
  Include/X64 # Includes specific to X64

[Includes.IPF]
  Include/Ipf # Includes specific to IA64

[Includes.EBC]
  Include/Ebc # Includes specific to EBC

[Includes.ARM]
  Include/Arm # Includes specific to ARM
```
