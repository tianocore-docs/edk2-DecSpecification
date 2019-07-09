<!--- @file
  3.2 Package Declaration (DEC) Definitions

  Copyright (c) 2007-2018, Intel Corporation. All rights reserved.<BR>

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

## 3.2 Package Declaration (DEC) Definitions

This section defines content and format of a package declaration file. The
`[Defines]` section must appear before any other section except the `<Header>`
comment block. (The header, when specified, is always the first section of a
DEC file.) The remaining sections may be specified in any order within the DEC
file.

#### Summary

The EDK II Package Declaration (DEC) file has the following format (using the
EBNF).

```c
<EDK_II_DEC> ::= <Header>?
                 <Defines>
                 <Includes>*
                 <LibraryClass>*
                 <Guids>*
                 <Protocols>*
                 <Ppis>*
                 <Pcd>*
                 <UserExtensions>*
```

### 3.2.1 Common Definitions

#### Summary

The following are common definitions used by multiple section types in EDK II
metadata documents. Not all of the definitions below pertain to entries in the
DEC file (for example, `<Expression>` statements are not permitted).

#### Prototype

```c
<Word>                ::= (a-zA-Z0-9_)(a-zA-Z0-9_-.)* Alphanumeric characters
                          with optional period ".", dash "-" and/or underscore
                          "_" characters. A period character may not be
                          followed by another period character.
                          No white space characters are permitted.
<SimpleWord>          ::= (a-zA-Z0-9)(a-zA-Z0-9_-)* A word that cannot contain
                          a period character.
<ToolWord>            ::= (A-Z)(a-zA-Z0-9)* Alphanumeric characters. white
                          space characters are not permitted.
<FileSep>             ::= "/"
<Extension>           ::= (a-zA-Z0-9_-)+ One or more alphanumeric characters.
<File>                ::= <Word> ["." <Extension>]
<PATH>                ::= [<MACROVAL> <FileSep>] <RelativePath>
<RelativePath>        ::= <DirName> [<FileSep> <DirName>]*
<DirName>             ::= {<Word>} {<MACROVAL>}
<FullFilename>        ::= <PATH> <FileSep> <File>
<Filename>            ::= [<PATH> <FileSep>] <File>
<Chars>               ::= (a-zA-Z0-9_)
<Digit>               ::= (0-9)
<NonDigit>            ::= (a-zA-Z_)
<Identifier>          ::= <NonDigit> <Chars>*
<CName>               ::= <Identifier> # A valid C variable name.
<CArrayName>          ::= <Identifier>["["[<Number>]"]"]+ # A valid C variable array name.
<AsciiChars>          ::= (0x21 - 0x7E)
<CChars>              ::= [{0x21} {(0x23 - 0x26)} {(0x28 - 0x5B)}
                          {(0x5D - 0x7E)} {<EscapeSequence>}]*
<DblQuote>            ::= 0x22
<SglQuote>            ::= 0x27
<EscapeSequence>      ::= "\" {"n"} {"t"} {"f"} {"r"} {"b"} {"0"} {"\"}
                          {<DblQuote>} {<SglQuote>}
<TabSpace>            ::= {<Tab>} {<Space>}
<TS>                  ::= <TabSpace>*
<MTS>                 ::= <TabSpace>+
<Tab>                 ::= 0x09
<Space>               ::= 0x20
<CR>                  ::= 0x0D
<LF>                  ::= 0x0A
<CRLF>                ::= <CR> <LF>
<WhiteSpace>          ::= {<TS>} {<CR>} {<LF>} {<CRLF>}
<WS>                  ::= <WhiteSpace>*
<Eq>                  ::= <TS> "=" <TS>
<FieldSeparator>      ::= "|"
<FS>                  ::= <TS> <FieldSeparator> <TS>
<Wildcard>            ::= "*"
<CommaSpace>          ::= "," <Space>*
<Cs>                  ::= "," <Space>*
<AsciiString>         ::= [ <TS>* <AsciiChars>* ]*
<EmptyString>         ::= <DblQuote><DblQuote>
<CFlags>              ::= <AsciiString>
<PrintChars>          ::= {<TS>} {<CChars>}
<QuotedString>        ::= <DblQuote> <PrintChars>* <DblQuote>
<SglQuotedString>     ::= <SglQuote> <PrintChars>* <SglQuote>
<CString>             ::= {<QuotedString>} {<SglQuotedString>}
<NormalizedString>    ::= <DblQuote> [{<Word>} {<Space>}]+ <DblQuote>
<GlobalComment>       ::= <WS> "#" [<TS> <AsciiString>] <EOL>+
<Comment>             ::= "#" <TS> <AsciiString> <EOL>+
<UnicodeString>       ::= "L" {<QuotedString>} {<SglQuotedString>}
<HexDigit>            ::= (a-fA-F0-9)
<HexByte>             ::= {"0x"} {"0X"} [<HexDigit>] <HexDigit>
<HexNumber>           ::= {"0x"} {"0X"} <HexDigit>+
<HexVersion>          ::= "0x" [0]* <Major> <Minor>
<Major>               ::= <HexDigit>? <HexDigit>? <HexDigit>?
                          <HexDigit>
<Minor>               ::= <HexDigit> <HexDigit> <HexDigit> <HexDigit>
<DecimalVersion>      ::= {"0"} {(1-9) [(0-9)]*} ["." (0-9)+]
<VersionVal>          ::= {<HexVersion>} {(0-9)+ "." (0-99)}
<GUID>                ::= {<RegistryFormatGUID>} {<CFormatGUID>}
<RegistryFormatGUID>  ::= <RHex8> "-" <RHex4> "-" <RHex4> "-" <RHex4> "-"
                          <RHex12>
<RHex4>               ::= <HexDigit> <HexDigit> <HexDigit> <HexDigit>
<RHex8>               ::= <RHex4> <RHex4>
<RHex12>              ::= <RHex4> <RHex4> <RHex4>
<RawH2>               ::= <HexDigit>? <HexDigit>
<RawH4>               ::= <HexDigit>? <HexDigit>? <HexDigit>? <HexDigit>
<OptRawH4>            ::= <HexDigit>? <HexDigit>? <HexDigit>? <HexDigit>?
<Hex2>                ::= {"0x"} {"0X"} <RawH2>
<Hex4>                ::= {"0x"} {"0X"} <RawH4>
<Hex8>                ::= {"0x"} {"0X"} <OptRawH4> <RawH4>
<Hex12>               ::= {"0x"} {"0X"} <OptRawH4> <OptRawH4> <RawH4>
<Hex16>               ::= {"0x"} {"0X"} <OptRawH4> <OptRawH4> <OptRawH4>
                          <RawH4>
<CFormatGUID>         ::= "{" <Hex8> <CommaSpace> <Hex4> <CommaSpace>
                          <Hex4> <CommaSpace> "{"
                          <Hex2> <CommaSpace> <Hex2> <CommaSpace>
                          <Hex2> <CommaSpace> <Hex2> <CommaSpace>
                          <Hex2> <CommaSpace> <Hex2> <CommaSpace>
                          <Hex2> <CommaSpace> <Hex2> "}" "}"
<CArray>              ::= "{" {<NList>} {<CArray>} "}"
<NList>               ::= <HexByte>
                          [<CommaSpace> <HexByte>]*
<RawData>             ::= <TS> <Number> [<Cs> <Number> [<EOL> <TS>]]*
<Integer>             ::= {(0-9)} {(1-9)(0-9)+}
<Number>              ::= {<Integer>} {<HexNumber>}
<TRUE>                ::= {"TRUE"} {"true"} {"True"} {"0x1"}
                          {"0x01"} {"1"}
<FALSE>               ::= {"FALSE"} {"false"} {"False"} {"0x0"}
                          {"0x00"} {"0"}
<BoolVal>             ::= {<TRUE>} {<FALSE>}
<BoolType>            ::= {<BoolVal>} {"{"<BoolVal>"}"}
<MACRO>               ::= (A-Z)(A-Z0-9_)*
<MACROVAL>            ::= "$(" <MACRO> ")"
<PcdName>             ::= <TokenSpaceGuidCName> "." <PcdCName>
<PcdFieldName>        ::= <TokenSpaceGuidCName> "." <PcdCName> ["["<Number>"]"]* "." <Field>
<PcdCName>            ::= <CName>
<TokenSpaceGuidCName> ::= <CName>
<PcdFieldEntry>       ::= <PcdFieldName> <FS> <PcdFieldValue> <EOL>
<PcdFieldValue>       ::= {<BoolType>} {<NumValUint8>} {<NumValUint16>} {<NumValUint32>} {<NumValUint64>} {<StringVal>} {<MACROVAL>} {<Expression>}
<UINT8>               ::= {"0x"} {"0X"} (\x0 - \xFF)
<UINT16>              ::= {"0x"} {"0X"} (\x0 - \xFFFF)
<UINT32>              ::= {"0x"} {"0X"} (\x0 - \xFFFFFFFF)
<UINT64>              ::= {"0x"} {"0X"} (\x0 - \xFFFFFFFFFFFFFFFF)
<UINT8z>              ::= {"0x"} {"0X"} <HexDigit> <HexDigit>
<UINT16z>             ::= {"0x"} {"0X"} <HexDigit> <HexDigit> <HexDigit>
                          <HexDigit>
<UINT32z>             ::= {"0x"} {"0X"} <HexDigit> <HexDigit>
                          <HexDigit> <HexDigit> <HexDigit> <HexDigit>
                          <HexDigit> <HexDigit>
<UINT64z>             ::= {"0x"} {"0X"} <HexDigit> <HexDigit>
                          <HexDigit> <HexDigit> <HexDigit> <HexDigit>
                          <HexDigit> <HexDigit> <HexDigit> <HexDigit>
                          <HexDigit> <HexDigit> <HexDigit> <HexDigit>
                          <HexDigit> <HexDigit>
<ShortNum>            ::= (0-255)
<IntNum>              ::= (0-65535)
<LongNum>             ::= (0-4294967295)
<LongLongNum>         ::= (0-18446744073709551615)
<ValUint8>            ::= {<ShortNum>} {<UINT8>} {<BoolVal>}
                          {<CString>} {<UnicodeString>}
<ValUint16>           ::= {<IntNum>} {<UINT16>} {<BoolVal>}
                          {<CString>} {<UnicodeString>}
<ValUint32>           ::= {<LongNum>} {<UINT32>} {<BoolVal>}
                          {<CString>} {<UnicodeString>}
<ValUint64>           ::= {<LongLongNum>} {<UINT64>} {<BoolVal>}
                          {<CString>} {<UnicodeString>}
<NumValUint8>         ::= {<ValUint8>} {"{"<ValUint8>"}"}
<NumValUint16>        ::= {<ValUint16>}
                          {"{"<ValUint8> [<CommaSpace> <ValUint8>]*"}"}
<NumValUint32>        ::= {<ValUint32>}
                          {"{"<ValUint8> [<CommaSpace> <ValUint8>]*"}"}
<NumValUint64>        ::= {<ValUint64>}
                          {"{"<ValUint8> [<CommaSpace> <ValUint8>]*"}"}
<StringVal>           ::= {<UnicodeString>} {<CString>} {<Array>}
<Array>               ::= "{" {<Array>} {[<Lable>] <ArrayVal> 
                           [<CommaSpace> [<Lable>] <ArrayVal>]* } "}"
<ArrayVal>            ::= {<Num8Array>} {<GuidStr>} {<DevicePath>} {<CodeStr>}
<NonNumType>          ::= {<BoolVal>}{<UnicodeString>} {<CString>}
                          {<Offset>} {<UintMac>}
<Num8Array>           ::= {<NonNumType>} {<ShortNum>} {<UINT8>}
<Num16Array>          ::= {<NonNumType>} {<IntNum>} {<UINT16>}
<Num32Array>          ::= {<NonNumType>} {<LongNum>} {<UINT32>}
<Num64Array>          ::= {<NonNumType>} {<LongLongNum>} {<UINT64>}
<GuidStr>             ::= "GUID(" <GuidVal> ")"
<CodeStr>             ::= "CODE(" <CData> ")"
<GuidVal>             ::= {<DblQuote> <RegistryFormatGUID> <DblQuote>}
                          {<CFormatGUID>} {<CName>}
<DevicePath>          ::= "DEVICE_PATH(" <DevicePathStr> ")"
<DevicePathStr>       ::= A double quoted string that follow the device path
                          as string format defined in UEFI Specification 2.6
                          Section 9.6
<UintMac>             ::= {<Uint8Mac>} {<Uint16Mac>} {<Uint32Mac>} {<Uint64Mac>}
<Uint8Mac>            ::= "UINT8(" <Num8Array> ")"
<Uint16Mac>           ::= "UINT16(" <Num16Array> ")"
<Uint32Mac>           ::= "UINT32(" <Num32Array> ")"
<Uint64Mac>           ::= "UINT64(" <Num64Array> ")"
<Lable>               ::= "LABEL(" <CName> ")"
<Offset>              ::= "OFFSET_OF(" <CName> ")"
<ModuleType>          ::= {"BASE"} {"SEC"} {"PEI_CORE"} {"PEIM"}
                          {"DXE_CORE"} {"DXE_DRIVER"} {"SMM_CORE"}
                          {"DXE_RUNTIME_DRIVER"} {"DXE_SAL_DRIVER"}
                          {"DXE_SMM_DRIVER"} {"UEFI_DRIVER"}
                          {"UEFI_APPLICATION"} {"USER_DEFINED"}
                          {"HOST_APPLICATION"}
<ModuleTypeList>      ::= <ModuleType> [" " <ModuleType>]*
<IdentifierName>      ::= <TS> {<MACROVAL>} {<PcdName>} <TS>
<Boolean>             ::= {<BoolType>} {<Expression>}
<EOL>                 ::= <TS> 0x0D 0x0A
<OA>                  ::= (a-zA-Z)(a-zA-Z0-9)*
<arch>                ::= {"IA32"} {"X64"} {"IPF"} {"EBC"} {<OA>}
```

