# DDE Messages

This chapter lists all DDE messages supported by Acrobat.

These DDE messages handle the display of the Acrobat application:

- [AppExit](IAC_API_DDE_Messages.md#50532407_21507)
- [AppHide](IAC_API_DDE_Messages.md#50532407_40535)
- [AppShow](IAC_API_DDE_Messages.md#50532407_36588)
- [CloseAllDocs](IAC_API_DDE_Messages.md#50532407_21798)
- [HideToolbar](IAC_API_DDE_Messages.md#50532407_41722)
- [MenuitemExecute](IAC_API_DDE_Messages.md#50532407_30748)
- [ShowToolbar](IAC_API_DDE_Messages.md#50532407_23287)

These DDE messages control the display of the document:

- [DocClose](IAC_API_DDE_Messages.md#50532407_35723)
- [DocDeletePages](IAC_API_DDE_Messages.md#50532407_17772)
- [DocInsertPages](IAC_API_DDE_Messages.md#50532407_24045)
- [DocOpen](IAC_API_DDE_Messages.md#50532407_31954)
- [DocReplacePages](IAC_API_DDE_Messages.md#50532407_32593)
- [DocSave](IAC_API_DDE_Messages.md#50532407_35684)
- [DocSaveAs](IAC_API_DDE_Messages.md#50532407_11107)
- [DocSetViewMode](IAC_API_DDE_Messages.md#50532407_33767)
- [FileOpen](IAC_API_DDE_Messages.md#50532407_13590)
- [FileOpenEx](IAC_API_DDE_Messages.md#50532407_17462)

These DDE messages handle printing of a document:

- [DocPrint](IAC_API_DDE_Messages.md#50532407_14556)
- [FilePrint](IAC_API_DDE_Messages.md#50532407_41414)
- [FilePrintEx](IAC_API_DDE_Messages.md#50532407_28199)
- [FilePrintSilent](IAC_API_DDE_Messages.md#50532407_15288)
- [FilePrintSilentEx](IAC_API_DDE_Messages.md#50532407_29945)
- [FilePrintTo](IAC_API_DDE_Messages.md#50532407_20716)
- [FilePrintToEx](IAC_API_DDE_Messages.md#50532407_42695)

These DDE messages control the view of a document.:

- [DocGoTo](IAC_API_DDE_Messages.md#50532407_55018)
- [DocGoToNameDest](IAC_API_DDE_Messages.md#50532407_79623)
- [DocPageDown](IAC_API_DDE_Messages.md#50532407_28808)
- [DocPageLeft](IAC_API_DDE_Messages.md#50532407_40373)
- [DocPageRight](IAC_API_DDE_Messages.md#50532407_14904)
- [DocPageUp](IAC_API_DDE_Messages.md#50532407_16952)
- [DocScrollTo](IAC_API_DDE_Messages.md#50532407_33970)
- [DocZoomTo](IAC_API_DDE_Messages.md#50532407_97206)

This DDE message is used for searching:

- [DocFind](IAC_API_DDE_Messages.md#50532407_77617)

Acrobat Reader supports the following subset of DDE messages:

- [AppExit](IAC_API_DDE_Messages.md#50532407_21507)
- [CloseAllDocs](IAC_API_DDE_Messages.md#50532407_21798)
- [DocClose](IAC_API_DDE_Messages.md#50532407_35723)
- [DocGoTo](IAC_API_DDE_Messages.md#50532407_55018)
- [DocGoToNameDest](IAC_API_DDE_Messages.md#50532407_79623)
- [DocOpen](IAC_API_DDE_Messages.md#50532407_31954)
- [FileOpen](IAC_API_DDE_Messages.md#50532407_13590)
- [FileOpenEx](IAC_API_DDE_Messages.md#50532407_17462)
- [FilePrint](IAC_API_DDE_Messages.md#50532407_41414)
- [FilePrintEx](IAC_API_DDE_Messages.md#50532407_28199)
- [FilePrintSilent](IAC_API_DDE_Messages.md#50532407_15288)
- [FilePrintSilentEx](IAC_API_DDE_Messages.md#50532407_29945)
- [FilePrintTo](IAC_API_DDE_Messages.md#50532407_20716)
- [FilePrintToEx](IAC_API_DDE_Messages.md#50532407_42695)

<a id="50532407_21507"></a>
## AppExit

Exits the Acrobat application.

`AppExit` is also supported in Acrobat Reader.

**Syntax**

```
[AppExit()]
```

**Returns**

`true` if the Acrobat application exits successfully, `false` otherwise.

**Related methods**

- [AppHide](IAC_API_DDE_Messages.md#50532407_40535)
- [AppShow](IAC_API_DDE_Messages.md#50532407_36588)

<a id="50532407_40535"></a>
## AppHide

Iconifies or hides the Acrobat application.

**Syntax**

```
[AppHide()]
```

**Returns**

`true` if the Acrobat application is hidden successfully, `false` otherwise.

**Related methods**

- [AppExit](IAC_API_DDE_Messages.md#50532407_21507)
- [AppShow](IAC_API_DDE_Messages.md#50532407_36588)

<a id="50532407_36588"></a>
## AppShow

Shows the Acrobat application.

**Syntax**

```
[AppShow()]
```

**Returns**

`true` if the Acrobat application is shown successfully, `false` otherwise.

**Related methods**

- [AppExit](IAC_API_DDE_Messages.md#50532407_21507)
- [AppHide](IAC_API_DDE_Messages.md#50532407_40535)

<a id="50532407_21798"></a>
## CloseAllDocs

Closes all open documents.

`CloseAllDocs` is also supported in Acrobat Reader.

**Syntax**

```
[CloseAllDocs()]
```

**Returns**

`true` if the documents are closed successfully, `false` otherwise.

**Related methods**

- [DocClose](IAC_API_DDE_Messages.md#50532407_35723)
- [DocOpen](IAC_API_DDE_Messages.md#50532407_31954)
- [FileOpen](IAC_API_DDE_Messages.md#50532407_13590)

<a id="50532407_35723"></a>
## DocClose

Closes the specified document without saving it, and without prompting the user to save the document if it has been modified.

`DocClose` is also supported in Acrobat Reader.

**Syntax**

```
[DocClose(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be closed. |

**Returns**

`true` if the document is closed successfully, `false` if the document does not exist or is not closed successfully.

**Related methods**

- [CloseAllDocs](IAC_API_DDE_Messages.md#50532407_21798)
- [DocOpen](IAC_API_DDE_Messages.md#50532407_31954)
- [FileOpen](IAC_API_DDE_Messages.md#50532407_13590)

<a id="50532407_17772"></a>
## DocDeletePages

Deletes the specified pages in the document. Requests to delete all pages in a document are ignored because a document must have at least one page.

**Syntax**

```
[DocDeletePages(char* fullPath, long fromPage, long toPage)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the document. |
| fromPage | The page number of the first page to be deleted. |
| toPage | The page number of the last page to be deleted. |

**Returns**

`true` if the pages are deleted successfully. Returns `false` if the document specified by `fullPath` does not exist, if the request was to delete all the document’s pages, or if the pages are not deleted successfully.

**Related methods**

- [DocInsertPages](IAC_API_DDE_Messages.md#50532407_24045)
- [DocReplacePages](IAC_API_DDE_Messages.md#50532407_32593)

<a id="50532407_77617"></a>
## DocFind

Finds a string in a specified file. This does not use a cross-document search, but instead performs a page-by-page search of the specified file.

**Syntax**

```
[DocFind(char* fullPath, char* string, boolean caseSensitive,

                 boolean wholeWords, boolean bReset)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be searched. |
| string | The string to be found. |
| caseSensitive | `true` if the search is case-sensitive, `false` otherwise. |
| wholeWords | `true` if the search will only match whole words, `false` otherwise. |
| bReset | `true` if the search begins on the first page of the document, `false` if the search begins on the current page. |

**Returns**

`false` if the document specified by `fullPath` does not exist or if the text is not found, `true` otherwise.

<a id="50532407_55018"></a>
## DocGoTo

Goes to the specified page.

`DocGoTo` is also supported in Acrobat Reader.

**Syntax**

```
[DocGoTo(char* fullPath, long pageNum)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file. |
| pageNum | The page number of the destination page. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

<a id="50532407_79623"></a>
## DocGoToNameDest

Goes to the specified named destination.

`DocGoToNameDest` is also supported in Acrobat Reader.

**Syntax**

```
[DocGoToNameDest(char* fullPath, char* nameDest)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file. |
| nameDest | The named destination. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

<a id="50532407_24045"></a>
## DocInsertPages

Inserts pages from one file into another.

**Syntax**

```
[DocInsertPages(char* fullPath, long insertAfterPage, char* sourcePath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the target document, which must already be open in the Acrobat application. |
| insertAfterPage | The page number after which pages are being inserted. Possible values can be a page number or one of the following:  `PDBeforeFirstPage`: Pages are inserted at the beginning of the document.  `PDLastPage`: Pages are inserted at the end of the document. |
| sourcePath | The full path of the source document. This file need not be open in the Acrobat application. |

**Returns**

`true` if the pages are inserted successfully, `false` if the document does not exist or the pages are not inserted successfully.

**Related methods**

- [DocDeletePages](IAC_API_DDE_Messages.md#50532407_17772)
- [DocReplacePages](IAC_API_DDE_Messages.md#50532407_32593)

<a id="50532407_31954"></a>
## DocOpen

Opens a document and adds it to the list of documents known to DDE, allowing it to be manipulated by other DDE messages (see [FileOpen](IAC_API_DDE_Messages.md#50532407_13590) ).

`DocOpen` is also supported in Acrobat Reader.

**Syntax**

```
[DocOpen(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be opened. |

**Returns**

`true` if the file is opened successfully, `false` otherwise.

**Related methods**

- [CloseAllDocs](IAC_API_DDE_Messages.md#50532407_21798)
- [DocClose](IAC_API_DDE_Messages.md#50532407_35723)
- [FileOpen](IAC_API_DDE_Messages.md#50532407_13590)

<a id="50532407_28808"></a>
## DocPageDown

Scrolls forward through the document by one screen area.

**Syntax**

```
[DocPageDown(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the document. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [DocPageLeft](IAC_API_DDE_Messages.md#50532407_40373)
- [DocPageRight](IAC_API_DDE_Messages.md#50532407_14904)
- [DocPageUp](IAC_API_DDE_Messages.md#50532407_16952)
- [DocScrollTo](IAC_API_DDE_Messages.md#50532407_33970)

<a id="50532407_40373"></a>
## DocPageLeft

Scrolls to the left by a small amount.

**Syntax**

```
[DocPageLeft(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the document. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [DocPageDown](IAC_API_DDE_Messages.md#50532407_28808)
- [DocPageRight](IAC_API_DDE_Messages.md#50532407_14904)
- [DocPageUp](IAC_API_DDE_Messages.md#50532407_16952)
- [DocPageUp](IAC_API_DDE_Messages.md#50532407_16952)

<a id="50532407_14904"></a>
## DocPageRight

Scrolls to the right by a small amount.

**Syntax**

```
[DocPageRight(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the document. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [DocPageDown](IAC_API_DDE_Messages.md#50532407_28808)
- [DocPageLeft](IAC_API_DDE_Messages.md#50532407_40373)
- [DocPageUp](IAC_API_DDE_Messages.md#50532407_16952)
- [DocPageUp](IAC_API_DDE_Messages.md#50532407_16952)

<a id="50532407_16952"></a>
## DocPageUp

Scrolls backward through the document by one screen area.

**Syntax**

```
[DocPageUp(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the document. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [DocPageDown](IAC_API_DDE_Messages.md#50532407_28808)
- [DocPageLeft](IAC_API_DDE_Messages.md#50532407_40373)
- [DocPageRight](IAC_API_DDE_Messages.md#50532407_14904)
- [DocScrollTo](IAC_API_DDE_Messages.md#50532407_33970)

<a id="50532407_14556"></a>
## DocPrint

Prints a specified range of pages from a document, without displaying any modal Print dialog box to the user. For PostScript printing, only Level 1 operators are used, only ASCII data is generated, and the document’s pages are not shrunk to fit into the imageable area of the printed page.

**Syntax**

```
[DocPrint(char* fullPath, long startPage, long endPage)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of document. |
| startPage | The page number of the first page to be printed. |
| endPage | The page number of the last page to be printed. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [FilePrint](IAC_API_DDE_Messages.md#50532407_41414)
- [FilePrintSilent](IAC_API_DDE_Messages.md#50532407_15288)
- [FilePrintTo](IAC_API_DDE_Messages.md#50532407_20716)

<a id="50532407_32593"></a>
## DocReplacePages

Replaces pages in the target document using the specified pages from the source document.

**Syntax**

```
[DocReplacePages(char* fullPath, long startDestPage,

                 char* sourcePath, long startSourcePage,

                 long endSourcePage)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the target document. This file must already be open in the Acrobat application. |
| startDestPage | The page number of the first page in the target document to be replaced. |
| sourcePath | The full path of the source document. This file does not have to be already open in the Acrobat application. |
| startSourcePage | The page number of the first page in the source document to use as a replacement page. |
| endSourcePage | The page number of the last page in the source document to use as a replacement page. |

**Returns**

`true` if the pages are replaced successfully. Returns `false` if the document does not exist or the pages are not replaced successfully.

**Related methods**

- [DocDeletePages](IAC_API_DDE_Messages.md#50532407_17772)
- [DocInsertPages](IAC_API_DDE_Messages.md#50532407_24045)

<a id="50532407_35684"></a>
## DocSave

Saves the specified file. The user is not warned if there are any problems saving the file.

**Syntax**

```
[DocSave(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be saved. |

**Returns**

`true` if the document is saved successfully, `false` if the document does not exist or is not saved successfully.

**Related methods**

- [DocSaveAs](IAC_API_DDE_Messages.md#50532407_11107)

<a id="50532407_11107"></a>
## DocSaveAs

Saves an open file to a new path. The user is not warned if there are any problems saving the file.

**Syntax**

```
[DocSaveAs(char* fullPath, char* newPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the existing file. |
| newPath | The full path of the new file. |

**Returns**

`true` if the document is saved successfully, `false` if the document does not exist or is not saved successfully.

**Related methods**

- [DocSave](IAC_API_DDE_Messages.md#50532407_35684)

<a id="50532407_33970"></a>
## DocScrollTo

Scrolls the view of the current page to the specified location.

**Syntax**

```
[DocScrollTo(char* fullPath, int x, int y)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the document. |
| x | The destination’s x–coordinate. |
| y | The destination’s y–coordinate. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [DocPageDown](IAC_API_DDE_Messages.md#50532407_28808)
- [DocPageLeft](IAC_API_DDE_Messages.md#50532407_40373)
- [DocPageRight](IAC_API_DDE_Messages.md#50532407_14904)
- [DocPageUp](IAC_API_DDE_Messages.md#50532407_16952)

<a id="50532407_33767"></a>
## DocSetViewMode

Determines whether bookmarks, thumbnail images, or neither are shown in addition to the document.

**Syntax**

```
[DocSetViewMode(char* fullPath, char* viewType)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the document. |
| viewType | The view mode to be used. Must be one of the following:  `PDUseThumbs`: Displays pages and thumbnail images.  `PDUseNone`: Displays only pages.  `PDUseBookmarks`: Displays pages and bookmarks. |

**Returns**

`true` if the view mode is set successfully, `false` if the document specified by `fullPath` does not exist or an unknown view mode is specified.

**Related methods**

- [FullMenus](IAC_API_DDE_Messages.md#50532407_36770)
- [ShortMenus](IAC_API_DDE_Messages.md#50532407_38602)

<a id="50532407_97206"></a>
## DocZoomTo

Sets the zoom for a specified document.

**Syntax**

```
[DocZoomTo(char* fullPath, char* zoomType, int scale)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file whose zoom to set. |
| zoomType | The zoom strategy to use. Must be one of the following:  `AVZoomNoVary`: A fixed zoom, such as 100%.  `AVZoomFitPage`: Fits the page in the window.  `AVZoomFitWidth`: Fits the page’s width into the window.  `AVZoomFitVisibleWidth`: Fits the page’s visible content into the window. |
| scale | The magnification specified as a percent (for example, 100 corresponds to a magnification of 1.0). `scale` is used only when `zoomType` is `AVZoomNoVary`. |

**Returns**

`false` if the document specified by `fullPath` does not exist, or if `zoomType` has an unknown value. Returns `true` otherwise.

<a id="50532407_13590"></a>
## FileOpen

Opens and displays the specified document. If the file is already open, it becomes the active document and appears in the front. This DDE message does not add the document to the list that can be manipulated using DDE messages; use [DocOpen](IAC_API_DDE_Messages.md#50532407_31954) to do that.

`FileOpen` is also supported in Acrobat Reader.

**Syntax**

```
[FileOpen(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be opened. |

**Returns**

`true` if the file is opened successfully, `false` otherwise.

**Related methods**

- [CloseAllDocs](IAC_API_DDE_Messages.md#50532407_21798)
- [DocClose](IAC_API_DDE_Messages.md#50532407_35723)
- [DocOpen](IAC_API_DDE_Messages.md#50532407_31954)

<a id="50532407_17462"></a>
## FileOpenEx

Opens and displays a file. If the file is already open, it becomes the active document and appears in the front. This DDE message does not add the document to the list that can be manipulated using DDE messages; use [DocOpen](IAC_API_DDE_Messages.md#50532407_31954) to do that.

This method allows documents that either take a long time to open or are password-protected to open without stopping the flow of DDE messages. Documents opened with `FileOpenEx` are opened during an idle period. This is useful in situations in which several DDE messages are sent at once, such as a multiple file select from Windows Explorer.

`FileOpenEx` is also supported in Acrobat Reader.

**Syntax**

```
[FileOpenEx(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be opened. |

**Returns**

`true` is always returned. The specified file may not actually open.

**Related methods**

- [FileOpen](IAC_API_DDE_Messages.md#50532407_13590)
- [CloseAllDocs](IAC_API_DDE_Messages.md#50532407_21798)
- [DocClose](IAC_API_DDE_Messages.md#50532407_35723)
- [DocOpen](IAC_API_DDE_Messages.md#50532407_31954)

<a id="50532407_41414"></a>
## FilePrint

Prints all pages in a document, displaying a modal print dialog box to the user. For PostScript printing, only Level 1 operators are used, only ASCII data is generated, and the document’s pages are not shrunk to fit into the imageable area of the printed page.

`FilePrint` is also supported in Acrobat Reader.

**Syntax**

```
[FilePrint(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be printed. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [DocPrint](IAC_API_DDE_Messages.md#50532407_14556)
- [FilePrintSilent](IAC_API_DDE_Messages.md#50532407_15288)
- [FilePrintTo](IAC_API_DDE_Messages.md#50532407_20716)

<a id="50532407_28199"></a>
## FilePrintEx

Prints all pages in a document, displaying a modal print dialog box to the user. For PostScript printing, only Level 1 operators are used, only ASCII data is generated, and the document’s pages are not shrunk to fit into the imageable area of the printed page.

Similar to `FileOpenEx`, this is a special DDE command that returns `true` right away and performs the action during idle periods. This ensures that no DDE commands are lost when printing a large number of files simultaneously.

`FilePrintEx` is also supported in Acrobat Reader.

**Syntax**

```
[FilePrintEx(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to print. |

**Returns**

`true` is always returned.

**Related methods**

- [DocPrint](IAC_API_DDE_Messages.md#50532407_14556)
- [FileOpenEx](IAC_API_DDE_Messages.md#50532407_17462)
- [FilePrint](IAC_API_DDE_Messages.md#50532407_41414)
- [FilePrintSilent](IAC_API_DDE_Messages.md#50532407_15288)
- [FilePrintSilentEx](IAC_API_DDE_Messages.md#50532407_29945)
- [FilePrintTo](IAC_API_DDE_Messages.md#50532407_20716)
- [FilePrintToEx](IAC_API_DDE_Messages.md#50532407_42695)

<a id="50532407_15288"></a>
## FilePrintSilent

Prints all pages in a document, without displaying a print dialog box to the user. For PostScript printing, only Level 1 operators are used, only ASCII data is generated, and the document’s pages are not shrunk to fit into the imageable area of the printed page.

`FilePrintSilent` is also supported in Acrobat Reader.

**Syntax**

```
[FilePrintSilent(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be printed. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [DocPrint](IAC_API_DDE_Messages.md#50532407_14556)
- [FilePrint](IAC_API_DDE_Messages.md#50532407_41414)
- [FilePrintTo](IAC_API_DDE_Messages.md#50532407_20716)

<a id="50532407_29945"></a>
## FilePrintSilentEx

Prints all pages in a document, without displaying a print dialog box to the user. For PostScript printing, only Level 1 operators are used, only ASCII data is generated, and the document’s pages are not shrunk to fit into the imageable area of the printed page.

Similar to `FileOpenEx`, this is a DDE command that returns `true` right away and does the action during idle periods. This is to ensure that no DDE commands are lost when printing a large number of files simultaneously.

`FilePrintSilentEx` is also supported in Acrobat Reader.

**Syntax**

```
[FilePrintSilentEx(char* fullPath)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be printed. |

**Returns**

`true` is always returned.

**Related methods**

- [DocPrint](IAC_API_DDE_Messages.md#50532407_14556)
- [FileOpenEx](IAC_API_DDE_Messages.md#50532407_17462)
- [FilePrintEx](IAC_API_DDE_Messages.md#50532407_28199)
- [FilePrintSilent](IAC_API_DDE_Messages.md#50532407_15288)
- [FilePrintTo](IAC_API_DDE_Messages.md#50532407_20716)
- [FilePrintToEx](IAC_API_DDE_Messages.md#50532407_42695)

<a id="50532407_20716"></a>
## FilePrintTo

Prints all pages in a document to a specified printer, using a specified driver and port, displaying a modal print dialog box to the user. For PostScript printing, only ASCII data is generated, and the document’s pages are not shrunk to fit into the imageable area of the printed page.

`FilePrintTo` is also supported in Acrobat Reader.

**Syntax**

```
[FilePrintTo(char* fullPath, char* printName,

                 char* driverName, char* portName)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be printed. |
| printName | The name of the printer. Required for Windows 95 and later. |
| driverName | Printer driver name. |
| portName | Port name. Required for Windows NT. |

**Returns**

`false` if the document specified by `fullPath` does not exist, `true` otherwise.

**Related methods**

- [DocPrint](IAC_API_DDE_Messages.md#50532407_14556)
- [FilePrint](IAC_API_DDE_Messages.md#50532407_41414)
- [FilePrintSilent](IAC_API_DDE_Messages.md#50532407_15288)

<a id="50532407_42695"></a>
## FilePrintToEx

Prints all pages in a document to a specified printer, using a specified driver and port, displaying a modal print dialog box to the user. For PostScript printing, only ASCII data is generated, and the document’s pages are not shrunk to fit into the imageable area of the printed page.

Similar to `FileOpenEx`, this is a DDE command that returns `true` right away and does the action during idle periods. This is to ensure that no DDE commands are lost when printing a large number of files simultaneously.

`FilePrintToEx` is also supported in Acrobat Reader.

**Syntax**

```
[FilePrintToEx(char* fullPath, char* printName,

                 char* driverName, char* portName)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fullPath | The full path of the file to be printed. |
| printName | The name of the printer. Required for Windows 95 and later. |
| driverName | Printer driver name. |
| portName | Port name. Required for Windows NT. |

**Returns**

`true` is always returned.

**Related methods**

- [DocPrint](IAC_API_DDE_Messages.md#50532407_14556)
- [FileOpenEx](IAC_API_DDE_Messages.md#50532407_17462)
- [FilePrintEx](IAC_API_DDE_Messages.md#50532407_28199)
- [FilePrintSilentEx](IAC_API_DDE_Messages.md#50532407_29945)
- [FilePrintTo](IAC_API_DDE_Messages.md#50532407_20716)
- [FilePrintToEx](IAC_API_DDE_Messages.md#50532407_42695)

<a id="50532407_36770"></a>
## FullMenus

Displays full menus, and sets this option in the Acrobat application’s preferences file.

With Acrobat 3.0 or later, all menus are displayed, and this function is ignored.

**Syntax**

```
[FullMenus()]
```

**Returns**

`true` if full menus are set successfully, `false` otherwise.

**Related methods**

- [DocSetViewMode](IAC_API_DDE_Messages.md#50532407_33767)
- [ShortMenus](IAC_API_DDE_Messages.md#50532407_38602)

<a id="50532407_41722"></a>
## HideToolbar

Hides the toolbar.

**Syntax**

```
[HideToolbar()]
```

**Returns**

`true` if the toolbar is hidden successfully, `false` otherwise.

**Related methods**

- [ShowToolbar](IAC_API_DDE_Messages.md#50532407_23287)

<a id="50532407_30748"></a>
## MenuitemExecute

Executes the menu item specified by its language-independent name.

**Syntax**

```
[MenuitemExecute(char* menuItemName)]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| menuItemName | The language-independent name of the menu item to execute. See the [Acrobat and PDF Library API Reference](./API_References/Acrobat_API_Reference/index.md) for a list of menu item names. |

<a id="50532407_38602"></a>
## ShortMenus

Displays short menus, and sets this option in the Acrobat application’s preferences file.

With Acrobat 3.0 or later, all menus are displayed, and this function is ignored.

**Syntax**

```
[ShortMenus()]
```

**Returns**

`true` if short menus are set successfully, `false` otherwise.

**Related methods**

- [DocSetViewMode](IAC_API_DDE_Messages.md#50532407_33767)
- [FullMenus](IAC_API_DDE_Messages.md#50532407_36770)

<a id="50532407_23287"></a>
## ShowToolbar

Shows the toolbar.

**Syntax**

```
[ShowToolbar()]
```

**Returns**

`true` if the toolbar is shown successfully, `false` otherwise.

**Related methods**

- [HideToolbar](IAC_API_DDE_Messages.md#50532407_41722)
