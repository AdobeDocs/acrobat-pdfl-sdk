# Common PDF Settings

This chapter describes the Adobe PDF settings that belong to the Common namespace. (See [Namespaces](index.md#90851).) These settings have historically been documented in *Acrobat Distiller Parameters* . They are supported by Distiller and may be supported by one or more of the applications in the Creative Suite, version 2.0 and later. The settings in other namespaces are described in [Other Namespaces](PDF_Create_NewNamespaces.md#69127).

The settings are grouped into the same categories that appear in the Distiller user interface (UI). The Creative Suite applications have similar interfaces for PDF creation settings, although they may differ in some respects. More information on the use of Adobe PDF settings can be found in Help for Distiller and the Creative Suite applications.

<a id="36016"></a>
## Settings descriptions

The possible values for the settings are enumerated, with their meanings.

**Supported by**

Indicates which of the applications (Distiller, Illustrator, InDesign, and Photoshop) support this setting.

**Type**

The type of data. The types are consistent with PostScript syntax and can include Boolean, number, string, array, and dictionary.

**UI name**

The name (if any) of the user interface control that corresponds to this setting. (There can be slight variations based on application)

**Default value**

Each setting has a default value, which is the value that is used when a setting is not specified in the settings file.

> **Note**
>
> The default values are the same as those in the `Standard.joboptions` file, with the following exceptions:

- *NeverEmbed* defaults to \[true\] (no list of fonts)
- *Description* is not provided
- *TransferFunctionInfo* defaults to Preserve
- *CompressObjects* defaults to Off
- *CalGrayProfile* defaults to ()
- *PassThroughJPEGImages* defaults to false

<a id="31533"></a>
## General settings

These settings are available in the General panel of the Distiller settings dialog box. Those settings that are supported by Creative Suite applications are indicated.

### AutoRotatePages

Allows Distiller to automatically orient (rotate) pages based on the predominant text orientation. Auto-rotation is not done if the file contains the `%%ViewingOrientation` DSC comment and `ParseDSCComments` is true. If `AutoRotatePages` is set to `None` , pages are not automatically oriented and the `%%ViewingOrientation` DSC comment is ignored.

| Value | UI equivalent | Description |
| --- | --- | --- |
| None | Off | No automatic page rotation. |
| All | Collectively by File | All pages are rotated to match the predominant text orientation. |
| PageByPage | Individually | Pages are rotated on a page-by-page basis. This value is useful for mixed portrait and landscape documents. |

**Supported by**

Distiller

**Type**

name

**UI name**

Auto-Rotate Pages

**Default value**

```
All
```

<a id="45892"></a>
### Binding

Controls the value of the `PageDirection` entry in the `ViewerPreferences` dictionary of the PDF file. `PageDirection` determines how the printed pages would be bound.

| Value | UI equivalent | Description |
| --- | --- | --- |
| Left | Left | For left binding |
| Right | Right | For right binding |

> **Note**
>
> InDesign does not use this setting but sets the binding through other UI controls.

**Supported by**

Distiller

**Type**

name

**UI name**

Binding

**Default value**

```
Left
```

<a id="88058"></a>
### CompatibilityLevel

The PDF version number: 1.2, 1.3, 1.4, 1.5, 1.6, or 1.7.

> **Note**
>
> Applications other than Distiller do not support saving files as PDF 1.2.

> **Note**
>
> If you create files with Acrobat 7.0 compatibility, the resulting PDF files may not be compatible with earlier Acrobat versions.

**Supported by**

all applications

**Type**

real

**UI name**

Compatibility

**Default value**

```
1.4
```

<a id="24772"></a>
### CompressObjects

Controls object-level compression, introduced in PDF 1.5. PDF objects that are not individually compressible can be combined into *object streams* that can be efficiently compressed. Only PDF consumers that support PDF 1.5 can process object streams.

| Value | UI equivalent | Description |
| --- | --- | --- |
| Off | Off | PDF 1.5 object compression is not used. |
| Tags | Tags Only | PDF 1.5 object compression is applied to the logical structure tree in a document. Versions 5 and earlier of Acrobat and Adobe Reader can open and use these documents, but cannot use the logical structure (tag) information. Versions 6 and later have full access to the tag information. |
| All | Maximum | Maximum compression of objects is performed. The compressed file is readable by Acrobat and Adobe Reader version 6 and later. Available only if `CompatibilityLevel` is 1.5 or higher. |

> **Note**
>
> Creative Suite applications do not provide a user interface for this setting. For InDesign, if `GenerateStructure` (in the `CreativeSuite` namespace) is `true` , Tagged PDF is generated and this setting is set to `Tags` (if `CompatibilityLevel` is 1.5 or higher). A value of `All` will be treated as `Tags` by Creative Suite applications.

**Supported by**

all applications

**Type**

name

**UI name**

Object-Level Compression Distiller

**Default value**

```
Off
```

### CoreDistVersion

*(Read only)* Version number of the Distiller implementation. This is neither the version number of the PostScript interpreter used in Distiller nor the version number displayed in the UI.

**Supported by**

Distiller

**Type**

integer

**Default value**

7000

<a id="34385"></a>
### Description

Provides a description of the Adobe PDF settings file that can be displayed in the UI. Each key in the dictionary is a standard 3-letter language code; for example, `ENU` for English (see the [Acrobat and PDF Library API Reference](./API_References/Acrobat_API_Reference/index.md) for a listing of these codes). The value associated with each language key is a string that contains the description of the settings file in that language. It is assumed that the string will be reflowed to fit the width of the display field.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Description

<a id="21672"></a>
### DoThumbnails

If `true` , thumbnails are created for the pages of the resulting PDF file.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Distiller: Embed Thumbnails
Creative Suite: Embed Page Thumbnails

**Default value**

```
false
```

### EndPage

The last page of the document to be produced.

`StartPage` and `EndPage` together determine the range of pages in the PostScript file that are converted to PDF. If `StartPage` is greater than 1 (the default), no PDF output is produced for the first (`StartPage` `-1` ) pages of PostScript. `StartPage` becomes page 1 of the PDF file. If `EndPage` is greater than `-1` , distilling stops after the `EndPage` of PostScript. Distiller checks these two settings at the time that the first PostScript marking operator is executed in a job.

> **Note**
>
> `StartPage` and `EndPage` are useful when debugging PostScript. They are not recommended for general purpose use, as Distiller does not retain page number references in document links.

**Supported by**

Distiller

**Type**

integer

**UI name**

All Pages, Pages From: To:

**Default value**

```
-1
```

### ExportLayers

Controls the layer output of exported spreads, based on their visibility & printability layer attributes.

**Supported by**

InDesign

**Type**

Name

**UI name**

Export Layers

**Default value**

```
ExportVisiblePrintableLayers
```

<a id="28903"></a>
### HWResolution

Provides the resolution for the PDF file if this value has not already been supplied by the PostScript file itself.

> **Note**
>
> This setting appears as part of the `setpagedevice` dictionary in a settings file, as described in [Organization of settings files](index.md#18721). See *PostScript Language Reference* for more information.

**Supported by**

Distiller

**Type**

array

**UI name**

Resolution

**Default value**

```
[600 600]
```

### ImageMemory

The number of bytes in the buffer used in the sample processing of color, grayscale, and monochrome images. When the buffer is full, Distiller writes its contents to disk.

The value of this setting should be between `0` and `1048576`.  If it is set to a negative integer, zero is used.

**Supported by**

Distiller

**Type**

integer

<a id="11145"></a>
### Namespace

This setting identifies the namespace to which all other settings in the same settings dictionary belong. This setting may appear in any namespace. For the `Common` namespace, it is optional. For all other namespaces, it is required. See [Namespaces](index.md#90851) for more information.

**Supported by**

all applications

**Type**

array

**Default value**

```
[ (Adobe) (Common) (1.0) ]
```

<a id="24205"></a>
### Optimize

If `true` , the PDF file is optimized for fast web viewing. This process is also referred to as *linearization* (see the [PDF Reference](https://www.adobe.com/go/pdfreference) for detailed information.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Optimize For Fast Web View

**Default value**

```
true
```

<a id="93531"></a>
### OtherNamespaces

This setting is an array containing additional settings dictionaries in namespaces other than the current namespace. See [Namespaces](index.md#90851) for more information.

**Supported by**

all applications

**Type**

array

<a id="42586"></a>
### PageSize

Provides the page size for the PDF file if this value has not already been supplied by the PostScript file itself.

> **Note**
>
> This setting appears as part of the `setpagedevice` dictionary in a settings file, as described in [Organization of settings files](index.md#18721). See *PostScript Language Reference* for more information.

**Supported by**

Distiller

**Type**

array

**UI name**

Default Page Size

**Default value**

```
[612.000 729.000]
```

<a id="75610"></a>
### StartPage

See the description of the `EndPage` setting.

**Supported by**

Distiller

**Type**

integer

**UI name**

All Pages, Pages From: To:

**Default value**

```
1
```

<a id="37637"></a>
## Image settings

This section lists the Adobe PDF settings that apply to each image type. In Distiller, these options appear in the “Images” panel of the user interface. For the Creative Suite applications, these settings appear in the “Compression” panel. (Photoshop does not present different options for the different image types but uses the settings that apply to the active image.)

For more information on how these settings are used together, see [Using the image settings](PDF_Create_UsingSettings.md#29125).

<a id="17123"></a>
## Color image settings

This section lists the compression and downsampling settings for color images (images that have more than one color component).

<a id="58917"></a>
### AntiAliasColorImages

If `true` , Distiller permits anti-aliasing on color images.

Anti-aliasing increases the number of bits per component in downsampled images to preserve some of the information that is otherwise lost by downsampling. Anti-aliasing is only performed if the image is actually downsampled and `ColorImageDepth` has a value greater than the number of bits per color component in the input image.

For more information on anti-aliasing see [Controlling bit depth](PDF_Create_UsingSettings.md#95410).

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
false
```

<a id="24040"></a>
### AutoFilterColorImages

If `true` , the compression filter for color images is chosen based on the properties of each image, in conjunction with the `ColorImageAutoFilterStrategy` setting. See [Automatic compression](PDF_Create_UsingSettings.md#99144) for more information.

If `false` , all color sampled images are compressed using the filter specified by `ColorImageFilter`.

This setting is relevant only if `EncodeColorImages` is `true`.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Compression: Automatic (JPEG) & Automatic (JPEG2000)

**Default value**

```
true
```

<a id="30939"></a>
### ColorACSImageDict

Dictionary of parameters for JPEG compression when JPEG is chosen from the Automatic filter selection (see [AutoFilterColorImages](PDF_Create_CommonSettings.md#24040)). `ColorACSImageDict` is based on the `DCTEncode` parameter dictionary described in Section 3.13.3 in the *PostScript Language Reference* .

See [Monochrome (black and white) images](PDF_Create_UsingSettings.md#90740) for details on the use of this dictionary.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Image Quality

**Default value**

```
<</Qfactor 0.76 /Hsamples [2 1 1 2] /Vsamples [2 1 1 2]>>
```

<a id="62153"></a>
### ColorImageAutoFilterStrategy

Specifies the automatic compression strategy that is used when `AutoFilterColorImages` is set to `true`.  Must be one of the following values:

| Value | UI equivalent | Description |
| --- | --- | --- |
| JPEG | Automatic (JPEG) | Lossy JPEG compression is used for low-frequency images and lossless Flate compression for high-frequency images. |
| JPEG2000 | Automatic (JPEG2000) | Applies only when `CompatibilityLevel` is set to 1.5 or higher. Lossy JPEG2000 compression is used for low-frequency images (images with smooth color changes) and lossless JPEG2000 compression for high-frequency images. |

See [Automatic compression](PDF_Create_UsingSettings.md#99144) for more information.

**Supported by**

Distiller, Illustrator, InDesign

**Type**

name.

**UI name**

Compression

**Default value**

```
JPEG
```

<a id="21873"></a>
### ColorImageDepth

Specifies the number of bits per color component in the output image. See [Controlling bit depth](PDF_Create_UsingSettings.md#95410) for more information.

Allowed values are:

- The number of bits per sample: `1` , `2` , `4` , or `8`.
- `-1` , which forces the downsampled image to have the same number of bits per color component as the original image

> **Note**
>
> Photoshop uses the `Downsample16BitImages` setting to decrease the bit depth of 16-bit images to 8 bits per sample so that JPEG compression can be used.

**Supported by**

Distiller

**Type**

integer

**Default value**

```
-1
```

<a id="13008"></a>
### ColorImageDict

Dictionary of parameters for JPEG compression. `ColorImageDict` is based on the `DCTEncode` parameter dictionary described in Section 3.13.3 in the *PostScript Language Reference* .

See [Monochrome (black and white) images](PDF_Create_UsingSettings.md#90740) for details on how this dictionary is used.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Image Quality

**Default value**

```
<</Qfactor 0.76 /Hsamples [2 1 1 2] /Vsamples [2 1 1 2]>>
```

### ColorImageDownsampleThreshold

Sets the downsample threshold for color images. This is the ratio of image resolution to output resolution above which downsampling may be performed. Must be between 1.0 through 10.0, inclusive. If you set the threshold out of range, it reverts to a default of 1.5.

See [Downsampling and subsampling images](PDF_Create_UsingSettings.md#68478) for details on using this setting.

**Supported by**

all applications

**Type**

number

**UI name**

pixels per inch; for images above: *value* pixels per inch

**Default value**

1.5 (UI shows 225 pixels-per-inch)

<a id="85568"></a>
### ColorImageDownsampleType

Must be one of the following values:

| Value | UI equivalent | Description |
| --- | --- | --- |
| Average | Average Downsampling to | Groups of samples are averaged to get the new downsampled value. |
| Bicubic | Bicubic Downsampling to | Bicubic interpolation is used on a group of samples to get a new downsampled value. |
| Subsample | Subsampling to | The center sample from a group of samples is used as the new downsampled value. |
| None | Distiller: Off<br><br>CS: Do Not Downsample | No sampling |

**Supported by**

all applications

**Type**

name

**UI name**

Sampling

**Default value**

```
Bicubic
```

<a id="24916"></a>
### ColorImageFilter

Specifies the compression filter to be used for color images. Ignored if `AutoFilterColorImages` is `true` or `EncodeColorImages` is `false`.

Must be one of the following values:

| Value | UI equivalent | Description |
| --- | --- | --- |
| DCTEncode | JPEG | Selects JPEG compression. |
| FlateEncode | ZIP | Selects Flate (ZIP) compression. |
| JPXEncode | JPEG2000 | Selects JPEG2000 compression. |

> **Note**
>
> JPEG2000 options only appear in UI if `CompatibilityLevel` is set to 1.5 or higher.

`DCTEncode` is used only if the output image has 8 bits per color component; otherwise `FlateEncode` is used.

For compatibility with Distiller 3.0 Adobe PDF settings files, Distiller 6.0 and later (as well as Creative Suite applications) revert to Flate compression if this setting is set to `LZWEncode`.  Other values cause Distiller to stop with a range error.

**Supported by**

all applications

**Type**

name

**UI name**

Compression

**Default value**

```
DCTEncode
```

<a id="62736"></a>
### ColorImageMinDownsampleDepth

If `DownsampleColorImages` is `true` , controls the range of bit depths for which color image downsampling occurs. Valid values are 1, 2, 4 or 8.

For more information, see [Controlling the range of bit depths for which downsampling occurs](PDF_Create_UsingSettings.md#70454).

**Supported by**

Distiller

**Type**

integer

**Default value**

```
1
```

<a id="11702"></a>
### ColorImageMinResolution

Imposes a lower limit to the resolution of sampled images. Valid values are from 9 to 64000, inclusive.

How this value is used is determined by `ColorImageMinResolutionPolicy`.  For more information, see [Specifying a minimum resolution of sampled images](PDF_Create_UsingSettings.md#75361).

**Supported by**

Distiller

**Type**

integer

**UI name**

Policy->Color Image Policy

**Default value**

```
150
```

<a id="97542"></a>
### ColorImageMinResolutionPolicy

Sets the policy for imposition of a lower limit to the resolution of sampled color images as specified by the `ColorImageMinResolution` setting. The following table shows the valid names.

| Value | UI equivalent | Description |
| --- | --- | --- |
| OK | Ignore | Distiller’s default behavior does not change—i.e., Distiller does not enforce any lower limit on image resolution, ignoring any value specified by `ColorImageMinResolution`. |
| Warning | Warn and continue | A warning is issued every time a sampled color image with resolution smaller than the value specified by `ColorImageMinResolution` is placed in the PDF file. The job continues after issuing the warning. |
| Error | Cancel job | An error occurs when a sampled color image with resolution smaller than the value specified by `ColorImageMinResolution` is placed in the PDF file. The job fails with a limit check error. |

For more information, see [Specifying a minimum resolution of sampled images](PDF_Create_UsingSettings.md#75361).

**Supported by**

Distiller

**Type**

name

**UI name**

Policy->Color Image Policy

**Default value**

```
OK
```

<a id="35897"></a>
### ColorImageResolution

Specifies the resolution to which downsampled color images are reduced; valid values are 9 to 2400 pixels per inch. A color image is downsampled if `DownsampleColorImages` is `true` and the resolution of the input image meets the criteria described in [Downsampling and subsampling images](PDF_Create_UsingSettings.md#68478).

**Supported by**

all applications

**Type**

integer

**UI name**

Sampling: pixels per inch

**Default value**

```
150
```

<a id="35272"></a>
### ConvertImagesToIndexed

If `true` , Distiller converts images that use fewer than 257 colors to an indexed color space for compactness. This conversion, when enabled, produces smaller PDF files but may make distillation slower.

> **Note**
>
> Creative Suite applications behave as if this setting is always `true`.

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
true
```

<a id="56842"></a>
### CropColorImages

If `CropColorImages` is `false` , color images are never cropped, whether or not the current clip would remove any image samples.

For more information, see [Disabling of image cropping](PDF_Create_UsingSettings.md#16777).

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
true
```

<a id="50851"></a>
### DownsampleColorImages

If `true` , color images are downsampled using the resolution specified by `ColorImageResolution` , assuming the threshold specified by `ColorImageDownsampleThreshold` is met. If `false` , downsampling is not done and the resolution of color images in the PDF file is the same as the source images.

See [Downsampling and subsampling images](PDF_Create_UsingSettings.md#68478) for more information.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Sampling

**Default value**

```
true
```

<a id="29745"></a>
### EncodeColorImages

If `true` , color images are encoded using the compression filter specified by the value of `ColorImageFilter`.  If `false` , compression filters are not applied to color images.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Compression

**Default value**

```
true
```

<a id="90844"></a>
### JPEG2000ColorACSImageDict

Dictionary of parameters for automatic JPEG2000 compression of color images. See [JPEG2000](PDF_Create_UsingSettings.md#60774) for details.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Image Quality, Tile Size

**Default value**

```
<</TileWidth 256/TileHeight 256/Quality 15 >>
```

<a id="80211"></a>
### JPEG2000ColorImageDict

Dictionary of parameters for JPEG2000 compression of color images. See [JPEG2000](PDF_Create_UsingSettings.md#60774) for details.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Image Quality, Tile Size

**Default value**

```
<</TileWidth 256/TileHeight 256/Quality 15 >>
```

<a id="87924"></a>
## Grayscale image settings

This section lists compression and downsampling settings for grayscale images (images with only one color component and more than one bit per sample).

<a id="98715"></a>
### AntiAliasGrayImages

If `true` , Distiller permits anti-aliasing on grayscale images. Anti-aliasing increases the number of bits per component in downsampled images to preserve some of the information that is otherwise lost by downsampling. Anti-aliasing is only performed if the image is actually downsampled and `GrayImageDepth` has a value greater than the number of bits per sample in the input image. For more information, see [Controlling bit depth](PDF_Create_UsingSettings.md#95410).

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
false
```

<a id="89851"></a>
### AutoFilterGrayImages

If `true` , the compression filter for gray images is chosen based on the properties of each image, in conjunction with the `GrayImageAutoFilterStrategy` setting. See [Automatic compression](PDF_Create_UsingSettings.md#99144) for more information. If `false` , all color sampled images are compressed using the filter specified by `GrayImageFilter`.  This setting is relevant only if `EncodeGrayImages` is `true`.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Compression

**Default value**

```
true
```

<a id="97898"></a>
### CropGrayImages

If `false` , gray images are never cropped, whether or not the current clip would remove any image samples. See [Disabling of image cropping](PDF_Create_UsingSettings.md#16777) for more information.

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
true
```

<a id="99054"></a>
### DownsampleGrayImages

If `true` , grayscale images are downsampled using the resolution specified by `GrayImageResolution`.  If `false` , downsampling does not occur, and the resolution of grayscale images in the PDF file is the same as the source images.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Sampling

**Default value**

```
true
```

<a id="16389"></a>
### EncodeGrayImages

If `true` , grayscale images are encoded using the compression filter specified by the value of `GrayImageFilter`.  If `false` , compression filters are not applied to grayscale sampled images.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Compression

<a id="38481"></a>
### GrayACSImageDict

Dictionary of parameters for JPEG compression when JPEG is chosen from the Automatic filter selection (see [AutoFilterGrayImages](PDF_Create_CommonSettings.md#89851)).

`GrayACSImageDict` is based on the `DCTEncode` parameter dictionary described in Section 3.13.3 in the *PostScript Language Reference* .

See [Monochrome (black and white) images](PDF_Create_UsingSettings.md#90740) for details on how this dictionary is used.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Image Quality

**Default value**

```
<</Qfactor 0.76 /Hsamples [2 1 1 2] /Vsamples [2 1 1 2]>>
```

<a id="99033"></a>
### GrayImageAutoFilterStrategy

Specifies the automatic compression strategy that is used when `AutoFilterGrayImages` is set to `true`.  The following table shows the valid values.

| Value | UI equivalent | Description |
| --- | --- | --- |
| JPEG | Automatic (JPEG) | Lossy JPEG compression is used for low-frequency images and lossless Flate compression for high-frequency images. |
| JPEG2000 | Automatic (JPEG2000) | Applies only if `CompatibilityLevel` is set to 1.5 or higher. Lossy JPEG2000 compression is used for low-frequency images (images with smooth color changes) and lossless JPEG2000 compression for high-frequency images. |

See [Automatic compression](PDF_Create_UsingSettings.md#99144) for more information.

**Supported by**

all applications

**Type**

name

**UI name**

Compression

**Default value**

```
JPEG
```

<a id="16705"></a>
### GrayImageDepth

Specifies the number of bits per sample in the image. The following values are valid:

- The number of bits per sample: `1` , `2` , `4` , or `8`.
- `-1` , which forces the downsampled image to have the same number of bits per sample as the original image

See [Controlling bit depth](PDF_Create_UsingSettings.md#95410) for more information.

**Supported by**

Distiller

**Type**

integer

**Default value**

```
-1
```

<a id="79547"></a>
### GrayImageDict

Dictionary of parameters for JPEG compression. `GrayImageDict` is based on the `DCTEncode` parameter dictionary described in Section 3.13.3 in the *PostScript Language Reference* .

See [Monochrome (black and white) images](PDF_Create_UsingSettings.md#90740) for details on how this dictionary is used.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Image Quality

**Default value**

```
<</Qfactor 0.76 /Hsamples [2 1 1 2] /Vsamples [2 1 1 2]>>
```

<a id="70763"></a>
### GrayImageDownsampleThreshold

Sets the image downsample threshold for grayscale images. This is the ratio of image resolution to output resolution above which downsampling may be performed.

See [Downsampling and subsampling images](PDF_Create_UsingSettings.md#68478) for details on using this setting.

**Supported by**

all applications

**Type**

number

**UI name**

pixels per inch, for images above: *value* pixels per inch

**Default value**

```
1.50000
```

<a id="87439"></a>
### GrayImageDownsampleType

Must be one of the following values.

| Value | UI equivalent | Description |
| --- | --- | --- |
| Average | Average Downsampling to | Groups of samples are averaged to get the new downsampled value. |
| Bicubic | Bicubic Downsampling to | Bicubic interpolation is used on a group of samples to get a new downsampled value. |
| Subsample | Subsampling to | The center sample from a group of samples is used as the new downsampled value. |
| None | Distiller: Off<br><br>CS: Do Not Downsample | No sampling |

**Supported by**

all applications

**Type**

name

**UI name**

Sampling

**Default value**

```
Bicubic
```

<a id="87077"></a>
### GrayImageFilter

Specifies the compression filter to be used for grayscale images. Ignored if `AutoFilterGrayImages` is `true` or `EncodeGrayImages` is `false`.  The following values are valid.

| Value | UI equivalent | Description |
| --- | --- | --- |
| DCTEncode | JPEG | Selects JPEG compression. |
| FlateEncode | ZIP | Selects Flate (ZIP) compression. |
| JPXEncode | JPEG2000 | Selects JPEG2000 compression. |

> **Note**
>
> JPEG2000 options only appear in UI if `CompatibilityLevel` is set to 1.5 or higher.

`DCTEncode` is used only if the output image has 8 bits per sample; otherwise `FlateEncode` is used. For compatibility with Distiller 3.0 Adobe PDF settings files, Distiller 6.0 and later (as well as Creative Suite applications) revert to Flate compression if this setting is set to `LZWEncode`.

**Supported by**

all applications

**Type**

name

**UI name**

Compression

**Default value**

```
DCTEncode
```

<a id="93916"></a>
### GrayImageMinDownsampleDepth

If `DownsampleGrayImages` is `true` , controls the range of bit depths for which gray image downsampling occurs. Valid values are 2, 4 or 8.

For more information, see [Controlling the range of bit depths for which downsampling occurs](PDF_Create_UsingSettings.md#70454).

**Supported by**

Distiller

**Type**

integer

**Default value**

```
2
```

<a id="83370"></a>
### GrayImageMinResolution

Imposes a lower limit to the resolution of sampled grayscale images. The legal values are from 9 to 64000, inclusive. How this value is used by Distiller is determined by `GrayImageMinResolutionPolicy`.  For more information, see [Specifying a minimum resolution of sampled images](PDF_Create_UsingSettings.md#75361).

**Supported by**

Distiller

**Type**

integer

**UI name**

Policy->Grayscale Image Policy

**Default value**

```
150
```

<a id="58792"></a>
### GrayImageMinResolutionPolicy

Sets the policy for imposition of a lower limit to the resolution of sampled images as specified by the `GrayImageMinResolution` setting. The following values are valid.

| Value | UI equivalent | Description |
| --- | --- | --- |
| OK | Ignore | Distiller’s default behavior does not change—i.e., Distiller does not enforce any lower limit on image resolution, ignoring any value specified by `GrayImageMinResolution`. |
| Warning | Warn and continue | A warning is issued every time a sampled grayscale image with resolution smaller than the value specified by `GrayImageMinResolution` is placed in the PDF file. The job continues after issuing the warning. |
| Error | Cancel job | An error occurs when a sampled grayscale image with resolution smaller than the value specified by `GrayImageMinResolution` is placed in the PDF file. The job fails with a limit check error. |

For more information, see [Specifying a minimum resolution of sampled images](PDF_Create_UsingSettings.md#75361).

**Supported by**

Distiller

**Type**

name

**UI name**

Policy->Grayscale Image Policy

**Default value**

```
OK
```

<a id="83653"></a>
### GrayImageResolution

Specifies the resolution to which downsampled gray images are reduced. Valid values are 9 to 2400 pixels per inch. A gray image is downsampled if `DownsampleGrayImages` is `true` and the resolution of the input image meets the criteria described in [Downsampling and subsampling images](PDF_Create_UsingSettings.md#68478).

**Supported by**

all applications

**Type**

integer

**UI name**

pixels per inch

**Default value**

```
150
```

<a id="90478"></a>
### JPEG2000GrayACSImageDict

Dictionary of parameters for automatic JPEG2000 compression of grayscale. See [JPEG2000](PDF_Create_UsingSettings.md#60774) for details.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Image Quality, Tile Size

**Default value**

```
<</TileWidth 256 /TileHeight 256 /Quality 15>>
```

<a id="99239"></a>
### JPEG2000GrayImageDict

Dictionary of parameters for JPEG2000 compression of grayscale images. See [JPEG2000](PDF_Create_UsingSettings.md#60774) for details.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Image Quality, Tile Size

**Default value**

```
<</TileWidth 256 /TileHeight 256 /Quality 15 >>
```

<a id="80036"></a>
## Monochrome image settings

This section lists the compression and downsampling settings for monochrome images (images with only one color component and one bit per sample). See [Monochrome (black and white) images](PDF_Create_UsingSettings.md#90740) for more information.

> **Note**
>
> With the exception of the `AntiAliasMonoImages` and `MonoImageDepth` settings, the compression settings also can be applied to stencil masks created by the `imagemask` operator. Settings behavior is the same in both cases. For details on `imagemask` , see the *PostScript Language Reference* .

<a id="60083"></a>
### AntiAliasMonoImages

If `true` , anti-aliasing is permitted on monochrome images.

Anti-aliasing increases the number of bits per sample in downsampled images to preserve some of the information that is otherwise lost by downsampling. Anti-aliasing is only performed if the image is actually downsampled and `MonoImageDepth` has a value greater than 1. For more information on anti-aliasing see [Controlling bit depth](PDF_Create_UsingSettings.md#95410).

> **Note**
>
> Distiller does not do anti-aliasing for image masks, regardless of the value of `AntiAliasMonoImages`.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Anti-Alias to gray

**Default value**

```
false
```

<a id="31068"></a>
### CropMonoImages

If `false` , monochrome images are never cropped, whether or not the current clip would remove any image samples.

For more information, see [Disabling of image cropping](PDF_Create_UsingSettings.md#16777).

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
true
```

<a id="91682"></a>
### DownsampleMonoImages

If `true` , monochrome images are downsampled using the resolution specified by `MonoImageResolution`.  If `false` , downsampling is not done and the resolution of monochrome images in the PDF file is the same as the source images.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Sampling

**Default value**

```
true
```

<a id="49057"></a>
### EncodeMonoImages

If `true` , monochrome images are encoded using the compression filter specified by the value of `MonoImageFilter`.  If `false` , no compression filters are applied to monochrome images.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Compression

**Default value**

```
true
```

<a id="72434"></a>
### MonoImageDepth

Specifies the number of bits per sample in a downsampled image. Allowed values are:

- The number of bits per sample: `1` , `2` , `4` , or `8`.  When the value is greater than `1` , monochrome images are converted to grayscale images.
- `-1` , which forces the downsampled image to have the same number of bits per sample as the original image. (For monochrome images, this is the same as a value of 1.)

`MonoImageDepth` is not used unless `DownsampleMonoImages` and `AntiAliasMonoImages` are `true`.  See [Controlling bit depth](PDF_Create_UsingSettings.md#95410) for more information.

> **Note**
>
> Distiller ignores `MonoImageDepth` for image masks.

**Supported by**

Distiller

**Type**

integer

**UI name**

Anti-Alias to gray

**Default value**

```
-1
```

<a id="79634"></a>
### MonoImageDict

Dictionary of parameters for CCITT compression. `MonoImageDict` is based on the `CCITTFaxEncode` parameter dictionary. A value of `-1` for `K` corresponds to CCITT Group 4; 0 corresponds to CCITT group 3. See [Monochrome (black and white) images](PDF_Create_UsingSettings.md#90740) for more information.

**Supported by**

all applications

**Type**

dictionary

**UI name**

Compression, Quality

**Default value**

```
<< /K -1 >>
```

<a id="61923"></a>
### MonoImageDownsampleThreshold

Sets the image downsample threshold for monochrome images. This is the ratio of image resolution to output resolution above which downsampling may be performed. See [Downsampling and subsampling images](PDF_Create_UsingSettings.md#68478) for more information.

**Supported by**

all applications

**Type**

number

**UI name**

pixels-per-inch for images above: *value* pixels-per-inch

**Default value**

`1.50000` (UI shows 450 pixels-per-inch)

<a id="27721"></a>
### MonoImageDownsampleType

Must be one of the following values.

| Value | UI equivalent | Description |
| --- | --- | --- |
| Average | Average Downsampling to | Groups of samples are averaged to get the new downsampled value. |
| Bicubic | Bicubic Downsampling to | Bicubic interpolation is used on a group of samples to get a new downsampled value. |
| Subsample | Subsampling to | The center sample from a group of samples is used as the new downsampled value. |
| None | Distiller: Off; CS: Do Not Downsample | No sampling |

**Supported by**

all applications

**Type**

name

**UI name**

Sampling

**Default value**

```
Bicubic
```

<a id="77003"></a>
### MonoImageFilter

Specifies the compression filter to be used for monochrome images. Must be one of the following values:

| Value | UI equivalent | Description |
| --- | --- | --- |
| CCITTFaxEncode | CCITT Group 3/<br><br>CCITT Group 4 | Selects CCITT Group 3 or 4 facsimile encoding |
| FlateEncode | ZIP | Selects Flate (ZIP) compression |
| RunLengthEncode | Run Length | Selects run length encoding |

For compatibility with Distiller 3.0 Adobe PDF settings files, Distiller 6.0 and later (as well as Creative Suite applications) revert to Flate compression if this setting is set to `LZWEncode`.  Other values cause Distiller to stop with a range error.

**Supported by**

all applications

**Type**

name

**UI name**

Compression

**Default value**

```
CCITTFaxEncode
```

<a id="27387"></a>
### MonoImageMinResolution

Imposes a lower limit to the resolution of sampled monochrome images. The legal values are from 9 to 64000, inclusive. How this value is used by Distiller is determined by `MonoImageMinResolutionPolicy`.  For more information, see [Specifying a minimum resolution of sampled images](PDF_Create_UsingSettings.md#75361).

**Supported by**

Distiller

**Type**

integer

**UI name**

Policy->Monochrome Image Policy

**Default value**

```
300
```

<a id="54212"></a>
### MonoImageMinResolutionPolicy

Sets the policy for imposition of a lower limit to the resolution of sampled images as specified by the `MonoImageMinResolution` setting. The following values are valid.

| Value | UI equivalent | Description |
| --- | --- | --- |
| OK | Ignore | Distiller’s default behavior does not change—i.e., Distiller does not enforce any lower limit on image resolution, ignoring any value specified by `MonoImageMinResolution`. |
| Warning | Warn and continue | A warning is issued every time a sampled monochrome image with resolution smaller than the value specified by `MonoImageMinResolution` is placed in the PDF file. The job continues after issuing the warning. |
| Error | Cancel job | An error occurs when a sampled monochrome image with resolution smaller than the value specified by `MonoImageMinResolution` is placed in the PDF file. The job fails with a limit check error. |

For more information, see [Specifying a minimum resolution of sampled images](PDF_Create_UsingSettings.md#75361).

**Supported by**

Distiller

**Type**

name

**UI name**

Policy->Monochrome Image Policy

**Default value**

```
OK
```

<a id="38342"></a>
### MonoImageResolution

Specifies the resolution to which downsampled monochrome images are reduced; valid values are 9 to 2400 pixels per inch. A monochrome image is downsampled if `DownsampleMonoImages` is `true` and the resolution of the input image meets the criteria described in [Downsampling and subsampling images](PDF_Create_UsingSettings.md#68478).

**Supported by**

all applications

**Type**

integer

**UI name**

pixels per inch

**Default value**

```
300
```

<a id="16406"></a>
## Page Compression Setting

This section describes the page compression setting.

<a id="84100"></a>
### CompressPages

If `true` , Flate compression is used to compress page content streams as well as form, pattern, and Type 3 font content streams.

InDesign also compresses ICC profiles, OutputIntentProfile and shading streams.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Distiller: *none*

InDesign: Compress Text and Line Art

**Default value**

```
true
```

<a id="38175"></a>
## Font settings

This section lists the settings available for controlling font embedding and subsetting. For more information on font embedding, see [Using the font settings](PDF_Create_UsingSettings.md#38175).

> **Note**
>
> Embedding is subject to license; specific fonts can indicate that embedding is not permitted.

<a id="41375"></a>
### AlwaysEmbed

An array consisting either entirely of font names, or of a Boolean value followed by font names. Each name is the PostScript language name of the font (the name given to `definefont` ).

- If the array consists entirely of names, Distiller sets its internal list of fonts that must be embedded to be exactly the list of names in the array.
- If the first array value is the Boolean `true` , Distiller adds the font names in the rest of the `AlwaysEmbed` array to its internal list of fonts that must be embedded.
- If the first array value is the Boolean `false` , Distiller removes the font names in the rest of the `AlwaysEmbed` array from its internal list of fonts to be embedded.

If a font name appears in both `AlwaysEmbed` and `NeverEmbed` , `NeverEmbed` takes precedence.

**Supported by**

Distiller

**Type**

array

**UI name**

Always Embed Font

**Default value**

```
[true]
```

### CannotEmbedFontPolicy

The policy Distiller uses if it cannot find, or cannot embed, the font. The following values are valid.

| Value | UI equivalent | Description |
| --- | --- | --- |
| OK | Ignore | Distiller ignores and continues. |
| Warning | Warn and continue | Distiller displays a warning and continues. |
| Error | Cancel job | Distiller quits distilling the current job. |

**Supported by**

Distiller

**Type**

name

**UI name**

When embedding fails

**Default value**

```
Warning
```

<a id="62786"></a>
### EmbedAllFonts

If `true` , all fonts that have correct permissions are embedded in the PDF file; if `false` , they are not embedded:

- Creative Suite applications automatically embed fonts.
- Distiller never embeds fonts in its `NeverEmbed` list even if this setting is `true`.

**Supported by**

Distiller

**Name:** Boolean

**UI name**

Embed all fonts

**Default value**

```
true
```

### EmbedOpenType

If `true` , OpenType fonts are embedded only if all of the following are true:

- The OpenType font is to be embedded within a Type 1 font descriptor
- `EmbedOpenType` is `true`
- `CompatibilityLevel` is 1.6 or higher
- `SubsetFonts` is `false` , or `SubsetFonts` is `true` and the percentage of characters used is greater than `MaxSubsetPct`.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Embed OpenType fonts

> **Note**
>
> Embed OpenType fonts can only be set from the UI if `CompatibilityLevel` is set to 1.6 or higher.

**Default value**

```
false
```

<a id="32083"></a>
### MaxSubsetPct

The maximum percentage of glyphs in a font that can be used before the entire font is embedded instead of a subset. The allowable range is 1 through 100.

Distiller only uses this value if `SubsetFonts` is `true`.  For example, a value of 30 means that a font will be embedded in full (not subset) if more than 30% of glyphs are used; a value of 100 means all fonts will be subset no matter how many glyphs are used (because you cannot use more than 100% of glyphs).

**Supported by**

all applications

**Type**

integer

**UI name**

Subset embedded fonts when percent of characters used is less than: *value* %

**Default value**

```
100
```

<a id="83204"></a>
### NeverEmbed

An array consisting either entirely of font names, or of a Boolean value followed by font names. Each font name must be the PostScript language name of the font (that is, the name given to `definefont` ).

- If the array consists entirely of names, Distiller sets its internal list of fonts that must never be embedded to be exactly the list of names in the array.
- If the first array value is the Boolean `true` , Distiller adds the font names in the rest of the `NeverEmbed` array to its internal list of fonts that must never be embedded.
- If the first array value is the Boolean `false` , Distiller removes the font names in the rest of the `NeverEmbed` array from its internal list of fonts to never be embedded.

If a font name appears in both `AlwaysEmbed` and `NeverEmbed` , `NeverEmbed` takes precedence.

**Supported by**

Distiller

**Type**

array

**UI name**

Never Embed Font

**Default value**

```
[true]
```

<a id="95022"></a>
### SubsetFonts

If `true` , font subsetting is enabled. If `false` , subsetting is not enabled. Font subsetting embeds only those glyphs that are used in a document, instead of the entire font. This reduces the size of a PDF file that contains embedded fonts. If font subsetting is enabled, the application determines whether to embed the entire font or a subset by the number of glyphs in the font that are used (including component glyphs referenced by ‘seac’ \[Type 1\] glyphs), and the value of `MaxSubsetPct`.

Subsetted fonts in the PDF file appear with a 6-letter prefix and a plus (+) sign. For example, Palatino subsetted may appear as:

```
NPBOME+Palatino-Roman
```

> **Note**
>
> Embedded instances of multiple master fonts and of Type 3, TrueType, and CID fonts are always subsetted, regardless of the value of `SubsetFonts`.

**Supported by**

all applications

**Type**

Boolean

**UI name**

Subset embedded fonts when percent of characters used is less than:

<a id="99371"></a>
## Color conversion settings

This section lists the color conversion settings supported by Distiller. Some are indicated as supported by Creative Suite applications and can approximate the settings defined in the `CreativeSuite` namespace, which provide greater control over color conversions. Creative Suite applications can use these settings if present and write them to settings files for compatibility. See [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for details.

<a id="20259"></a>
### CalCMYKProfile

The name of the ICC profile that is used for tagging or converting CMYK images, text, and/or graphics.

> **Note**
>
> Creative Suite applications give precedence to their own color management settings and may use this setting for compatibility with Distiller; see [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for details.

**Supported by**

all applications

**Type**

string

**UI name**

Working Spaces: CMYK

**Default value**

```
(U.S. Web Coated SWOP v2)
```

<a id="59365"></a>
### CalGrayProfile

The name of the ICC profile that is used for tagging or converting Gray images, text, and/or graphics.

> **Note**
>
> Creative Suite applications give precedence to their own color management settings and may use this setting for compatibility with Distiller; see [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for details.

**Supported by**

all applications

**Type**

string

**UI name**

Working Spaces: Gray

<a id="95437"></a>
### CalRGBProfile

The name of the ICC profile that is used for tagging or converting RGB images, text, and/or graphics.

> **Note**
>
> Creative Suite applications give precedence to their own color management settings and may use this setting for compatibility with Distiller; see [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for details.

**Supported by**

all applications

**Type**

string

**UI name**

Working Spaces: RGB

**Default value**

```
(sRGB IEC61966-2.1)
```

<a id="13366"></a>
### ColorConversionStrategy

Sets the color conversion strategy, which includes the output color family and color space and the inclusion of ICC profiles.

See [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for details on how to use this setting.

The section [Color settings interchange](PDF_Create_UsingSettings.md#35911) describes how the values of this setting map to those in the `CreativeSuite` `namespace`.

The following values are valid.

| Value | UI equivalent |
| --- | --- |
| LeaveColorUnchanged | Leave Color Unchanged |
| UseDeviceIndependentColor | Tag Everything for Color Management<br>(no conversion) |
| UseDeviceIndependendColor-ForImages | Tag Only Images for Color Management<br>(no conversion) |
| sRGB | Convert All Colors to sRGB |
| CMYK | Convert All Colors to CMYK |

**Supported by**

all applications

**Type**

name

**UI name**

Distiller: Color Management Policies

Creative Suite: no single setting (see below)

**Default value**

```
sRGB
```

<a id="26433"></a>
### ColorSettingsFile

Specifies the name of a color settings file to be used for color conversions. When this file is specified as a non-empty value, all other color conversion settings are ignored and not selectable in the UI.

If the name is `(None)` or `()` , the other settings are used.

The Creative Suite applications use color settings files but do not use this setting. See [Using the color conversion settings](PDF_Create_UsingSettings.md#86731) for more information.

**Supported by**

Distiller

**Type**

string

**UI name**

Settings File

**Default value**

```
()
```

<a id="17572"></a>
### DefaultRenderingIntent

Specifies the rendering intent for objects to be written to the PDF document, when not otherwise specified in the PostScript job by means of the `findcolorrendering` and `setcolorrendering` operators (see Section 7.1.3 in the *PostScript Language Reference* for details).

If the value of this setting is `Default` , no rendering intent is written to the PDF document. The following values are valid.

| Value | UI equivalent |
| --- | --- |
| Default | Preserve |
| Perceptual | Perceptual |
| Saturation | Saturation |
| AbsoluteColorimetric | Absolute Colorimetric |
| RelativeColorimetric | Relative Colorimetric |

**Supported by**

Distiller

**Type**

name

**UI name**

Document Rendering Intent

**Default value**

```
Default
```

<a id="53017"></a>
### ParseICCProfilesInComments

If `true` , Distiller honors EPS embedded ICC profiles when distilling. ICC profiles are honored only if they are enclosed in two DSC pairs: `ICCProfile` and `SetColorSpace`.  See the ICC specification (available at [http://www.color.org](http://www.color.org) ), section B.2, for details on the syntax of these comment pairs.

This setting is ignored if `CompatibilityLevel` is set to 1.2.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

*none*

**Default value**

```
true
```

<a id="50470"></a>
### PreserveDICMYKValues

Describes what to do with color values for device-independent CMYK color spaces. This setting is used only if `ColorConversionStrategy` is `CMYK`.

If `true` , CIEBasedDEFG CMYK color values are treated as DeviceCMYK values; CIEBasedDEFG color spaces will be ignored and discarded. If `false` , a conversion from CIEBasedDEFG color space to CMYK working space is performed.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Preserve CMYK values for calibrated CMYK color spaces

**Default value**

```
true
```

<a id="93521"></a>
### PreserveHalftoneInfo

If `true` , Distiller passes halftone screen information (frequency, angle, and spot function) into the PDF file. If `false` , halftone information is not passed in.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Preserve Halftone Information

**Default value**

```
false
```

<a id="25712"></a>
### sRGBProfile

*(Read Only)* The name of the ICC profile that is used for converting device-dependent or device-independent color spaces to CalRGB (PDF 1.2) or ICCBased (PDF 1.3 and above).

**Supported by**

all applications

**Type**

string

**Default value**

```
(sRGB IEC61966-2.1)
```

<a id="12788"></a>
### TransferFunctionInfo

Determines how Distiller handles transfer functions, which are traditionally used to compensate for dot gain or dot loss that may occur when an image is transferred to film. For example, a file that is intended for output on a particular imagesetter may contain transfer functions that compensate for the dot gain inherent with that printer. The following values are valid.

| Value | UI equivalent | Description |
| --- | --- | --- |
| Preserve | Preserve | Distiller preserves (passes into the PDF file) transfer functions. |
| Remove | Remove | Distiller ignores transfer functions. They are neither applied to the color values by Distiller nor passed into the PDF file. |
| Apply | Apply | Distiller uses the transfer function to modify the data it writes to the PDF file, instead of writing the transfer function itself to the file. This value is ignored by Distiller 4.0 but supported by Distiller 5.0 and later. It is sometimes used to achieve artistic effects (although the *PostScript Language Reference* discourages such usage). |

If you are generating PDF/X-compliant files, do not set this to `Preserve`.

**Supported by**

Distiller

**Type**

name

**UI name**

When transfer functions are found:

**Default value**

```
Preserve
```

<a id="19009"></a>
### UCRandBGInfo

Tells Distiller whether to pass the arguments to `setundercolorremoval` and `setblackgeneration` into the PDF file.

Must be one of the following values.

| Value | UI equivalent | Description |
| --- | --- | --- |
| Preserve | checked | Distiller preserves (passes into the PDF file) the arguments. |
| Remove | unchecked | Distiller ignores the arguments. |

See Section 7.2.3 in the *PostScript Language Reference* for details on the `setundercolorremoval` and `setblackgeneration` operators and descriptions of undercolor removal (UCR) and black generation (BG)

**Supported by**

Distiller

**Type**

name

**UI name**

Preserve Under Color Removal and Black Generation

**Default value**

```
Remove
```

<a id="86103"></a>
## Advanced Adobe PDF settings

This section lists the settings in the Advanced panel of the Distiller settings dialog box. Some of these settings are also supported by Creative Suite applications, as indicated.

### AllowPSXObjects

If `true` , allow PostScript XObjects. For a description of PostScript XObjects, see the [PDF Reference](https://www.adobe.com/go/pdfreference).

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Allow PostScript XObjects

**Default value**

```
true
```

<a id="30729"></a>
### AllowTransparency

The `SetTransparency pdfmark` is a `pdfmark` extension used to produce transparency in PDF 1.4 and later. For more details, see the [PDFMark Reference](../pdfmark/index.md). If this setting is `true, [... /SetTransparency pdfmark` is allowed in PS jobs if `CompatibilityLevel` is 1.4 or higher. If `false` , this `pdfmark` is treated as error.

> **Note**
>
> Creative Suite applications always include transparency in the exported PDF if `CompatibilityLevel` is 1.4 or higher.

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
false
```

### ASCII85EncodePages

If `true` , Distiller ASCII85-encodes binary streams such as page content streams, sampled images, and embedded fonts, resulting in a PDF file that is pure ASCII. If `false` , Distiller does not encode the binary streams, resulting in a PDF file that may contain substantial amounts of binary data. Distiller checks the value of this setting only once per document. Any change to it must be made before any marks are placed on the first page of the document.

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
false
```

### AutoPositionEPSFiles

If `true` , Distiller resizes the created page to the size of the EPS file using the `%%BoundingBox` comment in the header of the file, and centers the EPS file on the page when the EPS file is distilled. Distiller ignores this setting if `ParseDSCComments` is `false`.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Resize page and center artwork for EPS files

**Default value**

```
true
```

<a id="76577"></a>
### CreateJDFFile

If `true` , Distiller produces a Job Definition Format (JDF) file that reflects the parameters used for distillation. If `false` , a JDF file is not produced.

The Job Definition Format (JDF) Specification is owned and maintained by the International Cooperation for the Integration of Processes in Prepress, Press and PostPress (CIP4) (www.cip4.org). Distiller 7.0 complies with JDF Specification Version 1.1 Revision A, published on September 5, 2002. It is available on the web at:

[http://www.cip4.org/documents/jdf\_specifications/index.html](http://www.cip4.org/documents/jdf_specifications/index.html)

> **Note**
>
> The Acrobat 7 Professional product now supports creation of both JDF 1.1- and JDF 1.2-compliant JDF files. For more information, see the *Acrobat Guide* in Distiller online Help.

The Adobe Normalizer product (see *Using Adobe Normalizer Server, Version 6.0.4* ) is also capable of producing JDF files, but it can consume them as well. [Conversions Related to JDF](PDF_Create_JDF.md#95687),” describes how Normalizer interprets and converts Distiller parameters; use this information to understand the JDF file created by Distiller.

The JDF file is output to the current directory with the `.jdf` extension. The filename is the same as the `.log` file and the file that is being distilled. (The “current directory” is the directory where the new PDF file is output.)

> **Note**
>
> The `JDF` pdfmark allows the PostScript file/stream being distilled to specify certain elements and attributes to be added to a JDF file. For details, see *Using Adobe Normalizer Server, Version 6.0.4* and the [PDFMark Reference](../pdfmark/index.md).

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Create Job Definition Format (JDF) file

**Default value**

```
false
```

<a id="60352"></a>
### CreateJobTicket

If `true` , Distiller creates a Job Ticket object in the PDF file that contains specific information about this file—such as trapping information—that can be passed along to another application or print device.

This setting pertains to Portable Job Ticket Format 1.1, as described in *Portable Job Ticket Format, version 1.1* (Technical Note #5620).

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Save Portable Job Ticket inside PDF file

**Default value**

```
false
```

<a id="40548"></a>
### DetectBlends

If `true` , Distiller enables the conversion of PostScript gradients to smooth shades. If `false` , Distiller disables conversion.

> **Note**
>
> If `CompatibilityLevel` is less than 1.3, Distiller disables conversion regardless of the value of `DetectBlends`.  In addition, Distiller always disables conversion if idiom recognition is turned off in the prologue file or in the PostScript file itself.

Distiller uses two methods to perform the conversion of gradients to smooth shades:

- The PostScript Language Level 3 feature called *idiom recognition* replaces certain procedures (idioms) with others having equivalent behavior but producing better quality results. (See “Idiom Recognition” on page 119 of the *PostScript Language Reference* for details.) `DetectBlends` enables the subset of idioms that detect gradients (or blends) for the following applications: Adobe Illustrator, Adobe Freehand, CorelDraw, and QuarkXPress.
- Distiller also converts gradients to smooth shades independently of idiom recognition. This method is application-independent, but it is less reliable than the first.

In Distiller 4.0, the blend detecting idioms (first method) was controlled by the `IdiomRecognition` PostScript feature, while the second method was controlled by `DetectBlends`.  You had to turn off `IdiomRecognition` to use `DetectBlends`.

In Distiller 5.0 and above, `DetectBlends` controls the blend detecting idioms. By default `IdiomRecognition` is turned on in Distiller 5.0 and above, and the blend detecting idioms are controlled using `DetectBlends`.  You can still use the PostScript feature `IdiomRecognition` with the `setuserparams` operator, if needed.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Convert gradients to smooth shades

**Default value**

```
true
```

### DetectCurves

The value of this setting must be in the range from 0.0000 to 10.0000. If the value is 0.0000, the feature is disabled. If positive, Distiller investigates graphics for curves that are not described efficiently and thus result in unacceptably large file sizes. Distiller converts these curves into bezier curves that take up much less file space.

This setting represents a value in user space (72 dpi) that controls Distiller’s curve-fitting algorithm: the curve-fitting results should not part from the original line segments by more than this number. Visual inspection of the results suggests that the 0.1000 value yields the closest approximation to the original curve.

**Supported by**

Distiller

**Type**

number

**UI name**

Convert smooth lines to curves

**Default value**

```
0.1
```

### DSCReportingLevel

Level can be either `0` , `1` , or `2`.  `0` means no additional reporting. Level 1 shows all input as it is parsed and shows a tree crawl when getting into bad states. Level 2 shows transitions in addition to the information in Level 1.

**Supported by**

Distiller

**Type**

integer

**Default value**

```
0
```

<a id="96989"></a>
### EmbedJobOptions

If `true` , the settings file used to create the PDF is embedded in the PDF file and is accessible through the Acrobat UI (the Attachments tab in Acrobat 7). In the PDF file, the Adobe PDF creation settings file becomes an item in the `Names->EmbeddedFiles` tree (see the [PDF Reference](https://www.adobe.com/go/pdfreference) ).

> **Note**
>
> Applications other than Distiller do not embed the settings file, regardless of the value of this setting.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Distiller: Save Adobe PDF settings inside PDF file

**Default value**

```
false
```

### EmitDSCWarnings

If `true` , Distiller displays warning messages about questionable or incorrect DSC comments during the distillation of the PostScript file. Distiller ignores this setting if `ParseDSCComments` is `false`.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Log DSC warnings

**Default value**

```
false
```

<a id="12775"></a>
### LockDistillerParams

If `true` , Distiller ignores any settings specified by `setdistillerparams` operators in the incoming PostScript file and uses only those settings present in the Adobe PDF settings file (or their default values if not present).

If `false` , any settings specified in the PostScript file override the initial settings. These settings are in effect for the duration of the current `save` level.

> **Note**
>
> There are a number of settings whose values cannot be changed by `setdistillerparams` in a PostScript file. See [Modifying settings during the job](index.md#68813) for a complete list.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Allow PostScript file to override Adobe PDF settings

**Default value**

```
false
```

<a id="80125"></a>
### OPM

Controls the overprint mode strategy in the job. Set to 0 for full overprint or 1 for non-zero overprint. For more information, refer to Technical Note #5044, *Color Separation Conventions for PostScript Language Programs* , and the [PDF Reference](https://www.adobe.com/go/pdfreference).

> **Note**
>
> Distiller ignores this setting if `PreserveOverprintSettings` is `false`.

**Supported by**

Distiller

**Type**

integer

**UI name**

Overprinting default is nonzero overprinting

**Default value**

```
1
```

<a id="90565"></a>
### ParseDSCComments

If `true` , Distiller parses the DSC comments for any information that might be helpful for distilling the file or for information that is passed into the PDF file. If `false` , Distiller treats the DSC comments as pure PostScript comments and ignores them.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Process DSC Comments

**Default value**

```
true
```

<a id="84937"></a>
### ParseDSCCommentsForDocInfo

If `true` , Distiller attempts to preserve the Document Information from the PostScript DSC comments as properties of the PDF document. The following table lists this information.

| Document Information | Source |
| --- | --- |
| Author | from DSC keyword: `%%For:` |
| Creator | from DSC keyword: `%%Creator:` |
| Title | from DSC keyword: `%%Title:` |
| Producer | from Distiller product name (“Acrobat Distiller 7.0”) |
| CreationDate | from Distiller time stamp (creation time of PDF file) |
| ModDate | from Distiller time stamp (creation time of PDF file) |

> **Note**
>
> Distiller ignores this setting if `ParseDSCComments` is `false`.

Distiller 4.0 and higher places the Document Information in the `Info` dictionary of the PDF file; you can view the information in Acrobat by clicking File > Document Properties. Starting with version 5, Distiller also embeds the Document Information as XML in the PDF file. To embed the information, Distiller adds a `Metadata` key in the Catalog dictionary whose value is an indirect reference to a metadata stream object. The metadata object contains the metadata (the Document Information) for the PDF document. The metadata is represented as RDF, in conformance with Adobe’s Extensible Metadata Platform (XMP).

> **Note**
>
> If `true` , document properties of Microsoft Office files are carried into the PDF. A setting of `false` prevents this transfer of information.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Preserve document information from DSC

**Default value**

```
true
```

<a id="38057"></a>
### PassThroughJPEGImages

If `true` , JPEG images (images that are already compressed with the `DCTEncode` filter) are “passed through” Distiller without re-compressing them. (Distiller does perform a decompression to ensure that images are not corrupt, but then passes the original compressed image to the PDF file.) Images that are not compressed will still be compressed according to the image settings in effect for the type of image (for example, `ColorImageFilter` , etc.).

If `false` , all JPEG encoded images are decompressed and recompressed according the compression settings in effect.

Note, however, that JPEG images that meet the following criteria are *not* passed through even if the value of `PassThroughJPEGImages` is `true` :

- The image will be downsampled.
- `ColorConversionStrategy` is `sRGB` and the current PostScript color space (for the image) is not `DeviceRGB` or `DeviceGray`.
- The image will be cropped—i.e., the clip path is such that more than 10% of the image pixels will be removed.

Creative Suite applications do not use this setting. However, Illustrator and InDesign normally behave as if it were `true` with regard to placed PDF files containing compressed images. That is, they do not normally uncompress and recompress them, unless color conversion or downsampling takes place.

Passing through JPEG images has these advantages:

**Performance** : Only decompression and not recompression occurs.

**No loss of image data** : DCT encoding inherently causes some loss of data; thus, with this option, since no recompression occurs, no data is lost.

**No loss of metadata** : When Distiller decompresses an image, all metadata is discarded; thus, with this option, no metadata is lost since no recompression on the decompressed image occurs.

> **Note**
>
> Distiller’s hard-coded default value of `PassThroughJPEGImages` is `false` to conform to older settings files where this setting did not exist. Most predefined Adobe PDF settings files set it to `true`.  The `Smallest File Size` settings file sets it to `false` since that generally results in smaller file sizes. However, in some cases this setting could actually increase file size, for example, if the original JPEG in the PostScript file was compressed with a `Quality` setting lower than the `Quality` setting in the settings file.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Save original JPEG images in PDF if possible

**Default value**

```
false
```

### PreserveCopyPage

**Default value**

```
true
```

If `true` , Distiller maintains PostScript Language Level 2 compatibility for the `copypage` operator. If `false` , Distiller uses the PostScript Language Level 3 definition of the `copypage` operator. See the *PostScript Language Reference* for more information.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Preserve Level 2 copypage semantics

<a id="89116"></a>
### PreserveEPSInfo

If `true` , and `ParseDSCComments` is `true` , Distiller attempts to preserve the encapsulated PostScript (EPS) information in the PostScript file as properties of the resulting PDF file. The distilled EPS content is identified as marked content using the `EmbeddedDocument` key.

The following table lists this information.

| Document Information | Source |
| --- | --- |
| Author | from DSC keyword: `%%For:` |
| Creator | from DSC keyword: `%%Creator:` |
| Title | from DSC keyword: `%%Title:` |

Starting with version 5, Distiller also embeds the information for embedded EPS files as XML in the PDF file. To do this, Distiller performs the following tasks:

- Adds a `Metadata` key in the property list of the marked content container for the EPS.
- Stores the property list as an indirect reference in the page resources object.

The value of the `Metadata` key is an indirect reference to the metadata stream object, which contains the metadata (the EPS information). The metadata is represented as RDF, in conformance with Adobe’s XMP.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Preserve EPS information from DSC

**Default value**

```
false
```

<a id="22620"></a>
### PreserveFlatness

If `true` , the PostScript flatness set by the `setflat` operator is preserved. If `false` , flatness is discarded. Preserving flatness can increase rendering and printing speeds, since less time is spent determining how to precisely render curves and circles.

**Supported by**

Distiller

**Type**

Boolean

**Default value**

```
true
```

<a id="71313"></a>
### PreserveOPIComments

If `true` , Distiller places the page contents within a set of Open Prepress Interface (OPI) comments in a Form XObject dictionary and preserves the OPI comment information in an OPI dictionary attached to the Form. Page contents data within a set of OPI comments may include proxy images, high-resolution images, or nothing.

If `PreserveOPIComments` is `false` , Distiller ignores OPI comments and their page contents. Setting `PreserveOPIComments` to `false` results in slightly simpler and smaller PDF files. Doing so is acceptable when use of an OPI server is not anticipated.

Distiller ignores `PreserveOPIComments` if `ParseDSCComments` is `false`.

Distiller recognizes both OPI 1.3 and OPI 2.0. See the [specifications for OPI 1.3 and 2.0 (TN #5660)](https://www.pdfa.org/norm-refs/5660_OPI_2_0.pdf).

> **Note**
>
> Creative Suite applications (Illustrator and InDesign) always behave as though this setting were `true`.

**Supported by**

Distiller, InDesign

**Type**

Boolean

**UI name**

Preserve OPI comments

**Default value**

```
false
```

<a id="63211"></a>
### PreserveOverprintSettings

If `true` , Distiller passes the value of the `setoverprint` operator through to the PDF file. If `false` , overprint is ignored (the information is not passed.

For Illustrator, this setting is relevant only when saving to PDF 1.3 (no transparency support) and the document contains overprint. If this setting is `true` , any overprint in the artwork is passed through to the PDF file unchanged. If `false` , any overprint in the artwork is stripped out and the resulting PDF file will not contain any.

> **Note**
>
> InDesign uses the `SimulateOverprint` setting that has additional options.

**Supported by**

Distiller, Illustrator

**Type**

Boolean

**UI name**

Distiller: Preserve overprint settings

Illustrator: Overprints: Preserve (Advanced panel)

**Default value**

```
true
```

### UsePrologue

If `true` , Distiller uses the `prologue.ps` file in the `Data` subdirectory and distills it prior to any PostScript job that is sent through. Distiller also distills the `epilogue.ps` file in the same directory after the same PostScript job is run. You can add any legal PostScript code and comments to these two files.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Use Prologue.ps and Epilogue.ps

**Default value**

```
false
```

<a id="77813"></a>
## Standards settings

This section lists the settings related to PDF/X and PDF/A compliance. See [Using the standards settings](PDF_Create_UsingSettings.md#86848) for more information.

<a id="17664"></a>
### CheckCompliance

Specifies the name of a standard to which the PDF file should comply. The value is an array of names; however, at the present time, only one name may be specified. The following table shows the valid values.

| Value | UI equivalent (Distiller) |
| --- | --- |
| None | None |
| PDF/A-1b:2005 (CMYK) | PDF/A (Acrobat 5.0 Compatible) |
| PDFX1a:2001 | PDF/X-1a (Acrobat 4.0 Compatible) |
| PDFX1a:2003 | PDF/X-1a (Acrobat 5.0 Compatible) |
| PDFX3:2002 | PDF/X-3 (Acrobat 4.0 Compatible) |
| PDFX3:2003 | PDF/X-3 (Acrobat 5.0 Compatible) |

> **Note**
>
> The Creative Suite UI uses the standards names in the first column. Creative Suite applications do not support PDF/A.

In Distiller 7 and the Creative Suite, this setting takes precedence over `PDFX1aCheck` and `PDFX3Check`.  For more information, see [Using the compliance checking settings](PDF_Create_UsingSettings.md#83753).

For Creative Suite applications, `CheckCompliance` also takes precedence over values of other settings (such as `ColorConversionStrategy` or `CompatibilityLevel` ) that could potentially result in a file that is not compliant, and the values of the other settings are adjusted accordingly.

**Supported by**

Distiller, Illustrator, InDesign, Photoshop

**Type**

array

**UI name**

Distiller: Compliance Standard

Creative Suite: Standard

**Default value**

```
[/None]
```

<a id="72679"></a>
### PDFX1aCheck

If `true` , checks compliance with the PDF/X-1a standard (ISO 15930-1:2001) and a PDF/X compliance report is written to the message log.

A value of `/PDFX1aCheck true` is equivalent in Distiller 7 to a value of `/CheckCompliance [ /PDFX1a:2001 ]`.

> **Note**
>
> This setting is retained for compatibility with Distiller 6. For more information on how this setting works, see [Using the standards settings](PDF_Create_UsingSettings.md#86848).

**Supported by**

Distiller, Illustrator, InDesign, Photoshop

**Type**

Boolean

**UI name**

*none*

**Default value**

```
false
```

<a id="18125"></a>
### PDFX3Check

If `true` , checks compliance with the PDF/X-3 standard (ISO 15930-3:2002) and a PDF/X compliance report is written to the message log. A value of `/PDFX3Check true` is equivalent in to a value of `/CheckCompliance [ /PDFX3:2002 ]`.

> **Note**
>
> This setting is retained for compatibility with Distiller 6. For more information on how this setting works, see [Using the standards settings](PDF_Create_UsingSettings.md#86848).

**Supported by**

Distiller, Illustrator, InDesign, Photoshop

**Type**

Boolean

**UI name**

*none*

**Default value**

```
false
```

### PDFXBleedBoxToTrimBoxOffset

If the `BleedBox` entry is not specified in the page object, `BleedBox` is set to `TrimBox` with offsets. Offsets are specified as `[` left right top bottom `]`.  All numbers must be greater than or equal to 0.0. `BleedBox` offsets place the `BleedBox` entirely outside the `TrimBox`.

> **Note**
>
> This setting is ignored if `PDFXSetBleedBoxToMediaBox` is `true`.

**Supported by**

Distiller

**Type**

array

**UI name**

Set BleedBox to TrimBox with offsets (Points)

**Default value**

```
[0.00000 0.00000 0.00000 0.00000]
```

### PDFXCompliantPDFOnly

Determines what to do when PDF/X compliance tests are not passed. The following table shows the valid values.

| Value | UI equivalent | Description |
| --- | --- | --- |
| true | Cancel job | A PDF document is produced only if PDF/X compliance tests are passed. |
| false | Continue | A PDF document is produced regardless of whether PDF/X compliance tests are passed. Distiller does not insert PDF/X additional key/value pairs into the created PDF file. |

> **Note**
>
> InDesign uses its `ErrorControl` setting to determine what to do in this situation.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

When not compliant

**Default value**

```
false
```

<a id="48641"></a>
### PDFXNoTrimBoxError

If `true` and both the `TrimBox` and `ArtBox` entries are not specified in the page object, the condition is reported as an error.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Report as error

**Default value**

```
true
```

<a id="16708"></a>
### PDFXOutputCondition

This setting provides an optional comment which, if present, is added to the PDF file and describes the intended printing condition in a form that should be meaningful to a human operator at the site receiving the PDF document.

**Supported by**

Distiller, Illustrator, InDesign, Photoshop

**Type**

string

**UI name**

Distiller: Output Condition

Creative Suite: Output Condition Name

**Default value**

```
()
```

<a id="23709"></a>
### PDFXOutputConditionIdentifier

This setting is a reference name that is specified by the output intent profile name registry. The entry is automatically entered for known output intent profile names.

For Distiller only, if the value of `PDFXOutputIntentProfile` is `(Use Output Condition Identifier)` , this setting must be provided for PDF/X validation to succeed.

For a description of how this setting is used to fill out entries in the PDF/X output intent dictionary, see [Using the PDF/X output intent settings](PDF_Create_UsingSettings.md#99125).

**Supported by**

Distiller, Illustrator, InDesign, Photoshop

**Type**

string

**UI name**

Output Condition Identifier

**Default value**

```
()
```

<a id="75677"></a>
### PDFXOutputIntentProfile

This setting indicates the characterized printing condition for which the document has been prepared and is required for PDF/X compliance. The value may be one of the following:

- The name of a specific profile. The UI lists a number of available profiles. This is the only value supported by Creative Suite applications.
- `(Use Output Condition Identifier)` The profile is specified by `PDFXOutputConditionIdentifier`.  This value is used by Distiller only.
- `(None)` This value should be used for workflows that require the output intent dictionary to be specified in the PostScript document and that require compliance checking to fail if it is not specified. In the UI, it corresponds to “No Default Profile”. This value is used by Distiller only.

For a description of how these values are used to fill out entries in the PDF/X output intent dictionary, see [Using the PDF/X output intent settings](PDF_Create_UsingSettings.md#99125).

**Supported by**

Distiller, Illustrator, InDesign, Photoshop

**Type**

string

**UI name**

Output Intent Profile Name

**Default value**

```
()
```

<a id="25498"></a>
### PDFXRegistryName

This setting specifies a URL where more information regarding the output intent profile can be obtained. This entry is automatically populated for recognized ICC profile names. If the value of `PDFXOutputIntentProfile` is `(Use Output Condition Identifier)` , this setting must be provided for PDF/X validation to succeed.

**Supported by**

Distiller, Illustrator, InDesign, Photoshop

**Type**

string

**UI name**

Registry Name (URL)

**Default value**

```
()
```

<a id="42971"></a>
### PDFXSetBleedBoxToMediaBox

If `true` and the `BleedBox` entry is not specified in the page object, `BleedBox` is set to `MediaBox`.

**Supported by**

Distiller

**Type**

Boolean

**UI name**

Set BleedBox to MediaBox

**Default value**

```
true
```

### PDFXTrapped

Indicates the state of trapping within the file. Can be one of the following values:

| Value | UI equivalent | Description |
| --- | --- | --- |
| Unknown | Leave Undefined | The trapped state indicated in the PostScript file is used if present; otherwise the state is undefined. |
| False | Insert False | The document is not trapped. |
| True | Insert True | The document is trapped. |

> **Note**
>
> `True` and `False` are name objects, not the Boolean values `true` and `false`.

A value of `True` or `False` is required for PDF/X compliance. If the PostScript file does not specify that the document is trapped, then the value provided here is used. `Unknown` should be used for workflows that require that the document specify a trapped state and for which compliance checking should fail if it is not present in the document.

> **Note**
>
> Illustrator can set this value to `True` or `False` via “Mark as Trapped.” InDesign always specifies `False` for PDF/X compliant files.

**Supported by**

Distiller, Illustrator

**Type**

name

**UI name**

Distiller: Trapped

Illustrator: Marked as Trapped

**Default value**

```
False
```

### PDFXTrimBoxtoMediaBoxOffset

If both the `TrimBox` and `ArtBox` entries are not specified in the page object, `TrimBox` is set to `MediaBox` with offsets. Offsets are specified as \[left right top bottom\]. All numbers must be greater than or equal to 0.0. `TrimBox` offsets place `TrimBox` entirely inside `MediaBox`.

> **Note**
>
> This setting is ignored if `PDFXNoTrimBoxError` is `true`.

**Supported by**

Distiller

**Type**

array

**UI name**

Set TrimBox to MediaBox with offsets *(units* )

**Default value**

```
[0.00000 0.00000 0.00000 0.00000]
```