**********
**Note:** When using CString, UnicodeString or byte array format as
UINT8/UINT16/UINT32/UINT64 values, please make sure they fit in the
target type's size, otherwise tool would report failure.
**********
**Note:** LABEL() macro in byte arrays to tag the byte offset of a
location in a byte array. OFFSET_OF() macro in byte arrays that returns
the byte offset of a LABEL() declared in a byte array.
**********
**Note:** When using the characters "|" or "||" in an expression, the
expression must be encapsulated in open "(" and close ")" parenthesis.
**********
**Note:** Comments may appear anywhere within a DEC file, provided they follow
the rules that a comment may not be enclosed within Section headers, and that
in line comments must appear at the end of a statement.
**********

#### Parameters

**_Expression_**

Expression syntax is defined the EDK II Expression Syntax Specification.

**_ExpressionVal_**

An expression that evaluates to a number that fits the datum types of the other
elements, For example, if one of the other elements is a `UINT8`, then the
expression must evaluate to a value that is byte. It is recommended that all
parameters be typecast to `UINT64` values before any operation performed, then
the result can be tested to ensure that the datum size of the result is
correct. PCD names can be used as parameters, and the value of the PCD is used
for evaluation purposes. Any result that exceeds the size of the datum type
must break the build.

**********
**Note:** Circular references (self-references are tight circular references)
must cause a build break.
**********

