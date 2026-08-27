---
title: Acrobat SDK Home
description: Home page for the Acrobat SDK.
contributors: Ben Rogers (Adobe Content Engineering)
source: https://github.com/Adobe-Print/Documentation_PDFL_Acrobat_SDK/blob/master/docbuild/acrobatsdk/index.rst
---

<a id="acrobat-sdk-2021"></a>
# Acrobat SDK 2021

Welcome to the 2021 release of the  Acrobat SDK.  The downloads are new and the documentation is rapidly evolving.

The Acrobat  SDK provides tools that help you develop software that interacts with Acrobat technology. The SDK contains header files, type libraries, simple utilities, sample code, and documentation. These tools provide several methods for developing software that integrates with Acrobat products, including JavaScript, plugins, and interapplication communication.

This SDK release introduces support for Windows 64-bit. Details include:

- You must upgrade 32-bit plugins to 64-bit for them to work with the 64-bit app.
- The SDK provides 64-bit public headers to 3rd party plug-in developers so that they can successfully create or upgrade their plugins to 64-bit.

<a id="master-search-and-toc"></a>
## Master search and TOC

> **Tip**
>
> While each document below has a unique search and TOC, you can [search all the docs at once or use the master TOC](../guides/index.md)

<a id="documentation"></a>
## Documentation

| Document | Description |
|----------|-------------|
| [SDK Overview](../guides/overview/index.md) | Overview, choosing a development methodology, differences between Acrobat and Reader, example features, FAQ |
| [Samples Guide](../guides/samples/index.md) | A guide to the sample code included with the Acrobat  SDK. |
| [Plugin Development](../guides/plugin/index.md) | Developing plugins for Acrobat and Acrobat Reader, as well as for PDF Library applications. |
| [Snippet Runner Cookbook](../guides/snippet/index.md) | Prototyping code without the overhead of writing and verifying a complete plugin or application. |
| [Extending the SaveAsXML Plugin](../guides/saveasxml/index.md) | Enabling Acrobat  to save documents in a customized text-based format. |
| [Interapplication Communication](../guides/interapp/index.md) | Using DDE, OLE, Apple events, and AppleScript to control the app and to render Adobe PDF documents, including detailed descriptions of DDE, OLE, Apple event, and AppleScript APIs. |
| [JavaScript Developer Guide](../guides/jsdevguide/index.md) | Using JavaScript to develop and enhance standard workflows in Acrobat  and Acrobat  Reader. |
| [JavaScript API Reference](../guides/jsapiref/index.md) | Detailed descriptions of JavaScript APIs for developing and enhancing workflows in Acrobat  and Acrobat  Reader. |
| [3D JavaScript API Reference](../guides/js3dapi/index.md) | Detailed descriptions of JavaScript APIs for adding interactivity to 3D annotations within PDF documents. |
| [Acrobat Tracker](../guides/tracker/index.md) | Using RSS to track remote resources in an occasionally-connected environment. |
| [Distiller API Reference](../guides/distiller/index.md) | Detailed descriptions of APIs for controlling Acrobat Distiller for PDF file creation. |
| [PDF Creation Settings](../guides/pdfcreation/index.md) | Specifying settings for the creation of PDF files. |
| [PDFmark Reference](../guides/pdfmark/index.md) | A detailed description of an extension to the PostScript language which allows the description of PDF features not found in standard PostScript. |
| [Accessibility API Reference](../guides/accessibility/index.md) | Detailed descriptions of the APIs for using assistive technology with PDF documents. |
| [Batch Sequences](../guides/batch/index.md) | Using JavaScript to perform repetitive operations on a collection of files. |
| [Acrobat API Reference](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/apireference/index.html) | A description of the APIs which help you develop Adobe Acrobat plug-ins and PDF Library applications. |
| [PDFL API Reference](https://opensource.adobe.com/dc-acrobat-sdk-docs/pdflsdk/apireference/index.html) | A description of the APIs which help you develop Adobe Acrobat plug-ins and PDF Library applications. |

<a id="related-specifications"></a>
## Related specifications

<a id="pdf-reference"></a>
### PDF Reference

- **Latest Adobe support**: [PDF Reference 1.7.pdf](../pdfstandards/PDF32000_2008.pdf)
- [PDF Reference 1.6.pdf](../pdfstandards/pdfreference1.6.pdf)
- [PDF Reference 1.5\_v6.pdf](../pdfstandards/pdfreference1.5_v6.pdf)
- [PDF Reference 1.4.pdf](../pdfstandards/pdfreference1.4.pdf)
- [PDF Reference 1.3.pdf](../pdfstandards/pdfreference1.3.pdf)
- [PDF Reference 1.2.pdf](../pdfstandards/pdfreference1.2.pdf)
- [PDF Reference 1.0.pdf](../pdfstandards/pdfreference1.0.pdf)

> **Note**
>
> You may also wish to refer to the latest [ISO reference](https://www.pdfa.org/resource/iso-32000-pdf/).

<a id="other-formats"></a>
### Other formats

Verify the latest versions from the organization’s home page:

- Commpact font format: [https://docs.microsoft.com/en-us/typography/opentype/spec/cff](https://docs.microsoft.com/en-us/typography/opentype/spec/cff)
- Open Prepress Interface (OPI): [https://www.pdfa.org/norm-refs/5660\_OPI\_2\_0.pdf](https://www.pdfa.org/norm-refs/5660_OPI_2_0.pdf)
- XFA: [https://www.pdfa.org/norm-refs/XFA-3\_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf)
- XFDF: [https://www.iso.org/standard/74272.html](https://www.iso.org/standard/74272.html)
- PRC (and U3D):  [https://www.iso.org/standard/54948.html](https://www.iso.org/standard/54948.html)

<a id="x-and-earlier-documentation"></a>
### 12.x and earlier documentation

Deprecated documentation is not available online. For access to other versions of the developer documentation, contact [acrobat-sdk-users@adobe.com](mailto:acrobat-sdk-users@adobe.com).
