---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/distiller/distiller-mac.md
type: reference
title: distiller-mac
name: distiller-mac
description: <a id="apple-events"></a>
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/distiller/distiller-mac.md
resource_root: C:/GIT
author: brogers
tags: [dev.adobe.com-rst2md-project, acrobat-pdfl-sdk, src, pages, guides, distiller]
domain: content
tokens: 801
generated: {by: 'human:brogers', at: '2026-08-27T13:20:57-04:00'}
okf_version: '0.2'
---
<a id="apple-events"></a>
# Apple Events

Apple events can be used from programming languages such as C or from AppleScript. Because AppleScript is more straightforward, it is recommended for use with Distiller.

Distiller supports the `application` object and the following Apple events:

- `Distill`
- `run`
- `quit`

<a id="objects"></a>
## Objects

[application](./distiller-mac.md#90916)

<a id="90916"></a>
<a id="application"></a>
### application

The top-level scripting object.

**Elements**

- `Document`
- `Window`

**Properties**

| Property | Class | Description |
|----------|-------|-------------|
| postScriptVersion | Unicode text \[r/o\] | PostScript interpreter version; for example, “3016.102”. |
| locale | Unicode text \[r/o\] | Three-character language code for the Distiller user interface (for example, “ENU” is English). |
| frontmost | Boolean \[r/o\] | True if Distiller is the active application. |
| name | Unicode text \[r/o\] | Name of the application. |
| version | Unicode text \[r/o\] | Version of the application. |

<a id="events"></a>
## Events

- [Distill](./distiller-mac.md#75815)
- [quit](./distiller-mac.md#12807)
- [run](./distiller-mac.md#39237)

<a id="75815"></a>
<a id="distill"></a>
### Distill

Distills a file.

**Syntax**

```
Distill
sourcePath UnicodeText [destinationPath UnicodeText]

    [adobePDFSettingsPath UnicodeText]
```

**Parameters**

| Parameter | Description |
|-----------|-------------|
| sourcePath | POSIX path to the input file (the file to be distilled). |
| destinationPath | POSIX path to the output file. If not specified, the PDF file is generated in the same folder as the input file. |
| adobePDFSettingsPath | Either the POSIX path to the Adobe PDF Settings file, or the name of one of the settings files in Distiller. If not specified, the settings file selected in the application is used. |

**Returns**

A Boolean value indicating status. If `true`, the command succeeded.

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
<a id="quit"></a>
### quit

Terminates the Distiller program.

**Syntax**

```
quit
```

<a id="39237"></a>
<a id="run"></a>
### run

Launches the Distiller program and invokes its standard startup procedures.

**Syntax**

```
run
```
