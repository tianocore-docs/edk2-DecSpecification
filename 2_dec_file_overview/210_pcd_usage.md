<!--- @file
  2.10 PCD Usage

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

## 2.10 PCD Usage

These are optional sections.

These sections are used to declare basic information about PCDs. Refer to the
_PI Specification_ as well as the EDK II Platform Configuration Database
Infrastructure Descriptions document for additional information regarding PCDs.
Only the DynamicEx access methods are defined in the _PI Specification_; the
remaining types are specific to this EDK II Build System.

Generally, PCDs using the FixedAtBuild and PatchableInModule access methods are
used to set static configuration elements that can be determined at build time
(or modified prior to inserting a module into a flash image). PCDs using the
Dynamic and DynamicEx access methods are used for configuration knobs that may
be manipulated by setup screens (or other methods) during the boot process.

Information in this section is used to create entries in the `AutoGen.c` and
`AutoGen.h` files for EDK II modules.

The PCD is used for configuration when the PCD value is produced and consumed
by drivers during execution, the value may be user configurable from setup or
the value is produced by the platform in a specified area. It is associated
with modules that are released in source code. The PatchableInModule and
DynamicEx PCD access methods are associated with modules that are released as
binary only modules. The FeatureFlag PCD is used to enable some code paths.

PCDs are usually defined by a specification that defines the name, token
number, token space GUID and datum type. A default value and valid access
methods may also be given in the industry specification. If a developer needs
to create a new PCD, they can, following the conventions listed in the PI
specification. Only PCDs that will be shared between multiple users need to be
defined in published architectural specs. If a PCD is only going to be used by
a single organization, then a new PCD can be created within the organization,
keeping all modules that use the PCD internal to the organization.

PCDs are defined with C structure type name. It means this PCD has the layout 
of C strucutre. PCD value can be assigned by its structure field. 

Every PCD (`PcdName`) is identified by a two part definition - the PCD's Token
Space Guid CName and the PCD CName. These two parts are separated by a period
"`.`" character. Together, these two parts make up the first field in a PCD
Entry. When the AutoGen code is created, the value of the Token Space GUID and
the token value are used to uniquely identify the PCD.

Refer to the PCD Sections definition later in this document for a complete
description of this section and its contents.

This section resembles one of the following section definitions:

```ini
[PcdsFeatureFlag]

[PcdsFeatureFlag.common]

[PcdsFixedAtBuild.IA32]

[PcdsPatchableInModule.X64]

[PcdsDynamic.IPF]

[PcdsDynamicEx.EBC]
```

The EDK II build system supports five PCD access methods: FeatureFlag,
FixedAtBuild, PatchableInModule, Dynamic and DynamicEx. These indicate access
methods for get/set operations. The PcdsDynamicEx method is defined by the _PI
Specification_. A PCD may be listed under multiple PCD access method sections,
except FeatureFlag PCDs. Listing a PCD in multiple sections indicates that
modules have been coded to use in any one of the non‐FeatureFlag access methods.

It recommended that modules use either the FeatureFlag PCD or use the flexible
(INF file's [Pcd] section) for access. If a module is coded for only one type
of access, such as FixedAtBuild, then it can only use the FixedAtBuild access
method in a platform, and therefore, it must not be listed in any other section
types in this file. Likewise, if the module is coded as a DynamicEx form, then
it can only be listed in the DynamicEx section. If a module is coded for the
Dynamic access method, then the platform integrator would be able to choose how
they want to use the PCD. It can then be specified to use either a
FixedAtBuild, PatchableInModule, Dynamic or DynamicEx access method in the
platform description (DSC) file. Using the Dynamic access method in module code
is the most flexible method, as platform integrators may chose a to use a
different type (such as fixed) for a given platform without modifying the
module's INF file or the code for the module.

The EDK II build tools will automatically generate a const definition for the
FeatureFlag and FixedAtBuild PCDs, while the PatchableInModule and both Dynamic
forms will have a volatile definition generated.

The two recommended access methods that are commonly specified in modules INF
files are: FeatureFlag (list in [FeaturePcd] sections) and Dynamic (listed in
[PCD] sections). For modules that will be distributed as binary modules, PCDs
in those modules that will be exposed by the binary must use PatchableInModule
or DynamicEx access mehtods.

It is recommended that PCDs be listed in PcdsFixedAtBuild,
PcdsPatchableInModule, PcdsDynamic and PcdsDynamicEx sections in the DEC file.

Module developers need to check what sections a specific PCD is listed in, in
order to code the module using the correct access type. Also, PCDs may have
different default values for different architectures.

The format for entries in the PCDs sections is four fields, with a pipe "|" character as the field separator, as shown below:

```ini
  # Comment
  TokenSpaceGuidCname.PcdCname|DefaultValue|DatumType|Token
```

The Comment section can be used to identify the list of supported module types
as well as to contain conditional test statements for acceptable values.

Default values listed in this file can be overridden by the default values
specified in INF files (provided all INF files use the same value for a PCD) or
by values specified in the DSC or FDF files of a platform.

The Token value is used programmatically in code. PCD Token numbers must be
unique to a Token Space GUID name space. The two PCD drivers use the token
number to locate a PCD's value.

#### FeatureFlag PCDs

FeatureFlag PCDs can only be listed in FeatureFlag access method sections in
the EDK II meta‐data files. The datum type of a FeatureFlag PCD must be BOOLEAN.

#### VOID* PCD DatumType

The declarations in this file do not include a maximum datum size for the
"`VOID`*" PCDs. It is recommended that the platform integrator allocate space
for the content, rather than depend on letting tools compute the maximum value
based on the greater of the lengths from the values in the DEC, DSC and INF
files. However, if the platform integrator does not specify a size in the DSC
file, the data size is calculated by the tools to be the greatest length of all
values specified for this PCD listed in the DEC, INF, FDF and DSC files.

If PCD is defined with C structure type name, it will also be VOID* PCD.