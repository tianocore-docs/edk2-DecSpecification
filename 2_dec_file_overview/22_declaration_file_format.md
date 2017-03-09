<!--- @file
  2.2 Declaration File Format

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

## 2.2 Declaration File Format {#2-2-declaration-file-format}

This section covers the content for the EDK II DEC files.

### 2.2.1 Section Entries {#2-2-1-section-entries}

To simplify parsing, the EDK II meta-data files continue using the INI format.
This style was introduced for EDK meta-data files, when only the Windows tool
chains were supported. It was decided that for compatibility purposes, that INI
format would continue to be used. EDK II formats differ from the defacto format
in that the semicolon ";" character cannot be used to indicate a comment.

Leading and trailing space/tab characters must be ignored.

Duplicate section names must be merged by tools.

This declaration file consists of sections delineated by section tags enclosed
within square [] brackets. Section tag entries are case-insensitive. The
different sections and their usage are described below. The text of a given
section can be used for multiple section names by separating the section names
with a comma. For example:

 `[Includes.X64, includes.IPF]`

The content below each section heading is processed by the parsing utilities in
the order that they occur in the file. The precedence for processing these
architecture section tags is from right to left, with sections defining an
architecture having a higher precedence than a section which uses common (or no
architecture extension) as the architecture.

It is not permissible to have an architectural modifier in the same section
tag as an entry with the common architectural modifier. Specifying entries as
only for IA32 and also valid for all other architectures (`[Includes.common,
Includes.IA32]`) is not valid.

**********
**Note:** Content such as filenames, directory names, MACROs and C variable
names within a section IS case sensitive. `IA32`, `Ia32` and `ia32` within a
section are processed as separate items. `IA32`, `Ia32` and `ia32` within a
section in a directory or file name are processed as separate items. (Refer
to Naming Conventions below for more information on directory and/or file
naming.)
**********

Sections are terminated by the start of another section or the end of the file.

Comments are not permitted between square brackets of a section specifier.

Duplicate sections (two sections with identical section tags) will be merged by
tools, with the second section appended to the first.

If architectural modifiers are used in the section tag, the section is merged
by tools with content from common sections (if specified) with the
architectural section appended to the first, into an architectural section. For
example, given the following:

```ini
[Includes]
  Includes/

[Includes.IA32]
  Includes/Ia32

[Includes.X64]
  Includes/X64
```

After the first pass of the tools, when building the module for IA32, the
source files will logically be:

```ini
[Includes.IA32]
  Includes/
  Includes/Ia32
```

When building the module for X64, the source files will logically be:

```ini
[Includes.X64]
  Includes/
  Includes/X64
```

The `[Defines]` section tag prohibits use of architectural modifiers. All other
sections can specify architectural modifiers.

### 2.2.2 Comments {#2-2-2-comments}

The hash `#` character indicates comments in the Declaration (DEC) file. In
line comments terminate the processing of a line. In line comments must be
placed at the end of the line, and may not be placed within the section
(`[`,`]`) tags.

Only `gPkgTSGuid.PcdFoo|TRUE|BOOLEAN|0x00000015` in the following example is
processed by tools; the remainder of the line is ignored:

`gPkgTSGuid.PcdFoo|TRUE|BOOLEAN|0x00000015 # EFI_COMPUTING_UNIT_MEMORY`

**********
**Note:** Blank lines and lines that start with the hash # character must be
ignored by tools.
**********

Hash characters appearing within a quoted string are permitted, with the string
being processed as a single token. The following example must handle the quoted
string as single element by tools.

`UI = "# Copyright 2007, No Such, LTD. All rights reserved."`

The line extension character, "\", cannot be used to extend a comment. Like the
comment character stops processing of a line, comments are always terminated by
the end of line. Doxygen tags are permitted in comment blocks preceding
individual GUID, Protocol, PPI and PCD entries. These tags are used as
containers for content required by the UEFI Packaging specification, and may
also be used by tools. Each section will define the valid Doxygen tags which
apply.

If a hash "`#`" character is required in a value field, the value field must be
encapsulated by double quotation marks.

#### `<CommentBlock>` Entries

Various elements in the DEC file have a recommended format for comment
information regarding the header files, module types an item supports and other
information. These special comment blocks are processed by tools used to create
a distribution package of the code that conforms to the UEFI Distribution
Package (UDP) Specification. Tools used to install a distribution package that
conforms to the UDP must add appropriate type information in these comment
blocks. The comment block formats are specified in chapter 3 of this document.

The general format of these comment blocks in the `[Guids]`, `[Protocols]` and
`[Ppis]` sections is:

