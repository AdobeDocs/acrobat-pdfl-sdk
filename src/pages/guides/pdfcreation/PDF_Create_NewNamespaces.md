# Other Namespaces

This chapter describes the settings that belong to namespaces other than the `Common` namespace. See [Namespaces](index.md#90851) for information on how namespaces are organized.

<a id="92173"></a>
## CreativeSuite namespace settings

The following settings belong to the `CreativeSuite` namespace. They are supported by one or more of the applications in Creative Suite version 2.0 and later (llustrator, InDesign, and Photoshop). The entries for each setting indicate which applications support it.

### AddBleedMarks

If `true` , bleed marks are included in the PDF file.

**Supported by**

InDesign

**Type**

Boolean

**UI name**

Add Bleed Marks

**Default value**

```
false
```

### AddColorBars

If `true` , color bars are included in the PDF file.

**Supported by**

Illustrator, InDesign

**Type**

Boolean

**UI name**

Color Bars

**Default value**

```
false
```

### AddCropMarks

If `true` , crop marks are included in the PDF file.

**Supported by**

Illustrator, InDesign

**Type**

Boolean

**UI name**

InDesign: Crop Marks

Illustrator: Trim Marks

**Default value**

```
false
```

### AddPageInfo

If `true` , page information (document name, page number, and time stamp) are included in the PDF file.

**Supported by**

Illustrator, InDesign

**Type**

Boolean

**UI name**

Page Information

**Default value**

```
false
```

### AddRegMarks

If `true` , registration marks are included in the PDF file.

**Supported by**

Illustrator, InDesign

**Type**

Boolean

**UI name**

Registration Marks

**Default value**

```
false
```

<a id="84563"></a>
### BleedOffset

An array of four floating point numbers with values between 0.0 to 432.0, representing the offsets of the bleed in points from the top, left, bottom, and right edges of the document.

In InDesign, if `UseDocumentBleed` is `true` , the bleed values are taken from the document bleed rather than the value of this setting.

**Supported by**

Illustrator, InDesign

**Type**

array

**UI name**

Bleeds

**Default value**

```
[0.0, 0.0, 0.0, 0.0]
```

<a id="39802"></a>
### ConvertColors

Specifies whether colors should be converted to CMYK or RGB. The following table shows the valid values.

| Value | UI equivalent | Description |
| --- | --- | --- |
| NoConversion | No Color Conversion | Colors are not converted. |
| ConvertToCMYK | *See below* | Colors are converted to CMYK |
| ConvertToRGB | *See below* | Colors are converted to RGB. |

`ConvertToCMYK` or `ConvertToRGB` do not map precisely to the UI options, which are “Convert to Destination” or “Convert to Destination (preserve numbers)”. The “destination” referred to is a specified by the appropriate profile (CMYK or RGB) and additional settings. See [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for more details.

> **Note**
>
> When converting to CMYK, the resulting Common settings are supported by Distiller 7.0, but previous versions of Distiller did not support conversion to CMYK.

**Supported by**

Illustrator, InDesign, Photoshop

**Type**

name

**UI name**

Color Conversion

**Default value**

```
NoConversion
```

<a id="55683"></a>
### DestinationProfileName

When the value of `DestinationProfileSelector` is `UseName` , this setting specifies the name of the destination profile to be used.

When the value of `DestinationProfileSelector` is one of the document or working space profiles, Creative Suite applications store the profile name in this setting when saving the settings. This enables determining whether a setting has been changed outside the application. For example, when converting to CMYK:

- If the value of this setting is a profile name, it should be the same as that of `CalCMYKProfile`.  Different profile names imply that `CalCMYKProfile` was changed in Distiller; therefore, Creative Suite applications will use `CalCMYKProfile` instead of `DestinationProfileName`.
- If the value of this setting is the empty string, Creative Suite applications will use the document CMYK profile regardless of the value of `CalCMYKProfile`.

**Supported by**

Illustrator, InDesign, Photoshop

**Type**

string

**UI name**

Destination

<a id="23735"></a>
### DestinationProfileSelector

Specifies which destination color profile should be used. The following table shows the valid values.

| Value | UI equivalent | Description |
| --- | --- | --- |
| NA | N/A | No profile |
| UseName | *Any named profile* | The profile specified by `DestinationProfileName` is used. |
| WorkingCMYK | Working CMYK | The effective working CMYK profile is used. The profile name is also written to `DestinationProfileName`. |
| WorkingRGB | Working RGB | The effective working RGB profile is used. |
| DocumentCMYK | Document CMYK | The effective document CMYK profile is used. The profile name is also written to `DestinationProfileName`. |
| DocumentRGB | Document RGB | The effective document RGB profile is used. |

**Supported by**

all applications

**Type**

name

**UI name**

Destination

**Default value**

```
NA
```

<a id="62333"></a>
### Downsample16BitImages

If `true` , 16 bits-per-channel images are converted to 8 bits-per-channel images. If `false` , 16-bit images are not converted, and Flate (ZIP) is the only compression method available.

This setting is available only if `CompatibilityLevel` is 1.5 or greater. For 1.4 or earlier, 16-bit images are always converted to 8 bits per channel.

**Supported by**

Photoshop

**Type**

Boolean

**UI name**

Convert 16 Bit/Channel Image to 8 Bit/Channel

**Default value**

```
true
```

### FlattenerPreset

A dictionary that specifies a preset or set of options for flattening transparency. One of the entries is `PresetSelector` , which is a string corresponding to a preset file. It can correspond to one of the preset files that specify transparency flattening: `LowResolution` , `MediumResolution` , or `HighResolution`.  It can also take the value `UseName` , which means that the `PresetName` entry specifies the name of the preset file.

The other entries are: `ClipComplexRegions` , `ConvertStrokesToOutlines` , `ConvertTextToOutlines` , `GradientResolution` , `LineArtTextResolution` , and `RasterVectorBalance`.  See Creative Suite application Help for more information on these transparency flattening options.

> **Note**
>
> This setting applies only when `CompatibilityLevel` is 1.3; that is, for PDF versions where transparency is not supported.

**Supported by**

Illustrator, InDesign

**Type**

dictionary

**UI name**

Transparency Flattener: Preset

**Default value**

```
<</PresetSelector /MediumResolution>>
```

<a id="55617"></a>
### GenerateStructure

If `true` , a Tagged PDF document is generated. Tagged PDF contains information about the logical structure of the document that can be used to provide document reflow, improved accessibility, and interchange with other file formats. See the [PDF Reference](https://www.adobe.com/go/pdfreference) for more information on Tagged PDF.

If `CompatibilityLevel` is 1.5 or later (that is, Acrobat 6 or later compatibility is chosen), tags are compressed for smaller file size.

**Supported by**

InDesign

**Type**

Boolean

**UI name**

Create Tagged PDF

**Default value**

```
false
```

### IncludeBookmarks

A Boolean value to include bookmarks, defined in an InDesign document, in generated PDF.

**Supported by**

InDesign

**Type**

Boolean

**UI name**

Bookmarks

**Default value**

```
false
```

If `true` , bookmarks are included in generated PDF.

### IncludeHyperlinks

A Boolean value to include hyperlinks in generated PDF.

**Supported by**

InDesign

**Type**

Boolean

**UI name**

Hyperlinks

**Default value**

```
false
```

If `true` , hyperlinks are included in generated PDF.

### IncludeInteractive

If `true` , interactive elements should be included in the PDF document. These can be:

**Multimedia elements** : If `true` , the `MultimediaHandling` setting controls how the elements should be included.

**Supported by**

InDesign

**Type**

Boolean

**UI name**

Interactive Elements

**Default value**

```
false
```

### IncludeLayers

If `true` , layers (optional content) are included in generated PDF; available in PDF 1.5 or later.

**Supported by**

Illustrator, InDesign

**Type**

Boolean

**UI name**

Create Acrobat Layers

**Default value**

```
false
```

<a id="51577"></a>
### IncludeProfiles

If `false` , color profiles are not included in generated PDF. This corresponds to Don’t Include Profiles in the UI. If `true` , which profiles are included is dependent on the value of other settings. See [Creative Suite color conversion settings](PDF_Create_UsingSettings.md#74214) for details.

**Supported by**

Illustrator, InDesign, Photoshop

**Type**

Boolean

**UI name**

Profile Inclusion Policy

**Default value**

```
false
```

### MarksOffset

A floating-point number between `0.0` and `6.0` indicating the printer offset in points.

**Supported by**

Illustrator, InDesign

**Type**

number

**UI name**

Offset

**Default value**

```
0
```

### MarksWeight

A floating-point number between `0.125` and `0.5` indicating the line weight in points to be used for printer’s marks.

**Supported by**

Illustrator, InDesign

**Type**

number

**UI name**

InDesign: Weight

Illustrator: Trim Mark Weight

**Default value**

```
0.25
```

<a id="34743"></a>
### MultimediaHandling

Specifies how multimedia objects (movies and sounds) are referenced in the PDF file. This setting is relevant only if `IncludeInteractive` is `true`.  Valid values are:

| Value | UI equivalent | Description |
| --- | --- | --- |
| UseObjectSettings | Automatic | If `CompatibilityLevel` is PDF 1.5 or later, all objects are embedded. If it is PDF 1.4 or earlier, all objects are linked.<br><br>- Used by InDesign only. |
| LinkAll | Link All | All objects are linked when `CompatibilityLevel` is PDF 1.5 or later; otherwise, sound clips are embedded and movies are linked. |
| EmbedAll | Embed All | All objects are embedded. This setting is valid only when `CompatibilityLevel` is PDF 1.5 or later. |

Embedding means that the multimedia object is included in the PDF file itself. Linking means that the PDF file contains a reference to an external file. (The user should make sure that the media files are in the same directory as the PDF file.)

**Supported by**

InDesign

**Type**

name

**UI name**

Multimedia

**Default value**

```
UseObjectSettings
```

### PageMarksFile

Specifies selection of the page marks file. Valid values are:

- `RomanDefault` : Use the built-in Roman page marks file
- `JapaneseWithCircle` : Use the built-in Japanese (with circle) page marks file.
- `JapaneseNoCircle` : Use the built-in Japanese (with no circle) page marks file.
- `UseName` : Use the value of `PageMarksFileName` for the page marks file

The files presented in the user interface vary according to application and language.

**Supported by**

Illustrator, InDesign

**Type**

name

**UI name**

InDesign: “Type” pop-up

Illustrator: Printer Mark Type

**Default value**

```
RomanDefault
```

<a id="39345"></a>
### PageMarksFileName

If `PageMarksFile` has the value `UseName` , this setting represents the page marks file that should be used.

**Supported by**

Illustrator, InDesign

**Type**

string

**UI name**

Page mark file name

**Default value**

```
""
```

<a id="84948"></a>
### PDFXOutputIntentProfileSelector

Specifies the PDF/X output intent profile to be used for PDF/X compliance. The values are similar to those for the `DestinationProfileSelector` setting.

Valid values are:

| Value | UI equivalent | Description |
| --- | --- | --- |
| NA | N/A | Indicates that no PDF/X compliance standard has been specified. |
| UseName | *Any named profile* | The profile specified by `PDFXOutputIntentProfile` is used as the PDF/X output intent profile. |
| WorkingCMYK | Working CMYK | The effective working CMYK profile is used as the PDF/X output intent profile. |
| WorkingRGB | Working RGB | The effective working RGB profile is used as the PDF/X output intent profile. |
| DocumentCMYK | Document CMYK | The effective document CMYK profile is used as the PDF/X output intent profile. |
| DocumentRGB | Document RGB | The effective document RGB profile is used as the PDF/X output intent profile. |

> **Note**
>
> When color management is on and PDF/X compliance has been specified, the effective profiles specified by `DestinationProfileName` , `CalCMYKProfile` and `PDFXOutputIntentProfile` must be the same.

See [Using the PDF/X output intent settings](PDF_Create_UsingSettings.md#99125) for more information about how this setting is used along with the other standards settings.

**Supported by**

Illustrator, InDesign, Photoshop

**Type**

name

**UI name**

Output Intent Profile Name

**Default value**

```
DocumentCMYK
```

### PreserveEditing

If `true` , data is saved in the PDF that allows you to subsequently re-open and edit the data in the authoring application.

> **Note**
>
> This capability is not available when specifying PDF/X compliance (see [CheckCompliance](PDF_Create_CommonSettings.md#17664)).

**Supported by**

Illustrator, Photoshop

**Type**

Boolean

**UI name**

Preserve *application name* Editing Capabilities

**Default value**

```
true
```

<a id="99249"></a>
### UntaggedCMYKHandling

Specifies whether untagged CMYK content (content with no embedded profiles) should be tagged. Valid values are:

- `LeaveUntagged` : Do not add profiles to untagged objects.
- `UseDocumentProfile` : Use document CMYK profile for untagged objects.

> **Note**
>
> In InDesign and Illustrator, this value applies to placed content originating in other applications. Native content is treated as inherently untagged unless the option to include all profiles is chosen.

See [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for details of how these settings interact with the other color settings and how they appear in the UI.

**Supported by**

Illustrator, InDesign, Photoshop

**Type**

name

**UI name**

Output panel: Color

**Default value**

```
LeaveUntagged
```

<a id="18660"></a>
### UntaggedRGBHandling

Specifies whether untagged RGB content (content with no embedded profiles) should be tagged. Valid values are:

- `LeaveUntagged` : Do not add profiles to untagged objects.
- `UseDocumentProfile` : Use document RGB profile for untagged objects.

See [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for details of how these settings interact with the other color settings and how they appear in the UI.

**Supported by**

all applications

**Type**

name

**UI name**

Output panel: Color

**Default value**

```
UseDocumentProfile
```

<a id="68036"></a>
### UseDocumentBleed

If `true` , the bleed values (otherwise specified by `BleedOffset` ) are populated based on the document’s bleed.

**Supported by**

InDesign

**Type**

Boolean

**UI name**

Use Document Bleed

**Default value**

```
false
```

<a id="46753"></a>
## InDesign namespace settings

The following settings belong to the `InDesign` namespace. They are supported by InDesign only.

### AsReaderSpreads

If `true` , spreads are exported as single PDF pages. A *spread* is a set of pages that are viewed together, such as the two pages that are visible when a magazine is opened.

**Type**

Boolean

**UI name**

Spreads

**Default value**

```
false
```

<a id="97401"></a>
### CropImagesToFrames

If `true` , only data that represents the visible (non-cropped) part of an image is exported in the PDF file.

> **Note**
>
> InDesign crops images to the visible portion of the frame. Distiller has settings for cropping (see [Disabling of image cropping](PDF_Create_UsingSettings.md#16777)) that use the clip area.

**Type**

Boolean

**UI name**

Crop Image Data to Frames

**Default value**

```
true
```

<a id="92883"></a>
### ErrorControl

Specifies what should be done when errors occur when generating a PDF file. The following table shows the valid values.

| Value | Description |
| --- | --- |
| WarnAndContinue | A warning dialog box is issued. The user can choose to continue and the PDF file will be produced. If the UI is disabled in scripting, the dialog box is automatically dismissed. |
| Ignore | Errors are ignored. |
| CancelJob | No PDF file is produced. |

**Type**

name

**UI name**

*none* (supported via scripting)

**Default value**

```
WarnAndContinue
```

### FlattenerIgnoreSpreadOverrides

If `true` , transparency flattener settings are applied to all spreads in a document, overriding the flattener settings for individual spreads.

**Type**

Boolean

**UI name**

Ignore Spread Overrides

**Default value**

```
false
```

### IncludeGuidesGrids

If `true` , visible grids and guides will appear in the PDF document.

**Type**

Boolean

**UI name**

Visible Guides and Baseline Grids

**Default value**

```
false
```

### IncludeNonPrinting

If `true` , non-printing objects (which have had the Nonprinting option applied in the Attributes palette) will appear in the PDF document.

**Type**

Boolean

**UI name**

Non-Printing Objects

**Default value**

```
false
```

### IncludeSlug

If `true` , the slug area (an area outside the page and bleed that contains information such as printer instructions) is included in the PDF document.

**Type**

Boolean

**UI name**

Include Slug area

**Default value**

```
false
```

### OmitPlacedBitmaps

If `true` , imported bitmap images are not included in the PDF document but are replaced by OPI comments.

**Type**

Boolean

**UI name**

Omit for OPI: bitmap images

**Default value**

```
false
```

### OmitPlacedEPS

If `true` , imported Encapsulated PostScript (EPS) images are not included in the PDF document but are replaced by OPI comments.

**Type**

Boolean

**UI name**

Omit for OPI: EPS

**Default value**

```
false
```

### OmitPlacedPDF

If `true` , PDF that has been placed (imported) into the document is not included in the PDF document but are replaced by OPI comments.

**Type**

Boolean

**UI name**

Omit for OPI: PDF

**Default value**

```
false
```

<a id="42609"></a>
### SimulateOverprint

Simulates the appearance of printing separations by maintaining the appearance of overprinting in composite output. The following values are valid.

| Value | UI equivalent | Description |
| --- | --- | --- |
| Legacy | unchecked | Preserve overprint & spot colors when flattening. |
| SimulatePress | checked | Spot colors are changed to process equivalents.<br><br>The transparency flattener simulates the appearance of overprinted objects using process colors. |

This setting applies only when the following conditions are met:

- `CompatibilityLevel` is 1.3 (Acrobat 4) or earlier (that is, when transparency is not supported)
- There is a CMYK or RGB output color space.

**Type**

name

**UI name**

Simulate Overprint check box

**Default value**

```
Legacy
```
