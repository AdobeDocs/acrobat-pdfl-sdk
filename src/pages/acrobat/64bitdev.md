---
title: Developing for 64-bit Windows
description: 64-bit Windows development guidance for the Acrobat SDK.
contributors: Ben Rogers (Adobe Content Engineering)
source: https://github.com/Adobe-Print/Documentation_PDFL_Acrobat_SDK/blob/master/docbuild/acrobatsdk/64bitdev.rst
---

<a id="developing-for-64-bit-windows"></a>
# Developing for 64-bit Windows

To start developing, download and unzip latest Acrobat SDK zip file.

<a id="system-requirements"></a>
## System requirements

- Platform: Windows 64-bit
- Operating System: Windows 10
- Compiler: Microsoft Visual Studio 2019 Min version – 16.4

<a id="upgrading-32-bit-plugins-to-64-bit"></a>
## Upgrading 32-bit plugins to 64-bit

1. Add 64-bit configuration in existing project and copy the settings from 32-bit configuration.
2. Replace headers files with header files present inside SDKPluginSupport of current Windows 64-bit Acrobat SDK Pre-Release package
3. Fix any build errors.

<a id="creating-a-64-bit-plugin"></a>
## Creating a 64-bit plugin

1. Follow the steps for creating simple plugin in [Developing plugins and Applications](pdfs/acrobatsdk_pluginguide.pdf).
2. Add the 64-bit configuration to plugin project.
3. Fix any build errors.

<a id="plugin-compatibility-unified-app"></a>
## Plugin compatibility: unified app

<a id="plugins-for-acrobat-mode"></a>
### Plugins for Acrobat mode

Check for the product mode and return *false* at the beginning of the handshake function of Reader mode. If the app mode changes to Acrobat, the plugin will be available in the next session after app relaunch.

```
ACCB1 ASBool ACCB2 PIHandshake(Uns32 handshakeVersion, void *handshakeData)
{
   char* product = (char*)ASGetConfiguration(ASAtomFromString("Product"));
  if(strcmp(product,"Reader") == 0)
  return false;

  // Insert existing code of your handshake function.

}
```

> **Tip**
>
> Use the approach above for Acrobat-only plugins. If above approach is not followed, then installing such plugin in application running in reader mode will show below dialog and app will quit.

[invalidplugin.png]

<a id="plugins-for-acrobat-reader-mode"></a>
### Plugins for Acrobat & Reader mode

Sign your plugin with the Arobat SDK’s signing tools. This will allow loading of plugin in Reader mode but restricts Acrobat functionality based on the product check. Disable some or all functionality based on the product check. It would become available as soon as the app mode changes to Acrobat. If you are caching the results of a product check, it’s advisable to refresh the cache in response to a product switch notification.

You can toggle functionality in response to a product mode check as follows:

```
bool IsXXXFunctionalityAllowed()
{
  char* product = (char*)ASGetConfiguration(ASAtomFromString("Product"));
  if(strcmp(product,"Reader") == 0)
  return false;
  return true;
}
//Alternative Implementation
bool IsXXXFunctionalityAllowed()
{
  char* product = (char*)ASGetConfiguration(ASAtomFromString("Product"));
  if((strcmp(product,"Exchange-Pro") == 0) || (strcmp(product,"Exchange-Std") == 0))
  return true;
  return false;
}
```

<a id="product-mode-strings"></a>
## Product mode strings

Possible string values include:

- “Reader”
- “Exchange-Std”
- “Exchange-Pro”.

The last two values are two different configurations of Acrobat, and 3rd party plugin developers need not use them.

<a id="plugin-behavior-app-mode-changes"></a>
## Plugin behavior: app mode changes

A plugin can react to application mode change by registering a callback for `AcroAppModeSwitch` notification.
Mode switch notification:

```
// Callback proc for mode switch notification.
ACCB1 void ACCB2 AcroAppModeSwitchNotification(void* clientData)
{
  AVAlertNote("Acrobat SDK - Mode Switch Notification");
}
// Refer BasicPlugin in SDK Samples.
ACCB1 ASBool ACCB2 PluginInit(void)
{
// Register for mode switch notification.
  AVAppRegisterNotification(AcroAppModeSwitchNSEL, gExtensionID,
  (void*)ASCallbackCreateNotification(AcroAppModeSwitch, AcroAppModeSwitchNotification), NULL);
  return MyPluginSetmenu();
}
```

<a id="plugins-enabling-reader-mode"></a>
## Plugins: enabling Reader mode

To enable Reader mode in the 64-bit unified application, perform the steps below.

<a id="compilation"></a>
### Compilation

Product differentiation (Reader vs Acrobat) at compile time is not currently possible; therefore, do not use  the READER\_PLUGIN macro during compilation.

<a id="signing-process"></a>
### Signing Process

The processs remains the same as with the previous SDK for 64-bit unified app in Reader mode:

1. Create the public/private key pairs via the MakeKey utility.
2. Submit the public key file to Adobe to generate the certificate.
3. Sign the plugin with the private key and certificate using the SignPlugin utility

Note the following:

- There are some enhancements in these utilities (64-bit) which improve security.
- You must generate separate keys and certificates for 64-bit Windows plugins using 64-bit signing utilities (PluginSupportToolsReader-enabling Toolswin64)

<a id="plugins-and-protected-mode"></a>
## Plugins: and Protected Mode

- The Acrobat May 2020 release (20.009.20063) supports Protected Mode for Windows.
- Protected Mode is enabled by default on Windows.
- You should test all plugins with Protected Mode enabled.
- Verify Protected Mode is enabled by checking the registry: `[HKEY_CURRENT_USER\Software\Adobe\(productname)\(version)\Privileged]"bProtectedMode"=(0|1)`
- Refer to “Sandbox Broker Extensibility” and “SampleExtn\_jSample\_PLug-in” for details about making a plugin sandbox-compatible.
- If you experience persistent issue, contact Adobe.

<a id="generic-recommendations"></a>
## Generic recommendations

- Use the `ASSize_t` and `ASIntPtr_t` portable data types instead of `long` and `int` and their unsigned versions.
  - Use `ASSize_t` for container length and in loop iterations.
  - `ASIntPtr_t` is good for storing pointer values.
- Fix warnings related to converting from type1 to type 2 (4244 and C4267) for bug-free code and to avoid possible data loss.
- Use the \_WIN64 macro for any 64-bit specific code.
- Use of property files: The SDK provides a common properties file to manage Visual Studio project properties. With a single  file, it becomes possible to centrally control these properties for all the projects from a single file. Files include:
  - SDK/Config/WinCommonSettings.props contains common properties
  - SDK/Config/Win64Settings.props contains specific properties for 64-bit projects
- Note that a 64-bit plugin will not work with Windows 32-bit Acrobat and vice-versa. The plugin bit must match the application bit.
