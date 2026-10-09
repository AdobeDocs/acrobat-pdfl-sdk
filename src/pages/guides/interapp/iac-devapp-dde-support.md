---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/interapp/iac-devapp-dde-support.md
type: reference
title: iac-devapp-dde-support
name: iac-devapp-dde-support
description: <a id="using-dde"></a>
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/interapp/iac-devapp-dde-support.md
resource_root: C:/GIT
author: brogers
tags: [dev.adobe.com-rst2md-project, acrobat-pdfl-sdk, src, pages, guides, interapp]
domain: content
tokens: 339
generated: {by: 'human:brogers', at: '2026-08-27T13:20:58-04:00'}
okf_version: '0.2'
---
<a id="using-dde"></a>
# Using DDE

AcrobatAlthough DDE is supported, you should use OLE automation instead of DDE whenever possible because DDE is not a COM technology.

For all DDE messages, the service name is `acroview`, the transaction type is `XTYPE_EXECUTE`, and the topic name is `control`. The data is the command to be executed, enclosed within square brackets. The item argument in the `DdeClientTransaction` call is `NULL`.

The following example sets up a DDE message:

```
DDE_SERVERNAME = "acroview";
DDE_TOPICNAME = "control";
DDE_ITEMNAME = "[AppHide()]";
```

The square bracket characters in DDE messages are mandatory. DDE messages are case-sensitive and must be used exactly as described.

To be able to use DDE messages on a document, you must first open the document using the `DocOpen` DDE message. You cannot use DDE messages to close a document that a user opened manually.

You can use `NULL` for pathnames, in which case the DDE message operates on the front document.

If more than one command is sent at once, the commands are executed sequentially, and the results appear to the user as a single action. You can use this feature, for example, to open a document to a certain page and zoom level.

Page numbers are zero-based: the first page in a document is page 0. Quotation marks are needed only if a parameter contains white space.

The document manipulation methods, such as those for deleting pages or scrolling, work only on documents that are already open.
