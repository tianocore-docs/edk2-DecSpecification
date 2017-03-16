<!--- @file
  README.md for EDK II Package Declaration (DEC) File Format Specification

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

<img src="media/TianocoreTitlePageLogo.jpg" width="300" />

### {{ book.title }}

{% if book.draft %}
** DRAFT FOR REVIEW **
{% else %}
** {{ book.version }} **
{% endif %}

** {{ gitbook.time|date('MM/DD/YYYY hh:mm:ss') }} **

{% if book.udkrelease %}
** {{ book.udkrelease }} **
{% endif %}


### Acknowledgements

Redistribution and use in source (original document form) and 'compiled'
forms (converted to PDF, epub, HTML and other formats) with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code (original document form) must retain the
   above copyright notice, this list of conditions and the following
   disclaimer as the first lines of this file unmodified.

2. Redistributions in compiled form (transformed to other DTDs, converted to
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

Copyright (c) 2007-2017, Intel Corporation. All rights reserved.

### Revision History

| Revision   | Revision History                                                                                                          | Date            |
| ---------- | ------------------------------------------------------------------------------------------------------------------------- | --------------- |
| 1.0        | Initial release.                                                                                                          | December 2007   |
| 1.1        | Updated based on errata                                                                                                   | August 2008     |
| 1.2        | Updated based on enhancement requests                                                                                     | June 2009       |
| 1.21       | Updated based on errata and for enhancement requests                                                                      | January 2010    |
|            | Standardized the format for common content.                                                                               |                 |
|            | Added support for @Keyword Doxygen tag                                                                                    |                 |
|            | Added support for @ModuleType Doxygen tags                                                                                |                 |
|            | Added support for @ValidList, @DefaultValue and @ValidRange Doxygen tags for PCDs                                         |                 |
|            | Added PKG_UNI_FILE element to [defines] section                                                                           |                 |
| 1.22       | Errata and grammatical editing                                                                                            | April 2010      |
| 1.22 w/    | Updates:                                                                                                                  | December 2011   |
| Errata A   | Updated to support UEFI version 2.3.1 and updated spec release dates in Introduction                                      |                 |
|            | Clarify UEFI's PI Distribution Package Specification                                                                      |                 |
|            | Standardize Common data definitions for all specifications                                                                |                 |
|            | Grammatical, formatting and spelling changes                                                                              |                 |
|            | Replaced "should" with wording saying that it is                                                                          |                 |
|            | "recommended"                                                                                                             |                 |
|            | Added EBNF for `<Extension>`                                                                                              |                 |
|            | Added scoping rules for Macros, clarified MACRO summary                                                                   |                 |
|            | Added an example of a binary only DEC file                                                                                |                 |
|            | Removed references to system environment variables in the Macros section                                                  |                 |
|            | Specifically state where `<MACROVAL>` can be used, and where it is prohibited;                                            |                 |
|            | specifically state that MACROVAL entries are expanded where they are used;                                                |                 |
|            | clarify that MACROS are only expanded, not evaluated during initial parsing of the DEC file                               |                 |
|            | Added table that shows that every part of a path name can be replaced by a MACROVAL                                       |                 |
|            | Clarify that C data arrays must be byte arrays for PCD value fields; prohibit C format and                                |                 |
|            | Registry Format GUID structures in VOID* PCD value fields                                                                 |                 |
|            | Update non-zero number is True, only 0 is consideered False                                                               |                 |
|            | Prohibit specifying items as architecturally specific and also common                                                     |                 |
|            | Changed `<RegistryGuid>` to `<RegistryFormatGUID>` in                                                                     |                 |
|            | 3.4                                                                                                                       |                 |
|            | Defined `<GuidValue>` as a `<CFormatGUID>` for this release (need to allow registry format in a future release)           |                 |
|            | Update the [Includes], [Guids], [Protocols], [PPIs], [LibraryClasses] and PCD sections to allow an empty section          |                 |
|            | Updated the format for `<QuotedString>`, `<CString>` and `<UnicodeString>`                                                |                 |
|            | Update PATH related EBNF                                                                                                  |                 |
|            | Add `<MacroDefinition>` to [Defines], [Includes] and                                                                      |                 |
|            | `[LibraryClasses] sections`                                                                                               |                 |
|            | Provide rules in 2.2.6 for how macros can be shared between different subsections                                         |                 |
| 1.22 w/    | Updates:                                                                                                                  | June 2012       |
| Errata B   | Added a + after `<Express>` in the DoxComment definition of PCDs, as more than one expression can be                      |                 |
|            | specified in the UEFI PI Distribution Package Specification.                                                              |                 |
|            | Added text describing the use of `<HexDigit>` for error numbers as well as how they are scoped.                           |                 |
| 1.22 w/    | Updates:                                                                                                                  | June 2012       |
| Errata B   | Updated UEFI/PI Spec version in chapter 1.3 to include Errata letters.                                                    |                 |
| (cont.)    | In Section 3.10 modified the optional error number in                                                                     |                 |
|            | DoxComment definitions for PCDs from `<HexDigit>`+ to                                                                     |                 |
|            | <ErrorCode> and defined <ErrorCode> to be of type <NumValUint32>;                                                         |                 |
|            | also added a "\|" after the value to separate the error code from numeric values                                          |                 |
|            | Added AsBuilt entries for Abstract and Description                                                                        |                 |
|            | Clarified that the file must use the DOS end-of-line character sequence, `0x0D 0x0A`                                      |                 |
| 1.22 w/    | Updates:                                                                                                                  | August 2013     |
| Errata C   | Updated UEFI/PI Specification version support in chapter 1                                                                |                 |
|            | Modified examples to correct previous errors                                                                              |                 |
|            | Removed errors from text                                                                                                  |                 |
|            | Updated examples                                                                                                          |                 |
|            | Modified EBNF to prevent using the architectural modifier of common with any other architecture.                          |                 |
|            | Ensure that wording specifically states that the architecture modifiers are not case sensitive.                           |                 |
|            | Add description of PCD processing rules in section 3.10                                                                   |                 |
|            | Allow registry format GUID values in GUIDs, Protocols,                                                                    |                 |
|            | PPIs sections instead of requiring C format GUID values                                                                   |                 |
|            | (which will continue to be allowed)                                                                                       |                 |
|            | The error codes are scoped to the TokenSpaceGUID, not to the PCD                                                          |                 |
|            | Added reference to the EDK II Build Specification for PCD processing rules.                                               |                 |
| 1.24       | `Updates;`                                                                                                                | August 2014     |
|            | Change revision number of this specification from 1.22 to                                                                 |                 |
|            | 1.24                                                                                                                      |                 |
|            | Updated `DEC_SPECIFICATION` to `0x00010017`                                                                               |                 |
|            | Added additional parameter definitions for clarification of the comment content for PCDs                                  |                 |
|            | Added the `PACKAGE_UNI_FILE` entry to the `[Defines]` section                                                             |                 |
|            | Added reserved TianoCore user extension, for                                                                              |                 |
|            | `"ExtraFiles"`                                                                                                            |                 |
|            | Added PCD comment type for # [Error] which is used to map an error code for a given token space to a specific string.     |                 |
| 1.24 w/    | Updates:                                                                                                                  | December 2014   |
| Errata A   | Changed DEC_SPECIFICATION to 0x00010018 and allow specifying it as a decimal, i.e., 1.24.                                 |                 |
|            | Updated specification dates and added two new specifications in section 1.2                                               |                 |
|            | Removed expression EBNF as it has been replaced by the EDK II Expression Syntax Specification.                            |                 |
| 1.24 w/    | Updates:                                                                                                                  | March 2015      |
| Errata B   | - Update link to the EDK II Specifications, fixed the name of the Multi-String .UNI File Format Specification             |                 |
| 1.24 w/    | Updates:                                                                                                                  | August 2015     |
| Errata C   | Clarify that #include statements are not permitted in UNI file specified in the PACKAGE_UNI_FILE entry                    |                 |
| 1.25       | Updates:                                                                                                                  | January 2015    |
|            | Specification revision to 1.25                                                                                            |                 |
|            | Revised WORKSPACE wording for updated build system that can handle                                                        |                 |
|            | packages located outside of the WORKSPACE directory tree (refer to                                                        |                 |
|            | the TianoCore.org EDKII website for additional instructions on setting                                                    |                 |
|            | up a development environment).                                                                                            |                 |
| 1.26       | Reformat for GitBook                                                                                                      | March 2017      |
