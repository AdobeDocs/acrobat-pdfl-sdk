---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/distiller/distiller-automationintro.md
type: reference
title: distiller-automationintro
name: distiller-automationintro
description: <a id="acrobat-distiller-api-reference"></a>
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/distiller/distiller-automationintro.md
resource_root: C:/GIT
author: brogers
tags: [dev.adobe.com-rst2md-project, acrobat-pdfl-sdk, src, pages, guides, distiller]
domain: content
tokens: 1744
generated: {by: 'human:brogers', at: '2026-08-27T13:20:57-04:00'}
okf_version: '0.2'
---
<a id="acrobat-distiller-api-reference"></a>
# Acrobat Distiller API Reference

<a id="restriction-on-directory-access"></a>
## Restriction on Directory Access

Distiller restricts the directories that PostScript file operators can access. The default behavior limits directory access to the temp and font cache directories. Earlier versions of Acrobat Distiller allowed PostScript file operators to have unlimited directory access.

The following Acrobat Distiller command line options (Windows) and user preference (Mac) enable unlimited directory access. Such unlimited access can pose security problems.

- Windows: -F command line option
- Mac OS: AllowPSFileOps user preference

For information on using these Acrobat Distiller command line options and preferences with the EMBED pdfMark command, refer to the *PDFmark Reference*.

<a id="43358"></a>
<a id="windows-automation"></a>
## Windows Automation

For most applications, the best way to automate Distiller under Windows is through the automation interface. The automation interface makes it easy to create and control Distiller from any programming language that supports automation. Distiller supports Visual Basic and Visual C++ with or without MFC.

Distiller exposes one interface: `PdfDistiller`.  This interface provides methods, properties, and events.

In Visual Basic, if you want to just create and use a Distiller instance without spooling or events, the code can be as simple as the following:

```
Dim pdf As PdfDistiller
 pdf.FileToPdf "My Test File.ps", "", ""
```

Unless otherwise noted, all examples in this chapter use Visual Basic notation.

<a id="57118"></a>
<a id="methods"></a>
## Methods

- [Create](./distiller-automationintro.md#85293)
- [FileToPDF](./distiller-automationintro.md#58197)
- [FileToPDF2](./distiller-automationintro.md#66622)

<a id="85293"></a>
<a id="create"></a>
### Create

Creates a Distiller instance. You do not need to call this method, because a Distiller instance is always created if one of the other methods needs it. However, you may want to call this method if you are handling events and want to display the Distiller startup messages before you submit any jobs.

Each user of the automation interface has its own Distiller instance. There is no sharing of a common Distiller as is done with the `WM_COPYDATA` interface.

<a id="58197"></a>
<a id="filetopdf"></a>
### FileToPDF

Submits a PostScript file job to Distiller.

This method always creates a log file, regardless of the setting of the Delete Log Files for Successful Jobs preference in Distiller.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| strInputPostScript | The PostScript file to process. |
| strOutputPDF | The name of the PDF file. |
| strPDFOptions | The name and path of the Adobe PDF settings file to use. |

**Returns**

`short int` (`true` on success, `false` otherwise)

If `0` is returned, the parameters are invalid; if `-1` is returned, the PDF creation itself failed. If the user set the `bSpoolJobs` flag before calling this method, then it returns an error only for invalid parameters.

<a id="66622"></a>
<a id="filetopdf2"></a>
### FileToPDF2

Submits a PostScript file job to Distiller. This method is the same as `FileToPDF` except for the addition of an option to apply security.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| strInputPostScript | The PostScript file to process. |
| strOutputPDF | The name of the PDF file. |
| strPDFOptions | The name and path of the Adobe PDF settings file to use. |
| long bApplySecurity | A Boolean value that, if greater than `0`, causes security to be applied to the PDF as currently defined in the Distiller application security dialog box. |

**Returns**

`short int` (`true` on success, `false` otherwise)

If `0` is returned, the parameters are invalid; if `-1` is returned, the PDF creation itself failed. If the user set the `bSpoolJobs` flag before calling this method, then it returns an error only for invalid parameters.

<a id="21067"></a>
<a id="properties"></a>
## Properties

[bShowWindow](./distiller-automationintro.md#53752)

[bSpoolJobs](./distiller-automationintro.md#12100)

<a id="53752"></a>
<a id="bshowwindow"></a>
### bShowWindow

Specifies whether Distiller opens with the status windows. This property takes effect only if you set it before calling the `Create` method or any other method. If you have already started Distiller, `bShowWindow` has no effect.

**Syntax**

```
[get/set] As Long
```

<a id="12100"></a>
<a id="bspooljobs"></a>
### bSpoolJobs

Specifies whether Distiller queues PDF jobs through its internal spooler or processes each job immediately.

By default, `bSpoolJobs` is `false`, and `FileToPDF` processes the PDF job immediately and does not return until the PDF file is created.

If `bSpoolJobs` is `true`, `FileToPDF` submits the PDF job to Distiller’s internal job queue and returns immediately. The job will be processed at some later time. To find out when the job is done, you can watch for the events Distiller runs during job processing.

**Syntax**

```
[get/set] As Long
```

<a id="20892"></a>
<a id="events"></a>
## Events

- [OnJobStart](./distiller-automationintro.md#85285)
- [OnJobDone](./distiller-automationintro.md#24413)
- [OnJobFail](./distiller-automationintro.md#34425)
- [OnLogMessage](./distiller-automationintro.md#98813)
- [OnPercentDone](./distiller-automationintro.md#85527)
- [OnPageNumber](./distiller-automationintro.md#65131)

<a id="85285"></a>
<a id="onjobstart"></a>
### OnJobStart

Run once when a job begins processing.

**Syntax**

```
OnJobStart( ByVal strInputPostScript As String,
   ByVal_ strOutputPDF As String )
```

<a id="24413"></a>
<a id="onjobdone"></a>
### OnJobDone

Run once when a job completes successfully.

**Syntax**

```
OnJobDone( ByVal strInputPostScript As String,
   _ByVal strOutputPDF As String )
```

<a id="34425"></a>
<a id="onjobfail"></a>
### OnJobFail

Run once when a job ends unsuccessfully.

**Syntax**

```
OnJobFail( ByVal strInputPostScript As String,
   _ByVal strOutputPDF As String )
```

<a id="98813"></a>
<a id="onlogmessage"></a>
### OnLogMessage

Run at various times with the text messages that normally appear in Distiller’s message log window.

A single call to `OnLogMessage` may contain multiple lines or partial lines of text. In the current version of Distiller, the text may contain line feed characters without carriage return characters. Your application should not make any assumptions about how this text is formatted and should be prepared to receive either line feed characters (LF) alone or carriage return - line feed (CR-LF) pairs.

**Syntax**

```
OnLogMessage( ByVal strMessage As String )
```

<a id="85527"></a>
<a id="onpercentdone"></a>
### OnPercentDone

Run periodically during a job to indicate overall progress.

**Syntax**

```
OnPercentDone( ByVal nPercentDone As Long )
```

<a id="65131"></a>
<a id="onpagenumber"></a>
### OnPageNumber

Run periodically during a job to indicate the current page number.

**Syntax**

```
OnPageNumber( ByVal nPageNumber As Long )
```
