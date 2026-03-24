# Acrobat Forms Plug-In

The Acrobat Forms plug-in allows a PDF document to act as a form; that is, the Acrobat equivalent of a paper form with fields. This chapter describes the OLE automation methods exported by the Acrobat AcroForm plug-in.

The Forms plug-in for Acrobat (versions 4.0 and above) allows users to author form fields. For Acrobat Reader, the Forms plug-in does not allow form authoring, but allows users to fill in data and print Acrobat forms. The Acrobat Reader Forms plug-in also does not allow users to save data to the local hard disk. Both Acrobat and Acrobat Reader allow Web designers to send data from the form back to a Web server.

> **Note**
>
> Forms as used here do not refer to `XObject` forms as defined in the [PDF Reference](https://www.adobe.com/go/pdfreference).

For more information on forms, see the Acrobat Help and the [PDF Library documentation](https://www.adobe.com/go/pdflibrary).

## Forms plug-in OLE automation

The Acrobat Forms plug-in works as an automation server in the Windows environment. Because the automation capabilities have been added to a plug-in, rather than an executable that can be directly launched, the following steps are necessary to access them from an automation controller. Instantiate the Acrobat application by using the Visual Basic `CreateObject` method. For example:

```
CreateObject("AcroExch.App")
```

This causes the Acrobat Forms plug-in to run, at which time it registers its class object with OLE. Instantiate the main exposed object:

```
CreateObject("AFormAut.App")
```

Registration in the Windows registry (which is different from the class object registration described above) happens every time Acrobat loads the plug-in. Therefore, you must run Acrobat at least once with the AForm32.api file in the Plugins folder before its type library can be found for object browsing within the Microsoft Visual Studio environment. This is also necessary in order to allow early binding. Declare the program variables as objects of the corresponding classes in `AFORMAUTLib`, and not simply as `Object`.

> **Note**
>
> Neither Acrobat nor the Acrobat Forms plug-in are thread-safe, and therefore Acrobat Forms OLE automation uses the single-threading model.

**Exceptions**

All methods and properties may return an exception. These may include standard OLE exceptions, such as:

- `E_OUTOFMEMORY` (0x8007000E)
- `E_INVALIDARG` (0x80070057)

These exceptions are not specifically listed in the descriptions of the methods and properties that appear in this chapter. Others are Acrobat Forms-specific, and are listed in the following table.

The actual numeric value of the returned exception is assembled as an `HRESULT`, uses the `FACILITY_ITF`, and starts with decimal 512 (hex 0x0200), as recommended by Microsoft. For example, the numeric value of the exception `AutErcNoForm` is 0x80040201. The important part is the right-most (0x201), which is the first error in the enumeration below.

| Exception name | Numeric value | Description |
| --- | --- | --- |
| AutErcNoDoc | 1 | No document is currently open in the Acrobat application. |
| AutErcNotTerminal | 2 | This property or method applies to terminal fields or their annotations. |
| AutErcNotToThisFieldType | 3 | This property or method is not applicable to this type of field. |

## AFormApp

`AFormApp` is the only object the controller can externally instantiate (that is, using `CreateObject`). All other objects must be created by navigating down the hierarchy with the methods and properties described in this section.

<a id="50532406_22685"></a>
## Field

A field in the document that is currently active in Acrobat.

### Methods

The `Field` object has the following methods.

- [PopulateListOrComboBox](IAC_API_FormsIntro.md#50532406_56488)
- [SetBackgroundColor](IAC_API_FormsIntro.md#50532406_74735)
- [SetBorderColor](IAC_API_FormsIntro.md#50532406_62611)
- [SetButtonCaption](IAC_API_FormsIntro.md#50532406_36426)
- [SetButtonIcon](IAC_API_FormsIntro.md#50532406_74678)
- [SetExportValues](IAC_API_FormsIntro.md#50532406_27660)
- [SetForegroundColor](IAC_API_FormsIntro.md#50532406_10127)
- [SetJavaScriptAction](IAC_API_FormsIntro.md#50532406_58837)
- [SetResetFormAction](IAC_API_FormsIntro.md#50532406_65423)
- [SetSubmitFormAction](IAC_API_FormsIntro.md#50532406_99295)

<a id="50532406_56488"></a>
### PopulateListOrComboBox

Specifies the item names and optionally exports values for a field of type listbox or combobox.

**Syntax**

```
void PopulateListOrComboBox ( const VARIANT& arrItems,
                 const VARIANT& arrExportVal);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| arrItems | An array of strings, with each element representing an item name.  There is a limit of 64K for string data in a combo or list box control on Windows platforms. For Mac OS systems, the limit is 200 entries for the combo or list box control. Using more than these limits degrades performance and makes the control unusable. |
| arrExportVal | Optional. An array of strings, the same size as the first parameter, with each element representing an export value.  Some of the elements in `exportString` may be empty strings. |

**Exceptions**

Raises [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) if the field is not of type listbox or combobox.

**Related methods**

- [Add](IAC_API_FormsIntro.md#50532406_43345)

<a id="50532406_74735"></a>
### SetBackgroundColor

Specifies the background color for a field. The background color is used to fill the field’s rectangle.

**Syntax**

```
void SetBackgroundColor (LPCTSTR bstrColorSpace, float GorRorC, float GorM, float BorY, float K);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrColorSpace | Values are defined by using a `transparent`, `gray`, `RGB` or `CMYK` color space. Valid strings include:   -  `T` -  `G` -  `RGB` -  `CMYK` |
| GorRorC | Used if `bstrColorSpace` is set to `T`, `G`, or `RGB`. A float range between zero and one inclusive. |
| GorM | Used if `bstrColorSpace` is set to `G`. A float range between zero and one inclusive. |
| BorY | Used if `bstrColorSpace` is set to `RGB`. A float range between zero and one inclusive. |
| K | Used if `bstrColorSpace` is set to `CMYK`. A float range between zero and one inclusive. |

**Related methods**

- [SetBorderColor](IAC_API_FormsIntro.md#50532406_62611)
- [SetForegroundColor](IAC_API_FormsIntro.md#50532406_10127)

**Example**

```
Field.SetBackgroundColor "RGB", 0.7, 0.3, 0.6, 0
```

<a id="50532406_62611"></a>
### SetBorderColor

Specifies the border color for a field. The border color is used to stroke the field’s rectangle with a line as large as the border width. The new border color is propagated to any child annotations underneath, so the field may be non-terminal.

**Syntax**

```
void SetBorderColor (LPCTSTR bstrColorSpace, float GorRorC, float GorM, float  BorY, float K);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrColorSpace | Values are defined by using a `transparent`, `gray`, `RGB` or `CMYK` color space. Valid strings include:   -  `T` -  `G` -  `RGB` -  `CMYK` |
| GorRorC | Used if `bstrColorSpace` is set to `T`, `G`, or `RGB`. A float range between zero and one inclusive. |
| GorM | Used if `bstrColorSpace` is set to `G`. A float range between zero and one inclusive. |
| BorY | Used if `bstrColorSpace` is set to `RGB`. A float range between zero and one inclusive. |
| K | Used if `bstrColorSpace` is set to `CMYK`. A float range between zero and one inclusive. |

**Related methods**

- [SetBackgroundColor](IAC_API_FormsIntro.md#50532406_74735)
- [SetForegroundColor](IAC_API_FormsIntro.md#50532406_10127)

**Example**

```
Field.SetBorderColor "RGB", 0.7, 0.3, 0.6, 0
```

<a id="50532406_36426"></a>
### SetButtonCaption

The caption to be used for the appearance of a field of type `button`.

**Syntax**

```
void SetButtonCaption (LPCTSTR bstrFace, LPCTSTR bstrCaption);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrFace | A string that specifies the face for which the caption will be used. Valid strings include:  `N`: Normal appearance  `D`: Down appearance  `R`: Appearance for rollover |
| bstrCaption | The caption for the button.  If a button’s layout is of type `icon` only, the caption is not used in generating its appearance. In addition, only the `Normal` face is displayed, unless the `Highlight` is of type `push`. |

**Exceptions**

Raises [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) if the field is not of type `button`. The new appearance is propagated to any child annotations underneath; the field may be non-terminal.

**Related methods**

- [SetButtonIcon](IAC_API_FormsIntro.md#50532406_74678)

**Example**

```
Field.SetButtonCaption "D", "Submit Form"
```

<a id="50532406_74678"></a>
### SetButtonIcon

Specifies the icon to be used for the appearance of a field of type `button`.

**Syntax**

```
void SetButtonIcon (LPCTSTR bstrFace, LPCTSTR bstrFullPath, short pageNum);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrFace | A string that specifies the face for which the icon will be used. Valid strings include:  `N`: Normal appearance  `D`: Down appearance  `R`: Appearance for rollover |
| bstrFullPath | The full path of the PDF file to be used as the source of the appearance. |
| pageNum | Used to select the page inside that PDF file (zero-based).  If a button’s layout is of type `icon` only, the caption is not used in generating its appearance. In addition, only the `Normal` face is displayed, unless the `Highlight` is of type `push`. |

**Exceptions**

Raises [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) if the field is not of type `button`. The new appearance is propagated to any child annotations underneath, so it is OK if the field is non-terminal.

**Related methods**

- [SetButtonCaption](IAC_API_FormsIntro.md#50532406_36426)

**Example**

```
Field.SetButtonIcon "N", "c:Clipart.pdf", 0
```

<a id="50532406_27660"></a>
### SetExportValues

Sets the export values for each of the annotations of a field of type radio button and checkbox.

For radio button fields, this is necessary to make the field work properly as a group. One button is checked at any given time, giving its value to the field as a whole.

For checkbox fields, unless an export value is specified, the default is used when the field checked is `Yes`. When it is unchecked, its value is `Off` (this is also true for a radio button field when none of its buttons are checked).

**Syntax**

```
void SetExportValues (const VARIANT& arrExportVal);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| arrExportVal | An array of strings, which is expected to have as many elements as there are annotations in the field. The elements of the array are distributed among the individual annotations comprising the field, using their tab order. |

**Exceptions**

Raises [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) if the field is not of type radio button or checkbox.

**Related methods**

- [Add](IAC_API_FormsIntro.md#50532406_43345)

**Example**

```
Dim arrExp(1) As String
arrExp(0) = "CreditCardA"
arrExp(1) = "CreditCardB"
Field.SetExportValues arrExp
```

<a id="50532406_10127"></a>
### SetForegroundColor

Specifies the foreground color for a field. It represents the text color for text, button, combobox, or listbox fields and the check color for checkbox or radio button fields.

The parameters are similar to `SetBorderColor` and `SetBackgroundColor`, except that the `transparent` color space is not allowed.

**Syntax**

```
void SetForegroundColor (LPCTSTR bstrColorSpace, float GorRorC, float GorM, float BorY, float K);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrColorSpace | Values are defined by using a `transparent`, `gray`, `RGB` or `CMYK` color space. Valid strings include:   -  `T` -  `G` -  `RGB` -  `CMYK` |
| GorRorC | Used if `bstrColorSpace` is set to `T`, `G`, or `RGB`. A float range between zero and one inclusive. |
| GorM | Used if `bstrColorSpace` is set to `G`. A float range between zero and one inclusive. |
| BorY | Used if `bstrColorSpace` is set to `RGB`. A float range between zero and one inclusive. |
| K | Used if `bstrColorSpace` is set to `CMYK`. A float range between zero and one inclusive. |

**Related methods**

- [SetBackgroundColor](IAC_API_FormsIntro.md#50532406_74735)
- [SetBorderColor](IAC_API_FormsIntro.md#50532406_62611)

**Example**

```
Field.SetForegroundColor "CMYK", 0.25, 0.25, 0.25, 0.1
```

<a id="50532406_58837"></a>
### SetJavaScriptAction

Sets the action of the field to be of type `JavaScript`. When using `SetJavaScriptAction` within Visual Basic, you can use Chr(13) to add a <CR>, and Chr(9) for tabs, so that the function is well formatted.

**Syntax**

```
void SetJavaScriptAction (LPCTSTR bstrTrigger, LPCTSTR bstrTheScript);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrTrigger | A string that specifies the trigger for the action. Valid strings include:  -  `up` -  `down` -  `enter` -  `exit` -  `calculate` -  `validate` -  `format` -  `keystroke` |
| bstrTheScript | The script itself.  If the trigger is `calculate`, an entry is added at the end of the calculation order array (see the [CalcOrderIndex](IAC_API_FormsIntro.md#50532406_91573) property). |

**Calculation script**

A simple calculate script is supplied with Acrobat.

```
AFSimple_Calculate(cFunction, cFields)
```

- cFunction is one of `AVG`, `SUM`, `PRD`, `MIN`, `MAX`
- cFields is the list of the fields to use in the calculation.

**Formatting scripts**

The following scripts and formats can be used for the `format` and `keystroke` triggers:

| Parameter | Description |
| --- | --- |
| AFDate\_KeystrokeEx(cFormat)AFDate\_Format(cFormat) | cFormat is one of:  “m/d”, “m/d/yy”, “mm/dd/yy”, “mm/yy”, “d-mmm”, “d-mmm-yy”, “dd-mmm-yy”, “yy-mm-dd”, “mmm-yy”, “mmmm-yy”, “mmm d, yyyy”, “mmmm d, yyyy”, “m/d/yy h:MM tt”, “m/d/yy HH:MM” |
| AFTime\_Keystroke(ptf)AFTime\_Format(ptf) | ptf is the time format:  0 = 24HR\_MM \[ 14:30 \]  1 = 12HR\_MM \[ 2:30 PM \]  2 = 24HR\_MM\_SS \[ 14:30:15 \]  3 = 12HR\_MM\_SS \[ 2:30:15 PM \] |
| AFPercent\_Keystroke(nDec,sepStyle)AFPercent\_Format(nDec,sepStyle) | nDec is the number of places after the decimal point.  sepStyle is an integer denoting whether to use a separator. If sepStyle is `0`, use commas. If sepStyle is `1`, do not separate. |
| AFSpecial\_Keystroke(psf)AFSpecial\_Format(psf) | psf is the type of formatting to use:  0 = zip code  1 = zip + 4  2 = phone  3 = SSN |
| AFNumber\_Format(nDec,sepStyle,negStyle,currStyle,strCurrency,bCurrencyPrepend)AFNumber\_Keystroke(nDec,sepStyle,negStyle,currStyle,strCurrency,bCurrencyPrepend) | nDec is the number of places after the decimal point.  sepStyle is an integer denoting whether to use a separator. If sepStyle is `0`, use commas. If sepStyle is `1`, do not separate.   sepStyle is the formatting used for negative numbers:  0 = MinusBlack  1 = Red  2 = ParensBlack  3 = ParensRed  currStyle is the currency style - not used.  strCurrency is the currency symbol.  bCurrencyPrepend is `true` to prepend the currency symbol; `false` to display on the end of the number. |

<a id="50532406_65423"></a>
### SetResetFormAction

Sets the action of the field to be of type `ResetForm`.

**Syntax**

```
void SetResetFormAction (LPCTSTR bstrTrigger, long theFlags, const VARIANT& arrFields);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrTrigger | A string that specifies which trigger is used for the action. Valid strings include:  `up`: Mouse up  `down`: Mouse down  `enter`: Mouse enter  `exit`: Mouse exit |
| theFlags | When `0` (`Include`), `arrFields` specifies which fields to include in the reset operation. When non-zero (`Exclude`), `arrFields` specifies which fields to exclude from the reset operation. |
| arrFields | Optional. An array of strings for the fully-qualified names of the fields. Depending on the value of `theFlags`, these fields are included in or excluded from the reset operation.   When the fields are included, the set can include the names of non-terminal fields, which is a fast and easy way to cause all their children to be included in the action.  When not supplied, all fields are reset. |

<a id="50532406_99295"></a>
### SetSubmitFormAction

Sets the action of the field to be of type `SubmitForm`.

**Syntax**

```
void SetSubmitFormAction (LPCTSTR bstrTrigger, LPCTSTR bstrTheURL, long theFlags, const VARIANT& arrFields);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrTrigger | A string that specifies which trigger is used for the action. Valid strings include:  `up`: Mouse up  `down`: Mouse down  `enter`: Mouse enter  `exit`: Mouse exit |
| bstrTheURL | A string containing the URL. |
| theFlags | A collection of flags that define various characteristics of the action.  See the [PDF Reference](https://www.adobe.com/go/pdfreference) to learn how the binary value of this `long` is interpreted. |
| arrFields | Optional. If specified, represents an array of strings for the fully-qualified names of the fields to submit when the action is executed. If the array is interpreted as fields to submit (as opposed to fields excluded from the submission, depending on the least-significant bit in the flags), then it may include the names of non-terminal fields, which is a way to cause all their children to be included in the submission.  If not specified, the created action does not include a `/Fields` key. |

### Properties

The `Field` object has the following properties.

- [Alignment](IAC_API_FormsIntro.md#50532406_44698)
- [BorderStyle](IAC_API_FormsIntro.md#50532406_71368)
- [BorderWidth](IAC_API_FormsIntro.md#50532406_34046)
- [ButtonLayout](IAC_API_FormsIntro.md#50532406_12361)
- [CalcOrderIndex](IAC_API_FormsIntro.md#50532406_91573)
- [CharLimit](IAC_API_FormsIntro.md#50532406_77672)
- [DefaultValue](IAC_API_FormsIntro.md#50532406_89449)
- [Editable](IAC_API_FormsIntro.md#50532406_95788)
- [Highlight](IAC_API_FormsIntro.md#50532406_59064)
- [IsHidden](IAC_API_FormsIntro.md#50532406_60029)
- [IsMultiline](IAC_API_FormsIntro.md#50532406_20163)
- [IsPassword](IAC_API_FormsIntro.md#50532406_44535)
- [IsReadOnly](IAC_API_FormsIntro.md#50532406_90143)
- [IsRequired](IAC_API_FormsIntro.md#50532406_37697)
- [IsTerminal](IAC_API_FormsIntro.md#50532406_55754)
- [Name](IAC_API_FormsIntro.md#50532406_47912)
- [NoViewFlag](IAC_API_FormsIntro.md#50532406_80007)
- [PrintFlag](IAC_API_FormsIntro.md#50532406_19778)
- [Style](IAC_API_FormsIntro.md#50532406_68974)
- [TextFont](IAC_API_FormsIntro.md#50532406_55208)
- [TextSize](IAC_API_FormsIntro.md#50532406_32614)
- [Type](IAC_API_FormsIntro.md#50532406_66486)
- [Value](IAC_API_FormsIntro.md#50532406_35523)

<a id="50532406_44698"></a>
### Alignment

The text alignment of a text field. Valid alignments are:

```
left
center
right
```

**Syntax**

```
[get/set] String
```

**Returns**

If the field is terminal and has multiple child annotations, a get returns the alignment for the first child, whichever annotation that happens to be.

On a set, the property is propagated to any child annotations underneath, so the field may be non-terminal.

**Exceptions**

If the field is not of type `text`, an exception [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) is returned.

On a get, if the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned.

**Example**

```
Field.Alignment = left
```

<a id="50532406_71368"></a>
### BorderStyle

The border style for a field. Valid border styles include `solid`, `dashed`, `beveled`, `inset`, and `underline`.

**Syntax**

```
[get/set] String
```

**Returns**

If it is terminal and has multiple child annotations, a get returns the value of the border style for the first child, whichever annotation that happens to be.

On a set, the property is propagated to any child annotations underneath, so the field may be non-terminal.

**Exceptions**

On a get, raises [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) if the field is non-terminal, an exception is returned.

**Example**

```
Field.BorderStyle = "beveled"
```

<a id="50532406_34046"></a>
### BorderWidth

The thickness of the border when stroking the perimeter of a field’s rectangle. If the border color is transparent, this property has no effect except in the case of a beveled border. The value `0` represents no border, and the value `3` represents a thick border.

**Syntax**

```
[get/set] short
```

**Returns**

If it is terminal and has multiple child annotations, a get returns the value of the border width for the first child, whichever annotation that happens to be.

On a set, the property is propagated to any child annotations underneath, so the field may be non-terminal.

**Exceptions**

On a get, if the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned.

**Example**

```
Field.BorderWidth = 1
```

<a id="50532406_12361"></a>
### ButtonLayout

The layout appearance of a button. Valid values include:

- `0`: Text only; the button has a caption but no icon.
- `1`: Icon only; the button has an icon but no caption.
- `2`: Icon over text; the icon should appear on top of the caption.
- `3`: Text over icon; the text should appear on top of the icon.
- `4`: Icon then text; the icon should appear to the left of the caption.
- `5`: Text then icon; the icon should appear to the right of the caption.
- `6`: Text over icon; the text should be overlaid on top of the icon.

If it is terminal and has multiple child annotations, a get returns the layout for the first child, whichever annotation that happens to be.

On a set, the property is propagated to any child annotations underneath, therefore the field can be non-terminal.

**Syntax**

```
[get/set] short
```

**Exceptions**

If the field is not of type `button`, an exception [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) is returned.

On a get, if the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned.

**Example**

```
Field.ButtonLayout = 2
```

<a id="50532406_91573"></a>
### CalcOrderIndex

The zero-based calculation order of fields in the document. If you want the calculation for a field `f2` to be performed after that for field `f1`, you need only set the `CalcOrderIndex` for `f2` to `f1` ‘s `CalcOrderIndex` + 1. The elements in the calculation order array are shifted to make room for the insertion, but the first calculation is still at index 0.

**Syntax**

```
[get/set] short
```

**Example**

```
Set F1 = Fields("SubTotal")
Set F2 = Fields("Total")
F2.CalcOrderIndex = F1.CalcOrderIndex + 1
```

<a id="50532406_77672"></a>
### CharLimit

The limit on the number of characters that a user can type into a text field.

On a set, the property is propagated to any child annotations underneath, if any.

**Syntax**

```
[get/set] short
```

**Exceptions**

If the field is not of type `text`, an exception [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) is returned.

<a id="50532406_89449"></a>
### DefaultValue

The default value of the field. It returns the empty string if the field has no default value. If the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned.

**Syntax**

```
[get/set] String
```

See also  [Value](IAC_API_FormsIntro.md#50532406_35523).

<a id="50532406_95788"></a>
### Editable

Determines whether the user can type in a selection or must choose one of the provided selections. Comboboxes can be editable; that is, the user can type in a selection.

On a set, the property is propagated to any child annotations underneath, if any.

**Syntax**

```
[get/set] Boolean
```

**Exceptions**

Returns  an exception of [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) if the field is not of type combobox.

**Example**

```
Field.Editable = False
```

<a id="50532406_59064"></a>
### Highlight

Defines how a button reacts when a user clicks it. The four highlight modes supported are:

- none
- invert
- push
- outline

If it is terminal and has multiple child annotations, a get returns the highlight for the first child, whichever annotation that happens to be.

On a set, the property is propagated to any child annotations underneath, so the field may be non-terminal.

**Syntax**

```
[get/set] String
```

**Exceptions**

If the field is not of type button, an exception [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) is returned.

On a get, if the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned.

**Example**

```
Field.Highlight = "invert"
```

<a id="50532406_60029"></a>
### IsHidden

Determines whether the field is hidden or visible to the user. If the value is `true` the field is invisible, and `false` indicates that the field is visible.

During get operations, if the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned. If it is terminal, and has multiple child annotations, a get returns the value of the hidden flag for the first child, whichever annotation that happens to be.

During set operations, the property is propagated to any child annotations underneath, therefore a field can be non-terminal.

**Syntax**

```
[get/set] Boolean
```

**Example**

```
'Hide "name.last"
Set Field = Fields("name.last")
Field.IsHidden = True
```

<a id="50532406_20163"></a>
### IsMultiline

Determines whether the text field is multi-line or single-line. On a set, the property is propagated to any child annotations underneath, if any.

**Syntax**

```
[get/set] Boolean
```

**Exceptions**

If the field is not of type `text`, an exception [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) is returned.

**Example**

```
Field.IsMultiline = True
```

<a id="50532406_44535"></a>
### IsPassword

Determines whether the field will display asterisks for the data entered. Upon submission, the actual data entered is sent. Fields that have the password attribute set will not have the data in the field saved when the document is saved to disk.

On a set, the property is propagated to any child annotations underneath, if any.

**Syntax**

```
[get/set] Boolean
```

**Exceptions**

If the field is not of type `text`, an exception [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) is returned.

**Example**

```
Field.IsPassword = True
```

<a id="50532406_90143"></a>
### IsReadOnly

The read-only characteristic of a field. When a field is read-only, the user can see the field but cannot change it. If a button is read-only, the user cannot click it to execute an action.

Because this is a field flag and not an annotation flag, both a get and a set of this property are allowed regardless of whether the field is terminal or non-terminal.

- A get on a non-terminal field retrieves that field’s flag.
- A set changes the flag on all its terminal children.

**Syntax**

```
[get/set] Boolean
```

<a id="50532406_37697"></a>
### IsRequired

The required characteristic of a field. When a field is required, its value must be non-`NULL` when the user clicks a submit button that causes the value of the field to be sent to the web. If the field value is `NULL`, the user receives a warning message and the submit does not occur.

Since this is a field flag and not an annotation flag, both a get and a set of this property are allowed, regardless of whether the field is terminal or non-terminal.

A get on a non-terminal field retrieves that field’s flag. A set changes the flag on all its terminal children.

**Syntax**

```
[get/set] Boolean
```

<a id="50532406_55754"></a>
### IsTerminal

`true` if the field is terminal, otherwise `false`.

**Syntax**

```
[read-only] Boolean
```

**Example**

```
Dim Field As AFORMAUTLib.Field
Dim bTerminal As Boolean

'bTerminal should be True
bTerminal = Field.IsTerminal
```

<a id="50532406_47912"></a>
### Name

The fully qualified name of the field. It is the default member of the `Field` interface.

**Syntax**

```
[read-only] String
```

<a id="50532406_80007"></a>
### NoViewFlag

Determines whether a given field prints but does not display on the screen.

Set the `NoViewFlag` property to `true` to allow the field to appear when the user prints the document but not when it displays on the screen; set it to `false` to allow both printing and displaying.

On a get, if the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned. If it is terminal, and has multiple child annotations, a get returns the value of the no-view flag for the first child, whichever annotation that happens to be.

On a set, the property is propagated to any child annotations underneath, so the field may be non-terminal.

**Syntax**

```
[get/set] Boolean
```

<a id="50532406_19778"></a>
### PrintFlag

Determines whether a field prints. Set the `PrintFlag` property to `true` to allow the field to appear when the user prints the document, set it to `false` to prevent printing.

On a get, if the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned. If it is terminal, and has multiple child annotations, a get returns the value of the print flag for the first child, whichever annotation that happens to be.

On a set, the property is propagated to any child annotations underneath, so the field may be non-terminal.

**Syntax**

```
[get/set] Boolean
```

<a id="50532406_68974"></a>
### Style

The style of a checkbox or a radio button (the glyph used to indicate that the check box or radio button has been selected).

Valid styles include:

```
check
cross
diamond
circle
star
square
```

If it is terminal and has multiple child annotations, a get returns the style for the first child, whichever annotation that happens to be.

On a set, the property is propagated to any child annotations underneath, therefore a field can be non-terminal.

**Syntax**

```
[get/set] String
```

**Exceptions**

During set, if the field is not of type checkbox or radio button, an exception [AutErcNotToThisFieldType](IAC_API_FormsIntro.md#50532406_95289) is returned.

On a get, if the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned.

**Example**

```
Field.Style = "star"
```

<a id="50532406_55208"></a>
### TextFont

The text font used when laying out the field. Valid fonts include:

```
Courier
Courier-Bold
Courier-Oblique
Courier-BoldOblique
Helvetica
Helvetica-Bold
Helvetica-Oblique
Helvetica-BoldOblique
Symbol
Times-Roman
Times-Bold
Times-Italic
Times-BoldItalic
ZapfDingbats
```

On a set, the property is propagated to any child annotations underneath, if any.

**Syntax**

```
[get/set] String
```

**Example**

```
Field.TextFont = "Times-BoldItalic"
```

<a id="50532406_32614"></a>
### TextSize

The text points size used in the field. In combobox and radio button fields, the text size determines the size of the check. Valid text sizes include zero and the range from 4 to 144 inclusive.

A text size of zero means that the largest point size that can still fit in the field’s rectangle should be used. In multi-line text fields and buttons this is always 12 points.

On a set, the property is propagated to any child annotations underneath, if any.

**Syntax**

```
[get/set] short
```

**Example**

```
Field.TextSize = 18
```

<a id="50532406_66486"></a>
### Type

The type of the field as a string. Valid types that are returned:

```
text
button
combobox
listbox
checkbox
radiobutton
signature
```

**Syntax**

```
[read-only] String
```

**Example**

```
Set Field = Fields("name.last")
'Should print "name.last"
print Field
' Should print the type of field. Example,
' "text"
print Field.Type
```

<a id="50532406_35523"></a>
### Value

A string that represents the value of the field.  Returns  the empty string if the field has no value. If the field is non-terminal, an exception [AutErcNotTerminal](IAC_API_FormsIntro.md#50532406_63155) is returned.

For fields of type checkbox, the value `Off` represents the unchecked state. The checked state is represented using the export value. This is also true for radio buttons (where each individual button in a group should have a different export value; see [SetExportValues](IAC_API_FormsIntro.md#50532406_27660)). For fields of type listbox or combobox, if an export value is defined, then that represents the value, otherwise the item name is used.

These remarks apply also to [DefaultValue](IAC_API_FormsIntro.md#50532406_89449).

**Syntax**

```
[get/set] String
```

**Example**

```
Dim arrExp(1) As String
arrExp(0) = "CreditCardV"
arrExp(1) = "CreditCardM"
Field.SetExportValues arrExp
Field.Value = arrExp(0)
```

## Fields

A collection of all the fields in the document that are currently active in Acrobat at the time `Fields` is instantiated.

The `Fields` collection includes both terminal and non-terminal fields. A terminal field is one that either does not have children, or if it does, they are simply multiple appearances (that is, child annotations) of the field in question.

> **Note**
>
> If you instantiate a `Fields` object, and subsequently fields are manually added or removed using the Forms tool in Acrobat, the `Fields` object will no longer be in sync with the document. You must re-instantiate the `Fields` object.

### Methods

The `Fields` object has the following methods.

- [Add](IAC_API_FormsIntro.md#50532406_43345)
- [AddDocJavascript](IAC_API_FormsIntro.md#50532406_52006)
- [ExecuteThisJavascript](IAC_API_FormsIntro.md#50532406_54145)
- [ExportAsFDF](IAC_API_FormsIntro.md#50532406_13920)
- [ExportAsHtml](IAC_API_FormsIntro.md#50532406_68256)
- [ImportAnFDF](IAC_API_FormsIntro.md#50532406_99067)
- [Remove](IAC_API_FormsIntro.md#50532406_97538)

<a id="50532406_43345"></a>
### Add

Dynamically adds a new field to the Acrobat form and to the `Fields` collection.

Returns  the newly-created `Field` object. You can pass the name of an existing field as a parameter, as long as that field is of the same type as the one being created.

This is useful in the following circumstances:

- For radio buttons to use the `SetExportValues` method to make the radio buttons mutually exclusive.
- For fields that should have multiple appearances (that is, child annotations) in the document.

**Syntax**

```
LPDISPATCH Add (LPCTSTR bstrFieldName, LPCTSTR bstrFieldType, short pageNum, float left, float top, float right, float bottom);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrFieldName | The fully-qualified name of the field. |
| bstrFieldType | Field type for the newly created field. Valid types are:  -  `text` -  `button` -  `combobox` -  `listbox` -  `checkbox` -  `radio button` -  `signature`  You must use the quotation marks. See the sample code below.  When creating list or combo boxes, there is a limit of 64K for string data on Windows platforms. Mac OS systems have a limit of 200 entries for the list or combo boxes. Using more than the limit degrades performance. You populate the fields of the list and combo boxes using the [PopulateListOrComboBox](IAC_API_FormsIntro.md#50532406_56488) method. |
| pageNum | The page number (zero-based). |
| left, top, right, bottom | These parameters are floats representing the left, top, right, and bottom coordinates of the field rectangle, measured in rotated page space; that is, \[0,0\] is always at the left bottom corner regardless of page rotation. |

**Returns**

The newly-created `Field` object.

**Related methods**

- [PopulateListOrComboBox](IAC_API_FormsIntro.md#50532406_56488)
- [Remove](IAC_API_FormsIntro.md#50532406_97538)

**Example**

```
Set Field = Fields.Add("payment",_ "radiobutton", 0, 100, 600, 130, 570)
```

<a id="50532406_52006"></a>
### AddDocJavascript

Adds a document-level JavaScript function to the PDF file. When using `AddDocJavascript`, within Visual Basic, you can use `Chr(13)` to add a <CR>, and `Chr(9)` for tabs, so that the function is well formatted.

**Syntax**

```
void AddDocJavascript (LPCTSTR bstrScriptName, LPCTSTR bstrTheScript);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrScriptName | The name of the function to be added to the document. |
| bstrTheScript | The definition to be added to the document. |

**Related methods**

- [ExecuteThisJavascript](IAC_API_FormsIntro.md#50532406_54145)

**Example**

```
'Adding a document-level JavaScript
'function, to compute factorials:
Fields.AddDocJavaScript "Fact", _
"function Fact(n)" & Chr(13) & _
"{" & Chr(13) & _
Chr(9) & "if (n <= 0)" & Chr(13) & _
Chr(9) & Chr(9) & "return 1;" & Chr(13) & _
Chr(9) & "else" & Chr(13) & _
Chr(9) & Chr(9) & "return n * Fact(n - 1);" & Chr(13) & _
"}"
```

<a id="50532406_54145"></a>
### ExecuteThisJavascript

Executes the specified JavaScript script.

**Syntax**

```
CString ExecuteThisJavascript (LPCTSTR bstrTheScript);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrTheScript | A string containing a JavaScript script, which is executed by Acrobat in the context of the currently active document.   See the [Acrobat SDK JavaScript API Reference](http://www.adobe.com/go/acrobatsdk_jsapiref) for information on event level values. |

**Returns**

Returns  a result by assigning it to event value.

**Related methods**

- [AddDocJavascript](IAC_API_FormsIntro.md#50532406_52006)

**Example**

```
Fields.ExecuteThisJavaScript "var f =_ this.getField(""myButton""); f.delay =_ false;"
```

To get the returns in Visual Basic:

```
Dim cSubmitName As String
cSubmitName = Fields.ExecuteThisJavaScript
   "event.value = this.getField(""myField"").submitName;"
```

<a id="50532406_13920"></a>
### ExportAsFDF

Exports the data as FDF from an Acrobat form.

**Syntax**

```
void ExportAsFDF (LPCTSTR bstrFullPath, LPCTSTR bstrSubmitButton, BOOL bEmptyFields, const VARIANT& arrFields);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrFullPath | A full path of the file to which the produced FDF file will be saved. |
| bstrSubmitButton | The name of an existing form field of type `button` (in case you want to include it in the FDF file, as if it had been used to trigger a `SubmitForm` action). You can specify an empty string. |
| bEmptyFields | A Boolean value to indicate whether fields with no value should be included in the produced FDF file. |
| arrFields | Optional. An array of strings representing the fully-qualified names of the fields to include in the FDF file. This array may include the names of non-terminal fields, which is a fast and easy way to cause all their children to be included in the FDF file. |

**Related methods**

- [ImportAnFDF](IAC_API_FormsIntro.md#50532406_99067)
- [ExportAsHtml](IAC_API_FormsIntro.md#50532406_68256)

**Example**

```
Dim arrFields(1) As String
arrFields(0) = "name"
arrFields(1) = "address"
'This will create an FDF that includes
'name.last, name.first, address.street,
'etc., but only if they have a value
'(since we are passing False for the
' "bEmptyFields" parameter.
Fields.ExportAsFDF "C:Tempout.fdf", "", False, arrFields
```

<a id="50532406_68256"></a>
### ExportAsHtml

Exports the data as HTML from an Acrobat form. This method is similar to [ExportAsFDF](IAC_API_FormsIntro.md#50532406_13920). The only difference is that the form data is exported in URL-encoded format.

**Syntax**

```
void ExportAsHtml (LPCTSTR bstrFullPath, LPCTSTR bstrSubmitButton, BOOL bEmptyFields, const VARIANT& arrFields);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrFullPath | A full path of the file to which the produced FDF file will be saved. |
| bstrSubmitButton | The name of an existing form field of type `button` (in case you want to include it in the FDF file, as if it had been used to trigger a `SubmitForm` action). You may pass an empty string. |
| bEmptyFields | A Boolean to indicate whether fields with no value should be included in the produced FDF file. |
| arrFields | Optional. An array of strings representing the fully-qualified names of the fields to include in the FDF file. This array may include the names of non-terminal fields, which is a fast and easy way to cause all their children to be included in the FDF file. |

**Related methods**

- [ExportAsFDF](IAC_API_FormsIntro.md#50532406_13920)

<a id="50532406_99067"></a>
### ImportAnFDF

Imports the FDF file into an Acrobat form.

**Syntax**

```
void ImportAnFDF (LPCTSTR bstrFullPath);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrFullPath | The full path of the file containing the FDF file to be imported. |

**Related methods**

- [ExportAsFDF](IAC_API_FormsIntro.md#50532406_13920)

<a id="50532406_97538"></a>
### Remove

Removes a field from the Acrobat Form and from the `Fields` collection.

**Syntax**

```
void Remove (LPCTSTR bstrFieldName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bstrFieldName | The fully-qualified name of the field to be removed from the Acrobat form. If the field has multiple child annotations, all of them are removed. If multiple fields have the same name, all are removed. |

**Related methods**

- [Add](IAC_API_FormsIntro.md#50532406_43345)

**Example**

```
'Remove fields you no longer used.
Fields.Remove("MyOldField")
```

### Properties

The `Fields` object has the following properties.

- [Count](IAC_API_FormsIntro.md#50532406_52838)
- [Item](IAC_API_FormsIntro.md#50532406_92333)
- [\_NewEnum](IAC_API_FormsIntro.md#50532406_49809)

<a id="50532406_52838"></a>
### Count

The number of items in the collection.

**Syntax**

```
[read-only] long
```

**Example**

```
Dim Field As AFORMAUTLib.Field
Dim nFields As Long

nFields = Fields.Count

For Each Field In Fields
If Field.IsTerminal Then
print Field.Value
End If
Next Field
```

<a id="50532406_92333"></a>
### Item

Takes the fully qualified name of the field (for example, `"name.last"`) as a parameter, and returns the `Field` object for it. It is the default member of the `Fields` interface. That is, `item` is the property invoked if the object name is specified by itself without a property or a method in the controller script.

**Syntax**

```
[read-only] IDispatch*
```

**Example**

```
Dim Field As AFORMAUTLib.Field
Dim nFields As Long

Set Field = Fields.Item("name.last")
'Since Item is the default_ property:
Set Field = Fields("name.last")
```

<a id="50532406_49809"></a>
### \_NewEnum

The `IEnumVariant` enumerator for the collection.

You do not need to call this property directly. Visual Basic calls it in the background whenever the code contains a `For Each Field In Fields` loop. For example:

```
For Each Field in Fields
If Field.IsTerminal
print Field.Value
End If
Next Field
```

**Syntax**

```
[read-only] IUnknown*
```