**_UnicodeString_**

When the `<UnicodeString>` element (these characters are string literals as
defined by the C99 specification: L"string"/L'string', not actual Unicode
characters) is included in a value, the build tools may be required to expand
the ASCII string between the quotation marks into a valid UCS-2 character format
string. The build tools parser must treat all content between the field separators
(excluding white space characters around the field separators) as ASCII literal
content when generating the AutoGen.c and AutoGen.h files.

**_Comments_**

Strings that appear in comments may be ignored by the build tools. An ASCII
string matching the format of the ASCII string defined by `<UnicodeString>`
(L"Foo" for example,) that appears in a comment must never be expanded by any
tool.

**_CFlags_**

CFlags refers to a string of valid arguments appended to the command line of
any third party or provided tool. It is not limited to just a compiler
executable tool. MACRO values that appear in quoted strings in CFlags content
must not be expanded by parsing tools.

**_OA_**

Other Architecture - One or more user defined target architectures, such as ARM
or PPC. The architectures listed here must have a corresponding entry in the
EDK II meta-data file, _Conf/tools_def.txt_.

**_FileSep_**

FileSep refers to either the back slash "\" or forward slash "/" characters
that are used to separate directory names. All EDK II DEC files must use the
"`/`" forward slash character when specifying the directory portion of a
filename. Microsoft operating systems, that normally use a back slash character
for separating directory names, will interpret the forward slash character
correctly.

