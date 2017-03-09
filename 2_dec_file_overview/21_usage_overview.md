<!--- @file
  2.1 Usage Overview

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

## 2.1 Usage Overview {#2-1-usage-overview}

The DEC file supports EDK II module builds. The file is used to define specific
information that will be shared between different EDK II Modules. There are
eight possible major section types in the DEC file, Defines, Includes,
LibraryClasses, Guids, Protocols, Ppis, PCD and UserExtensions.

Within a DEC file, comments are encouraged, with the hash "#" character
identifying a comment. All text after a comment character must be ignored by
any parsing tool. Comment characters can be at the start of a line, or after a
data element (there must be one or more white space characters between the data
element and the comment character. Examples:

```ini
# this is a comment line
[includes.common] # This is also a valid comment.

[includes.common # This is not valid]
```

The last example is not valid, as the section header data element format is
[text] with the square brackets included as part of the data element.

**********
**Note:** All EDK II DEC files MUST use the forward slash character for all
directory paths specified.
**********

The remainder of this chapter discusses the different section content usage.
