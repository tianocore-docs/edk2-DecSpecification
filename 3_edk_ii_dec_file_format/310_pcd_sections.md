<!--- @file
  3.10 PCD Sections

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

## 3.10 PCD Sections {#3-10-pcd-sections}

These are optional sections. However, if modules in this package's directory
tree use a PCD that is not declared in other DEC files, then the package
creator must list the PCD in this file.

#### Summary

Defines the PCDs section tags in the DEC files.

There are five defined PCD access method types. Do not confuse these access
types with the data types of the PCDs. The five access method types are:
`PcdsFeatureFlag`, `PcdsFixedAtBuild`, `PcdsPatchableInModule`, `PcdsDynamic`
and `PcdsDynamicEx`. The PCD is used to define potential values that a module
might be coded against, and if a module uses the access methods for
`PcdsDynamic`, then the platform can define the final usage. PCDs listed as
`PcdsDynamic` or `PcdsDynamicEx` will only have one value in the final binary
image - the PEI and DXE PCD Drivers that maintain these values use a single
database for all architectures, with a unique value for a PCD (identified by
the Token Space GUID value and the Token Number).

If a PCD is only listed under a `PcdsFixedAtBuild` or `PcdsPatchableInModule`,
then modules are restricted, and cannot be coded to use either of the dynamic
PCD access methods.

Using the "`common`" architectural modifier is exactly the same as specifying a
PCD section type without an architectural modifier. A PCD listed in an INF or
DSC file which uses an architectural modifier may be listed in the '`common`'
section in the DEC file; it is not required to list PCDs in architectural
sections in the DEC. If a PCD is only listed under a section with an
architectural modifier that is not 'common', then it may only be used by
modules build for that specific architecture.

Each PCD entry must be listed only once per section. If a PCD is listed more
than once within one section, the last entry takes precedence.

The PCD values in this file are the default values. Default values listed in
architectural sections override default values specified in a 'common'
architectural section. The EDK II build system allows these values may be
overridden by default values in the INF files (provided all INF files use the
same default value for PCDs that are used by multiple modules) and by values
specified in the DSC or FDF file. A PCD's Datum type cannot be changed for
different access methods, only one datum type is permitted.

PCD entries may be put into any or all PCD section types except
`PcdsFeatureFlag` sections.

The use of a `<MACROVAL>` element in this section is prohibited.

The Token number specified in a PCD entry is used in code (auto-generated files
by the EDK II build system), along with the Token Space GUID value to uniquely
identify a given PCD. The Token number must be identical for every entry of a
PCD in this file (using a different token number for a PCD listed in
`PcdsDynamic` and `PcdsDynamicEx` sections for example, will result in a build
break).

PCDs listed in `PcdsFeatureFlag` sections must only be listed in
`PcdsFeatureFlag` sections.

#### Prototype

