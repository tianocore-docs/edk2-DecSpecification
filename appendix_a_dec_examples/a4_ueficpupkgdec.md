<!--- @file
  A.4 UefiCpuPkg.dec

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

## A.4 UefiCpuPkg.dec {#a-4-ueficpupkg-dec}

```ini
### @file UefiCpuPkg.dec
# This Package provides UEFI compatible CPU modules and libraries.
#
# Copyright (c) 2007 - 2016, Intel Corporation. All rights reserved.<BR>
#
# This program and the accompanying materials are licensed and made
# available under the terms and conditions of the BSD License which
# accompanies this distribution.
# The full text of the license may be found at:
# http://opensource.org/licenses/bsd-license.php
#
# THE PROGRAM IS DISTRIBUTED UNDER THE BSD LICENSE ON AN "AS IS" BASIS,
# WITHOUT WARRANTIES OR REPRESENTATIONS OF ANY KIND, EITHER EXPRESS OR
# IMPLIED.
#
##
[Defines]
  DEC_SPECIFICATION = 0x00010019
  PACKAGE_NAME      = UefiCpuPkg
  PACKAGE_UNI_FILE  = UefiCpuPkg.uni
  PACKAGE_GUID      = 2171df9b-0d39-45aa-ac37-2de190010d23
  PACKAGE_VERSION   = 0.2

[Includes]
  Include

[LibraryClasses]
  ## @libraryclass Defines some routines that are generic for IA32
  # family CPU to be UEFI specification compliant.
  ##
  UefiCpuLib|Include/Library/UefiCpuLib.h

[LibraryClasses.IA32, LibraryClasses.X64]
  ## @libraryclass Provides functions to manage MTRR settings on IA32
  # and X64 CPUs.
  ##
  MtrrLib|Include/Library/MtrrLib.h
  ## @libraryclass Provides functions to manage the Local APIC on IA32
  # and X64 CPUs.
  ##
  LocalApicLib|Include/Library/LocalApicLib.h

[Guids]
  gUefiCpuPkgTokenSpaceGuid = { 0xac05bf33, 0x995a, 0x4ed4,{ 0xaa, 0xb8, 0xef, 0x7a, 0xe8, 0xf, 0x5c, 0xb0 }}

#
# [Error.gUefiCpuPkgTokenSpaceGuid]
# 0x80000001 | Invalid value provided.
#
[PcdsFixedAtBuild, PcdsPatchableInModule]
  ## This value is the CPU Local Apic base address, which aligns the
  # address on a 4-KByte boundary.
  # @Prompt Configure base address of CPU Local Apic
  # @Expression 0x80000001 |(gUefiCpuPkgTokenSpaceGuid.PcdCpuLocalApicBaseAddress & 0xfff) == 0
  gUefiCpuPkgTokenSpaceGuid.PcdCpuLocalApicBaseAddress|0xfee00000|UINT32|0x00000001
```
