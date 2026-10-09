---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/interapp/iac-api-catalogcatintro.md
type: reference
title: iac-api-catalogcatintro
name: iac-api-catalogcatintro
description: <a id="acrobat-catalog-plug-in"></a>
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/interapp/iac-api-catalogcatintro.md
resource_root: C:/GIT
author: brogers
tags: [dev.adobe.com-rst2md-project, acrobat-pdfl-sdk, src, pages, guides, interapp]
domain: content
tokens: 603
generated: {by: 'human:brogers', at: '2026-08-27T13:20:58-04:00'}
okf_version: '0.2'
---
<a id="acrobat-catalog-plug-in"></a>
# Acrobat Catalog Plug-In

This chapter describes IAC support for the Acrobat Catalog plug-in, which allows you to create a full-text index of a set of PDF documents. A full-text index is a searchable database of all the text in the documents. After building an index, you can use the Acrobat Search command to search the entire library quickly. Searches of full-text indexes created using Catalog are faster and more convenient than using the Find command.

For more information on Catalog, see the Acrobat Help and the *Acrobat and PDF Library API Reference*.

<a id="catalog-windows-messages"></a>
## Catalog Windows messages

Catalog broadcasts a set of Windows messages when certain operations occur. These messages are broadcast whether the operations are initiated from the user interface, HFT methods, or DDE methods.

- `AcrobatCatalogBuildSuccess`: On every successful build.
- `AcrobatCatalogBuildFail`: On every failed build.
- `AcrobatCatalogBuildStopped`: When a build has stopped.

<a id="catalog-dde-methods"></a>
## Catalog DDE methods

Clients can connect to the Catalog plug-in through DDE using the service name `Acrobat` and the topic name `Control`. This section lists the available DDE methods.

<a id="appexit"></a>
### AppExit

Exits Acrobat Catalog.

**Syntax**

```
[AppExit()]
```

**Returns**

If `true`, Catalog exited successfully, otherwise `false`.

<a id="appfront"></a>
### AppFront

Brings Catalog to the front.

**Syntax**

```
[AppExit()]
```

<a id="filebuild"></a>
### FileBuild

Builds an index based on the specified index definition file.

**Syntax**

```
[FileBuild(char* fullPath)]
```

**Parameters**

| Parameter | Description |
|-----------|-------------|
| fullPath | The full path of the file to be opened, including the.pdx extension. |

**Returns**

If `true`, the file opened successfully, otherwise `false`.

<a id="fileopen"></a>
### FileOpen

Opens an index definition file and displays the Edit Index Definition dialog box.

**Syntax**

```
[FileOpen(char* fullPath)]
```

**Parameters**

| Parameter | Description |
|-----------|-------------|
| fullPath | The full path of the file to be opened, including the.pdx extension. |

**Returns**

`true` if the file opened successfully, otherwise `false`.

<a id="filepurge"></a>
### FilePurge

Purges an index definition file.

**Syntax**

```
[FilePurge(char* fullPath)]
```

**Parameters**

| Parameter | Description |
|-----------|-------------|
| fullPath | The full path of the file to be purged, including the.pdx extension. |

**Returns**

`true` if the file was successfully purged, otherwise `false`.
