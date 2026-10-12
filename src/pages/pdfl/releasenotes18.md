---
title: PDFL SDK Release Notes v. 18.x
description: PDFL SDK Release Notes v. 18.x for the PDFL SDK.
contributors: Ben Rogers (Adobe Content Engineering)
source: https://github.com/Adobe-Print/Documentation_PDFL_Acrobat_SDK/blob/master/docbuild/pdfl/releasenotes18.rst
---

<a id="release-notes-v-18-x"></a>
# Release Notes v. 18.x

<a id="february-23-2022"></a>
## 18.0.5, February 23, 2022

<a id="changes-for-this-release"></a>
### Changes for this release

- ICU Libraries have been upgraded to the latest version: 67.1.
- The `PDPageDrawContentsToMemoryEx` API can now process files at high resolutions
- The transparency flattening process is improved exponentially.
- MissingWidth in the font descriptor dictionary is now able to handle fixed type values which enable in merging PDFs with different fonts without garbling the text.
- `PDPageSetPDEContent` API updates fix text-related issues: including text duplication, garbled text, shifted strings, and so on.

<a id="fixed-bugs"></a>
### Fixed bugs

- 4176533: Transparency flattening is very slow with PDFL 18.
- 4176526: Internal links don’t work after PDDocInsertPages()
- 4176520: PDPageGetCosObj() returns null if multiple count entries present
- 4176518: Text is lost after merging specific PDFs with different fonts
- 4176502: Text Duplication after processing specific PDF
- 4176515: Text is garbled after calling PDPageSetPDEContent
- 4176479: String gets shifted after processing specific PDF
- 4176536: PDPageDrawContentsToMemoryEx() throws exception at higher resolution

<a id="known-issues-and-bugs"></a>
### Known issues and bugs

- PDF/A-b conversion fails if embedded fonts have empty files: Until PDFL SDK 15.0.6, text marked with rendering mode 3 was deleted from a PDF when it was converted to PDF/A-1b. While this problem has been fixed in 15.0.7, the conversion fails if the embedded fonts have empty font files.
- Loss of text in Type 3 fonts during PDF/A and PDF/X conversion: This is a known issue with PDF files having images or path elements inline with text in Type 3 fonts. The text following the inline element is lost during conversion to the PDF/A or the PDF/X format.
- Stamp annotations missing on conversion to PDF/X: If the value of `Rect` lies outside of the BleedBox, on conversion to the PDF/Xformat stamp annotations in the source are not retained in the resultant PDF. **Note**: `Rect` is the annotation rectangle which defines the location of the annotation on the page in default user space units.

<a id="version-18-0-4-august-7-2020"></a>
## Version 18.0.4, August 7, 2020

Major updates in PDFL SDK XVIII release include:

- ICU libraries have been upgraded to the latest version i.e. 64.2.
- All files are now in.cpp extension. With this change, default compiler settings would work to build the entire PDFL. For backward compatibility, we have not removed.c files.
- PDEFormIsLeadingSet API has been added which checks whether the Text Leading (TL) is set in the graphics state or not.
- Parameter ‘pathDPI’ of PDFlattenRec structure has been enabled which affects the degree of flattening Beziers..
- Location of resources for Type3 fonts are aligned with PDF specification.

<a id="version-18-0-3"></a>
## Version 18.0.3

- Support for UTF-8 character encoding as per PDF 2.0 specification has been added.
- From 18.0.3 onwards, Mac Builds are BAST V3 signed following the Apple Notarization Guidelines.

<a id="version-18-0-2"></a>
## Version 18.0.2

- Support for new era glyph - Updated CMaps and Font resources to support Japanese new era characters.
- Support for Windows 7 has been discontinued.
- PDEExtGStateGetSoftMaskMatrix and PDEExtGStateSetSoftMaskMatrix APIs have been added to get and set the soft mask matrix in external gstate respectively.

<a id="version-18-0-1"></a>
## Version 18.0.1

- Two new APIs PDEFormGetLeading and PDEFormSetLeading have been added to get and set respectively the Leading in the parent of Form.
- A new parameter weight of type unsigned integer is added in PDEFontAttrs structure.

<a id="version-18-0"></a>
## Version 18.0

- Support for PDF 2.0 file version - PDF Library can now read and edit files with PDF 2.0 version. Two new APIs PDDocGetAdobePDFVersion and PDDocSetAdobePDFVersion have been introduced in this release for getting and setting new PDF versions respectively.
- Support of Black point compensation (BPC) flag - UseBlackPtComp has been added to the graphic state parameter dictionary. Two new APIs PDEExtGStateGetBPC and PDEExtGStateSetBPC have been added to get and set the UseBlackPtComp flag value respectively.
- Support for Page-Level Output Intent - User can set Output Intent for each Page as well. Two new APIs PDDocColorConvertEmbedOutputIntentEx and PDPageColorConvertEmbedOutputIntent have been added to support new output intent subtypes added in PDF 2.0. Appropriate subtype like GTS\_PDFX, GTS\_PDFA, and ISO\_PDFE1 can be added to the output profile as per the value passed to these APIs.
- If output intent already exists at Doc/Page level, then new output intent gets added to the existing one.
- PDColorConvertPDEElementEx2 API has been added to support conversion to a PDEElement to the supplied color space.
- PDSysEncodingSetIsUTF16 API has been added to check if an encoding is UTF-16 or not.
- In PDF 2.0, versioning model has been changed and now support 2-part version system which is a combination of Major and Minor versions like Major.Minor as compared to 3-part version system Major.Minor.ExtensionLevel in PDF 1.7.
- Updated Decryption Sample to showcase the support for Unicode based password protected PDFs.
- Updated CMaps and mapping resources to support Adobe-Japan1-7 fonts.
- Full compatibility with Acrobat.
- The current release includes the following changes to the supported platforms. In version 18.0 and later:
  - Windows 10 is the primary operating system for Windows platforms.
  - The supported compiler for all Windows platforms is Visual Studio 2017(version 15.3.3).
  - Mac OS X 10.12 (Sierra) is supported on 64-bit platforms.
  - The supported operating system for Linux platforms is CentOS 7.3, with the Clang 3.9.1 compiler. The glibc version to be used is 2.17.
  - The supported compiler for all Macintosh platforms is Xcode Developer Tools 8.2.1.
  - Support for the following platforms has been discontinued:
    - Red Hat Enterprise Linux 7 on 32-bit platform.
    - Red Hat Enterprise Linux 7 on 64-bit platform.
    - Mac OS X 10.9 (Mavericks) on 64-bit platform.
