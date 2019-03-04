<!--- @file
  2.6 [Guids] Usage

  Copyright (c) 2007-2019, Intel Corporation. All rights reserved.<BR>

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

## 2.6 [Guids] Usage

This is an optional section.

This section is used to define the GUID Value for Guid C Names.

The section tag modifier, `Private`, is used to restrict the EDK II build
system by preventing references to content in these sections from being used by
modules outside of the package.

This section uses one of the following section definitions:

```ini
[Guids]

[Guids.common]

[Guids.common.Private]

[Guids.IA32]

[Guids.IA32.Private]

[Guids.X64]

[Guids.X64.Private]

[Guids.EBC]

[Guids.EBC.Private]
```

Architectural sections may also be combined, as in:

```ini
[Guids.IA32, Guids.X64]

[Guids.IA32.Private, Guids.X64.Private]
```

Format for the entries in this section is two fields with an equal "="
character separating the fields as shown below.

`GuidCName = {C Format Guid Value} # Comment`

The Comment section can be used to identify the list of supported module types.
