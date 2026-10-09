---
title: Acrobat SDK Technologies
description: Choosing an Acrobat SDK development technology.
contributors: Ben Rogers (Adobe Content Engineering)
source: https://github.com/Adobe-Print/Documentation_PDFL_Acrobat_SDK/blob/master/docbuild/acrobatsdk/choose.rst
---

<a id="acrobat-sdk-technologies"></a>
# Acrobat SDK technologies

You can develop software that integrates with Acrobat and Adobe Reader in three ways: JavaScript, Plug-ins, and IAC. Chart your path forward based on your application’s requirements.  While the desired functionality may  only be available using one technology, it’s often the case than one option provides the required features. For example, you can add menu items to Acrobat using either JavaScript or a plugin. Moreover, you can also use more than one technology in a single application or single document; for example, you can use both plugins and JavaScript to implement a particular feature.

> **Note**
>
> The Acrobat  SDK provides a large number of sample applications, plug-ins, and scripts to demonstrate how to use the SDK technologies. If you need help choosing a development path, check out the [SDK Overview](https://www.adobe.com/go/acrobatsdk_overview) as well as the  [Acrobat SDK Samples Guide](https://www.adobe.com/go/acrobatsdk_samplesguide).

<a id="javascript"></a>
## JavaScript

Acrobat exposes much of the functionality of Acrobat and its plug-ins to the document author via JavaScript extensions. You can also access JavaScript objects, properties and methods through Visual Basic or C# to automate the processing of PDF documents. Acrobat defines several objects that allow your code to interact with the  application, a PDF document, or fields within a PDF document. The most commonly used objects control the Acrobat or Adobe Reader application, the JavaScript console, the PDF document, SOAP web services, databases, security, searches, and JavaScript events. JavaScript can be internal or external to a PDF, and its location controls the context in which processing occurs, when the scripts are loaded, how they are accessed, and their reusability.

> **Tip**
>
> For details, see the [Acrobat JavaScript Developer Guide](https://www.adobe.com/go/acrobatsdk_jsdevguide)

<a id="plugins"></a>
## Plugins

Plugins are dynamically-linked extensions to the product. They hook to the user interface in a number of ways and can be called for a variety of events. Write plugins in ANSI C/C++ with the Acrobat public APIs and place it in the Plug\_ins folder or directory so that it’s initialized during application startup. On Windows, plug-ins are DLLs. However, plug-in names must end in.API, not.DLL. On Mac OS, plug-ins are code fragments.

> **Tip**
>
> For details, see [Developing plugins and Applications](https://www.adobe.com/go/acrobatsdk_pluginguide)

<a id="interapplication-communication-iac"></a>
## Interapplication Communication (IAC)

Write a separate application process that uses IAC to control app functionality. Windoes supports DDE and OLE, and Mac supports Apple events/AppleScript. IAC allows programs to control the app in much the same way a user would. You can also use IAC support to render a PDF file into an external application window instead of the product window. The IAC methods and events serve as wrappers for some of the core API calls in the SDK. On Windows, you can develop IAC applications using Visual Basic.NET, Visual C++.NET, or Visual C#.NET. On Mac OS, you develop IAC applications using Xcode. CodeWarrior is not supported.

> **Tip**
>
> For details, see [Interapplication Communication Developer Guide](https://www.adobe.com/go/acrobatsdk_iacguide)