**_CArray_**

All C data arrays used in PCD value fields must be byte arrays. The C format
GUID style is a special case that is permitted in some fields that use the
`<CArray>` nomenclature.

**_CData_**

All C data used in PCD value CODE syntax can be C style value to initialize 
C structure or Array in C source code.

**_EOL_**

The DOS End Of Line: "0x0D 0x0A" character sequence must be used for all EDK II
meta-data files. All *Nix based tools can properly process the DOS EOL
characters. Microsoft based tools cannot process the *Nix style EOL characters.

### 3.2.2 MACROs

Use of MACRO statements is optional.

#### Summary

Macro statements are characterize by a `DEFINE` line. Macro statements in DEC
files are only permitted to describe a path (shortcut name). If the Macro
statement is within the `[Defines]` section, then the Macro is common to the
entire file, with local definitions taking precedence (if the same MACRO name
is used in subsequent sections, then the MACRO value is local to only that
section.)

Macro statements in comments must also be ignored by parsing tools.

Macros may not be referenced before they are defined.

A previously defined macro is permitted to be used as $(MACRO) in the right
side of a different Macro (in the value) statement.

Macro names must not use the name of the tokens defined in this file, such as
PACKAGE_GUID is defined as a token in the `[Defines]` section of this document,
and therefore cannot be used as the `<MACRO>` name in a `<MacroDefinition>`
statements, `<MACRO>` variable.

