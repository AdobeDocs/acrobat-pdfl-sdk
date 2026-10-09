---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/acrobat/releasenotes.md
type: reference
title: Acrobat SDK Release Notes
name: releasenotes
description: Release Notes for the Acrobat SDK.
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/acrobat/releasenotes.md
resource_root: C:/GIT
author: brogers
tags: [format-conversion, dev.adobe.com-rst2md-project, acrobat-pdfl-sdk, src, pages, acrobat]
domain: content
tokens: 2482
generated: {by: 'human:brogers', at: '2026-08-27T14:35:10-04:00'}
okf_version: '0.2'
contributors: Ben Rogers (Adobe Content Engineering)
source: https://github.com/Adobe-Print/Documentation_PDFL_Acrobat_SDK/blob/master/docbuild/acrobatsdk/releasenotes.rst
---
<a id="release-notes-all-versions"></a>
# Release Notes (All Versions)

<a id="downloads"></a>
## Downloads

To access the downloads:

1. Go to [https://developer.adobe.com/console/servicesandapis](https://developer.adobe.com/console/servicesandapis).
2. Download the SDK:
   - **Windows**: SDK (pick your version).
   - **Macintosh**: SDK (pick your version).

> **Note**
>
> Adobe recommends you use the most recent version which provides the latest features, bug fixes, and other updates.

<a id="installers"></a>
### Installers

- Adobe Acrobat Reader: 32 and 64 bit
- Adobe Acrobat Pro: 32 and 64 bit

> **Tip**
>
> The 32-bit Windows and Mac platform uses separate installers for Reader and Acrobat. Windows 64-bit installers combine the two into a single installer.

<a id="system-requirements"></a>
## System requirements

The SDK supports the following:

- Dec., 2023: : No changes for Windows or Macintosh
- May, 2023: No changes for Windows or Macintosh
- Sept., 2021:
  - **Windows**: No changes
  - **Macintosh**: X-CODE 12.3
- March, 2021:
  - **Windows**: Samples have been upgraded to compile using VS2019 for Windows 7, 8, and 10.
  - **Macintosh**: X-CODE 9.2. Target Mac OS Deployment version is 10.11.

<a id="december-2023"></a>
## December, 2023

Macintosh-only changes: API updates:

- `AVPageViewGetAperture`: Previously, this API mapped `AVPageView` device space coordinates into the coordinate space of `CGContext` returned by `AVPageViewAcquireDrawContext`. Since the SDK has migrated to the NSScroll framework, `CGContext` returned by `AVPageViewAcquireDrawContext` now maps to the entire scroll-area instead of the aperture. To mitigate issues, the SDK provides a new API: `AVPageViewGetScrollAreaRect`.
- `AVPageViewGetScrollAreaRect`: This API api returns the entire scroll area rect of `pageview` in the device space coordinates. This can be mapped to `CGContext` returned by `AVPageViewAcquireDrawContext` whose origin is at the bottom left corner of scroll area rect.

<a id="may-2023"></a>
## May, 2023

> **Note**
>
> This May Acrobat SDK package must be used with the January 2023 release Reader version 22.003.20310 or higher.

<a id="changes-for-this-release"></a>
### Changes for this release

Apple Notarization Support: There is a new signing mechanism for third-party plugins for Adobe Reader which is compatible with Apple’s  notarization requirement.

Apple’s Catalina release introduced notarization for all binaries on Mac; therefore, third-party plugins for Adobe Reader should also be signed by Apple. However, Apple’s notarization was breaking Adobe’s signature for third-party plugins and prevented them from loading in Adobe Reader. This release provides a new SignPlugin utility which fixes the issue. If your plugin should be Reader-enabled, use the SignPlugin utility before sending it to Apple for notarization.

<a id="september-2021"></a>
## September, 2021

<a id="id1"></a>
### Changes for this release

<a id="avwindowgetplatformthing-deprecated"></a>
#### AVWindowGetPlatformThing deprecated

Because AVWindowGetPlatformThing(AVWindow win) on Macintosh returns WindowRef and WindowRef references Carbon (likely to be deprecated in near future), the AVWindowGetPlatformThing API is also being deprecated.

Actions

- Developers must migrate to AVWindowGetPlatformThingEx(AVWindow win).
- SDK vendors must replace AVWindowGetPlatformThing(AVWindow win)with a call to the new API AVWindowGetPlatformThingEx(AVWindow win) to get the platform handle to the window object.
- Use of AVWindowGetPlatformThing(AVWindow win) can lead to undefined behavior.

Macintosh (Returns the NSWindow pointer for the window)

```
AVDoc avDoc = AVAppGetActiveDoc();
if (avDoc)
{
AVWindow win = AVDocGetAVWindow();
if(win)
NSWindow* nsWin = reinterpret_cast<NSWindow*>(AVWindowGetPlatformThingEx(win));
}
```

Windows (Returns HWND)

```
AVDoc avDoc = AVAppGetActiveDoc();
if (avDoc)
{
AVWindow win = AVDocGetAVWindow();
if(win)
HWND hwnd = reinterpret_cast<HWND>(AVWindowGetPlatformThingEx(win));
}
```

<a id="apple-silicon-support"></a>
#### Apple Silicon support

Because Apple is releasing new devices with their own chip instead of Intel’s, the SDK now supports native Apple Silicon mode for third party plugins. The Apple silicon chip is based on an ARM architecture which requires app and plugin migration. Although the apps compiled for Intel work on the Apple silicon devices with the help of Rosetta translation, there is a performance degradation.

Going forward, plugins must be universal binaries so that they can work seamlessly with both Intel and Apple silicon mode. The SDK samples also now produce universal binaries and require Xcode12 to build. All macOS plugins should be built using Xcode12 for supporting Apple Silicon. For existing plugins, set the architecture to `$(ARCHS_STANDARD)` as shown:

[applesilicon.png]

In the app running natively on Apple silicon devices, plugins compiled for Intel architecture are not loaded. While the app will continue to load existing Intel-based plugins when running under Rosetta translation, developers should migrate their plugins to the ARM architecture so they can load in the native mode of the app.

> **Note**
>
> Rollout for native support will be staggered, and any user having an Intel architecture based plug-in won’t be migrated right away. However, Adobe recommends that plugin vendors to migrate as soon as possible.

<a id="march-2021"></a>
## March 2021

<a id="id2"></a>
### Changes for this release

All code samples, tools, and other API dependent assets are updated for compatibility with the latest compilers.

<a id="windows"></a>
#### Windows

- General changes for 64-bit Windows:
  - You must upgrade 32-bit plugins to 64-bit for them to work with the 64-bit app.
  - The SDK provides 64-bit public headers to 3rd party plug-in developers so that they can successfully create or upgrade their plugins.
  - Acrobat and Reader use the same, single installer. The unified application determines the mode in which it’s running (Reader/Acrobat) at run time. Plugins must dynamically check the whether the app is in Acrobat or Reader mode in order to determine what functionality should be available.
  - The application can transition from Reader mode to Acrobat mode without a relaunch, so plugins must react to mode notifications accordingly.
  - If any Acrobat-specific HFT is invoked in Reader Mode, it could throw a run-time exception. Plugins need to ensure Acrobat specific HFTs are not invoked while the application is running in Reader mode.
  - Existing plugins with different binaries for Acrobat and Reader must combine into a single binary. Product differentiation (Reader vs Acrobat) at install time is not possible.
- Installation path
  - 64-bit: /Program Files/Adobe/<app name>/Acrobat/plug\_ins
  - 32-bit: /Program Files (x86)/Adobe/<app name>/Acrobat/plug\_ins
  - There is no “Acrobat Reader” specific path for 64-bit; there is for 32-bit.
  - The app name in the path is Acrobat.
- Samples
  - App Wizard: The App wizard has been upgraded and will only work with VS2019.
  - wxPlugin: Upgraded to use wxWidgets 3.1.3. Developers must compile wxwidgets and copy the generated libs to `NonAdobeSupport\wxWidgets\win\lib` and header files to `NonAdobeSupport\wxWidgets\win\include`. File paths may vary with a user’s project configuration.
  - Removed unsupported CommonInterfaceAIR.air from snippetRunner Sample.
  - All existing samples are ported from Microsoft Visual Studio 2013 to Microsoft Visual Studio 2019. Microsoft Visual Studio 2019 is recommended to create and upgrade 64-bit native plugins.
  - Public header and sample plugins are updated.
- Config folder: A new folder  contains the common Visual Studio Settings for import by all VS project solutions: `Adobe\Acrobat  SDK\Version 1\Config`.
- Code changes:

| Module | Impacted API | Change |
|--------|--------------|--------|
| AccessibilitySupport (AcrobatAccess.idl) | `get_accID`. See [PDF Accessibility API Reference](http://www.adobe.com/go/acrobat_access) | 32-bit: `HRESULT get_accID(long *id)`; 64-bit: `HRESULT get_accID(long long *id)` |

- New data type

The following new data scalar type is added to the [data types](https://help.adobe.com/en_US/acrobat/acrobat_dc_sdk/2015/HTMLHelp/index.html#t=Acro12_MasterBook%2FPlugins_Introduction%2FData_types.htm&rhsearch=data%20type&rhsyns=%20):

| Type | Byte size | Description |
|------|-----------|-------------|
| ASIntPtr\_t | 4 ( win-32); 8 (win-64) | `intptr_t`: Signed integer of size equal to a pointer |
| ASSize\_t | 4 ( win-32); 8 (win-64) | size of objects (as in `size_t`) |

<a id="macintosh"></a>
#### Macintosh

- Plugin samples
  - MultiTab: To run the sample, place multitab\_icons.pdf (from the SDK package) in `/users/{username}/documents`
  - wxPlugin: This plugin is delivered as Windows only due to dependency on the wxwidget library in Macintosh. TBD
- AppleScript: `WatermarkJsoAs`: you must place the  package input files present on the desktop. On script execution, users are prompted to specify an output folder in which to save the stamped file.
- Tools
  - verifyUrl.acroplugin: Removed since it uses `HITToolBox` which is deprecated by Mac.
  - Sign Plugin.exe: Upgraded to 64 Bit to support Mac OS Catalina.

<a id="known-issues"></a>
### Known issues

- Mac only: Acrobat crashes while running media in RunMediaPlayers.pdf
- Mac only: Flash player crashes while running media in ScriptEvents.pdf
- “SHA1 algorithm warning message” appears when signing using DocSign SDK sample
- When protected mode is ON:
  - PDF file will  open in a temporary window while using StaticViewVC.exe/StaticViewVB.exe
  - WatermarkJsoVB.exe will not work

Other issues:

- 4301819: PDDomView present in Acrobat SDK sometimes doesn’t work
- 4316221: Snippet Runner and Weblink Demo are not working on 64-Bit Acrobat due to dependency on the CommonInterfaceAIR.air
- 4315936: \[Protected mode\] DMS integration sample is not working
- 4315935: \[Protected mode\] Error coming while running ClienApp.exe for the DDE server sample
- 4324516: Acrobat cannot launch if PDFLib TET Plugin is present. Note: this bug is fixed in the 3/11/2021 update (v2 - Mar 2021).
