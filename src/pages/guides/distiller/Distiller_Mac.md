# Apple Events

Apple events can be used from programming languages such as C or from AppleScript. Because AppleScript is more straightforward, it is recommended for use with Distiller.

Distiller supports the `application` object and the following Apple events:

- `Distill`
- `run`
- `quit`

## Objects

[application](Distiller_Mac.md#90916)

<a id="90916"></a>
### application

The top-level scripting object.

**Elements**

- `Document`
- `Window`

**Properties**

| Property | Class | Description |
| --- | --- | --- |
| postScriptVersion | Unicode text \[r/o\] | PostScript interpreter version; for example, “3016.102”. |
| locale | Unicode text \[r/o\] | Three-character language code for the Distiller user interface (for example, “ENU” is English). |
| frontmost | Boolean \[r/o\] | True if Distiller is the active application. |
| name | Unicode text \[r/o\] | Name of the application. |
| version | Unicode text \[r/o\] | Version of the application. |

## Events

- [Distill](Distiller_Mac.md#75815)
- [quit](Distiller_Mac.md#12807)
- [run](Distiller_Mac.md#39237)

<a id="75815"></a>
### Distill

Distills a file.

**Syntax**

```
Distill
sourcePath UnicodeText [destinationPath UnicodeText]

    [adobePDFSettingsPath UnicodeText]
```

**Parameters**

**Returns**

A Boolean value indicating status. If `true` , the command succeeded.

**Examples**

These examples assume the presence of an appropriate *tell – end* construct, for example:

```
tell application "Acrobat Distiller 8.0"
         [Your code]
 end tell
```

Ensure each command is on one line without line breaks. Some of the following examples appear on two lines solely to fit the page.

```
Distill sourcePath "/hello.ps"
Distill sourcePath "/hello.ps" destinationPath "/Users/username/Desktop"
          adobePDFSettingsPath "Standard"
Distill sourcePath "/hello.ps" adobePDFSettingsPath "/Library/
          Application Support/Adobe PDF/Settings/"
```

The following example uses application properties to determine which settings file is used:

```
set distSetting to "Standard"
 if (postScriptVersion as string) is equal to "3015.102" then
         set distSetting to "High Quality"
 end if
 if locale is "CHT" then
         set distSetting to "Smallest File Size"
 end if
 Distill sourcePath "/hello.ps" adobePDFSettingsPath distSetting
```

<a id="12807"></a>
### quit

Terminates the Distiller program.

**Syntax**

```
quit
```

<a id="39237"></a>
### run

Launches the Distiller program and invokes its standard startup procedures.

**Syntax**

```
run
```
