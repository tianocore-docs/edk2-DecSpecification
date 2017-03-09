<!--- @file
  3.1 General Rules

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

## 3.1 General Rules {#3-1-general-rules}

The general rules for EDK II INI style documents follow.

**********
**Note:** Path and Filename elements within the DEC are case-sensitive in order
to support building on UNIX style operating systems. Additionally, names that
are C variables or used as a macro are case sensitive. Other elements such as
section tags or hex digits, in the DEC file are not casesensitive. The use of
"..", "../" and "./" in paths and filenames is strictly prohibited.
**********

* Only one DEC file is permitted per directory.

* Text in section tags (text within square brackets) is not case sensitive.

* A section terminates with either another section definition or the end of the
  file.

* Entries terminate with either a comment or the end of line character sequence.

* To append comment information to any item, the comment must start with a hash
  "#" character.

* All comments terminate with the end of line character sequence.

* Any comment not associated with a defined comment format is considered a
  global comment.

* Global comments must be separated from formatted comments with a blank line.

* Comment lines cannot be extended using the line extension character.

* Field separators for lines that contain more than one field are pipe "|"
  characters. This character was selected to reduce the possibility of having
  the field separator character appear in a string, such as a filename or text
  string.

**********
**Note:** The only notable exception is the PcdName which is a combination of
the
**********

_PcdTokenSpaceGuidCName and the PcdCName that are separated by the period "."
character. This notation for a PCD name is used to uniquely identify the PCD._

* When processing numeric values, either integer or hex, leading zeros
  specified in the entry may be ignored. For example, 0x00000000000000000000001
  can be a valid value for a `UINT8` data type, as the actual value is 1.

### 3.1.1 Backslash {#3-1-1-backslash}

The backslash "`\`" character is used in this document when an example entry
cannot fit between the margins of this file. It must not be used in the DEC
file to extend an entry.

### 3.1.2 White space characters {#3-1-2-white-space-characters}

Whitespace (space and tab) characters are permitted between token and field
separator

January 2016

elements for all entries.

Whitespace characters are not permitted between the PcdTokenSpaceGuidCName and
the dot, nor are they permitted between the dot and the PcdCName.

### 3.1.3 Paths for filenames {#3-1-3-paths-for-filenames}

Note that for specifying the path for a file name, if the path value starts
with a dollar sign "$" character, a local MACRO is being specified. White space
characters are not permitted in path names.

**********
**Caution:** The use of "..", "./" and "../" in a path element is prohibited.
**********

For all EDK II DEC files, the directory path must use the forward slash
character for separating directories. For example, MdePkg/Include/ is Valid.

Unless otherwise noted, all file names and paths must be relative to the
directory where the DEC file is located.
