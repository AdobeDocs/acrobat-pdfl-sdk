# Apple Event Objects and Apple Events

This chapter describes the supported Apple event objects, with descriptions of each object’s elements and properties, and the supported Apple events.

## Objects

Acrobat presents the following objects to the Apple event interface:

- `annotation`
- `application`
- `bookmark`
- `conversion`
- `document`
- `Link Annotation`
- `menu`
- `menu item`
- `page`
- `PDF Window`
- `Text Annotation`

<a id="50532410_25583"></a>
### annotation

An annotation on a page in a PDF file that corresponds to `PDAnnot`, an internal Acrobat class. This object was formerly known as `PDAnnot`.

Acrobat also has two built-in annotation objects. For more information, see [Link Annotation](IAC_API_AppleEvtObjects.md#50532410_90412) and [Text Annotation](IAC_API_AppleEvtObjects.md#50532410_22569).

**Plural form**

Annotations

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| best type | type class \[r/o\] | The best descriptor type. |
| bounds | a list of small real | The boundary rectangle for the annotation in PDF space (left, top, right, bottom). |
| class | type class \[r/o\] | The class. |
| color | ‘RGB’ | The color of the border around the annotation. |
| contents | international text | Text annotations only. The textual contents of the note. |
| default type | type class \[r/o\] | The default descriptor type. |
| destination page number | integer | Link annotations only. The page number to appear in the PDF window when the annotation link is activated. |
| destination rectangle | a list of small real | Link annotations only. The boundary rectangle (specified in user space) for the view of the destination. Coordinates are specified in the following order: left, top, right, bottom. |
| fit type | constant | Link annotations only. Determines how the destination rectangle is fitted to the window when the link is activated. Values are: `Left Top Zoom`, `Fit Page`, `Fit Width`, `Fit Height`, `Fit Rect`, `Fit BBox`, `Fit BB Width`, `Fit BB Height`<br><br>These are described in the [PDF Reference](https://www.adobe.com/go/pdfreference). |
| index | integer \[r/o\] | The annotation’s index within the [page](IAC_API_AppleEvtObjects.md#50532410_24065) object. |
| modification date | date | The date and time the annotation was last modified. |
| name | string | Text annotations only. The annotation’s label. |
| open state | Boolean | Text annotations only. Whether the annotation is open. |
| subtype | international text \[r/o\] | The subtype of the annotation. |
| zoom factor | small real | Link annotations only. If `fit type` is `Left Top Zoom`, this specifies the zoom factor; otherwise it is ignored. Setting this property automatically sets `fit type` to `Left Top Zoom`. |

**Related methods**

- [delete](IAC_API_AppleEvtObjects.md#50532410_41487)
- [perform](IAC_API_AppleEvtObjects.md#50532410_27016)

<a id="50532410_98408"></a>
### application

The Acrobat or Acrobat Reader application itself.

**Elements**

| Element | Accessed by |
| --- | --- |
| [document](IAC_API_AppleEvtObjects.md#50532410_48845) | name, numeric index |
| [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) | name, numeric index |
| [menu](IAC_API_AppleEvtObjects.md#50532410_45214) | name, numeric index |
| [menu item](IAC_API_AppleEvtObjects.md#50532410_78053) | name |

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| active doc | reference | The active document. |
| active tool | international text | The type of the currently active tool. See the *Acrobat and PDF Library API Reference* for a list of tool names. |
| anti\_alias text | Boolean | Determines whether to anti-alias text and monochrome images. |
| best type | type class \[r/o\] | The best descriptor type. |
| case sensitivity | Boolean | Determines whether searches are case- sensitive. |
| class | type class \[r/o\] | The class. |
| default type | type class \[r/o\] | The default descriptor type. |
| default zoom factor | small real | The default zoom factor, in percent, used for displaying new documents. For example, a value of 100 corresponds to a zoom factor of 1.0 (100%). |
| default zoom type | constant | The default zoom type when opening a new document. Valid values are `no vary`, `fit page`, `fit width`, `fit height`, and `fit visible width`. |
| download entire file | Boolean | Determines whether to download the entire file. |
| frontmost | Boolean | Determines whether Acrobat is the frontmost application. Value can be set to true only. |
| fullscreen click advances | Boolean | Determines whether mouse click advances in fullscreen mode. |
| fullscreen cursor | Boolean | Determines whether to hide the cursor in fullscreen mode. |
| fullscreen escape | Boolean | Determines whether the Esc key can be used to exit fullscreen mode. |
| fullscreen loop | Boolean \[r/o\] | Determines whether the document’s pages are displayed in a loop while in fullscreen mode. |
| fullscreen timer delay | integer | The number of seconds to advance to the next page in fullscreen mode. |
| fullscreen transition | international text \[r/o\] | Default fullscreen transition. |
| highlight color | ‘RGB ‘ | Color used to highlight selections. |
| maximum documents | integer \[r/o\] | Maximum number of open documents. |
| name | string \[r/o\] | The application’s name. |
| note color | ‘RGB ‘ | A list of three values between 0 and 65535 representing the color of the border around text annotations. For example, the following sets the note color to deep blue:`set the note color to {0, 0, 32768}`. |
| note font name | international text | Deprecated. |
| note font size | integer | Deprecated. |
| open in place | Boolean | Determines whether to open cross-document links in the same window. |
| page layout | international text | Default page layout. Values are: `Single Page`, `Continuous`, `Facing`, and `Continuous - Facing`. |
| page units | international text | Default page display units: `Points`, `Inches` or `Millimeters.` |
| PS level | integer | Deprecated. Set the PostScript level when using [save](IAC_API_AppleEvtObjects.md#50532410_32794) or [print pages](IAC_API_AppleEvtObjects.md#50532410_40027) commands. |
| save as linearize | Boolean | Determines whether to save the document as optimized for the web. |
| show splash at startup | Boolean | Determines whether the splash screen is shown at startup. |
| skip warnings | Boolean | Determines whether to skip warning dialog boxes during program execution. |
| shrink to fit | Boolean | Deprecated. |
| text note label | international text | The text that will appear in the title bar of all newly created text notes. |
| toolbar visibility | Boolean | Determines whether the toolbar is visible. |
| UI language | international text \[r/o\] | A three-character language code identifying which language is used in the Acrobat user interface. Example: `ENU` represents English. |
| use fullscreen timer | Boolean | Determines whether to use a timer to advance pages in fullscreen mode |
| version | string \[r/o\] | The version number of the application. |
| whole word searching | Boolean | Determines whether searches are applied to whole words only. |

**Related methods**

- [close all docs](IAC_API_AppleEvtObjects.md#50532410_31136)
- [count](IAC_API_AppleEvtObjects.md#50532410_16155)
- [make](IAC_API_AppleEvtObjects.md#50532410_24328)
- [open](IAC_API_AppleEvtObjects.md#50532410_41641)
- [print](IAC_API_AppleEvtObjects.md#50532410_29870)
- [quit](IAC_API_AppleEvtObjects.md#50532410_37698)
- [run](IAC_API_AppleEvtObjects.md#50532410_40886)

### AVPageView

> **Note**
>
> Deprecated. Use [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) instead.

<a id="50532410_75140"></a>
### bookmark

A bookmark on a page in a PDF file. Corresponds to Acrobat’s `PDBookmark` object.

> **Note**
>
> This object was formerly known as `PDBookmark`.

**Plural form**

Bookmarks

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| best type | type class \[r/o\] | The best descriptor type. |
| class | type class \[r/o\] | The class. |
| default type | type class \[r/o\] | The default descriptor type. |
| destination page number | integer | The page number to which the [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) goes when the bookmark’s action is performed. |
| destination rectangle | list of small real | Boundary rectangle (specified in user space) for the view of the destination when the bookmark’s action is performed. Coordinates are specified in the following order: (left, top, right, bottom).<br><br>- Set this only after setting `fit type`. |
| fit type | constant | Controls how the destination rectangle is fitted to the window when the bookmark’s action is performed. Possible values:<br><br>`Left Top Zoom`: Sets a specified zoom and a specified location on the page.<br><br>`Fit Page`: Sets the zoom factor so that the entire page fits into the window.<br><br>`Fit Width`: Sets the zoom factor so that the width of the page fits into the window.<br><br>`Fit Height`: Sets the zoom factor so that the height of the page fits into the window.<br><br>`Fit Rect`: Sets the zoom factor so that the specified rectangle fits into the window.<br><br>`Fit BBox`: Sets the zoom so that the rectangle enclosing all marks on the page (known as the bounding box) fits into the window.<br><br>`Fit BB Width`: Sets the zoom factor so that the width of the bounding box fits into the window.<br><br>`Fit BB Height`: Sets the zoom factor so that the height of the bounding box fits into the window. |
| index | integer \[r/o\] | The bookmark’s index within the [document](IAC_API_AppleEvtObjects.md#50532410_48845). |
| name | international text | The bookmark’s title. |
| zoom factor | small real | The zoom factor used when `fit type` is `Left Top Zoom` ; ignored otherwise. Setting this property automatically sets `fit type` to `Left Top Zoom`. |

**Related methods**

- [insert pages](IAC_API_AppleEvtObjects.md#50532410_35783)
- [perform](IAC_API_AppleEvtObjects.md#50532410_27016)

<a id="50532410_56571"></a>
### conversion

A file type converter that exports PDF files into other formats. Conversions correspond to the list of formats specified in the Acrobat Save As menu. A list of formats can be obtained as follows:

```
get every conversion
```

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| best type | type class \[r/o\] | The best descriptor type. |
| class | type class \[r/o\] | The class. |
| default type | type class \[r/o\] | The default descriptor type. |
| index | integer \[r/o\] | The index number of the converter. |
| name | international text | The conversion’s description. |

**Related methods**

- [save](IAC_API_AppleEvtObjects.md#50532410_32794)

<a id="50532410_48845"></a>
document

Represents a single open document in Acrobat or Acrobat Reader.

**Elements**

| Element | Accessed by |
| --- | --- |
| [page](IAC_API_AppleEvtObjects.md#50532410_24065) | Numeric index. The first page in a document is page 1. |
| [bookmark](IAC_API_AppleEvtObjects.md#50532410_75140) | Name or numeric index. |
| [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) | An index of 1 or with the `some` keyword in AppleScript. No document has more than one `PDF Window`. |

**Plural form**

documents

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| best type | type class \[r/o\] | The best descriptor type. |
| bounds | bounding rectangle \[r/o\] | The boundary rectangle for the document’s window, in screen coordinates (left, top, right, bottom). |
| class | type class \[r/o\] | The class. |
| default type | type class \[r/o\] | The default descriptor type. |
| file alias | alias \[r/o\] | An alias for the file to which the document will be saved if no other name is specified; this is usually the same path from which the document was read. |
| modified | Boolean \[r/o\] | Determines whether the document has been modified and should be saved. |
| name | international text \[r/o\] | The document’s name as it appears in the window’s titlebar. |
| view mode | constant | The viewing mode of the document. Possible values: `just pages`, `pages and thumbs`, or `pages and bookmarks`. |

**Related methods**

- [bring to front](IAC_API_AppleEvtObjects.md#50532410_19936)
- [clear selection](IAC_API_AppleEvtObjects.md#50532410_33043)
- [close](IAC_API_AppleEvtObjects.md#50532410_39856)
- [count](IAC_API_AppleEvtObjects.md#50532410_16155)
- [create thumbs](IAC_API_AppleEvtObjects.md#50532410_15865)
- [delete](IAC_API_AppleEvtObjects.md#50532410_41487)
- [delete pages](IAC_API_AppleEvtObjects.md#50532410_15460)
- [delete thumbs](IAC_API_AppleEvtObjects.md#50532410_29225)
- [find next note](IAC_API_AppleEvtObjects.md#50532410_15335)
- [find text](IAC_API_AppleEvtObjects.md#50532410_15620)
- [get info](IAC_API_AppleEvtObjects.md#50532410_19217)
- [insert pages](IAC_API_AppleEvtObjects.md#50532410_35783)
- [maximize](IAC_API_AppleEvtObjects.md#50532410_26208)
- [print pages](IAC_API_AppleEvtObjects.md#50532410_40027)
- [replace pages](IAC_API_AppleEvtObjects.md#50532410_27808)
- [save](IAC_API_AppleEvtObjects.md#50532410_32794)
- [set info](IAC_API_AppleEvtObjects.md#50532410_18444)

<a id="50532410_79350"></a>
### EPS Conversion

A file type converter that exports PDF files into EPS format.

**Properties**

Inherits from [PostScript Conversion](IAC_API_AppleEvtObjects.md#50532410_17521).

**Related methods**

- [save](IAC_API_AppleEvtObjects.md#50532410_32794)

<a id="50532410_90412"></a>
### Link Annotation

A link annotation on a page in a PDF file. Can only be used as the target of a [make](IAC_API_AppleEvtObjects.md#50532410_24328) event. All other access is via the [annotation](IAC_API_AppleEvtObjects.md#50532410_25583) class.

> **Note**
>
> This object was formerly known as [PDLinkAnnot](IAC_API_AppleEvtObjects.md#50532410_21206).

**Properties**

Inherits from [annotation](IAC_API_AppleEvtObjects.md#50532410_25583).

**Related methods**

- [delete](IAC_API_AppleEvtObjects.md#50532410_41487)
- [perform](IAC_API_AppleEvtObjects.md#50532410_27016)

<a id="50532410_45214"></a>
### menu

A menu in the Acrobat or Acrobat Reader menu bar.

**Elements**

| Element | Accessed by |
| --- | --- |
| [menu item](IAC_API_AppleEvtObjects.md#50532410_78053) | name, numeric index. |

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| best type | type class \[r/o\] | The best descriptor type. |
| class | type class \[r/o\] | The class. |
| default type | type class \[r/o\] | The default descriptor type. |
| name | international text \[r/o\] | The menu’s name (a language-independent name that uniquely identifies the menu). See the *Acrobat and PDF Library API Reference* for a list of menu names. |
| title | string \[r/o\] | The menu’s title as it would appear in the user interface. |

**Related methods**

- [execute](IAC_API_AppleEvtObjects.md#50532410_21312)

<a id="50532410_78053"></a>
### menu item

A menu item contained within a menu in Acrobat or Acrobat Reader.

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| best type | type class \[r/o\] | The best descriptor type. |
| class | type class \[r/o\] | The class. |
| default type | type class \[r/o\] | The default descriptor type. |
| enabled | Boolean \[r/o\] | Determines whether the menu item is enabled. |
| has submenu | Boolean \[r/o\] | Determines whether the menu item has a hierarchical sub-menu. |
| marked | Boolean \[r/o\] | Determines whether the menu item is checked. |
| name | international text \[r/o\] | The menu item’s language-independent name. See the *Acrobat and PDF Library API Reference* for a list of menu item names. |
| title | string \[r/o\] | The menu’s title as it would appear in the user interface. |

**Related methods**

- [execute](IAC_API_AppleEvtObjects.md#50532410_21312)

<a id="50532410_24065"></a>
page

A single page in the PDF representation of a document. Corresponds to Acrobat’s internal `PDPage` object.

> **Note**
>
> This object was formerly known as `PDPage`.

**Elements**

| Element | Accessed by |
| --- | --- |
| annotation | numeric index. |

**Plural form**

Pages

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| best type | type class \[r/o\] | The best descriptor type. |
| bounds | list of small real | The boundary rectangle for the page in user space (left, top, right, bottom). |
| class | type class \[r/o\] | The class. |
| default type | type class \[r/o\] | The default descriptor type. |
| page number | integer \[r/o\] | The page’s number. The first page in a document is page 1. |
| rotation | integer | The rotation angle of the page in degrees (0, 90, 180, or 270). |

**Related methods**

- [delete pages](IAC_API_AppleEvtObjects.md#50532410_15460)
- [insert pages](IAC_API_AppleEvtObjects.md#50532410_35783)
- [replace pages](IAC_API_AppleEvtObjects.md#50532410_27808)
- [goto](IAC_API_AppleEvtObjects.md#50532410_16433)
- [move](IAC_API_AppleEvtObjects.md#50532410_34612)

### PDAnnot

> **Note**
>
> Deprecated. Use [annotation](IAC_API_AppleEvtObjects.md#50532410_25583) instead.

### PDBookMark

> **Note**
>
> Deprecated. Use [bookmark](IAC_API_AppleEvtObjects.md#50532410_75140) instead.

<a id="50532410_21206"></a>
### PDLinkAnnot

> **Note**
>
> Deprecated. Use [Link Annotation](IAC_API_AppleEvtObjects.md#50532410_90412) instead.

### PDPage

> **Note**
>
> Deprecated. Use [page](IAC_API_AppleEvtObjects.md#50532410_51939) instead.

### PDTextAnnot

> **Note**
>
> Deprecated. Use [Text Annotation](IAC_API_AppleEvtObjects.md#50532410_22569) instead.

<a id="50532410_29037"></a>
### PDF Window

The area of the Acrobat or Acrobat Reader window that displays the contents of a page within the document. Corresponds to the Acrobat internal `AvPageView` object. A document that is not visible does not have a `PDF Window`.

> **Note**
>
> This object was formerly known as `AVPageView`.

**Elements**

| Element | Accessed by |
| --- | --- |
| [page](IAC_API_AppleEvtObjects.md#50532410_24065) | numeric index. The first page in a document is page 1. |

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| best type | type class \[r/o\] | The best descriptor type. |
| bounds | bounding rectangle | The boundary rectangle for the window. |
| class | type class \[r/o\] | The class. |
| default type | type class \[r/o\] | The default descriptor type. |
| document | document \[r/o\] | The document that owns this window. |
| index | integer | The number of the window. |
| name | international text \[r/o\] | The document’s name as shown in the window’s titlebar. |
| page number | integer | The number of the currently displayed page. |
| position | point \[r/o\] | The upper left coordinates of the window. |
| visible | Boolean \[r/o\] | Whether the window is visible. |
| zoomed | Boolean | Whether the window is zoomed. |
| zoom factor | small real | The current zoom factor specified as a percentage. For example, a value of 100 corresponds to a zoom factor of 1.0 (100%). |
| zoom type | constant | The zooming and content fitting algorithm currently employed. Possible values: `no vary`, `fit page`, `fit width`, `fit height`, and `fit visible width`. |

**Related methods**

- [go backward](IAC_API_AppleEvtObjects.md#50532410_33904)
- [go forward](IAC_API_AppleEvtObjects.md#50532410_30533)
- [goto](IAC_API_AppleEvtObjects.md#50532410_16433)
- [goto next](IAC_API_AppleEvtObjects.md#50532410_24656)
- [goto previous](IAC_API_AppleEvtObjects.md#50532410_21200)
- [read page down](IAC_API_AppleEvtObjects.md#50532410_32063)
- [read page up](IAC_API_AppleEvtObjects.md#50532410_37225)
- [scroll](IAC_API_AppleEvtObjects.md#50532410_21493)
- [select text](IAC_API_AppleEvtObjects.md#50532410_27478)
- [zoom](IAC_API_AppleEvtObjects.md#50532410_35096)

<a id="50532410_17521"></a>
### PostScript Conversion

A file type converter that exports PDF files into PostScript format.

**Properties**

Inherits other properties from [conversion](IAC_API_AppleEvtObjects.md#50532410_56571).

| Property | Class | Description |
| --- | --- | --- |
| annotations | Boolean \[r/o\] | Determines whether to include annotations. |
| binary | Boolean \[r/o\] | Determines whether the output file should be in binary or ASCII text format. |
| embedded fonts | Boolean \[r/o\] | Determines whether to include fonts. |
| halftones | Boolean \[r/o\] | Determines whether to use halftone screens. |
| images | Boolean \[r/o\] | Determines whether to include RGB and LAB images. |
| postScript level | integer \[r/o\] | The PostScript Language level. Only levels 2 and 3 are supported. |
| preview | Boolean \[r/o\] | Determines whether to include preview in output. |
| TrueType | Boolean \[r/o\] | Determines whether to convert TrueType fonts to Type 1. |

**Related methods**

- [save](IAC_API_AppleEvtObjects.md#50532410_32794)

<a id="50532410_22569"></a>
### Text Annotation

A PDF text annotation (note) on a page in a PDF file. Can only be used as the target of a [make](IAC_API_AppleEvtObjects.md#50532410_24328) event. All other access is via the [annotation](IAC_API_AppleEvtObjects.md#50532410_25583) class.

> **Note**
>
> This object was formerly known as `TextAnnot`.

**Properties**

Inherits from [annotation](IAC_API_AppleEvtObjects.md#50532410_25583).

**Related methods**

- [find next note](IAC_API_AppleEvtObjects.md#50532410_15335)
- [perform](IAC_API_AppleEvtObjects.md#50532410_27016)
- [replace pages](IAC_API_AppleEvtObjects.md#50532410_27808)

## Required suite events

The following events are sent by the Finder to all applications:

- `open`
- `print`
- `quit`
- `run`

> **Note**
>
> Most of these events have counterparts in the Core suite that have greater functionality. The Required suite is not listed in the AppleScript dictionary, even though it is implemented.

Acrobat Reader also supports the Required suite events, but no others.

<a id="50532410_99533"></a>
### open

Opens a file.

**Syntax**

```
open [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| open | The file or files to open. |

<a id="50532410_29870"></a>
### print

Prints one or more files.

**Syntax**

```
print
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| print | The file or files to print. |

<a id="50532410_37698"></a>
### quit

Terminates an application. For information on a variant event in the Core suite that accepts options, see [quit](IAC_API_AppleEvtObjects.md#50532410_14269).

**Syntax**

```
quit
```

<a id="50532410_40886"></a>
### run

Launches the application and invokes its standard startup procedures.

**Syntax**

```
run
```

## Core suite events

Acrobat supports the following subset of the Core suite of Apple events:

- `close`
- `count`
- `delete`
- `exists`
- `get`
- `make`
- `move`
- `open`
- `quit`
- `save`
- `set`

<a id="50532410_39856"></a>
### close

Closes a document.

**Syntax**

```
close
 [reference] saving
 [constant] linearize
 [boolean]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| close | The document to close. |
| saving | Determines whether to save a document that has been modified before quitting. Possible values:  `yes`: Save the document.  `no`: Do not save the document.  `ask`: Ask the user whether to save the document.  The default value is `ask`. |
| linearize | Determines whether the document should be optimized for the web when saving before closing. |

**Related events**

- [open](IAC_API_AppleEvtObjects.md#50532410_41641)

<a id="50532410_16155"></a>
### count

Counts the number of instances of a particular class.

**Syntax**

```
count
 [type class] of
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| count | The class whose instances are to be counted. |
| each | The class whose instances are to be counted. This keyword is optional. |

> **Note**
>
> There is an alternate form using the keyword `each` in which the parameters are reversed:

```
      count
[reference] each
[type class]
```

**Returns**

An integer specifying the number of elements.

**AppleScript example**

```
count annotation of document "dev_acro.pdf"
count menu item of menu "View"
count document 1 each bookmark
```

<a id="50532410_41487"></a>
### delete

Deletes one or more objects.

**Syntax**

```
delete
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| delete | The object to be deleted. |

**Related events**

- [make](IAC_API_AppleEvtObjects.md#50532410_24328)
- [exists](IAC_API_AppleEvtObjects.md#50532410_24542)

**AppleScript example**

```
delete first bookmark of document "test.pdf"
```

<a id="50532410_24542"></a>
### exists

Tests whether a specified object exists.

**Syntax**

```
[reference] exists

exists
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| exists | Object whose existence is checked. |

**Returns**

`true` if the object exists, `false` otherwise.

**AppleScript example**

```
exists second document

second document exists
```

<a id="50532410_32661"></a>
### get

Retrieves the value of an object or property.

**Syntax**

```
get [reference] as [class]
```

> **Note**
>
> The keyword `get` is optional.

**Parameters**

| Parameter | Description |
| --- | --- |
| get | The object or property whose value is returned. |
| as | The form in which the data is returned. |

**Returns**

The value of the specified property or object. If the specified object does not exist, no result is returned.

**Related events**

- [set](IAC_API_AppleEvtObjects.md#50532410_41279)

**AppleScript example**

```
get the name of last bookmark
get the index of last bookmark as string
```

<a id="50532410_24328"></a>
### make

Creates a new object.

**Syntax**

```
make
 new [
type class] at
 [location reference] with data
 [anything] with properties
 [record]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| make \[new\] | The class of the new object. |
| at | The location at which to insert the new object. |
| with data | The initial data for the new object. |
| with properties | The initial values for the properties of the new object. |

**Returns**

A reference to the newly created object.

**Related events**

- [delete](IAC_API_AppleEvtObjects.md#50532410_41487)
- [exists](IAC_API_AppleEvtObjects.md#50532410_24542)

**AppleScript example**

```
set myAnnotation to make TextAnnotation at beginning
set name of myAnnotation to "Werner Heisenberg"
set contents of myAnnotation to "Might have been here"
```

<a id="50532410_34612"></a>
### move

Moves a [page](IAC_API_AppleEvtObjects.md#50532410_24065) object.

**Syntax**

```
move
 [reference] to
 [location reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| move | The page object to move. The first page in a document is page 1. |
| to | The new location for the page. |

**Returns**

A reference to the page that is moved.

**AppleScript example**

```
move page 3 to before page 1
```

<a id="50532410_41641"></a>
### open

Opens a document or documents.

**Syntax**

```
open
 [list of alias] invisible
 [boolean] options
 [string]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| open | The document or documents to open. |
| invisible | Whether the opened document should be hidden. Default is `false`. |
| options | Optional parameter string of open actions. |

**Related events**

- [close](IAC_API_AppleEvtObjects.md#50532410_39856)

<a id="50532410_14269"></a>
### quit

Causes the Acrobat application to quit.

**Syntax**

```
quit
 saving [constant]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| saving | Determines whether to save documents that have been modified before quitting. Possible values:  `yes`: Save the document.  `no`: Do not save the document.  `ask`: If the documents have been modified, ask the user whether to save them.  The default value is `ask`. |

**AppleScript example**

```
quit saving yes
```

<a id="50532410_32794"></a>
### save

Saves a document.

**Syntax**

```
save
 [reference] to
 [file specification] using
 [reference] linearize[
 boolean]
```

**Parameters**

| save | The document to be saved. |
| --- | --- |
| to | The file into which the document is to be saved. This parameter is optional in Acrobat 6.0 and higher. Specifying the `to` parameter is equivalent to doing a Save As. You can save a document in one of the supported formats with the `using` parameter. |
| linearize | Determines whether the document should be optimized for the web. |
| using | The conversion method used to save the document in the desired format. Supported conversions by name are [EPS Conversion](IAC_API_AppleEvtObjects.md#50532410_79350) and [PostScript Conversion](IAC_API_AppleEvtObjects.md#50532410_17521). All others can be specified by index using the [conversion](IAC_API_AppleEvtObjects.md#50532410_56571) object. |

**AppleScript example**

```
save document 1 to file "MyHardDrive:tempBig.ps" using PostScript Conversion with embedded fonts, images, preview, and annotation without binary given postScript level: 1
```

<a id="50532410_41279"></a>
### set

Sets an object’s data or properties.

**Syntax**

```
set
 [reference] to
 [anything]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| set | The object or property whose value is set. |
| to | The new value. |

**Related events**

- [get](IAC_API_AppleEvtObjects.md#50532410_32661)

**AppleScript example**

```
set the name of first bookmark to "Chapter 1"
```

## Acrobat application events

This section describes a number of Acrobat API calls for the Apple event interface that are specific to Acrobat applications. The supported events in this suite are:

- `bring to front`
- `clear selection`
- `close all docs`
- `create thumbs`
- `delete pages`
- `delete thumbs`
- `execute`
- `find next note`
- `find text`
- `get info`
- `go backward`
- `go forward`
- `goto`
- `goto next`
- `goto previous`
- `insert pages`
- `is toolbutton enabled`
- `maximize`
- `perform`
- `print pages`
- `read page down`
- `read page up`
- `remove toolbutton`
- `replace pages`
- `scroll`
- `select text`
- `set info`
- `zoom`

Apple encourages the use of an application’s signature as the name of its class for application-specific Apple events. The string `CARO` is the name of the class for Acrobat-specific Apple events:

```
#define kAEAcrobatViewerClass 'CARO'
```

AppleScript does not need this information.

<a id="50532410_19936"></a>
### bring to front

Brings the specified document’s window to the front.

**Syntax**

```
bring to front
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bring to front | The document to be displayed as the active document in the front window. |

**AppleScript example**

```
bring to front document "AppleEvt.pdf"
```

**Apple event ID**

```
kAEBringToFront ('bfrt')
```

<a id="50532410_33043"></a>
### clear selection

Clears the document’s current selection, if any.

**Syntax**

```
clear selection
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| clear selection | The document containing the selection to be cleared |

**Related events**

- [select text](IAC_API_AppleEvtObjects.md#50532410_27478)

**AppleScript example**

```
clear selection document "PLUGINS.PDF"
```

**Apple event ID**

```
kAEClearSelection ('clsl')
```

<a id="50532410_31136"></a>
### close all docs

Closes all documents.

**Syntax**

```
close all docs
 saving
 [constant]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| saving | Determines whether to save modified documents before closing. Possible values:  `yes`: Save the document.  `no`: Do not save the document.  `ask`: If the document has been modified, ask the user whether to save it.  The default value is `ask`. |

**Related events**

- [open](IAC_API_AppleEvtObjects.md#50532410_99533) (Required suite)
- [open](IAC_API_AppleEvtObjects.md#50532410_41641) (Core suite)

**AppleScript example**

```
close all docs
```

**Apple event ID**

```
kAECloseAllDocs ('cldc')
```

<a id="50532410_15865"></a>
### create thumbs

Creates thumbnail images for all pages in the document.

**Syntax**

```
create thumbs
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| create thumbs | The document in which thumbnails are created. |

**Related events**

- [delete thumbs](IAC_API_AppleEvtObjects.md#50532410_29225)

**AppleScript example**

```
create thumbs document "roadmap.pdf"
```

**Apple event ID**

```
kAECreateThumbs ('crtb')
```

<a id="50532410_15460"></a>
### delete pages

Deletes the specified pages in the document.

**Syntax**

```
delete pages
 [reference] first
 [integer] last [
integer]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| delete pages | The document containing the pages to be deleted. |
| first | The first page to be deleted. The first page in a document is page 1. |
| last | The last page to be deleted. |

**Related events**

- [insert pages](IAC_API_AppleEvtObjects.md#50532410_35783)
- [replace pages](IAC_API_AppleEvtObjects.md#50532410_27808)

**AppleScript example**

```
delete pages document "AppleEvt.pdf" first 1 last 3
```

**Apple event ID**

```
kAEDeletePages ('dlpg')
```

**Apple event parameters**

```
keyAEFirstPage ('frpg')
keyAELastPage ('lapg'')
```

<a id="50532410_29225"></a>
### delete thumbs

Deletes all thumbnails from the document.

**Syntax**

```
delete thumbs
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| delete thumbs | The document from which thumbnails are deleted. |

**Related events**

- [create thumbs](IAC_API_AppleEvtObjects.md#50532410_15865)

**AppleScript example**

```
delete thumbs document "AppleEvt.pdf"
```

**Apple event ID**

```
kAEDeleteThumbs ('dltb')
```

<a id="50532410_21312"></a>
### execute

Executes the specified menu item.

**Syntax**

```
execute
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| execute | The menu item to execute. See the *Acrobat and PDF Library API Reference* for a list of menu item names. |

**AppleScript example**

```
activate
execute menu item "Open"
```

**Apple event ID**

```
kAEExecute ('exec')
```

<a id="50532410_15335"></a>
### find next note

Finds and selects the next text note in a document.

**Syntax**

```
find next note
 [reference] wrap around
 [boolean]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| find next note | The document in which to find the next text note. |
| wrap around | Determines whether to continue the search at the beginning of a document if a note has not been found after the end of the document is reached. If `true`, the search wraps around; otherwise it does not. The default value is `false`. |

**Returns**

The text annotation found.

**Related events**

- [find text](IAC_API_AppleEvtObjects.md#50532410_15620)

**AppleScript example**

```
find next note document "dev_acro.pdf"
```

**Apple event ID**

```
kAEFindNextNote ('fnnt')
```

**Apple event parameters**

```
keyAEWrapAround ('wrar')
```

<a id="50532410_15620"></a>
### find text

Finds text in a document.

**Syntax**

```
find text
 [reference] string
 [international text] case sensitive
 [boolean] whole words
 [boolean] wrap around
 [boolean]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| find text | The document to be searched. |
| string | The string to be found. |
| case sensitive | Determines whether searching is case-sensitive. The default value is `false`. |
| whole words | Determines whether to search only for whole words. The default value is `false`. |
| wrap around | Determines whether to continue the search at the beginning of a document if the specified text has not been found after the end of the document is reached. If `true`, the search wraps around; otherwise it does not. The default value is `false`. |

**Related events**

- [find next note](IAC_API_AppleEvtObjects.md#50532410_15335)

**AppleScript example**

```
find text document "PLUGINS.PDF" string "Develop" whole words true
```

**Apple event ID**

```
kAEFindText ('ftxt')
```

**Apple event parameters**

```
keyAESearchString ('sstr')
keyAECaseSensitive ('case')
keyAEWholeWordsOnly ('whwd')
keyAEWrapAround ('wrar')
```

<a id="50532410_19217"></a>
### get info

Gets the value of the specified key in the document’s `Info` dictionary.

**Syntax**

```
get info
 [reference] key
 [international text]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| get info | The document from which to obtain the `Info` dictionary entry. |
| key | The case-sensitive `Info` dictionary key whose value is to be obtained. The predefined keys are: `Creator`, `Producer`, `CreationDate`, `Author`, `Title`, `Subject`, and `Keywords`. None of these is required in the PDF file. |

**Returns**

A string containing the specified key’s value, or an empty string if the key is not found.

**AppleScript example**

```
get info document "PLUGINS.PDF" key "CreationDate"
```

**Apple event ID**

```
kAEGetInfo ('gnfo')
```

**Apple event parameters**

```
keyAEInfoKey ('inky')
```

<a id="50532410_33904"></a>
### go backward

Goes to the previous view in the stored view history. Does nothing if the current view is the first view in the history.

**Syntax**

```
go backward
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| go backward | A [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object |

**Related events**

- [go forward](IAC_API_AppleEvtObjects.md#50532410_30533)
- [goto](IAC_API_AppleEvtObjects.md#50532410_16433)
- [goto next](IAC_API_AppleEvtObjects.md#50532410_24656)
- [goto previous](IAC_API_AppleEvtObjects.md#50532410_21200)

**AppleScript example**

```
go backward first PDF Window
```

**Apple event ID**

```
kAEGoBack ('gbck')
```

<a id="50532410_30533"></a>
### go forward

Goes to the next view in the stored view history. Does nothing if the current view is the last view in the history.

**Syntax**

```
go forward
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| go forward | A [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object |

**Related events**

- [go backward](IAC_API_AppleEvtObjects.md#50532410_33904)
- [goto](IAC_API_AppleEvtObjects.md#50532410_16433)
- [goto next](IAC_API_AppleEvtObjects.md#50532410_24656)
- [goto previous](IAC_API_AppleEvtObjects.md#50532410_21200)

**AppleScript example**

```
go forward first PDF Window
```

**Apple event ID**

```
kAEGoForward ('gfwd')
```

<a id="50532410_16433"></a>
### goto

Displays the page that has the specified page number.

**Syntax**

```
goto
 [reference] page
 [integer]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| goto | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object in which to change the page. |
| page | The page number of the page to be displayed. The first page in a document is page 1. |

**Related events**

- [go backward](IAC_API_AppleEvtObjects.md#50532410_33904)
- [go forward](IAC_API_AppleEvtObjects.md#50532410_30533)
- [goto next](IAC_API_AppleEvtObjects.md#50532410_24656)
- [goto previous](IAC_API_AppleEvtObjects.md#50532410_21200)

**AppleScript example**

```
goto first PDF Window page 2
```

**Apple event ID**

```
kAEGotoPage ('gtpg')
```

**Apple event parameters**

```
keyAEPageNumber ('pg #')
```

<a id="50532410_24656"></a>
### goto next

Displays the next page after the one currently displayed in the [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037). Does nothing if the current page is the last page in the document.

**Syntax**

```
goto next
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| goto next | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object in which to change the page. |

**Related events**

- [go backward](IAC_API_AppleEvtObjects.md#50532410_33904)
- [go forward](IAC_API_AppleEvtObjects.md#50532410_30533)
- [goto](IAC_API_AppleEvtObjects.md#50532410_16433)
- [goto previous](IAC_API_AppleEvtObjects.md#50532410_21200)

**AppleScript example**

```
goto next first PDF Window
```

**Apple event ID**

```
kAEGotoNextPage ('nxpg')
```

<a id="50532410_21200"></a>
### goto previous

Displays the previous page before the one currently displayed in the [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037). Does nothing if the current page is the first page in the document.

**Syntax**

```
goto previous
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| goto previous | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object in which to change the page. |

**Related events**

- [go backward](IAC_API_AppleEvtObjects.md#50532410_33904)
- [go forward](IAC_API_AppleEvtObjects.md#50532410_30533)
- [goto](IAC_API_AppleEvtObjects.md#50532410_16433)
- [goto next](IAC_API_AppleEvtObjects.md#50532410_24656)

**AppleScript example**

```
goto previous first PDF Window
```

**Apple event ID**

```
kAEGotoPrevPage ('pvpg')
```

<a id="50532410_35783"></a>
### insert pages

Inserts one or more pages from one document into another.

**Syntax**

```
insert pages
 [reference] after
 [integer] from
 [reference] starting with
 [integer] number of pages
 [integer] insert bookmarks
 [boolean]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| insert pages | The target document in which to insert the page or pages. |
| after | The number of the page after which the pages will be inserted. The first page in a document is page 1. |
| from | The source document containing the page or pages to be inserted. |
| starting with | The first page to be inserted. |
| number of pages | The number of pages to be inserted. |
| insert bookmarks | Determines whether to copy bookmarks that point to the inserted pages. Default is `true`. |

**Related events**

- [delete pages](IAC_API_AppleEvtObjects.md#50532410_15460)

**AppleScript example**

```
insert pages document "AppleEvt.pdf" after 2 from document "dev_acro.pdf" starting with 1 number of pages 4
```

**Apple event ID**

```
kAEInsertPages ('inpg')
```

**Apple event parameters**

```
keyAEInsertAfter ('inaf')
keyAESourceDoc ('srdc')
kAESourceStartPage ('stpg')
keyAENumPages ('nmpg')
keyAEInsertBookmarks ('inbm')
```

<a id="50532410_40528"></a>
### is toolbutton enabled

Determines whether the specified toolbar button is enabled.

**Syntax**

```
is toolbutton enabled named
 [international text]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| named | Button name. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of toolbar button names. |

**Returns**

`true` if the toolbar button is enabled, `false` otherwise.

**Related events**

- [remove toolbutton](IAC_API_AppleEvtObjects.md#50532410_11291)

**AppleScript example**

```
is toolbutton enabled named "AcroSrch:Query"
```

**Apple event ID**

```
kAEIsToolButtonEnabled ('tben')
```

**Apple event parameters**

```
keyAEButtonname ('tbnm')
```

<a id="50532410_26208"></a>
### maximize

Sets the document’s window size to either its maximum or original size.

**Syntax**

```
maximize
 [reference] max size
 [integer]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| maximize | The document whose window is to be resized. |
| max size | If `true`, the document’s window is set to full size. If `false`, the window is returned to its original size. |

**AppleScript example**

```
maximize document "AppleEvt.pdf" max size false
```

**Apple event ID**

```
kAEMaximize ('maxi')
```

**Apple event parameters**

```
keyAEMaxSize ('mxsz')
```

<a id="50532410_27016"></a>
### perform

Executes a bookmark’s or link annotation’s action.

**Syntax**

```
perform
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| object | The [bookmark](IAC_API_AppleEvtObjects.md#50532410_75140) or [page](IAC_API_AppleEvtObjects.md#50532410_24065) object whose action is to be performed. |

**AppleScript example**

```
perform last bookmark
```

**Apple event ID**

```
kAEPerform ('prfm')
```

<a id="50532410_40027"></a>
### print pages

Prints one or more pages from a document without displaying a modal Print dialog box.

**Syntax**

```
print pages
 [reference] first
 [integer] last
 [integer] PS Level
 [integer] binary output
 [boolean] shrink to fit
 [boolean]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| print pages | The document containing the page or pages to be printed. This keyword and the actual filename must be specified. |
| first | The first page to be printed. The default value is 1. |
| last | The last page to print. The default value is the number of the last page in the document. |
| PS Level | The PostScript language level (1 or 2) to use when printing to a PostScript printer. The default value is 1. |
| binary output | Determines whether binary output is permitted (used for PostScript printing only). The default value is `false`. |
| shrink to fit | Determines whether pages should be shrunk to fit paper in printer. The default value is `false`. |

**AppleScript example**

```
print pages document "AppleEvt.pdf" first 1 last 3 PS Level 2 binary output true shrink to fit true
```

**Apple event ID**

```
kAEPrintPages ('prpg')
```

**Apple event parameters**

```
keyAEFirstPage ('frpg')
keyAELastPage ('lapg')
keyAEPSLevel ('pslv')
keyAEBinaryOK ('binO')
keyAEShrinkToFit ('s2ft')
```

<a id="50532410_32063"></a>
### read page down

Scrolls forward through the document by one screen.

**Syntax**

```
read page down
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| read page down | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object to be scrolled. |

**Related events**

- [read page up](IAC_API_AppleEvtObjects.md#50532410_37225)
- [scroll](IAC_API_AppleEvtObjects.md#50532410_21493)

**AppleScript example**

```
read page down first PDF Window
```

**Apple event ID**

```
kAEReadPageDown ('pgdn')
```

<a id="50532410_37225"></a>
### read page up

Scrolls backward through the document by one screen.

**Syntax**

```
read page up
 [reference]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| read page up | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object to be scrolled. |

**Related events**

- [read page down](IAC_API_AppleEvtObjects.md#50532410_32063)
- [scroll](IAC_API_AppleEvtObjects.md#50532410_21493)

**AppleScript example**

```
read page up first PDFPageWindow
```

**Apple event ID**

```
kAEReadPageUp ('pgup')
```

<a id="50532410_11291"></a>
### remove toolbutton

Removes the specified button from the toolbar.

**Syntax**

```
remove toolbutton named
 [international text]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| named | The name of the toolbar button to be removed. See the *Acrobat and PDF Library API Reference* for a list of toolbar button names. |

**Related events**

- [is toolbutton enabled](IAC_API_AppleEvtObjects.md#50532410_40528)

**AppleScript example**

```
remove toolbutton named "ZoomIn"
```

**Apple event ID**

```
kAERemoveToolButton ('rmtb')
```

**Apple event parameters**

```
keyAEButtonname ('tbnm')
```

<a id="50532410_27808"></a>
### replace pages

Replaces one or more pages in a document with pages from another document.

**Syntax**

```
replace pages
 [reference] over
 [integer] from
 [reference] starting with
 [integer] number of pages
 [integer] merge notes
 [boolean]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| replace pages | The target document whose pages are to be replaced. |
| over | The first page to be replaced. The first page in a document is page 1. |
| from | The source document from which the replacement page or pages are obtained. |
| starting with | The first page in the source document to be copied. |
| number of pages | The number of pages to be replaced. |
| merge notes | Determines whether to copy notes from the source document. The default value is `true`. |

**Related events**

- [delete pages](IAC_API_AppleEvtObjects.md#50532410_15460)
- [insert pages](IAC_API_AppleEvtObjects.md#50532410_35783)

**AppleScript example**

```
replace pages document "AppleEvt.pdf" over 2 from document "dev_acro.pdf" starting with 1 number of pages 4 merge notes false
```

**Apple event ID**

```
kAEReplacePages ('rppg')
```

**Apple event parameters**

```
keyAEDestStartPage ('dtpg')
keyAESourceDoc ('srdc')
keyAESourceStartPage ('stpg')
keyAENumPages ('nmpg')
keyAEMergeNotes ('mgnt')
```

<a id="50532410_21493"></a>
### scroll

Scrolls the view of a page by the specified amount.

**Syntax**

```
scroll
 [reference] X Amount
 [integer] Y Amount
 [integer]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| scroll | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object in which to scroll the view. |
| X Amount | The amount to scroll in the horizontal direction, in pixels. Positive values move the view to the right. |
| Y Amount | The amount to scroll in the vertical direction, in pixels. Positive values move the view down. |

**Related events**

- [read page down](IAC_API_AppleEvtObjects.md#50532410_32063)
- [read page up](IAC_API_AppleEvtObjects.md#50532410_37225)

**AppleScript example**

```
scroll first PDFWindow X Amount 20 Y Amount 100
```

**Apple event ID**

```
kAEScroll ('scrl')
```

**Apple event parameters**

```
keyAEXDelta ('xdlt')
keyAEYDelta ('ydlt')
```

<a id="50532410_27478"></a>
### select text

Selects text as specified by either character or word offsets.

**Syntax**

```
select text
 [reference] from words
 [list of integer] from chars
 [list of integer]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| select text | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object in which to select text. |
| from words | The words to be selected. This consists of one or more pairs of word offsets from the beginning of the document and word lengths (the number of contiguous words). |
| from chars | Characters to be selected. This consists of one or more pairs of character offsets from the beginning of the document and character lengths (the number of contiguous characters). |

**Related events**

- [clear selection](IAC_API_AppleEvtObjects.md#50532410_33043)

**AppleScript example**

```
repeat with i from 1 to 10
       repeat with j from 1 to (10 - i)
       select text from words {i, j}
   end repeat
end repeat
```

**Apple event ID**

```
kAESetTextSelection ('stxs')
```

**Apple event parameters**

```
keyAEWordList ('fmwd')
keyAECharList ('fmch')
```

<a id="50532410_18444"></a>
### set info

Sets the value of a specified key in the document’s `Info` dictionary

**Syntax**

```
set info
 [reference] key
 [international text] value
 [international text]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| set info | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) in which to set the value of an `Info` dictionary entry. |
| key | The `Info` dictionary key whose value is to be set. |
| value | The value to be stored. |

**AppleScript example**

```
set info document "PlugIns.pdf" key "Author"

value "Wolfgang Pauli"
```

**Apple event ID**

```
kAESetInfo ('snfo')
```

**Apple event parameters**

```
keyAEInfoKey ('inky')
keyAEInfoValue ('invl')
```

<a id="50532410_35096"></a>
### zoom

Changes the zoom level of the specified [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037).

**Syntax**

```
zoom
 [reference] to
 [small real]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| zoom | The [PDF Window](IAC_API_AppleEvtObjects.md#50532410_29037) object to be zoomed. |
| to | The zoom factor specified as a percentage. For example, a value of 100 (100%) displays the document with a magnification of 1.0. |

**AppleScript example**

```
zoom first PDFWindow to 150
```

**Apple event ID**

```
kAEZoomTo ('zmto')
```

**Apple event parameters**

```
keyAEZoomFactor ('zmft')
```

## Miscellaneous events

Acrobat provides an Apple event that does not fall into one of the regular suites: [do script](IAC_API_AppleEvtObjects.md#50532410_82140)

<a id="50532410_82140"></a>
### do script

Executes the specified JavaScript script.

**Syntax**

```
do script
 [international text] file
 [alias]
```

**Parameters**

| Parameter | Description |
| --- | --- |
| do script | The JavaScript script to be executed. |
| file | File holding the JavaScript script to be executed. |

**Returns**

Result of JavaScript execution as text.

**AppleScript example**

```
do script MyJavaScriptFile.js
```