If the tools encounters a macroval, as in $(MACRO), that is not defined, the
build tools must break.

#### Prototype

```c
<MacroDefinition> ::= <TS> "DEFINE" <TS> <MACRO> <Eq> [<Value>] <EOL>
<Value>           ::= {<PATH>} {<Filename>}
```

#### Examples

```ini
DEFINE GEN_SKU_DIR = MyPlatformPkg/GenPei
DEFINE SKU1_Dir = MyPlatformPkg/Sku1/Pei
DEFINE LIB = Include/Library
DEFINE PROTO_HDRS = $(LIB)/Protocol
```

#### Parameters

**`<PATH>`**

Any part of the path line can be replaced by a MACRO as shown in the following
table.

###### Table 1 MACRO Usages

| MACRO DEFINITION                        | MACRO USAGE                 |
| --------------------------------------- | --------------------------- |
| DEFINE MY_MACRO = test1                 | $(MY_MACRO)/test2/test3.inf |
| DEFINE MY_MACRO = test1/                | $(MY_MACRO)test2/test3.inf  |
| DEFINE MY_MACRO = test3.inf             | test1/test2/$(MY_MACRO)     |
| DEFINE MY_MACRO = test3                 | test1/test2/$(MY_MACRO).inf |
| DEFINE MY_MACRO = test1/test2/test3.inf | $(MY_MACRO)                 |

### 3.2.3 Conditional Statements

The conditional statements are not permitted anywhere within the DEC file.

### 3.2.4 !include Statement

The !include statement is not permitted in an EDK II DEC file.

### 3.2.5 !error Statement

The `!error` statement is not permitted in an EDK II DEC file.

### 3.2.6 Special Comment Blocks

This section defines special format comment blocks that contain information
about this package. These command blocks are not required.

The _UEFI Distribution Package Specification_ states the for a given PCD Token
Space, Error numbers must be unique. Since there may be multiple PCD that may
have identical error types, an error number with an associated error message
may be shared. The syntax described here can be used by tools to map these
error numbers by a token space GUID C name. These comment blocks must appear
before content might be used (in later sections of the DEC file).

#### Prototype

```c
<ErrNoBlock> ::= <TS> "#" <EOL>
                 <TS> "#" <MTS> "[Error." <TSpaceGuidCName> "]" <EOL>
                 [<TS> "#" <MTS> <UINT32> <FS> <AsciiString> <EOL>]+
                 <TS> "#" <EOL>+
```

#### Example

```ini
#
# [Error.gEfiIntelFrameworkModulePkgTokenSpaceGuid]
# 0x80000001 | Invalid value provided.
# 0x80000002 | Reserved bits must be set to zero.
#
```