```ini
  "##" Path/To/HeaderFile.h
  GUID_C_Name = <GUID> ["##" <ModuleTypeList>] ["#" <HelpText>]
```

#### Example

```
  ## Include/Guid/GlobalVariable.h
  gEfiGlobalVariableGuid = {0x8BE4DF61,0x93CA,0x11D2,{0xAA,0x0D,0x00,0xE0,0x98,0x03,0x2B,0x8C}}
  # Include/Protocol/DebugPort.h
  gEfiDebugPortDevicePathGuid = {0xEBA4E8D2, 0x3858, 0x41EC,{0xA2, 0x81, 0x26, 0x47, 0xBA, 0x96, 0x60, 0xD0}}
  #
  # UEFI_DRIVER
  # Guid for EFI_DISK_INFO_PROTOCOL.Interface to specify Ide interface.
{0xAF, 0x17, 0x61, 0x02, 0x87, 0x18, 0x8D, 0xEC}} ## DXE_DRIVER, UEFI_DRIVER

} ## SMM_CORE, DXE_SMM_DRIVER
```

**********
**Note:** In the above example, the line has been extended so that the field is
continued to the last line (the "}" character) so that the comment at the end of
the line can be processed correctly by the _Intel(R) UEFI Packaging Tool_.
**********

Additional informational help text is also defined in the `<CommentBlock>` tag.
The format defined for comment blocks that are at the end of lines listed in
all of the examples must not continue on following lines. If the
`<CommentBlock>` information is long, the information is allowed to be split
into multiple comment lines that immediately precede the element. For example:

```ini
  ## Include/Guid/DebugAgentGuid.h
  # PEIM, DXE_DRIVER, DXE_SMM_DRIVER
  # MdeModule Debug Agent GUID
  gEfiDebugAgentGuid = {0x865a5a9b,0xb85d,0x474c,{0x84,0x55,0x65,0xd1,0xbe,0x84,0x4b,0xe2}}
```

Unlike GUIDs, Protocols and PPIs, the PCD entries are not associated with a
header file, so the general format is:

```ini
## CommentBlock
[# CommentBlockCont]
  Entry [<ShortSingleCommentBlock>]
```

#### Example

```ini
  # DXE_DRIVER, DXE_SMM_DRIVER
  # S3 support
  # The PCD is used to specify memory size with page number for a
  # pre-allocated ACPI NVS memory to be used by PEI in S3 phase.
  # The default size 32K.
  # When changing the value of this PCD, the platform developer should
  # make sure the memory size is large enough to meet PEI requirement in
  # S3 phase.
  gEfiTModPkgTokenSpaceGuid.PcdS3AcpiReservedMemorySize |0x8000 | UINT32 | 0x30000007
```

### 2.2.3 Valid Entries {#2-2-3-valid-entries}

Processing of the line is terminated if a comment is encountered or by the end
of the line. Entries in this file (not comments) are not allowed to span
multiple lines.

Items in quotation marks are treated as a single token and have the highest
precedence. All expressions must be written using in-fix notation (operators
are written between the operands). Parenthesis surrounding groups of operands
and operators are recommended to determine the order in which operations are to
be performed to remove ambiguity. All other processing occurs from left to
right.

In the following example, B - C is processed first, then result is added to A
followed by adding 2; finally 3 is added to the result.

`(A + (B - C) + 2) + 3`

In the next example, A + B is processed first, then C + D is processed and
finally the two results are added.

`(A + B) + (C + D)`

Space and tab characters are permitted around field separators.

### 2.2.4 Naming Conventions {#2-2-4-naming-conventions}

The EDK II build infrastructure is supported under Microsoft* Windows*, Linux*
and MAC OS/X* operating systems. As a result of multiple environment support,
all directory and file names must be treated as case sensitive.

* The use of special characters in directory names and file names is restricted
  to the dash, underscore, and period characters, respectively "-", "_", and
  ".".

* Period characters must not be followed by another period character. File and
  Directory names must not start with "./", "." or "..".

* Directory names and file names must not contain space or tab characters.

* Directory Names must only contain alphanumeric, underscore, dash and period
  characters (period characters must not be sequential) and it is recommended
  that they start with an alpha character.

* All files must reside in the directory containing the DEC file or in
  sub-directories of the directory containing the DEC file.

* It is recommended that filenames start with an alpha character.

* All EDK II directories that are architecturally dependent must use a name
  with only the first character capitalized followed by lower case characters
  or numeric characters. Ia32, Ipf, X64 and Ebc are valid architectural
  directory names. IA32, IPF and EBC are not acceptable directory names, and
  may cause build breaks. From a build tools perspective, an IA32 directory
  name is not equivalent to Ia32 or ia32.