```c
<PCDs>            ::= <PcdSections>*
<PcdSections>     ::= {<PcdFeature>} {<PcdOther>}
<PcdFeature>      ::= <FFSectionTag> <FFEntries>*
<FFEntries>       ::= ["##" <TS> <PcdDescription>]
                      [<TS> <Prompt>]
                      [{<List>} {<Express>}]
                      <TS> <PcdBool>
<FFSectionTag>    ::= "[" "PcdsFeatureFlag" [<com_FFattribs>} "]" <EOL>
<com_FFattribs>   ::= {".common"} {<FFattribs>}
<FFattribs>       ::= <attrs> ["," <TS> "PcdsFeatureFlag" <attrs>]*
<PcdOther>        ::= "[" <PcdType> [<com_or_attribs>] "]" <EOL>
                      <PcdEntries>*
<PcdType>         ::= {"PcdsPatchableInModule"} {"PcdsFixedAtBuild"}
                      {"PcdsDynamic"} {"PcdsDynamicEx"}
<com_or_attribs>  ::= {<com_attribs>} {<attribs>}
<com_attribs>     ::= [".common"] ["," <TS> <PcdType> [".common"]]*
<attribs>         ::= <attrs> ["," <TS> <PcdType> <attrs>]*
<attrs>           ::= "." <arch>
<PcdEntries>      ::= ["##" <TS> <PcdDescription>]
                      [<TS> <Prompt>]
                      [<DoxComment>] <PcdEntry>
<PcdEntry>        ::= <TS> {<PcdBool>} {<PcdNumEntry>} {<PcdPtr>}
<PcdNumEntry>     ::= {<Pcd8>} {<Pcd16>} {<Pcd32>} {<Pcd64>}
<PcdBool>         ::= <PcdName> <FS> <BoolPcd> <FS> <Token> <CbOrEol>
<BoolPcd>         ::= <BoolType> <FS> "BOOLEAN"
<CbOrEol>         ::= {<CommentBlock>} {<EOL>}
<Pcd8>            ::= <PcdName> <FS> <PcdUint8> <FS> <Token> <CbOrEol>
<PcdUint8>        ::= <NumValUint8> <FS> "UINT8"
<Pcd16>           ::= <PcdName> <FS> <PcdUint16> <FS> <Token> <CbOrEol>
<PcdUint16>       ::= <NumValUint16> <FS> "UINT16"
<Pcd32>           ::= <PcdName> <FS> <PcdUint32> <FS> <Token> <CbOrEol>
<PcdUint32>       ::= <NumValUint32> <FS> "UINT32"
<Pcd64>           ::= <PcdName> <FS> <PcdUint64> <FS> <Token> <CbOrEol>
<PcdUint64>       ::= <NumValUint64> <FS> "UINT64"
<PcdPtr>          ::= <PcdName> <FS> <PcdPtrVal> <FS> <Token> <CbOrEol>
<PcdPtrVal>       ::= <PtrVal> <FS> "VOID*"
<PtrVal>          ::= {<CString>} {<CArray>}
<Token>           ::= <NumValUint32>
<DoxComment>      ::= <TS> {<Range>+} {<List>} {<Express>+}
<Prompt>          ::= "#" <TS> "@Prompt <MTS> <AsciiString> <EOL>
<Range>           ::= "#" <TS> "@ValidRange" <TS> <ERangeValues> <EOL>
<ERangeValues>    ::= [<ErrorCode> <TS>] <RangeValues>
<List>            ::= "#" <TS> "@ValidList" <TS> <EValidValueList> <EOL>
<EValidValueList> ::= [<ErrorCode> <TS>] <ValidValueList>
<Express>         ::= "#" <TS> "@Expression" <TS> <EExpression> <EOL>
<EExpression>     ::= [<ErrorCode> <TS>] <Expression>
<ErrorCode>       ::= <NumValUint32> <FS>
<PcdDescription>  ::= <AsciiString> <EOL>
                      [<TS> "#" <AsciiString> <EOL>]*
<CommentBlock>    ::= <TS> "##" <TS> <ModuleTypeList> {<Comment>} {<EOL>}
<RangeValues>     ::= {<ValidRange>} {<RangeExpress>}
<RngOp>           ::= <TS> {"AND"} {"and"} {"OR"} {"or"} <TS>
<RangeExpress>    ::= {"(" <ValidRng> ")" <RngOp> "(" <ValidRng> ")"}
                      {"NOT" <TS> "(" <ValidRng> ")"}
<ValidRng>        ::= ["NOT" <TS>] "(" <ValidRangeIn> ")"
<ValidRangeIn>    ::= ["NOT" <TS>] {<Integer> <TS> "-" <TS> <Integer>}
                      {<HexValue> <TS> "-" <TS> <HexValue>}
                      {"LT" <TS> {<Integer>} {<HexValue>}}
                      {"GT" <TS> {<Integer>} {<HexValue>}}
                      {"LE" <TS> {<Integer>} {<HexValue>}}
                      {"GE" <TS> {<Integer>} {<HexValue>}}
                      {"XOR" <TS> {<Integer>} {<HexValue>}}
                      {"EQ" <TS> {<Integer>} {<HexValue>}}
<ValidValueList>  ::= <Number> ["," <TS> <Number>]*
```

#### Parameters

**_Expression_**

The expression in the @Expression entry must evaluate to True in order for the value to be valid.

**_RangeExpressions_**

This is required to be an in-fix logical expression, evaluated left to right, for a range of values, using Relational, Equality and Logical Operators (LT, LE, GT, GE.) The forms PcdCName and/or PcdTokenSpaceGuidCName.PcdCName are permitted. Parentheses are recommended for clarity. Since there may be different error numbers associated with valid ranges (one for less than, another for greater than) more than one ValidRange entry is permitted.

**_HexDigit_**

This value, if specified corresponds to the ErrorNumber of an Error Message
defined in a UEFI PI Distribution Package. Each error number is related to a
single error message (translations of message text are not considered as
separate error messages), with the text of error messages included in the
Unicode file specified in the `PACKAGE_UNI_FILE` element in the `[Defines]`
section.

**_TokenNumber_**

Each PCD declared within a token space (defined by the Token Space GUID) must
be assigned a unique 32-bit value. This token number and an optional token
space GUID are used in code for accessing a PCD's value.

**_ErrorCode_**

