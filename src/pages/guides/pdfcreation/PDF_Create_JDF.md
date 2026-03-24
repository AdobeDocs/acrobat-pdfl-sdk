# Conversions Related to JDF

This appendix describes how Distiller converts `setpagedevice` -type PostScript key-word pairs and parameters into a job description file (JDF). Distiller creates a JDF file if the `CreateJDFFile` parameter is set to true. The version of JDF created is 1.1. For more information, see the JDF specification at [http://www.cip4.org/documents/jdf\_specifications](http://www.cip4.org/documents/jdf_specifications) .

This appendix uses XPath expressions to identify specific attributes. *XPath* is a language for addressing parts of an XML document, as defined in XML Path Language (XPath) Version 1.0, which is available from http [://www.w3.org/TR/xpath](http://www.w3.org/TR/xpath). The conventions that appear in the following tables are shown below:

- Expression = JDFRoot’/’Attribute | JDFRoot’/’Children’/’Attribute
- JDFRoot = ‘/JDF’
- Children = Element | Element’/’Children
- Element = element
- Attribute = [‘@’attribute](mailto:'@'attribute)

## Creation of the basic JDF file

Distiller creates a basic JDF document whose root node is a JDF element with Type=”Product”. Under that root node, Distiller creates three sub-elements:

- A JDF element with `Type = "Combined"`
- A ResourcePool element that describes the document produced
- An AuditPool element that describes the results of distillation

The resulting root node is populated with elements that describe the incoming PostScript stream, `Combined` process node, and the following items:

- `setpagedevice` - *type operators* . Whenever Distiller encounters a supported `setpagedevice` -type operator, it represents the key value as an entry in one of the parameter resources associated with the `ResourceDedfinition` process. ([Representation of PostScript keys as JDF entries](PDF_Create_JDF.md#10930))
- *DSC comments* . Whenever Distiller encounters certain DSC comments, it represents those comments in the RunList for the PDF file. ([Mapping of DSC comments into JDF elements and attributes](PDF_Create_JDF.md#35100))
- *Parameters* . Distiller creates a `PSToPDFConversionParams` resource which it populates with attributes that correspond to the settings of the parameters as of the end of the first page of the job. If the parameter `ColorConversionStrategy` is NOT `LeaveColorUnchanged` , Distiller also creates a `ColorSpaceConversionParams` resource, which it populates as it does for `PSToPDFConversionParams`.  ([Mapping of parameters into JDF elements and attributes](PDF_Create_JDF.md#32105))

<a id="10930"></a>
## Representation of PostScript keys as JDF entries

Distiller represents selected `setpagedevice` , `settrapparams` , or `settrapzone` PostScript key-word pairs as JDF entries. It does so by creating and populating corresponding JDF resource elements in a `ResourceDefinition` resource pool, as described in the table [PostScript keys converted into JDF ResourceDefinition resources](PDF_Create_JDF.md#43338).

On occasion, a PostScript key contradicts a Distiller parameter. For information on how this conflict is resolved, see *Using Adobe Normalizer Server, Version 6.0.4* , section 7.2.

PostScript keys converted into JDF ResourceDefinition resources
+———————————–+————————————————————————————————————————————————————————————————————————————————————————————————————————–+
| PostScript key                    | Representation in JDF ResourceDefinition resources                                                                                                                                                                                                                                                                       |
+===================================+==========================================================================================================================================================================================================================================================================================================================+
|                                   | Distiller converts the `setpagedevice` key-word pairs into the `ResourceDefinition` attributes described in the table “Mapping from setpagedevice keys to JDF entries”. Some keys are omitted from the table because they do not have logical equivalents in the *JDF Specification* .                               |
|                                   |                                                                                                                                                                                                                                                                                                                          |
|    setpagedevice                  |                                                                                                                                                                                                                                                                                                                          |
+———————————–+————————————————————————————————————————————————————————————————————————————————————————————————————————–+
|                                   | Distiller converts the `settrapparam` key-word pairs into the ResourceDefinition attributes described in the table “Mapping from settrapparms keys to JDF TrappingDetails entries”.                                                                                                                                    |
|                                   |                                                                                                                                                                                                                                                                                                                          |
|    settrapparms                   |                                                                                                                                                                                                                                                                                                                          |
+———————————–+————————————————————————————————————————————————————————————————————————————————————————————————————————–+
|                                   | Distiller converts the `settrapzone` key-word pairs into the ResourceDefinition attributes described in the table “Mapping from settrapzone keys to JDF TrappingDetails entries”.                                                                                                        |
|                                   |                                                                                                                                                                                                                                                                                                                          |
|    settrapzone                    |                                                                                                                                                                                                                                                                                                                          |
+———————————–+————————————————————————————————————————————————————————————————————————————————————————————————————————–+

Mapping from setpagedevice keys to JDF entries
+———————————–+————————————————————-+
| Key Name                          | Entry in /JDF / ResourcePool                                |
+===================================+=============================================================+
|                                   |                                                             |
|                                   |                                                             |
|    Collate                        |    DigitalPrintingParams /@ Collate                         |
|                                   |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    DeviceRenderingInfo            |    RenderingParams /@ ColorantDepth                         |
|                                   |                                                             |
|    <<ValuesPerColorComponent>>    |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    Duplex                         |    LayoutPreparationParams /@ Sides                         |
|                                   |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    HWResolution                   |    RenderingParams / ObjectResolution /@ Resolution         |
|                                   |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    Jog                            |    Component / Disjointing /@ OffsetAmount                  |
|                                   |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    ManualFeed                     |    DigitalPrintingParams /@ ManualFeed                      |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    MediaColor                     |    DigitalPrintingParams / Media /@ MediaColorName          |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    MediaPosition                  |    DigitalPrintingParams / Media / Location /@ LocationName |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    MediaType                      |    DigitalPrintingParams / Media /@ UserMediaType           |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    MediaWeight                    |    DigitalPrintingParams / Media /@ Weight                  |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    MirrorPrint                    |    ImageSetterParams /@ MirrorAround                        |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    NegativePrint                  |    ImageSetterParams /@ Polarity                            |
+———————————–+————————————————————-+
|                                   | If `Collate` is `TRUE` , `RunList /@ PageCopies`.     |
|                                   |                                                             |
|    NumCopies                      | Otherwise, `RunList /@ DocCopies`                         |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    PageSize                       |    DigitalPrintingParams / Media /@ Dimension               |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    ProcessColorModel              |    ColorantControl /@ ProcessColorModel                     |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    SeparationColorNames           |    ColorantControl /@ ColorantParams                        |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    SeparationOrder                |    ColorantControl /@ ColorantOrder                         |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    Separations                    |    ColorantControl /@ ForceSeparations                      |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    Trapping                       |    TrappingDetails /@ Trapping                              |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    TrappingDetails <<Type>>       |    TrappingDetails /@ TrappingType                          |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    TrappingDetails                |    ColorantControl / ColorPool /@ ColorName                 |
|                                   |                                                             |
|    <<ColorantDetails              |                                                             |
|                                   |                                                             |
|    <<ColorantName>> >>            |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    TrappingDetails                |    ColorantControl / ColorPool / Color /@ ColorType         |
|                                   |                                                             |
|    <<ColorantDetails              |                                                             |
|                                   |                                                             |
|    <<ColorantType>> >>            |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    TrappingDetails                |    ColorantControl / ColorPool / Color /@ NeutralDensity    |
|                                   |                                                             |
|    <<ColorantDetails              |                                                             |
|                                   |                                                             |
|    <<NeutralDensity>> >>          |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    TrappingDetails                |    TrappingDetails /@ TrappingOrder                         |
|                                   |                                                             |
|    <<TrappingOrder>>              |                                                             |
+———————————–+————————————————————-+
|                                   |                                                             |
|                                   |                                                             |
|    Tumble                         |    LayoutPreparation /@ Sides                               |
+———————————–+————————————————————-+

Mapping from settrapparms keys to JDF TrappingDetails entries

| Key Name | Entry in /JDF / ResourcePool / TrappingDetails / TrapRegion / TrappingParams |
| --- | --- |
| BlackColorLimit | @ BlackColorLimit |
| BlackDensityLimit | @ BlackDensityLimit |
| BlackWidth | @ BlackWidth |
| ColorantZoneDetails<br><br><<StepLimit>> | @ ColorantZoneDetails /@ StepLimit |
| ColorantZoneDetails<br><br><<TrapColorScaling>> | @ ColorantZoneDetails /@ TrapColorScaling |
| ColorantZoneDetails<br><br><<TrapPlacement>> | @ ColorantZoneDetails /@ ADBE 1:TrapPlacement |
| Enabled | @ Enabled |
| ImageInternalTrapping | @ ImageInternalTrapping |
| ImageMaskTrapping | @ ImageMaskTrapping |
| ImageResolution | @ ImageResolution |
| ImageToImageTrapping | @ ImageToImageTrapping |
| ImageToObjectTrapping | @ ImageToObjectTrapping |
| ImageTrapPlacement | @ ImageTrapPlacement |
| ImageTrapWidth | @ ADBE:ImageTrapWidth |
| MinimumBlackWidth | @ MinimumBlackWidth |
| SlidingTrapLimit | @ SlidingTrapLimit |
| StepLimit | @ StepLimit |
| TrapColorScaling | @ TrapColorScaling |
| TrapEndStyle | @ TrapEndStyle |
| TrapJoinStyle | @ TrapJoinStyle |
| TrapWidth | @ TrapWidth |

> **Note**
>
> In the JDF document, Distiller defines `ADBE` as the namespace *http://ns.adobe.com/JDF* .

| Key name | Entry in /JDF/ResourcePool/TrappingDetails |
| --- | --- |
| settrapzone | TrapRegion /@ TrappingZone |

<a id="85825"></a>
### Conversion of the linear representation of setpagedevice keys

The `setpagedevice` keys that appear in PostScript streams/files are presented in a linear fashion. That is, hierarchical relationships are represented by repeating higher level information. In contrast, the JDF format represents a hierarchy.

This section describes how Distiller converts between that linear representation and the JDF hierarchy.

For example, the *JDF Specification* allows the `TrapParams` resource element to appear as a child of the `TrappingDetails` resource element and the `TrapZones` resource element, as in the following code.

```
<TrappingDetails>
     <TrapRegion>
         <TrapParams …/>
     </TrapRegion.>
 </TrappingDetails>
```

Distiller always subordinates `TrapParams` resources to `TrapRegion` resources. That is, Distiller never produces entries, such as the first `TrapParams` resource.

Instead, if Distiller has set a default trapping zone, it is set for all the pages (using the second TrapParam). Subsequently any settrapzone/settrapparam settings cause a new TrapZone with associated TrapParams. There can be many of these per page.

`TrapRegions` elements (with associated `TrapParams` elements) are created from each `settrapzone` PostScript call using the `trapparams` set at the time (by `settrapparams` ) and the `Page` key is set. Default `trapzones` (set as part of an unencapsulated PostScript job as per the *PostScript Language Reference* ) are turned in to a `trapregion` that applies to all pages.

More specifically, the trapping settings may be different for two separate regions of a particular page. For example, the title text and logo of a page might have different settings compared to those used for the body text. A particular image could then also have different settings. As a result, a `TrapZone` is drawn around each object (a normal PostScript path) and different `trapparams` set for each object.

<a id="35100"></a>
## Mapping of DSC comments into JDF elements and attributes

The presence of the `%%Page` DSC comment in a PostScript stream indicates the beginning of a page in the stream. The presence of the %%PlateColor DSC comment in conjunction with `%%Page` indicates the beginning of a pre-separated page for a particular colorant.

Distiller may use the `%%Page` and `%%PlateColor` comments to create a partitioned `RunList` that represents the structure of the full-document PDF file it produces for a PostScript stream, depending on the document structure implied by those comments, as described in the following subsections. The `RunList` is in the ResourcePool, which is at the same level as the Combined process node.

### Composite jobs

Composite jobs are indicated by the absence of any `%%PlateColor` comments in the PostScript stream.

Normalizer produces un-partitioned `RunLists` for composite jobs. Changes in page device key values are not considered.

<a id="26538"></a>
### Pre-separated jobs with interleaved separations

Pre-separated jobs with interleaved separations are indicated by the appearance of `%%PlateColor` comments soon after each `%%Page` comment, with each `%%PlateColor` specifying the next colorant in the sequence. That is, the separations that compose a single page appear sequentially, (i.e. cyan separation, magenta separation, yellow separation, and black separation).

When processing pre-separated jobs with interleaved separations, Distiller uses the `%%Page` and `%%PlateColor` DSC comments to create a `RunList` element partitioned on the keys `Run` and `Separation` and to create a `RunIndex` that references the pages in that `RunList`.

Distiller creates an additional `RunIndex` range for the pages that apply to each set of page device key values.

### Pre-separated single-colorant jobs

Pre-separated single-colorant jobs are the same as [Pre-separated jobs with interleaved separations](PDF_Create_JDF.md#26538), except all `%%PlateColor` comments describe a single colorant.

When processing pre-separated single-colorant jobs, Distiller uses the `%%Page` and `%%PlateColor` DSC comments as described for pre-separated jobs with interleaved separations, except the RunList contains a single partition with `Run=1` and `Separation` set to the colorant name provided in `%%PlateColor`.

<a id="32105"></a>
## Mapping of parameters into JDF elements and attributes

This section describes how Distiller converts parameter settings into JDF element and attribute settings. It presents one section for each category of parameter, as follows:

- [General](PDF_Create_JDF.md#13790)
- [Image compression](PDF_Create_JDF.md#32363)
- [Fonts](PDF_Create_JDF.md#57108)
- [Color conversion](PDF_Create_JDF.md#92088)
- [Advanced](PDF_Create_JDF.md#32417)

Distiller produces only those JDF attributes described in this section. Some parameters (such as `CreateJobTicket` ) do not have JDF attribute counterparts. In contrast, some JDF attributes in applicable elements do not correlate with parameters, such as the `RenderingIntent` attribute in the `ColorSpaceConversionParams` element.

Distiller represents parameters as values for the attributes in the following resource elements:

- `PSToPDFConversionParams`
- `FontParams`
- `ImageCompressionParams`
- `ColorSpaceConversionParams`

Distiller does not create the optional `ColorantControl` element.

> **Note**
>
> Version 1.1a of the JDF Specification changed the `ColorantControl` element in a PSToPDFConversion process node from required to optional.

<a id="13790"></a>
### General

The following table specifies the conversion from Distiller general parameters into JDF elements.

Conversion from Distiller general parameters into JDF attributes

| Parameter | Attribute name in the PSToPDFConversionParams resource |
| --- | --- |
| AutoRotatePages | @ AutoRotatePages |
| Binding | @ Binding |
| CompatibilityLevel | @ PDFVersion and ColorSpaceConversionParams /@ Operation<br><br>The table [Conversion from ColorConversionStrategy into Operation](PDF_Create_JDF.md#73690) describes the role of `CompatibilityLevel` in deriving the `Operation` value |
| CompressObjects | @ADBE:CompressObjects |
| CoreDistVersion | Not represented in JDF. `CoreDistVersion` is a read-only parameter that is meaningless in JDF. |
| DoThumbnails | @ DoThumbnails |
| EndPage | @ EndPage |
| ImageMemory | @ ImageMemory |
| Optimize | @ Optimize |
| StartPage | @ StartPage |

<a id="32363"></a>
### Image compression

The Distiller image compression parameters map into the JDF `ImageCompressionParams` element, which may have up to three `ImageCompression` subelements, one for each of the following image types:

- Color
- Grayscale
- Monochrome

Each `ImageCompression` subelement contains an `ImageType` attribute that identifies the type of image it represents.

Conversion from Distiller Image Compression parameters
into JDF ImageCompression subelement

| Parameter | Attribute name in the color, grayscale or monochrome ImageCompression subelement |
| --- | --- |
| `AntiAliasColorImages` , `AntiAliasGrayImages` , or `AntiAliasMonoImages` | @ AntiAliasImages |
| `AutoFilterColorImages` or `AutoFilterGrayImages`<br><br>(Not relevant to monochrome images.) | @ AutoFilterImages |
| AutoFilterColorImages AutoFilterGrayImages /ColorACSImageDict<br><br><</QFactor>> /GrayACSImageDict <</QFactor>><br><br>/ColorImageDict <</QFactor>> /GrayImageDict<br><br><</QFactor>> /MonoImageDict <</QFactor>><br><br>The table [Conversion from Parameters into the JDF DCTQuality attribute](PDF_Create_JDF.md#69009) describes how the auto filter parameter influences selection of a /QFactor value.<br><br>The compression quality dictionaries described above may contain other factors that influence compression; however, they are not represented in JDF attributes. | @ DCTQuality<br><br>Distiller calculates `DCTQuality` by dividing the selected QFactor by 100. For example: |
| `ColorImageDepth` , `GrayImageDepth` , or `/MonoImageDepth` | @ ImageDepth |
| `ColorImageDownsampleThreshold` , `GrayImageDownsampleThreshold` , or `MonoImageDownsampleThreshold` | @ ImageDownsampleThreshold |
| `ColorImageDownsampleType` , `GrayImageDownsampleType` , or `MonoImageDownsampleType` | @ ImageDownsampleType |
| `ColorImageFilter` , `GrayImageFilter` , or `MonoImageFilter` | `ImageFilter` or `ADBE:ImageFilter`<br><br>The latter being used to represent the value `JPXEncode` , `LZWEncode` , or `RunLengthEncode`. |
| `ColorImageResolution` , `GrayImageResolution` , or `MonoImageResolution` | @ ImageResolution |
| JPEG2000ColorACSImageDict <</Quality>><br><br>JPEG2000GrayACSImageDict <</Quality>><br><br>JPEG2000ColorImageDict <</Quality>><br><br>JPEG2000GrayImageDict <</Quality>> | @ADBE2:JPXQuality |
| ConvertImagesToIndexed | @ ConvertImagesToIndexed<br><br>(Represented only in an `ImageCompressionParams` element with `ImageType = "Color"`. ) |
| `DownsampleColorImages` , `DownsampleGrayImages` , or `DownsampleMonoImages` | @ DownsampleImages |
| `EncodeColorImages` , `EncodeGrayImages` , or `EncodeMonoImages` | @ EncodeImages |

> **Note**
>
> ADBE must be defined as the namespace [http://ns.adobe.com/JDF](http://ns.adobe.com/JDF). That is, JDF files that contain elements or attributes that use the ADBE prefix must also contain the definition xmlns:ADBE=”http://ns.adobe.com/JDF”.

Conversion from Parameters into the JDF DCTQuality attribute

| Condition | Distiller compression dictionary key-word pair used to derive the value of *ImageCompression /@ DCTQuality* |
| --- | --- |
| If AutoFilterColorImages is `true` | /ColorACSImageDict <</QFactor>> |
| If AutoFilterColorImages is `false` | /ColorImageDict <</QFactor>> |
| If AutoFilterGrayImages is `true` | /GrayACSImageDict <</QFactor>> |
| If AutoFilterGrayImages is `false` | /GrayImageDict <</QFactor>> |
| If AutoFilterGrayImages value is irrelevant | /MonoImageDict <</QFactor>> |

### Page compression

`CompressPages` is the sole Distiller page compression parameter. Distiller converts it into the `PSToPDFConversionParams CompressPages` attribute.

<a id="57108"></a>
### Fonts

Distiller converts each Distiller font parameter into the attribute in the JDF `FontParams` resource element with the same name. In other words, for each Distiller font parameter, there is an identically-named attribute in the `FontParams` element.

<a id="92088"></a>
### Color conversion

If `ColorConversionStrategy` is `LeaveColorUnchanged` , `ColorSpaceConversionParams` element is omitted from the JDF. Otherwise, conversion is as described in the following table.

Conversion from Distiller color conversion parameters to
JDF ColorSpaceConversionParams attributes

| Parameter | Attribute name in ColorSpaceConversionParams |
| --- | --- |
| CalCMYKProfile<br><br>Used as the ICC profile FileSpec in the `ColorSpaceConversionOp` resource that contains Type = “CMYK”. | `FileSpec` and `@ Type` |
| CalGrayProfile<br><br>Used as the ICC profile FileSpec in the `ColorSpaceConversionOp` resource that contains Type = “Gray”. | `ColorSpaceConversionOp / FileSpec` and `ColorSpaceConversionOp /@ Type` |
| CalRGBProfile<br><br>Used as the ICC profile FileSpec in the `ColorSpaceConversionOp` resource that contains Type = “RGB”. | `ColorSpaceConversionOp / FileSpec` and `ColorSpaceConversionOp /@ Type` |
| ColorConversionStrategy | `ColorSpaceConversionOp /@ Operation` and `ColorSpaceConversionOp  /@ SourceObjects` , as described in the tables [Conversion from ColorConversionStrategy into Operation](PDF_Create_JDF.md#73690) and [Conversion from /ColorConversionStrategy into SourceObjects](PDF_Create_JDF.md#96280). |
| DefaultRenderingIntent | PSToPDFConversionParams /@ DefaultRenderingIntent |
| PreserveHalftoneInfo | @ PreserveHalftoneInfo |
| PreserveOverprintSettings | @ PreserveOverprintSetting |
| sRGBProfile | FileSpec<br><br>If ColorConversionStrategy is sRGB, Distiller creates a FileSpec element with Usage=”FinalTargetDevice” and a UID value that reflects the ICC profile used for converting color spaces to CalRGB (PDF 1.2) or sRGB (PDF 1.3 and above). |
| TransferFunctionInfo | @ TransferFunctionInfo |
| UCRandBGInfo | @ UCRandBG |
| None; however, Distiller specifies the built-in color management system. | @ ColorManagementSystem |

Conversion from ColorConversionStrategy into Operation

| ColorConversionStrategy value | Operation attribute value |
| --- | --- |
| Device independent color [3](#pgfId-1516377) and CompatibilityLevel < = 1.2 | Convert |
| Device independent color and CompatibilityLevel > 1.2 | Tag |
| sRGB | Convert |

> **Note**
>
> ColorConversionStrategy = = UseDeviceIndependentColor || ColorConversionStrategy = = UseDeviceIndependentColorForImages.

Conversion from /ColorConversionStrategy into SourceObjects

| ColorConversionStrategy value | SourceObjects attribute value |
| --- | --- |
| UseDeviceIndependentColor | All |
| sRGB | `All` and `FinalTargetDevice` set to sRGB.<br><br>- If the conversion is sRGB, then we do NOT create a `ColorSpaceConversionOp` of `SourceCS = Gray` because the Gray colors are not changed. |
| UseDeviceIndependentColorForImages | ImagePhotographic<br><br>ImageScreenShot |

<a id="32417"></a>
### Advanced

The following table specifies the conversion from Distiller advanced parameters into JDF elements.

Conversion from Distiller advanced parameters into JDF elements

| Parameter | Attribute name in the PSToPDFConversion resource |
| --- | --- |
| AllowPSXObjects | @ADBE4:AllowPSXObjects |
| AllowTransparency | @ADBE:AllowTransparency |
| ASCII85EncodePages | @ ASCII85EncodePages |
| AutoPositionEPSFiles | AdvancedParams  /@ AutoPostitionEPSInfo |
| CreateJobTicket | Not represented in JDF. |
| DetectBlends | @ DetectBlend<br><br>- This is the correct spelling. |
| EmbedJobOptions | @ADBE:EmbedJobOptions |
| EmitDSCWarnings | AdvancedParams  /@ EmitDSCWarnings |
| LockDistillerParams | AdvancedParams  /@ LockDistillerParams |
| OPM | @ OverPrintMode |
| ParseDSCComments | AdvancedParams /@ ParseDSCComments |
| ParseDSCCommentsForDocInfo | AdvancedParams /@ ParseDSCCommentsForDocInfo |
| PassThroughJPEGImages | @ADBE:PassThroughJPEGImages |
| PreserveCopyPage | AdvancedParams /@ PreserveCopyPage |
| PreserveEPSInfo | AdvancedParams /@ PreserveEPSInfo |
| PreserveOPIComments | AdvancedParams /@ PreserveOPIComments |
| UsePrologue | AdvancedParams /@ UsePrologue |

> **Note**
>
> In the JDF document, Distiller defines `ADBE` as the namespace *http://ns.adobe.com/JDF* .

### PDF/X

The following table specifies the conversion from Distiller PDF/X parameters into JDF elements.

Conversion from Distiller PDF/X parameters into JDF elements

| Parameter | ADBE:PDFXParams attribute name |
| --- | --- |
| PDFX1aCheck | @ADBE : PDFX1aCheck |
| PDFX3Check | @ADBE : PDFX3Check |
| PDFXCompliantPDFOnly | @ADBE : PDFXCompliantPDFOnly |
| PDFXNoTrimBoxError | @ADBE : PDFXNoTrimBoxError |
| PDFXTrimBoxToMediaBoxOffset | PDFXTrimBoxToMediaBoxOffset |
| PDFXSetBleedBoxToMediaBox | PDFXSetBleedBoxToMediaBox |
| PDFXBleedBoxToTrimBoxOffset | PDFXBleedBoxToTrimBoxOffset |
| PDFXOutputIntentProfile | PDFXOutputIntentProfile |
| PDFXOutputCondition | PDFXOutputCondition |
| PDFXRegistryName | PDFXRegistryName |
| PDFXTrapped | PDFXTrapped |

### Conversion of parameters not available through the user interface

All parameters that cannot be set through the user interface are converted into attributes in the ADBE:ThinPDFParams element, as specified in the following table.

Conversion from parameters that cannot be set through the Distiller UI

| Parameter set using the setdistillerparam key | ADBE:ThinPDFParams attribute name |
| --- | --- |
| sidelineEPS | @ ADBE 5:SidelineEPS |
| filePerPage | @ FilePerPage |
| sidelineFonts | @ SidelineFonts |
| sidelineImages | @ SidelineImages |

> **Note**
>
> In the JDF document, Distiller defines `ADBE` as the namespace *http://ns.adobe.com/JDF* .
