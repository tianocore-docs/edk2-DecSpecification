<!--- @file
  Summary

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

# Summary

* [EDK II Package Declaration (DEC) File Format Specification](README.md#edk-ii-package-declaration-dec-file-format-specification)
* [1 Introduction](1_introduction/README.md#1-introduction)
  * [1.1 Overview](1_introduction/11_overview.md#11-overview)
  * [1.2 Terms](1_introduction/12_terms.md#12-terms)
  * [1.3 Related Information](1_introduction/13_related_information.md#13-related-information)
  * [1.4 Target Audience](1_introduction/14_target_audience.md#14-target-audience)
  * [1.5 Conventions Used in this Document](1_introduction/15_conventions_used_in_this_document.md#15-conventions-used-in-this-document)
* [2 DEC File Overview](2_dec_file_overview/README.md#2-dec-file-overview)
  * [2.1 Usage Overview](2_dec_file_overview/21_usage_overview.md#21-usage-overview)
  * [2.2 Declaration File Format](2_dec_file_overview/22_declaration_file_format.md#22-declaration-file-format)
  * [2.3 EDK II DEC Format](2_dec_file_overview/23_edk_ii_dec_format.md#23-edk-ii-dec-format)
  * [2.4 [Defines] Usage](2_dec_file_overview/24_[defines]_usage.md#24-defines-usage)
  * [2.5 [Includes] Usage](2_dec_file_overview/25_[includes]_usage.md#25-includes-usage)
  * [2.6 [Guids] Usage](2_dec_file_overview/26_[guids]_usage.md#26-guids-usage)
  * [2.7 [Protocols] Usage](2_dec_file_overview/27_[protocols]_usage.md#27-protocols-usage)
  * [2.8 [Ppis] Usage](2_dec_file_overview/28_[ppis]_usage.md#28-ppis-usage)
  * [2.9 [LibraryClasses] Usage](2_dec_file_overview/29_[libraryclasses]_usage.md#29-libraryclasses-usage)
  * [2.10 PCD Usage](2_dec_file_overview/210_pcd_usage.md#210-pcd-usage)
  * [2.11 [UserExtensions] Usage](2_dec_file_overview/211_[userextensions]_usage.md#211-userextensions-usage)
* [3 EDK II DEC File Format](3_edk_ii_dec_file_format/README.md#3-edk-ii-dec-file-format)
  * [3.1 General Rules](3_edk_ii_dec_file_format/31_general_rules.md#31-general-rules)
  * [3.2 Package Declaration (DEC) Definitions](3_edk_ii_dec_file_format/32_package_declaration_dec_definitions.md#32-package-declaration-dec-definitions)
  * [3.3 Header Comment Section](3_edk_ii_dec_file_format/33_header_comment_section.md#33-header-comment-section)
  * [3.4 [Defines] Section](3_edk_ii_dec_file_format/34_[defines]_section.md#34-defines-section)
  * [3.5 [Includes] Sections](3_edk_ii_dec_file_format/35_[includes]_sections.md#35-includes-sections)
  * [3.6 [Guids] Sections](3_edk_ii_dec_file_format/36_[guids]_sections.md#36-guids-sections)
  * [3.7 [Protocols] Sections](3_edk_ii_dec_file_format/37_[protocols]_sections.md#37-protocols-sections)
  * [3.8 [PPIs] Sections](3_edk_ii_dec_file_format/38_[ppis]_sections.md#38-ppis-sections)
  * [3.9 [LibraryClasses] Sections](3_edk_ii_dec_file_format/39_[libraryclasses]_sections.md#39-libraryclasses-sections)
  * [3.10 PCD Sections](3_edk_ii_dec_file_format/310_pcd_sections.md#310-pcd-sections)
  * [3.11 [UserExtensions] Sections](3_edk_ii_dec_file_format/311_[userextensions]_sections.md#311-userextensions-sections)
* [Appendix A DEC Examples](appendix_a_dec_examples/README.md#appendix-a-dec-examples)
  * [A.1 EDK II IntelFrameworkPkg Example](appendix_a_dec_examples/a1_edk_ii_intelframeworkpkg_example.md#a1-edk-ii-intelframeworkpkg-example)
  * [A.2 EDK II EmulatorPkg Example](appendix_a_dec_examples/a2_edk_ii_emulatorpkg_example.md#a2-edk-ii-emulatorpkg-example)
  * [A.3 ShellBinPkg.dec](appendix_a_dec_examples/a3_shellbinpkgdec.md#a3-shellbinpkgdec)
  * [A.4 UefiCpuPkg.dec](appendix_a_dec_examples/a4_ueficpupkgdec.md#a4-ueficpupkgdec)
* [Appendix B EDK II Module Types](appendix_b_edk_ii_module_types.md#appendix-b-edk-ii-module-types)
---
* Tables
  * [Table 1 MACRO Usages](3_edk_ii_dec_file_format/32_package_declaration_dec_definitions.md#table-1-macro-usages)
  * [Table 2 EDK II Module Types](appendix_b_edk_ii_module_types.md#table-2-edk-ii-module-types)
