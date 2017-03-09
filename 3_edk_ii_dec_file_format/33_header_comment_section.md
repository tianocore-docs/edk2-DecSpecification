<!--- @file
  3.3 Header Comment Section

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

## 3.3 Header Comment Section {#3-3-header-comment-section}

This is an optional section for EDK II packages that will not be distributed
using tools that create UEFI Distribution Packages. It is required for EDK II
packages that will be distributed using tools that create UEFI Distribution
Packages.

#### Summary

The Copyright and License notices for the DEC file are in the comments that
start the file. The format for the comment section is:

```ini
## @file
# Abstract
#
# Description
#
# Copyright
#
# License
#
##
```

This information can be derived from an XML Distribution package file (UEFI
Packaging

Specification) or from a developer creating a new package declaration (DEC)
document.

#### Prototype

```c
<Header>         ::= <SourceHeader>
                     [<BinaryHeader>]
<SourceHeader>   ::= <Comment>*
                     "##" [<Space>] <Space> "@file" [<TS> <File>] <EOL>
                     [<Abstract>]
                     [<Description>]
                     <Copyright>+
                     "#" <EOL>
                     <License>
                     "##" <EOL>
<Filename>       ::= <Word> "." <Extension>
<Abstract>       ::= "#" <AsciiString> <EOL> ["#" <EOL>]
<Description>    ::= ["#" <AsciiString> <EOL>]+ ["#" <EOL>]
<Copyright>      ::= "#" <TabSpace> <CopyName> <Date> "," <CompInfo>
<CopyName>       ::= ["Portions" <MTS>] "Copyright (c)" <MTS>
<Date>           ::= <Year> [<TS> {<DateList>} {<DateRange>}]
<Year>           ::= "2" (0-9)(0-9)(0-9)
<DateList>       ::= <CommaSpace> <Year> [<CommaSpace> <Year>]*
<DateRange>      ::= "-" <TS> <Year>
<CompInfo>       ::= (0x20 - 0x7e)* <MTS> <Arr>
<Arr>            ::= "All rights reserved." [<TS> "<BR>"] <EOL>
<License>        ::= ["#" <TS> <AsciiString> <EOL>]+ ["#" <EOL>]
<BinaryHeader>   ::= "##" <Space> <Space> "@BinaryHeader" <EOL>
                     <BinaryAbstract> "#" <EOL>
                     <BinDescription>
                     "#" <EOL>
                     <Copyright>+
                     "#" <EOL>
                     <BinaryLicense>
                     "#" <EOL>
                     "##" <EOL>
<Filename>       ::= <Word> "." <Extension>
<BinaryAbstract> ::= "#" <TS> <AsciiString> <EOL>
<BinDescription> ::= ["#" <TS> <AsciiString> <EOL>]+
<Copyright>      ::= "#" <MTS> <CopyName> <Date> "," <CompInfo>
<CopyName>       ::= ["Portions" <MTS>] "Copyright (c)" <MTS>
<Date>           ::= <Year> [<TS> {<DateList>} {<DateRange>}]
<Year>           ::= "2" (0-9)(0-9)(0-9)
<DateList>       ::= <CommaSpace> <Year> [<CommaSpace> <Year>]*
<DateRange>      ::= "-" <TS> <Year>
<CompInfo>       ::= (0x20 - 0x7e)* <MTS> <Arr>
<Arr>            ::= "All rights reserved." [<TS> "<BR>"] <EOL>
<BinaryLicense>  ::= ["#" <TS> <AsciiString> <EOL>]+
```

#### Parameters

**_Abstract_**

A brief one line description of what the package provides.

**_BinaryAbstract_**

A brief one line description of what the packages provides that may be
different from a source abstract.

**_Description_**

A detailed description of what the package provides.

**_BinaryDescription_**

A detailed description of what the package provides that may be different from
a source description.

**_Copyright_**

The copyright date should be modified if there is a functional change to the
source code. Since binaries are constructed from source, the binary file uses
the same copyright date as the source DEC, however tools are not required to
ensure that the dates are identical.

**_License_**

One or more licenses that the package with source code is released under.

**_BinaryLicense_**

One or more licenses that the binary package is released under that may be
different from the licenses used for distributing the package with source code.

#### Example

```ini
## @file
# Framework Module Development Environment Industry Standards
#
# This Package provides headers and libraries that conform to
# EFI/Framework Industry standards.
#
# Copyright (c) 2006 - 2007, Intel Corporation.
#
# All rights reserved.
# This program and the accompanying materials are licensed and made
# available under the terms and conditions of the BSD License which
# accompanies this distribution.
# The full text of the license may be found at
# http://opensource.org/licenses/bsd-license.php
#
# THE PROGRAM IS DISTRIBUTED UNDER THE BSD LICENSE ON AN "AS IS" BASIS,
# WITHOUT WARRANTIES OR REPRESENTATIONS OF ANY KIND, EITHER EXPRESS OR
# IMPLIED.
#
##
```