* When an architecture is used in a directory name, the directory content must
  be listed in a section that uses the matching architecture modifier. If a
  common section contains filenames that have directories with architecture
  modifiers, the file will be processed for all architectures, not just the
  architecture specified in the directory name.

* Absolute paths are not permitted in EDK II DEC files. All paths specified are
  relative to the EDK II package directory containing the DEC file.

Space Characters in filenames: The build tools must be able to process the tool
definitions file: tools_def.txt (describing the location and flags for compiler
and user defined tools), which may contain space characters in paths on
Windows* systems.

The EDK II Coding Style specification covers naming conventions for use within
C Code files, and as well as specifying the rules for directory and file names.
This section is meant to highlight those rules as they apply to the content of
the DEC files.

Architecture keywords (IA32, IPF, X64 and EBC) are used by build tools and in
metadata files for describing alternate threads for processing of files. These
keywords must not be used for describing directory paths. Additionally,
directory names with architectural names (Ia32, Ipf, X64 and Ebc) do not
automatically cause the build tools or meta-data files to follow these
alternate paths. Directories and Architectural Keywords are similar in name
only.

For clarity, this specification will use all upper case letters when describing
architectural keywords, and the directory names with only the first letter in
upper case.

All directory paths within EDK II DEC files must use the "/" forward slash
character to separate directories as well as directories from filenames.

#### Example

`C:/Work/Edk2/edksetup.bat`

File names must also follow the same naming convention required for
directories. No white space characters are permitted. The special characters
permitted in directory names are the only special characters permitted in file
names.

Absolute paths or relative paths outside of the directory the DEC file resides
must not be used when specifying directories or filenames in any section of the
DEC file.

### 2.2.5 !include Statements {#2-2-5-include-statements}

The `!include` statement is NOT permitted in DEC files.

### 2.2.6 Macro Statements {#2-2-6-macro-statements}

Macro statements are permitted in the EDK II DEC files. Macro statements assign
a Value to a Variable Name, and are only valid during the processing of the DEC
specifying the value. Macro statements are local to the file - global macro
values are not permitted. Use of system environment variables is also
prohibited in value fields; they may appear in comments, however during the
build, comment content is ignored. This decision was made in order to support
UEFI's PI Distribution Package Specification requirements.

Macro Definition statements that appear within a section of the file (other
than the `[Defines]` section) are scoped to the section they are defined in. If
the Macro statement is within the `[Defines]` section, then the Macro is common
to the entire file, with local definitions taking precedence (if the same MACRO
name is redefined in subsequent sections, then the MACRO value is local to only
that section).

Any defined MACRO definitions will be expanded by tools when they encounter the
entry in the section. All macros are local to the DEC file (this is a
requirement for UEFI distribution of source and binary content).

The macro statements are positional, in that only statements following a macro
definition are permitted to use the macro - a macro cannot be used before it
has been defined.

Macros defined the `[Defines]` section are common to all sections.

Macros defined in a common architectural section may be used in the
architecturally modified sections of the same section type. Macros defined in
architectural sections cannot be used in other architectural sections, nor can
they be used in the common section.

Macro expansion is done at the time the macro is used.

#### Example

```ini
[LibraryClasses.common]
  # Can use $(MDE)
  # Cannot use either $(SMM) or $(SAL)
  DEFINE MDE = Include/Library
  BaseLib|$(MDE)/BaseLib.inf

[LibraryClasses.X64, LibraryClasses.IA32]
  # Can use $(MDE) and local $(SMM)
  # Cannot use $(SAL)
  DEFINE SMM = Include/Library SmmLib|$(SMM)/SmmLib.h

[LibraryClasses.IPF]
  # Can use $(MDE) from the common section and local $(SAL)
  # Cannot use $(SMM)
  DEFINE SAL = Include/Library
  SalLib|$(SAL)/SalLib.h
  PalLib|$(MDE)/PalLib.h
```

In the previous example, the directory and filename for a library instance is
the header file that can be used for all modules that provide the library
implementations that conform to the definitions in the file.

### 2.2.7 PCD Names {#2-2-7-pcd-names}

Unique PCD names are defined as PCD Token Space Guid C name and the PCD C name
separated by a period "." character:

`PcdTokenSpaceGuidCName.PcdCName`

The PCD's Name `(PcdName)` is defined as PCD Token Space Guid C name and the
PCD C name separated by a period "`.`" character. PCD C names are used in C
code and must follow the C variable name rule.

### 2.2.8 Conditional Directive Statements (!if...) {#2-2-8-conditional-directive-statements-if}

Conditional statements are NOT permitted in EDK II DEC files.