This value, if specified corresponds to the ErrorNumber of an Error Message
defined in a UEFI PI Distribution Package. Each error number is related to a
single error message.

**_Token_**

Each PCD declared within a token space (defined by the Token Space GUID) must
be assigned a unique 32-bit value. This token number and an optional token
space GUID are used in code for accessing a PCD's value.

#### Restrictions

It is permissible to list a PCD entry under common and under a specific
architecture.

It is permissible to specify PCD entries under all architectures except
"`common`" if different default values may be required for different
architectures. The tools must use architectural specific recommended values
over recommended values listed in the common sections. This technique is
permitted to allow unique recommendations for individual architectures.

It is not permissible to list command modifier and an architectural modifier in
a section header. The following example is not permitted:

`[PcdsPatchableInModule.IA32, PcdPatchableInModule.common]`

It is permissible to specify multiple architectures for like PcdType items in
the same section header. For example:

`[PcdsFeatureFlag.IA32, PcdsFeatureFlag.X64]`

It is permissible to mix PcdsPatchableInModule, PcdsFixed, PcdsDynamic and
PcdsDynamicEx PcdType elements within an architecture section. For example:

`[PcdsPatchableInModule.IA32, PcdsFixedAtBuild.IA32]`

The `PcdsFeatureFlag` PcdType may not be mixed with any other PcdType elements
in the section header. The following example is NOT VALID:

`[PcdsFeatureFlag.IA32, PcdsFixedAtBuild.IA32]`

While allowed by this specification, it is not recommended to mix different

PcdType.architecture values in a single section. The following example is
valid, but not recommended:

`[PcdsDynamicEx.IA32, PcdsFixedAtBuild.X64, PcdPatchableInModule.IPF]`

Refer to the _PI Specification_ for more information.

#### Example

```ini
########################################################################
#
#
# PCD Declarations section - list of all PCDs Declared by this package
# Only this package should be providing the
# declaration, other packages should not.
#
#
#
[PcdsFeatureFlag.common]
  ## If TRUE, the component name protocol will not be installed.
  gEfiMdePkgTokenSpaceGuid.PcdComponentNameDisable | FALSE |BOOLEAN | 0x0000000d
  ## If TRUE, the driver diagnostics protocol will not be installed.
  gEfiMdePkgTokenSpaceGuid.PcdDriverDiagnosticsDisable | FALSE |BOOLEAN | 0x0000000e

[PcdsFixedAtBuild.common]
  ## Indicates the maximum length of unicode string
  gEfiMdePkgTokenSpaceGuid.PcdMaximumUnicodeStringLength |1000000 | UINT32 | 0x00000001
  ## Indicates the maximum length of ascii string
  gEfiMdePkgTokenSpaceGuid.PcdMaximumAsciiStringLength | 1000000 |UINT32 | 0x00000002
  ## Indicates the maximum node number of linked list
  gEfiMdePkgTokenSpaceGuid.PcdMaximumLinkedListLength | 1000000 |UINT32 | 0x00000003

[PcdsFixedAtBuild.common, PcdsPatchableInModule.common] ## This flag is used to control the printout of DebugLib
gEfiMdePkgTokenSpaceGuid.PcdDebugPrintErrorLevel | 0x80000000 |UINT32 | 0x00000006
  ## Indicates the allowable maximum number in extract handler table
  gEfiMdePkgTokenSpaceGuid.PcdMaximumGuidedExtractHandler | 0x10 |UINT32 | 0x00000025

[PcdsFixedAtBuild.IPF]
  ## This flag is used to control the printout of DebugLib
  gEfiMdePkgTokenSpaceGuid.PcdIoBlockBaseAddressForIpf |0x0ffffc00000 | UINT64 | 0x0000000c

[PcdsFixedAtBuild, PcdsPatchableInModule, PcdsDynamic, PcdsDynamicEx] ## This value is used to set the base address of pci express hierarchy
gEfiMdePkgTokenSpaceGuid.PcdPciExpressBaseAddress | 0xE0000000 |UINT64 | 0x0000000a
  ## Default current ISO 639-2 language: English & French
  gEfiMdePkgTokenSpaceGuid.PcdUefiVariableDefaultLangCodes |"engfraengfra" | VOID* | 0x0000001c
  ## Default current ISO 639-2 language: English
  gEfiMdePkgTokenSpaceGuid.PcdUefiVariableDefaultLang | "eng" |VOID* | 0x0000001d
```

**********
**Note:** In the above example, the backslash character is used to show a line
continuation for readability. Use of a backslash character in the actual DEC file
is not permitted.
**********
