# Annotation APIs

<a id="annotattachment"></a>
<a id="id12"></a>
## annotAttachment

The `annotAttachment` object represents the file stored as the attachment for a `FileAttachment` type annotation. `annotAttachment` is similar to the `Data` object and represents the file content and metadata of the attachment.

See the [PDF Reference](https://adobe.com/go/pdfreference) for additional details on annotations.

<a id="annotattachment-properties"></a>
<a id="id14"></a>
### annotAttachment properties

<a id="72818"></a>
<a id="contentstream"></a>
<a id="id15"></a>
#### contentStream

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | All | object | R |

A `ReadStream` property representing the file attachment stream. This property enables access to the contents of the file attachment associated with an `annotAttachment` object.

A `NotAllowedError` is thrown and the method fails if it attempts to access the content of an embedded file attachment for which any of the following conditions is true (all file name extension matching is case-insensitive):

- The attachment’s file name extension is “.SWF”. If a legitimate.SWF application or module run as part of Acrobat’s Rich Media Annotation or PDF Portfolio navigator is allowed access to the content bytes of.SWF embedded file attachments, it is possible that the legitimate.SWF will load a malicious.SWF.

> **Note**
>
> If you use the `Data.MIMEType` property to check whether a Data object represents a.SWF file, note that the MIME type for.SWF files is `application/x-shockwave-flash`.

- The attachment’s file name extension is “.GIF”, “.JPG”, “.JPEG”, or “.PNG” and the first three bytes of its content have the header signature of a.SWF file (“FWS” or “CWS”). The reason for this security restriction is that the same `ActionScriptflash.display.Loader class load()` method that can be used to load GIF, JPEG, and PNG images can also be used to load a SWF file. If a malicious SWF file’s extension has been altered to that of one of these image types, the SWF could be loaded.

<a id="34862"></a>
<a id="creationdate"></a>
<a id="id16"></a>
#### creationDate

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | All | date | R |

The date of creation of the attached file.

<a id="43017"></a>
<a id="mimetype"></a>
<a id="id17"></a>
#### MIMEtype

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | All | string | R |

The MIME type of the attached file.

<a id="87427"></a>
<a id="moddate"></a>
<a id="id18"></a>
#### modDate

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | No | date | R |

The date of modification of the attached file.

<a id="39211"></a>
<a id="name"></a>
<a id="id19"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | All | string | R |

The name of the attached file.

<a id="17608"></a>
<a id="pathname"></a>
<a id="id20"></a>
#### pathname

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | All | string | R |

The pathname of the attached file.

<a id="22417"></a>
<a id="size"></a>
<a id="id21"></a>
#### size

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | All | number | R |

The size, in bytes, of the uncompressed attachment.

Example:

```
var annot = this.addAnnot({
    page: 0
    type: "FileAttachment",
    point: [400,500],
    author: "A. C. Robat",
    contents: "Call Smith to get help on this paragraph.",
    cAttachmentPath: "/d/a.pdf",
});
var attachObj = annot.attachment;
console.println("Name: " + attachObj.name);
console.println("Type: " + attachObj.MIMEType);
console.println("Size: "+ attachObj.size);
console.println("==============Content=================");
var stm = attachObj.contentStream;
console.println(util.stringFromStream(stm));
```

<a id="annotation"></a>
<a id="id22"></a>
## Annotation

This object represents an Acrobat annotation. Annotations can be created using the Acrobat annotation tool or by using the Doc object method `addAnnot`.

Before an annotation can be accessed, it must be bound to a JavaScript variable through a Doc object method such as `getAnnot` :

```
var a = this.getAnnot(0, "Important");
```

The script can then manipulate the annotation named “Important” on page 1 (0-based page numbering system) by means of the variable `a`. For example, the following code first stores the type of annotation in the variable `thetype`, then changes the author to “John Q. Public”.

```
var thetype = a.type;          // read property
a.author = "John Q. Public";   // write property
```

Another way of accessing the Annotation object is through the Doc object `getAnnots` method.

> **Note**
>
> In Adobe Reader 5.1 or later, you can get the value of any annotation property except `contents`. The ability to set these properties depends on Comments document rights, as indicated by the *C* icon.

> **Note**
>
> The user interface in Acrobat refers to annotations as *comments*.

<a id="51128"></a>
<a id="annotation-types"></a>
<a id="id23"></a>
### Annotation types

Annotations are of different types, as reflected in the `type` property. Each type is listed in the table below, along with all documented properties returned by the `getProps` method.

| Annotation type | Properties |
|-----------------|------------|
| `Caret` | author, borderEffectIntensity, borderEffectStyle, caretSymbol, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `Circle` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, dash, delay, fillColor, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `FileAttachment` | attachIcon, attachment, author, borderEffectIntensity, borderEffectStyle, cAttachmentPath, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, point, print, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `FreeText` | alignment, author, borderEffectIntensity, borderEffectStyle, callout, contents, creationDate, dash, delay, fillColor, hidden, inReplyTo, intent, lineEnding, lock, modDate, name, noView, opacity, page, print, readOnly, rect, refType, richContents, richDefaults, rotate, seqNum, strokeColor, style, subject, textFont, textSize, toggleNoView, type, width |
| `Highlight` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, quads, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `Ink` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, dash, delay, gestures, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `Line` | arrowBegin, arrowEnd, author, borderEffectIntensity, borderEffectStyle, contents, creationDate, dash, delay, doCaption, fillColor, hidden, inReplyTo, intent, leaderExtend, leaderLength, lock, modDate, name, noView, opacity, page, points, popupOpen, popupRect, print, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `Polygon` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, dash, delay, fillColor, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, vertices, width |
| `PolyLine` | arrowBegin, arrowEnd, author, borderEffectIntensity, borderEffectStyle, contents, creationDate, dash, delay, fillColor, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, vertices, width |
| `Redact` | In addition to all the usual properites of a markup type annotation (see for example, the property list of the `Highlight` type), the properties `alignment`, `overlayText` and `repeat` are particular to the `Redact` annotation. |
| `Sound` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, point, print, readOnly, rect, refType, richContents, rotate, seqNum, soundIcon, strokeColor, style, subject, toggleNoView, type, width |
| `Square` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, dash, delay, fillColor, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `Squiggly` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, quads, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `Stamp` | AP, author, borderEffectIntensity, borderEffectStyle, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, readOnly, rect, refType, rotate, seqNum, strokeColor, style, subject, toggleNoView, type |
| `StrikeOut` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, quads, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |
| `Text` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, noteIcon, opacity, page, point, popupOpen, popupRect, print, readOnly, rect, refType, richContents, rotate, seqNum, state, stateModel, strokeColor, style, subject, toggleNoView, type, width |
| `Underline` | author, borderEffectIntensity, borderEffectStyle, contents, creationDate, delay, hidden, inReplyTo, intent, lock, modDate, name, noView, opacity, page, popupOpen, popupRect, print, quads, readOnly, rect, refType, richContents, rotate, seqNum, strokeColor, style, subject, toggleNoView, type, width |

<a id="annotation-properties"></a>
<a id="id24"></a>
### Annotation properties

The [PDF Reference](https://adobe.com/go/pdfreference) documents all Annotation properties and specifies how they are stored.

Some property values are stored in the PDF document as names and others are stored as strings (see the [PDF Reference](https://adobe.com/go/pdfreference) for details). A property stored as a name can have only 127 characters.

**Examples** of properties that have a 127-character limit include `AP`, `beginArrow`, `endArrow`, `attachIcon`, `noteIcon`, and `soundIcon`.

<a id="99809"></a>
<a id="alignment"></a>
<a id="id27"></a>
#### alignment

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | D | No | C | number | R/W |

Controls the alignment of the text for a `FreeText` annotation.

Beginning with version 8.0, when the annotation is of type `Redact`, this property determines the alignment of the overlayText.

| Alignment | Value |
|-----------|-------|
| Left aligned | 0 |
| Centered | 1 |
| Right aligned | 2 |

**Annotations**: FreeText, Redact

<a id="75359"></a>
<a id="attachment"></a>
<a id="id28"></a>
#### attachment

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | All | object | R |

Represents the `annotAttachment` object for a `FileAttachment` type annotation.

Beginning with version 11.0, when the annotation is of type `FileAttachment`, this property determines the object to be attached. For annotation types other than `FileAttachment`, an undefined value is returned. The `ESErrorGenral` exception occurs if the attachment is invalid.

**Annotations**: FileAttachment

Example:

```
var annot = this.addAnnot({
       page: 0,
       type: "FileAttachment",
       point: [400,500],
       author: "A. C. Robat",
       contents: "Call Smith to get help on this paragraph.",
       cAttachmentPath: "/d/a.pdf"
   });
   var attachmentObj = annot.attachment;
```

<a id="13531"></a>
<a id="ap"></a>
<a id="id29"></a>
#### AP

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

The named appearance of the stamp to be used in displaying a stamp annotation. The names of the standard stamp annotations are given below:

- Approved
- AsIs
- Confidential
- Departmental
- Draft
- Experimental
- Expired
- Final
- ForComment
- ForPublicRelease
- NotApproved
- NotForPublicRelease
- Sold
- TopSecret

**Annotations**: Stamp

Example: Programmatically add a stamp annotation.

```
var annot = this.addAnnot({
    page: 0,
    type: "Stamp",
    author: "A. C. Robat",
    name: "myStamp",
    rect: [400, 400, 550, 500],
    contents: "Try it again, this time with order and method!",
    AP: "NotApproved" });
```

> **Note**
>
> The name of a particular stamp can be found by opening the PDF file in the `Stamps` folder that contains the stamp in question. For a list of stamp names currently in use in the document, see the Doc object icons property.

<a id="17692"></a>
<a id="arrowbegin"></a>
<a id="id30"></a>
#### arrowBegin

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

Determines the line cap style that specifies the shape to be used at the beginning of a line annotation. Permissible values are:

- None (default)
- OpenArrow
- ClosedArrow
- ROpenArrow\*   // Acrobat 6.0
- RClosedArrow\* // Acrobat 6.0
- Butt\*         // Acrobat 6.0
- Diamond
- Circle
- Square
- Slash            // Acrobat 7.0

**Annotations**: Line, PolyLine

Example: See the setProps method.

<a id="57468"></a>
<a id="arrowend"></a>
<a id="id31"></a>
#### arrowEnd

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

Determines the line cap style that specifies the shape to be used at the end of a line annotation. The following list shows the allowed values:

- None (default)
- OpenArrow
- ClosedArrow
- ROpenArrow\*     // Acrobat 6.0
- RClosedArrow\*   // Acrobat 6.0
- Butt\*           // Acrobat 6.0
- Diamond
- Circle
- Square
- Slash              // Acrobat 7.0

**Annotations**: Line, PolyLine

Example: See the setProps method.

<a id="97925"></a>
<a id="attachicon"></a>
<a id="id32"></a>
#### attachIcon

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

The name of an icon to be used in displaying the annotation. Possible values include:

- Paperclip
- PushPin (default)
- Graph
- Tag

**Annotations**: FileAttachment

<a id="80493"></a>
<a id="author"></a>
<a id="id33"></a>
#### author

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

Gets or sets the author of the annotation.

**Annotations**: All

Example: See the contents property.

<a id="14280"></a>
<a id="bordereffectintensity"></a>
<a id="id34"></a>
#### borderEffectIntensity

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

The intensity of the border effect, if any. This represents how cloudy a cloudy rectangle, polygon, or oval is.

**Annotations**: All

<a id="98183"></a>
<a id="bordereffectstyle"></a>
<a id="id35"></a>
#### borderEffectStyle

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

If non-empty, the name of a border effect style. Currently, the only supported border effects are the empty string (nothing) or “C” for cloudy.

**Annotations**: All

<a id="99031"></a>
<a id="callout"></a>
<a id="id36"></a>
#### callout

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | C | array | R/W |

**Annotations**: FreeText

<a id="43581"></a>
<a id="cattachmentpath"></a>
<a id="id37"></a>
#### cAttachmentPath

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | D | No | C | string | W |

(Optional) Represents the device-independent path of the file to be attached. If this property is not set, the user is prompted to select a data file using the File Open dialog box. This property does not apply to annotation types other than `FileAttachment`. See the [PDF Reference](https://adobe.com/go/pdfreference) for additional details.

**Annotations**: FileAttachment

Example:

```
var annot = this.addAnnot({
       page: 0,
       type: "FileAttachment",
       point: [400,500],
       author: "A. C. Robat",
       contents: "Call Smith to get help on this paragraph.",
       cAttachmentPath: "/d/a.pdf"
   });
```

<a id="41597"></a>
<a id="caretsymbol"></a>
<a id="id39"></a>
#### caretSymbol

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

The symbol associated with a Caret annotation, which is a visual symbol that indicates the presence of text edits. Valid values are “” (nothing), “P” (paragraph symbol) or “S” (space symbol).

**Annotations**: Caret

<a id="62713"></a>
<a id="contents"></a>
<a id="id40"></a>
#### contents

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

Accesses the contents of any annotation that has a pop-up window. For sound and file attachment annotations, specifies the text to be displayed as a description.

**Annotations**: All

Example: Create a text annotation, with author and contents specified.

```
var annot = this.addAnnot({
    page: 0,
    type: "Text",
    point: [400,500],
    author: "A. C. Robat",
    contents: "Call Smith to get help on this paragraph.",
    noteIcon: "Help"
});
```

See also the Doc object addAnnot method.

<a id="59581"></a>
<a id="id41"></a>
<a id="id42"></a>
#### creationDate

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | C | date | R |

The date and time when the annotation was created.

**Annotations**: All

<a id="48107"></a>
<a id="dash"></a>
<a id="id43"></a>
#### dash

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | array | R/W |

A dash array defining a pattern of dashes and gaps to be used in drawing a dashed border. For example, a value of \[3, 2\] specifies a border drawn with 3-point dashes alternating with 2-point gaps.

To set the dash array, the `style` property must be set to `D`.

**Annotations**: FreeText, Line, PolyLine, Polygon, Circle, Square, Ink

Example: Assuming `annot` is an `Annotation` object, this example changes the border to dashed.

```
annot.setProps({ style: "D", dash: [3,2] });
```

See also the example following the delay property.

<a id="44387"></a>
<a id="delay"></a>
<a id="id44"></a>
#### delay

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | C | boolean | R/W |

If `true`, property changes to the annotation are queued and then executed when `delay` is set back to `false`. (Similar to the Field object `delay` property.)

**Annotations**: All

Example: Assuming `annot` is an `Annotation` object, the code below changes the border to dashed.

```
annot.delay=true;
annot.style = "D";
annot.dash = [4,3];
annot.delay = false;
```

<a id="61639"></a>
<a id="doc"></a>
<a id="id45"></a>
#### doc

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | C | object | R |

The Doc object of the document in which the annotation resides.

**Annotations**: All

Example: Construct an annotation, and illustrate the use of the `doc` property.

```
var inch = 72;
var annot = this.addAnnot({
    page: 0,
    type: "Square",
    rect: [1*inch, 3*inch, 2*inch, 3.5*inch]
});
/* displays, for example, "file:///C|/Adobe/Annots/myDoc.pdf" */
console.println(annot.doc.URL);
```

<a id="42571"></a>
<a id="docaption"></a>
<a id="id46"></a>
#### doCaption

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | C | boolean | R/W |

**Annotations**: Line

Example: See the example following the points property.

<a id="69717"></a>
<a id="fillcolor"></a>
<a id="id47"></a>
#### fillColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | color | R/W |

Sets the background color for circle, square, line, polygon, polyline, and free text annotations. Values are defined by using `transparent`, `gray`, `RGB` or `CMYK` color. See Color arrays for information on defining color arrays and how values are used with this property.

**Annotations**: Circle, Square, Line, Polygon, PolyLine, FreeText

Example: Create a Circle annotation and set the background color.

```
var annot = this.addAnnot(
{
    type: "Circle",
    page: 0,
    rect: [200,200,400,300],
    author: "A. C. Robat",
    name: "myCircle",
    popupOpen: true,
    popupRect: [200,100,400,200],
    contents: "Hi World!",
    strokeColor: color.red,
    fillColor: ["RGB",1,1,.855]
});
```

<a id="72469"></a>
<a id="gestures"></a>
<a id="id48"></a>
#### gestures

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | array | R/W |

An array of arrays, each representing a stroked path. Each array is a series of alternating *x* and *y* coordinates in default user space, specifying points along the path. When drawn, the points are connected by straight lines or curves in an implementation-dependent way. See the [PDF Reference](https://adobe.com/go/pdfreference) for more details.

**Annotations**: Ink

<a id="72369"></a>
<a id="hidden"></a>
<a id="id50"></a>
#### hidden

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | boolean | R/W |

If `true`, the annotation is not shown and there is no user interaction, display, or printing of the annotation.

**Annotations**: All

<a id="58242"></a>
<a id="inreplyto"></a>
<a id="id51"></a>
#### inReplyTo

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

If non-empty, specifies the `name` value of the annotation that this annotation is in reply to.

**Annotations**: All

<a id="42956"></a>
<a id="intent"></a>
<a id="id52"></a>
#### intent

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | C | string | R/W |

This property allows a markup annotation type to behave differently, depending on the intended use of the annotation. For example, the Callout Tool is a free text annotation with `intent` set to `FreeTextCallout`.

Though this property is defined for all annotations, currently, only free text, polygon, and line annotations have non-empty values for `intent`.

**Annotations**: All

The table below lists the tools available through the UI for creating annotations with special appearances.

| UI | Annotation type | Intent |
|----|-----------------|--------|
| Callout Tool | `FreeText` | `FreeTextCallout` |
| Cloud Tool | `Polygon` | `PolygonCloud` |
| Arrow Tool | `Line` | `LineArrow` |
| Dimensioning Tool | `Line` | `LineDimension` |

<a id="88415"></a>
<a id="leaderextend"></a>
<a id="id53"></a>
#### leaderExtend

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | C | number | R/W |

Specifies the length of *leader line extensions* that extend from both endpoints of the line, perpendicular to the line. These lines extend from the line proper 180 degrees from the leader lines. The value should always be greater than or equal to zero.

The default is zero (no leader line extension).

**Annotations**: Line

<a id="18708"></a>
<a id="leaderlength"></a>
<a id="id54"></a>
#### leaderLength

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | C | number | R/W |

Specifies the length of *leader lines* that extend from both endpoints of the line, perpendicular to the line. The value may be negative to specify an alternate orientation of the leader lines.

The default is 0 (no leader line).

**Annotations**: Line

<a id="46482"></a>
<a id="lineending"></a>
<a id="id55"></a>
#### lineEnding

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | C | string | R/W |

This property determines how the end of a callout line is stroked. It is relevant only for a free text annotation when the value of `intent` is `FreeTextCallout`. Possible values include:

- None (default)
- OpenArrow
- ClosedArrow
- ROpenArrow: Acrobat 6.0
- RClosedArrow: Acrobat 6.0
- Butt: Acrobat 6.0
- Diamond
- Circle
- Square
- Slash:  Acrobat 7.0

**Annotations**: FreeText

<a id="59735"></a>
<a id="lock"></a>
<a id="id56"></a>
#### lock

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | boolean | R/W |

If `true`, the annotation is locked, which is equivalent to `readOnly` except that the annotation is accessible through the properties dialog box in the UI.

**Annotations**: All

<a id="22713"></a>
<a id="id57"></a>
<a id="id58"></a>
#### modDate

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | C | date | R/W |

The last modification date for the annotation.

**Annotations**: All

Example: Print the modification date to the console.

```
console.println(util.printd("mmmm dd, yyyy", annot.modDate));
```

<a id="95838"></a>
<a id="id59"></a>
<a id="id60"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

The name of an annotation. This value can be used by the Doc object `getAnnot` method to find and access the properties and methods of the annotation.

**Annotations**: All

Example: Locate the annotation named `myNote` and appends a comment.

```
var gannot = this.getAnnot(0, "myNote");
gannot.contents += "rrDon't forget to check with Smith";
```

<a id="14440"></a>
<a id="noteicon"></a>
<a id="id61"></a>
#### noteIcon

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

The name of an icon to be used in displaying the annotation. Possible values include:

- Check
- Circle
- Comment
- Cross
- Help
- Insert
- Key
- NewParagraph
- Note(default)
- Paragraph
- RightArrow
- RightPointer
- Star
- UpArrow
- UpLeftArrow

**Annotations**: Text

Example: See the contents property.

<a id="51663"></a>
<a id="noview"></a>
<a id="id62"></a>
#### noView

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | boolean | R/W |

If `true`, the annotation is hidden, but if the annotation has an appearance, that appearance should be used for printing only.

**Annotations**: All

Example: See the toggleNoView property.

<a id="91716"></a>
<a id="opacity"></a>
<a id="id63"></a>
#### opacity

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | number | R/W |

The constant opacity value to be used in painting the annotation. This value applies to all visible elements of the annotation in its closed state (including its background and border), but not to the pop-up window that appears when the annotation is opened. Permissible values are 0.0 - 1.0. A value of 0.5 makes the annotation semitransparent.

**Annotations**: All

<a id="77086"></a>
<a id="overlaytext"></a>
<a id="id64"></a>
#### overlayText

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | D | No | C | string | R/W |

A text string specifying the overlay text that should be drawn over the redacted region after the affected content has been removed.

**Annotations**: Redact

Example: Set the redaction properties of a particular redaction annotation.

```
var a = this.getAnnots();                              // get all annotations in doc
var r = a[0]           ;                               // the first one is Redact type
r.setProps({                                           // now set its properties
   overlayText: " A.C. Robat ",
   alignment: 0,
   repeat: true,
   fillColor:color.blue,
   textColor: color.green
});
```

There is a popup associated with a `Redact` annotation, now add content to this popup note.

```
r.setProps({ contents: "Shall we redact this paragraph?" });
```

See also the applyRedactions method of the Doc object.

<a id="18012"></a>
<a id="page"></a>
<a id="id65"></a>
#### page

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | integer | R/W |

The page on which the annotation resides.

**Annotations**: All

Example: The following code moves the `Annotation` object `annot` from its current page to page 3 (0-based page numbering system).

```
annot.page = 2;
```

<a id="25272"></a>
<a id="point"></a>
<a id="id66"></a>
#### point

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | array | R/W |

An array of two numbers, \[ *x* *ul*, *y* *ul* \] that specifies the upper left-hand corner in default user space of the icon for a text, sound or file attachment annotation.

**Annotations**: Text, Sound, FileAttachment

Example: Place a help note icon at specified coordinates. The icon is located at the upper right corner of the popup note.

```
var annot = this.addAnnot({
    page: 0,
    type: "Text",
    point: [400,500],
    contents: "Call Smith to get help on this paragraph.",
    popupRect: [400,400,550,500],
    popupOpen: true,
    noteIcon: "Help"
});
```

See also the noteIcon property and the Doc object addAnnot method.

<a id="47728"></a>
<a id="points"></a>
<a id="id67"></a>
#### points

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | array | R/W |

An array of two points, \[\[ *x* *1* *, y* *1* \], \[ *x* *2* *, y* *2* \]\], specifying the starting and ending coordinates of the line in default user space.

**Annotations**: Line

Example: Draw a line between two specified points.

```
var annot = this.addAnnot({
    type: "Line",
    page: 0,
    author: "A. C. Robat",
    doCaption: true,
    contents: "Look at this again!",
    points: [[10,40],[200,200]],
});
```

See the arrowBegin and arrowEnd properties, the setProps method, and the Doc object addAnnot method.

<a id="13181"></a>
<a id="popupopen"></a>
<a id="id68"></a>
#### popupOpen

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | boolean | R/W |

If `true`, the pop-up text note appears open when the page is displayed.

**Annotations**: All except FreeText, Sound, FileAttachment

Example: See the print property.

<a id="35916"></a>
<a id="popuprect"></a>
<a id="id69"></a>
#### popupRect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | array | R/W |

An array of four numbers \[ *x* *ll*, *y* *ll*, *x* *ur* *,* *y* *ur* \] specifying the lower-left *x*, lower-left *y*, upper-right *x*, and upper-right *y* coordinates—in default user space—of the rectangle of the pop-up annotation associated with a parent annotation. It defines the location of the pop-up annotation on the page.

**Annotations**: All except FreeText, Sound, FileAttachment

Example: See the print property.

<a id="25722"></a>
<a id="print"></a>
<a id="id70"></a>
#### print

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | boolean | R/W |

Indicates whether the annotation should be printed (`true`) or not (`false`).

**Annotations**: All

<a id="42514"></a>
<a id="quads"></a>
<a id="id71"></a>
#### quads

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | array | R/W |

An array of 8 x *n* numbers specifying the coordinates of *n* quadrilaterals in default user space. Each quadrilateral encompasses a word or group of contiguous words in the text underlying the annotation. See the [PDF Reference](https://adobe.com/go/pdfreference) for more details. The `quads` for a word can be obtained through calls to the Doc object `getPageNthWordQuads` method.

**Annotations**: Highlight, StrikeOut, Underline, Squiggly,Redact

Example: See the Doc object getPageNthWordQuads method.

<a id="31420"></a>
<a id="rect"></a>
<a id="id73"></a>
#### rect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | array | R/W |

The `rect` array consists of four numbers \[ *x* *ll*, *y* *ll*, *x* *ur*, *y* *ur* \] specifying the lower-left *x*, lower-left *y*, upper-right *x*, and upper-right *y* coordinates—in default user space—of the rectangle defining the location of the annotation on the page. See also the popupRect property.

**Annotations**: All

<a id="64008"></a>
<a id="readonly"></a>
<a id="id74"></a>
#### readOnly

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | boolean | R/W |

**Annotations**: All

<a id="77065"></a>
<a id="reftype"></a>
<a id="id75"></a>
#### refType

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | C | string | R/W |

The reference type of the annotation. The property distinguishes whether `inReplyTo` indicates a plain threaded discussion relationship or a group relationship. Recognized values are “R” and “Group”. See the [PDF Reference](https://adobe.com/go/pdfreference) for additional details.

**Annotations**: All

<a id="60232"></a>
<a id="repeat"></a>
<a id="id77"></a>
#### repeat

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | D | No | C | boolean | R/W |

If `true`, the text specified by overlayText should be repeated to fill the redacted region after the affected content has been removed. Default value: `false`.

**Annotations**: Redact

<a id="52718"></a>
<a id="richcontents"></a>
<a id="id78"></a>
#### richContents

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | Array of `Span` objects | R/W |

This property gets the text contents and formatting of an annotation. The rich text contents are represented as an array of `Span` objects containing the text contents and formatting of the annotation.

**Annotations**: All except Sound, FileAttachment

Example: Create a text annotation and give it some rich text contents.

```
var annot = this.addAnnot({
    page: 0,
    type: "Text",
    point: [72,500],
    popupRect: [72, 500,6*72,500-2*72],
    popupOpen: true,
    noteIcon: "Help"
});

var spans = new Array();
spans[0] = new Object();
spans[0].text = "Attention:r";
spans[0].textColor = color.blue;
spans[0].textSize = 18;

spans[1] = new Object();
spans[1].text = "Adobe Acrobat 6.0r";
spans[1].textColor = color.red;
spans[1].textSize = 20;
spans[1].alignment = "center";

spans[2] = new Object();
spans[2].text = "will soon be here!";
spans[2].textColor = color.green;
spans[2].fontStyle = "italic";
spans[2].underline = true;
spans[2].alignment = "right";

// Now give the rich field a rich value
annot.richContents = spans;
```

See also the Field object richValue method and the `event` object methods richValue, richChange, and richChangeEx for examples of using the `Span` object.

<a id="95750"></a>
<a id="richdefaults"></a>
<a id="id79"></a>
#### richDefaults

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | `Span` object | R/W |

This property defines the default style attributes for a free text annotation. See the description of the Field object defaultStyle property for additional details.

**Annotations**: FreeText

<a id="37250"></a>
<a id="rotate"></a>
<a id="id80"></a>
#### rotate

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | integer | R/W |

The number of degrees (0, 90, 180, 270) the annotation is rotated counterclockwise relative to the page. This property is only significant for free text annotations.

**Annotations**: FreeText

<a id="46593"></a>
<a id="seqnum"></a>
<a id="id81"></a>
#### seqNum

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | C | integer | R |

A read-only sequence number for the annotation on the page.

**Annotations**: All

<a id="27366"></a>
<a id="soundicon"></a>
<a id="id82"></a>
#### soundIcon

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

The name of an icon to be used in displaying the sound annotation. A value of “Speaker” is recognized.

**Annotations**: Sound

<a id="11707"></a>
<a id="state"></a>
<a id="id83"></a>
#### state

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

The state of the text annotation. The values of this property depend on the stateModel. For a state model of Marked, values are Marked and Unmarked. For a Review state model, the values are Accepted, Rejected, Cancelled, Completed and None.

**Annotations**: Text

<a id="51718"></a>
<a id="statemodel"></a>
<a id="id84"></a>
#### stateModel

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

Beginning with Acrobat 6.0, annotations may have an author-specific state associated with them. The state is specified by a separate text annotation that refers to the original annotation by means of its IRT entry (see the inReplyTo property). There are two types of state models, “Marked” and “Review”.

**Annotations**: Text

See also the getStateInModel method.

<a id="14118"></a>
<a id="strokecolor"></a>
<a id="id85"></a>
#### strokeColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | color | R/W |

Sets the appearance color of the annotation. Values are defined by using `transparent`, `gray`, `RGB` or `CMYK` color. In the case of a free text annotation, `strokeColor` sets the border and text colors. See Color arrays for information on defining color arrays and how values are used with this property.

**Annotations**: All

Example: Make a text note red.

```
var annot = this.addAnnot({type: "Text"});
annot.strokeColor = color.red;
```

<a id="29533"></a>
<a id="style"></a>
<a id="id86"></a>
#### style

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

This property gets and sets the border style. Recognized values are `S` (solid) and `D` (dashed). The style property is defined for all annotation types but is only relevant for line, free text, circle, square, polyline, polygon and ink annotations.

**Annotations**: All

See the dash property for an example.

<a id="49482"></a>
<a id="subject"></a>
<a id="id87"></a>
#### subject

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

Text representing a short description of the subject being addressed by the annotation. The text appears in the title bar of the pop-up window, if there is one, or the properties dialog box.

**Annotations**: All

<a id="93184"></a>
<a id="textfont"></a>
<a id="id88"></a>
#### textFont

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | string | R/W |

Determines the font that is used when laying out text in a free text annotation. Valid fonts are defined as properties of the `font` object (see the Field object textFont property).

An arbitrary font can be used when laying out a free text annotation by setting the value of `textFont` equal to a string that represents the PostScript name of the font.

**Annotations**: FreeText

Example: Create a FreeText annotation using the Helvetica font.

```
var annot = this.addAnnot({
    page: 0,
    type: "FreeText",
    textFont: font.Helv, // or, textFont: "Viva-Regular",
    textSize: 10,
    rect: [200, 300, 200+150, 300+3*12], // height for three lines
    width: 1,
    alignment: 1 });
```

<a id="79538"></a>
<a id="textsize"></a>
<a id="id89"></a>
#### textSize

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | number | R/W |

The text size (in points) for a free text annotation. Valid text sizes include zero and the range from 4 to 144, inclusive. Zero indicates the largest point size that allows all the text to fit in the annotation’s rectangle.

**Annotations**: FreeText

Example: See the textFont property.

<a id="70681"></a>
<a id="togglenoview"></a>
<a id="id90"></a>
#### toggleNoView

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | string | R/W |

If `true`, the noView flag is toggled when the mouse hovers over the annotation or the annotation is selected.

If an annotation has both the `noView` and `toggleNoView` flags set, the annotation is usually invisible. However, when the mouse is over it or it is selected, it becomes visible.

**Annotations**: All

<a id="68108"></a>
<a id="id91"></a>
<a id="id92"></a>
#### type

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | C | string | R |

The type of annotation. The type of an annotation can only be set within the object-literal argument of the Doc object addAnnot method. The valid values are:

- Text
- FreeText
- Line
- Square
- Circle
- Polygon
- PolyLine
- Highlight
- Underline
- Squiggly
- StrikeOut
- Stamp
- Caret
- Ink
- FileAttachment
- Sound

**Annotations**: All

<a id="33431"></a>
<a id="vertices"></a>
<a id="id93"></a>
#### vertices

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | C | Array of arrays | R/W |

An array of coordinate arrays representing the alternating horizontal and vertical coordinates, respectively, of each vertex, in default user space of a polygon or polyline annotation. See the [PDF Reference](https://adobe.com/go/pdfreference) for details.

**Annotations**: Polygon, PolyLine

<a id="86349"></a>
<a id="width"></a>
<a id="id95"></a>
#### width

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | C | number | R/W |

The border width in points. If this value is 0, no border is drawn. The default value is 1.

**Annotations**: Square, Circle, Line, Ink, FreeText

<a id="annotation-methods"></a>
<a id="id96"></a>
### Annotation methods

- destroy
- getProps
- getStateInModel
- setProps
- transitionToState

<a id="47511"></a>
<a id="destroy"></a>
<a id="id97"></a>
#### destroy

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | C |

Destroys the annotation, removing it from the page. The object becomes invalid.

Example: Remove all “FreeText” annotations on page 0.

```
var annots = this.getAnnots({ nPage:0 });
for (var i = 0; i < annots.length; i++)
    if (annots[i].type == "FreeText") annots[i].destroy();
```

<a id="43743"></a>
<a id="getprops"></a>
<a id="id98"></a>
#### getProps

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | No | C |

Get the collected properties of an annotation. Can be used to copy an annotation.

**Returns**

An object literal of the properties of the annotation. The object literal is just like the one passed to the Doc object `addAnnot` method.

Example 1: Copy a given annotation to every page in the document.

```
var annot = this.addAnnot({
    page: 0,
    type: "Text",
    rect: [40, 40, 140, 140]
});

// Make a copy of the properties of annot
var copy_props = annot.getProps();

// Now create a new annot with the same properties on every page
var numpages = this.numPages;
for (var i=0; i < numpages; i++) {
    var copy_annot = this.addAnnot(copy_props);
    // but move it to page i
    copy_annot.page=i;
}
```

Example 2: Display all properties and values of an annotation.

```
var a = this.getAnnots(0);     // get all annots on page 0
if ( a != null ) {
    var p = a[0].getProps();     // get the properties of first one
    for ( o in p ) console.println( o + " : " + p[o] );
}
```

<a id="88159"></a>
<a id="getstateinmodel"></a>
<a id="id99"></a>
#### getStateInModel

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | No | C |

Gets the current state of the annotation in the context of a state model. See also the transitionToState method.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cStateModel` | The state model to determine the state of the annotation. |

**Returns**

The result is an array of the identifiers for the current state of the annotation:

- If the state model was defined to be exclusive, there is only a single state (or no states if the state has not been set).
- If the state model is non-exclusive, there may be multiple states (or no entries if the state has not been set and there is no default).

Example: Report on the status of all annotations on all pages of this document.

```
annots = this.getAnnots()
for ( var i= 0; i< annots.length; i++) {
    states = annots[i].getStateInModel("Review");
    if ( states.length > 0 ) {
        for(j = 0; j < states.length; j++)
        {
            var d = util.printd(2, states[j].modDate);
            var s = states[j].state;
            var a = states[j].author;

            console.println(annots[i].type + ": " + a + " "
                + s + " " + d + "on page "
                + (annots[i].page+1) );
        }

    }
}
```

<a id="59338"></a>
<a id="setprops"></a>
<a id="id100"></a>
#### setProps

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | No | C |

**Parameters**

| Parameter | Description |
|-----------|-------------|
| object literal | A generic object that specifies the properties of the `Annotation` object to be created (such as `type`, `rect`, and `page`). This object is the same as the parameter of the Doc object `addAnnot` method. |

**Returns**

The `Annotation` object

Example: Set various properties of a Line annotation.

```
var annot = this.addAnnot({type: "Line"})
annot.setProps({
    page: 0,
    points: [[10,40],[200,200]],
    strokeColor: color.red,
    author: "A. C. Robat",
    contents: "Check with Jones on this point.",
    popupOpen: true,
    popupRect: [200, 100, 400, 200], // Place rect at tip of the arrow
    arrowBegin: "Diamond",
    arrowEnd: "OpenArrow"
});
```

<a id="92934"></a>
<a id="transitiontostate"></a>
<a id="id101"></a>
#### transitionToState

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | No | C |

Sets the state of the annotation to `cState` by performing a state transition. The state transition is recorded in the audit trail of the annotation.

See also the getStateInModel method.

> **Note**
>
> For the states to work correctly in a multiuser environment, all users must have the same state model definitions. Therefore, it is best to place state model definitions in a folder-level JavaScript file that can be distributed to all users or installed on all systems.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cStateModel` | The state model in which to perform the state transition. `cStateModel` must have been previously added by calling the `Collab` method `addStateModel`. |
| `cState` | A valid state in the state model to transition to. |

Example: Define a custom set of transition states, then set the state of an annotation.

```
try {
    // Create a document
    var myDoc = app.newDoc();
    // Create an annot
    var myAnnot = myDoc.addAnnot
    ({
        page: 0,
        type: "Text",
        point: [300,400],
        name: "myAnnot",
    });
    // Create the state model
    var myStates = new Object();
    myStates["initial"] = {cUIName: "Haven't reviewed it"};
    myStates["approved"] = {cUIName: "I approve"};
    myStates["rejected"] = {cUIName: "Forget it"};
    myStates["resubmit"] = {cUIName: "Make some changes"};
    Collab.addStateModel({
        cName: "ReviewStates",
        cUIName: "My Review",
        oStates: myStates,
        cDefault: "initial"
    });
} catch(e) { console.println(e); }
// Change the states
myAnnot.transitionToState("ReviewStates", "resubmit");
myAnnot.transitionToState("ReviewStates", "approved");
```

<a id="99657"></a>
<a id="annotrichmedia"></a>
<a id="id102"></a>
## AnnotRichMedia

An AnnotRichMedia object represents a particular rich media annotation; that is, an annotation created using one of the tools 3D, Flash, Video, or Sound from the Multimedia toolbar. The AnnotRichMedia object can be acquired from the getAnnotRichMedia and getAnnotsRichMedia methods of the Doc object.

<a id="annotrichmedia-properties"></a>
<a id="id103"></a>
### AnnotRichMedia properties

<a id="35022"></a>
<a id="activated"></a>
<a id="id104"></a>
#### activated

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | boolean | R/W |

A Boolean value that indicates whether the annotation is enabled and interactive (`true`) or just displaying the poster artwork (`false`). Setting this property to `true` activates the annotation.

<a id="94284"></a>
<a id="context3d"></a>
<a id="id105"></a>
#### context3D

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | `global` object or `undefined` | R |

If `activated` is `true` and `subtype` is `"3D"`, this property returns the global scripting context of the annotation (a `global` object containing the 3D scene.) (See the [JS 3D API Reference](../js3dapi/index.md) for more information.) If `activated` is `false` or `subtype` is not `"3D"`, this property returns `undefined`.

<a id="65756"></a>
<a id="id106"></a>
<a id="id107"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | string | R |

The name of the rich media annotation.

<a id="67124"></a>
<a id="id108"></a>
<a id="id109"></a>
#### page

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | integer | R |

The 0-based page number of the page containing the annotation.

<a id="62225"></a>
<a id="id110"></a>
<a id="id111"></a>
#### rect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | array | R/W |

**Returns** an array of four numbers \[xll, yll, xur, yur\] specifying the lower-left x, lower-left y, upper-right x and upper-right y coordinates, in default user space, of the rectangle defining the location of the annotation on the page.

<a id="53504"></a>
<a id="subtype"></a>
<a id="id112"></a>
#### subtype

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | string | R |

The subtype of the annotation. The property will have a value of `"3D"`, `"Flash"`, `"Video"`, or `"Sound"`.

<a id="annotrichmedia-methods"></a>
<a id="id113"></a>
### AnnotRichMedia methods

<a id="36391"></a>
<a id="callas"></a>
<a id="id114"></a>
#### callAS

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 9.0 | No | No | All |

Calls into ActionScript with the `ExternalInterface` calling convention to an exposed method
(`ExternalInterface.addCallback` in ActionScript). The `callAS` method returns the return value of the method specified as the first parameter.

> **Note**
>
> The  [JS 3D API Reference](../js3dapi/index.md) has the `call` method of the FlashMovie object that uses the same mechanism as the `callAS` method.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `methodName` | The string name of the exposed method in ActionScript to be called. |
| `arguments` | A series of arguments of arbitrary type to be passed to the ActionScript method being called. |

**Returns**

The return value from the called function, which can be of any type.

The Multimedia Operation (Acrobat 9 and later) is an Action type for rich media annotations that can be used to perform Play, Pause, Rewind, Next Chapter Point, Previous Chapter Point, Seek to time, Mute, Volume, and Custom actions. The same actions can be executed through the `callAS` method.

The following lists some custom ActionScript methods that are visible through the Multimedia Operations dialog box, and can be used in the `callAS` method.

- Custom ActionScript Methods
- `multimedia_play():void` Play the video or sound clip from the current location.
- `multimedia_pause():void` Pause playback of the current media.
- `multimedia_rewind():void` Rewind the media clip to the beginning. This method does not pause the clip.
- `multimedia_nextCuePoint():void` Move the play head to the next cue (chapter) point.
- `multimedia_prevCuePoint():void` Move the play head to the previous (chapter) point.
- `multimedia_seek(time:Number):void` Move the play location to an offset of `time` from the beginning of the media, where `time` is measured in seconds.
- `multimedia_mute():void` Mute the audio of the media.
- `multimedia_volume(volume:Number):void` Set the volume level. The `volume` is a number between 0 and 1 inclusive. A value of 0 mutes the audio, while a volume of 1 sets the volume level to the maximum level.

Example: In this example, it is assumed that a video has been embedded in the current PDF using the Video tool, and that the video has a number of Chapter Points, perhaps created through the Video tab of the Insert Video dialog box. Below are several Run a JavaScript actions for buttons that control the video. The annotation targeted is the first rich media annotation on the first page.

```
// Code for a Play button
var rm = this.getAnnotsRichMedia(0)[0];
if (!rm.activated) rm.activated=true;
rm.callAS("multimedia_play");

// Code for a Pause button
var rm = this.getAnnotsRichMedia(0)[0];
if (rm.activated) { rm.callAS("multimedia_pause"); }

// Code for a Next Chapter Point button
var rm = this.getAnnotsRichMedia(0)[0];
if (rm.activated) { rm.callAS("multimedia_nextCuePoint"); }

// Code for a simple Volume button, set volume to the 50% level.
var rm = this.getAnnotsRichMedia(0)[0];
if (rm.activated) { rm.callAS("multimedia_volume", 0.5); }
```

<a id="98081"></a>
<a id="annot3d"></a>
<a id="id115"></a>
## Annot3D

An Annot3D object represents a particular Acrobat 3D annotation; that is, an annotation created using the Acrobat 3D Tool. The Annot3D object can be acquired from the Doc object methods getAnnot3D and getAnnots3D.

<a id="annot3d-properties"></a>
<a id="id116"></a>
### Annot3D properties

<a id="87772"></a>
<a id="id117"></a>
<a id="id118"></a>
#### activated

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | boolean | R/W |

A Boolean value that indicates whether the annotation is displaying the 3D artwork (`true`) or just the posterboard picture (`false`).

See the context3D property.

<a id="38599"></a>
<a id="id119"></a>
<a id="id120"></a>
#### context3D

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | `global` object | R |

If `activated` is `true`, this property returns the context of the 3D annotation (a `global` object containing the 3D scene.) See the [JS 3D API Reference](../js3dapi/index.md) for more information. If `activated` is `false`, this property returns `undefined`.

<a id="98501"></a>
<a id="innerrect"></a>
<a id="id121"></a>
#### innerRect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | array | R/W |

An array of four numbers \[x *ll*, y *ll*, x *ur*, y *ur* \] specifying the lower-left x, lower-left y, upper-right *x* and upper-right *y* coordinates, in the coordinate system of the annotation (lower-left is \[0, 0\], top right is \[width, height\]), of the 3D annotation’s 3DB box, where the 3D artwork is rendered.

<a id="29343"></a>
<a id="id122"></a>
<a id="id123"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | string | R |

The name of the annotation.

<a id="53981"></a>
<a id="id124"></a>
<a id="id125"></a>
#### page

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | integer | R |

The 0-based page number of the page containing the annotation.

<a id="24770"></a>
<a id="id126"></a>
<a id="id127"></a>
#### rect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | array | R/W |

**Returns** an array of four numbers \[x *ll*, y *ll*, x *ur*, y *ur* \] specifying the lower-left x, lower-left y, upper-right *x* and upper-right *y* coordinates, in default user space, of the rectangle defining the location of the annotation on the page.
