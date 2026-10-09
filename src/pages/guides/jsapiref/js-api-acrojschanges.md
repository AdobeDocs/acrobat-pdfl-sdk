---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/jsapiref/js-api-acrojschanges.md
type: reference
title: js-api-acrojschanges
name: js-api-acrojschanges
description: <a id="changes-across-versions"></a>
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/src/pages/guides/jsapiref/js-api-acrojschanges.md
resource_root: C:/GIT
author: brogers
tags: [dev.adobe.com-rst2md-project, acrobat-pdfl-sdk, src, pages, guides, jsapiref]
domain: content
tokens: 11642
generated: {by: 'human:brogers', at: '2026-08-27T13:20:58-04:00'}
okf_version: '0.2'
---
<a id="changes-across-versions"></a>
<a id="id1"></a>
# Changes Across Versions

This section summarizes the new features and changes introduced in Acrobat and earlier.

<a id="acrobat-xi-changes"></a>
<a id="id2"></a>
## Acrobat XI changes

For more information on the following changes, see the JavaScript for Acrobat API Reference and Developing Acrobat Applications Using JavaScript.

<a id="changes-to-printparams-object"></a>
<a id="id3"></a>
### Changes to PrintParams object

The `colorOverride` property of the `PrintParams` object is no longer supported.

<a id="acrobat-x-changes"></a>
<a id="id4"></a>
## Acrobat X changes

For more information on the following changes, see the JavaScript for Acrobat API Reference and Developing Acrobat Applications Using JavaScript.

<a id="new-javascript-version"></a>
<a id="id5"></a>
### New JavaScript version

This release supports JavaScript version 1.8.

<a id="impact-of-acrobat-menu-restructuring-on-javascript-apis"></a>
<a id="id6"></a>
### Impact of Acrobat menu restructuring on JavaScript APIs

Starting Acrobat X, the number of top-level menu items has been reduced. The menu items available from Acrobat X onwards are: File, Edit, View, Window, and Help. If any of your previous scripts referred to a top-level menu item that no longer exists, the reference will not work.

Starting Acrobat X, the toolbar commands are available through the Tools pane on the right side of the display. Accordingly, methods and properties to customize the toolbar such as `app.addToolButton`, `hideToolBarButton`, and `removeToolButton`, now apply to the Tools pane area. For example, `app.addToolButton` adds a button to the Plugin Addon Tools panel in the Tools pane.

<a id="new-util-method"></a>
<a id="id7"></a>
### New util method

The new `readFileIntoStream` util method loads an external file into a JavaScript stream, optionally encodes it as base64, and returns the content as a base64 encoded stream.

<a id="changes-to-search-object"></a>
<a id="id8"></a>
### Changes to search object

The following changes have been made to the “search” object properties

- The `thesaurus` and `soundex` properties have been removed
- The `legacySearch` property is now deprecated and always returns false.

<a id="changes-to-searchexecutequery"></a>
<a id="id9"></a>
### Changes to SearchExecuteQuery

The following have been removed from `nWordOptions` parameter of `SearchExecuteQuery` :

- `kWordOptionSoundsLike`
- `kWordOptionThesaurus`

<a id="function-searchislegacysearchavailable-deprecated"></a>
<a id="id10"></a>
### Function SearchIsLegacySearchAvailable deprecated

The function `SearchIsLegacySearchAvailable` has been deprecated and will always return false.

<a id="enhancements-to-pdfoptpdfversion"></a>
<a id="id11"></a>
### Enhancements to PDFOptPDFVersion

The following have been added to `PDFOptPDFVersion` :

- `kPDFOptAcrobat9`
- `kPDFOptAcrobat10`

<a id="enhancements-to-doc-object"></a>
<a id="id12"></a>
### Enhancements to Doc object

In this release, the following enhancements have been made to the `Doc` object:

<a id="enhancements-to-the-getdataobjectcontents-method"></a>
<a id="id13"></a>
#### Enhancements to the getDataObjectContents method

A `NotAllowedError` is thrown and the method fails if it attempts to access the content of an embedded file attachment for which any of the following conditions is true (all file name extension matching is case-insensitive):

- The attachment’s file name extension is “.SWF”. If a legitimate.SWF application or module run as part of Acrobat’s Rich Media Annotation or PDF Portfolio navigator is allowed access to the content bytes of.SWF embedded file attachments, it is possible that the legitimate.SWF will load a malicious.SWF.

> **Note**
>
> If you use the `Data.MIMEType` property to check whether a Data object represents a.SWF file, note that the MIME type for.SWF files is `application/x-shockwave-flash`.

- The attachment’s file name extension is “.GIF”, “.JPG”, “.JPEG”, or “.PNG” and the first three bytes of its content have the header signature of a.SWF file (“FWS” or “CWS”). The reason for this security restriction is that the same `ActionScriptflash.display.Loader class load()` method that can be used to load GIF, JPEG, and PNG images can also be used to load a SWF file. If a malicious SWF file’s extension has been altered to that of one of these image types, the SWF could be loaded.

<a id="enhancements-to-the-saveas-method"></a>
<a id="id14"></a>
#### Enhancements to the SaveAs Method

The following enhancements have been made to the `SaveAs` method of the `Doc` object:

<a id="new-values-of-cconvid"></a>
##### New Values of cConvID

The following new values of cConvID have been added:

| Value | Valid Extension |
|-------|-----------------|
| `com.adobe.acrobat.docx` | `docx` |
| `com.adobe.acrobat.xlsx` | `xlsx` |

<a id="deprecated-values-of-cconvid"></a>
##### Deprecated Values of cConvID

The conversion IDs listed below are deprecated in Acrobat X. They are not registered but (only when used with the JavaScript `doc.saveAs` call) are internally mapped to valid, registered conversion IDs. Support for the deprecated conversion IDs will be fully removed in subsequent Acrobat releases.

| Deprecated cConvID | Equivalent Valid cConvID |
|--------------------|--------------------------|
| `com.adobe.acrobat.html-3-20` | `com.adobe.acrobat.html` |
| `com.adobe.acrobat.htm l- 4-01-css-1-00` | `com.adobe.acrobat.html` |

<a id="new-timestampsign-and-certifyinvisiblesign-doc-methods"></a>
<a id="id15"></a>
#### New timestampSign and certifyInvisibleSign Doc methods

For more information on the new Doc methods `timestampSign and certifyInvisibleSign`, see the next section, Signature support for Emerging PAdES ETSI ESI standard.

<a id="84989"></a>
<a id="signature-support-for-emerging-pades-etsi-esi-standard"></a>
<a id="id16"></a>
### Signature support for Emerging PAdES ETSI ESI standard

The European Telecommunications Standards Institute (ETSI) has published a multi-part standard that defines a series of profiles for PAdES—Advanced Electronic Signatures for Portable Document Format (PDF) documents. For more information, see: [http://www.etsi.org/website/newsandevents/200909\_electronicsignature.aspx](http://www.etsi.org/website/newsandevents/200909_electronicsignature.aspx)

The standard includes a new feature to “timestamp the document”, which adds an invisible timestamp signature to a document. This release provides a corresponding JavaScript `Doc` method to do the same. Additionally, the release provides a `Doc` method to apply an invisible certification (this is already available as a menu item in Acrobat and is now supported in JavaScript as well). Both these methods take the same parameters as `field.signatureSign`, but are at the `Doc` level. These methods can only be executed during a batch, console, or application initialization event.

<a id="adding-an-invisible-timestamp"></a>
<a id="id17"></a>
#### Adding an invisible timestamp

The new `timestampSign` Doc method adds an invisible timestamp to a document.

NOTE: This method is not available in Reader.

<a id="adding-an-invisible-certification"></a>
<a id="id18"></a>
#### Adding an invisible Certification

The new `certifyInvisibleSign` Doc method adds an invisible certification to a document.

For more information on these methods, see the description of the `Doc` object in the JavaScript API reference.

<a id="adbc-support-removed-from-documentation"></a>
<a id="id19"></a>
### ADBC Support Removed from Documentation

ADBC is not supported since the previous release of Acrobat. In this release, the section on ADBC support has been removed from Acrobat SDK documentation.

<a id="acrobat-9-0-changes"></a>
<a id="id20"></a>
## Acrobat 9.0 changes

Important: For the Mac OS, the location of the user JavaScript folder has changed. Developers may locate this folder by executing the command `app.getPath("user",` `"javascript")` in the JavaScript debugger console window. Any user folder JavaScript files need to be moved to the new location.

The `util`. `crackURL` method can now break a URL that uses IPv6 addressing into its components. A new property, `nURLType`, is added to the return value object.

The two field properties `display` and `hidden` no longer require forms rights for them to function in Adobe Reader.

There are two new methods. The app. `loadPolicyFile` method is used to specify a cross-domain policy file and the Doc. `applyRedactions` method applies redaction marks.

Two new printing parameters were introduced with version 8, but were undocumented. The properties `DuplexType` and `NumCopies` of the `PrintParams` object allow users to set the duplex mode and the number of copies to be printed. There is also a change of status of the `printerName`, this property is now available for the Mac OS. The description of the choice of the printer when `printerName` is set to the empty string has changed as well.

The property Doc. `nocache`, introduced in version 7.0, is now undefined and is removed from the documentation. Beginning with version 8.0, within a browser, when a user navigates away from a page containing a PDF, Acrobat and Adobe Reader now exit very quickly and any temporary data is deleted. If the user navigates back to the PDF, any form data is gone.

There is a new `Authors` property to the `info` object. This property should be used with a semi-colon delimited list of multiple authors.

Acrobat 9 introduces JavaScript API in support of PDF portfolios (also called portable collections and PDF packages). These are list in the table below.

|  |  |
|---|---|
| App object | methods: * `newCollection` |
| Doc object | properties: * `collection` |
| Data object | methods: * `getFieldValue` * `setFieldValue` |
| `Collection` object | properties: * `fields` * `initialDoc` * `initialView`  methods: * `addField` * `getField` * `removeField` |
| `collectionField` object | properties: * `name` * `order` * `readOnly` * `sort` * `text` * `type` |

Acrobat 6.0 (and Later) Compatible Media relies on the underlying operating system to locate and launch a multimedia player residing on the user’s system; however, Acrobat 9.0 natively supports Flash video (FLV) and Flash applications (SWF) which can be embedded in, or streamed to, a PDF document. Native support for Flash enables reliable cross-platform playback. No additional media player or specific codec is necessary.

Acrobat 6.0 (and Later) Compatible Media is superseded by the multimedia of Acrobat 9.0, which uses rich media annotations. Developers of PDFs with multimedia assets are, therefore, strongly encouraged to use the rich media annotations of Acrobat 9.

Below is a listing of the JavaScript API that support rich media annotations.

|  |  |
|---|---|
| Doc object | methods: * `getAnnotRichMedia` * `getAnnotsRichMedia` |
| `AnnotRichMedia` object | properties: * `activated` * `context3D` * `name` * `page` * `rect` * `subtype`  methods: * `callAS` |

<a id="acrobat-8-1-changes"></a>
<a id="id21"></a>
## Acrobat 8.1 changes

There are new security restrictions for the `search` object’s `addIndex`, `query`, and `removeIndex` methods, as well as the `spell` object’s `removeWord` method. For more information, see those method descriptions.

<a id="acrobat-8-0-changes"></a>
<a id="id22"></a>
## Acrobat 8.0 changes

The JavaScript interpreter now supports E4X, ECMA-357. “EMCAScript for XML (E4X) Specification”, *http://www.ecma-international/publications/standards/Ecma-357.htm*, documents this specification. An example following `metadata` illustrates E4X usage.

The JavaScript category in the Preferences dialog box (Ctrl + K) has a new security check box, “Enable global object security policy”.

- When checked, the default, each time a global variable is written to, the origin which set it is remembered. Only origins that match can then access the variable. For files, this means only the file that set it, having the same path it had when the variable was set, can access the variable. For documents from URLs, it means only the web host which set it can access the variable.

There is an important exception to the restrictions described above. Global variables can be defined and accessed in a privileged context, in the console, in a batch sequence and in folder JavaScript.

- When not checked, documents from different origins are permitted to access the variable; this is the behavior previous to version 8.0.

See the section on the `global` object for additional details and examples.

There is a new restriction on the use of `app.execMenuItem` to a list of safe menu items. See the security note.

The following properties and methods are introduced in Acrobat 8.0:

|  |  |
|---|---|
| `Certificate` object | properties: * `privateKeyValidityEnd` * `privateKeyValidityStart` * `validityEnd` (First introduced in version 7.0.5, but undocumented.) * `validityStart` (First introduced in version 7.0.5, but undocumented.) |
| CertificateSpecifier Object | properties: * `subjectDN` * `keyUsage` * `urlType` * Expanded description of the `url` property. * Added four new bit flags to the `flags` property: `subjectDN`, `issuerDN`, `keyUsage`, `url`. |
| `colorConvertAction` object | properties: * `action` * `alias` * `colorantName` * `convertIntent` * `convertProfile` * `embed` * `isProcessColor` * `matchAttributesAll` * `matchAttributesAny` * `matchIntent` * `matchSpaceTypeAll` * `matchSpaceTypeAny` * `preserveBlack` * `useBlackPointCompensation` |
| `Doc` object | properties: * `xfa` (First introduced in version 6.0.2, but undocumented.) * `XFAForeground`  methods: * `colorConvertPage` * `embedOutputIntent` * `exportAsFDFStr` * `exportAsXFDFStr` * `getColorConvertAction` |
| `Net` object | properties: * `SOAP`  (`Net.SOAP` has properties and methods aliased with `SOAP.wireDump`, `SOAP.connect`, `SOAP.request`, `SOAP.response`.) * `Discovery`  (`Net.Discovery` has methods aliased with `SOAP.queryServices` and `SOAP.resolveService`.) * `HTTP`  methods: \* `streamDecode` \* `streamDigest` \* `streamEncode` |
| [Net.HTTP](./js-api-acrojs.md#37414)  object | methods: * `request` |
| `PrintParams` | properties: * `booklet` * `constants`. bookletBindings * `constants`. bookletDuplexModes * `constants`.handling.booklet ( See * `pageHandling` for a description.) |
| `RDN` object | properties: Added 22 properties to the RDN object:  `businessCategory`, `countryOfCitizenship`, `countryOfResidence`, `dateOfBirth`, `dc`, `dnQualifier`, `gender`, `generationQualifier`, `givenName`, `initials`, `l`, `name`, `nameAtBirth`, `placeOfBirth`, `postalAddress`, `postalCode`, `pseudonym`, `serialNumber`, `sn`, `st`, `street`, `title` |
| `SecurityHandler` object | properties: The following three properties were previously undocumented. * `docDecrypt` * `docEncrypt` * `validateFDF` |
| SeedValue Object | - Added three new flags: `legalAttestations`, `shouldAddRevInfo`, `digestMethod`. * Change of behavior of the `reasons` property. * Added the `digestMethod` property. * Change in wording of the description of the `version` property. * Added the `shouldAddRevInfo` property. |
| `SignatureInfo`  object | properties:  digestMethod |

The following properties and methods are modified in Acrobat 8.0:

|  |  |
|---|---|
| `app` object | methods: * `openDoc` (`cDest` parameter added) |
| `Doc` object | methods: * `addAnnot` (New default values for the `author` property.) * `addRecipientListCryptFilter` (Added note for Acrobat 7.0.) * `getLegalWarnings` (No longer dirties document. Return value changed.) * `importTextData` (Can be only executed during a console or batch event.) |
| FDF object | methods: * `addEmbeddedFile` (Updated description of the `nSaveOption` parameter for version 8.) |
| `Field` object | methods: * `buttonImportIcon` (Can be executed only during a console or batch event) |
| `FullScreen`  object | properties: * `escapeExits` (Can be set to `false` only during console and batch events) |
| LoginParameters Object | Modified wording of the `cURI` and `cUserId` properties. |
| `submitForm` method | The `cPassword` parameter can no longer be used. As of Acrobat 8.0, you cannot create password-encrypted FDF files. If this parameter is used, a form trying to submit a password-encrypted FDF will throw an `ESErrorInvalidArgs` exception and the form submission will not occur. |

<a id="acrobat-7-0-5-changes"></a>
<a id="id23"></a>
## Acrobat 7.0.5 changes

Columns 5 and 6 of the quick bars have been removed.

The following properties and methods were introduced in Acrobat 7.0.5:

|  |  |
|---|---|
| `Collab` object | methods: * `documentToStream` |
| `Data` object | properties: * `description` |
| `Doc` object | properties: * `hostContainer` * `isModal` * `viewState`  methods: * `addRequirement` * `removeRequirement` |
| Embedded PDF object | properties: * `messageHandler`  method:  `postMessage` |
| `HostContainer` object | properties: * `messageHandler`  methods: * `postMessage` |
| `util` object | methods: * `crackURL` |

The following properties and methods were modified in Acrobat 7.0.5:

|  |  |
|---|---|
| `SOAP` object | methods: * `request` (`cRequestStyle` and `cContent` parameters added) * `response` (`cRequestStyle` and `cContent` parameters added) |

<a id="acrobat-7-0-changes"></a>
<a id="id24"></a>
## Acrobat 7.0 changes

The *Acrobat Multimedia JavaScript Reference*, which appeared as a separate document in version 6.0.2, was merged into the *Acrobat JavaScript Scripting Reference*, now named *JavaScript for Acrobat API Reference*. See the section [Introduced in Acrobat 6.0.2](./js-api-acrojschanges.md#30696) for a listing of all multimedia JavaScript objects, properties and methods.

Execution of JavaScript through a menu event is no longer privileged. There is now support for executing privileged code in a non-privileged context.

In versions of Acrobat earlier than 7.0, the JavaScript files `AForm.js`, `ADBC.js`, `Annots.js`, `AnWizard.js`, `media.js`, and `SOAP.js` resided in the App JavaScript folder. Beginning with Acrobat 7.0, these files are not shipped with Acrobat Pro, Acrobat Standard or Adobe Reader. In their place, a precompiled bytecode is used to improve performance. The `debugger.js` file in the App folder is not included in the bytecode.

Files in the User JavaScript folder are not included in the precompiled bytecode file.

It is recommended that users put their own `.js` files in the user JavaScript folder, the same place where `glob.js` resides. JavaScript code that sets up menu items ([addMenuItem](./js-api-acrojs.md#52015)) should be put in `config.js` in the User JavaScript folder. The location of this folder can be found programmatically by executing `app.getPath("user","javascript")` from the console.

Adobe Reader now has a console window. Under Edit > Preferences > JavaScript select Show Console on Errors and Messages. In addition to errors and exceptions, the console can also be opened programmatically with `console.show()`. See the `console` object for a few other details.

The debugging capability of the JavaScript Debugging window can be made available for Adobe Reader for the Windows and Mac OS platforms. To debug within Adobe Reader, the JavaScript file `debugger.js` must be installed, and the Windows registry must be edited appropriately.

<a id="38168"></a>
<a id="introduced-in-acrobat-7-0"></a>
<a id="id25"></a>
### Introduced in Acrobat 7.0

The following properties and methods were introduced in Acrobat 7.0.

|  |  |
|---|---|
| `Alerter` object | methods: * `dispatch` |
| `Annotation` object | properties: * `callout` * `caretSymbol` * Present in version 6.0, documented in version 7.0.  `creationDate` * Present in version 6.0, documented in version 7.0.  `dash` * Present in version 5.0, documented in version 7.0.  `delay` * Present in version 5.0, documented in version 7.0.  `doCaption` * `intent` * `leaderExtend` * `leaderLength` * `lineEnding` * `opacity` * Present in version 5.0, documented in version 7.0.  `refType` * `richDefaults` * Present in version 6.0, documented in version 7.0.  `seqNum` * Present in version 5.0, documented in version 7.0.  `state` * Present in version 6.0, documented in version 7.0.  `stateModel` * Present in version 6.0, documented in version 7.0.  `style` * Present in version 6.0, documented in version 7.0. `subject` |
| `Annot3D` object | properties: * `activated` * `context3D` * `innerRect` * `name` * `page` * `rect` |
| `app` object | properties: * `constants`  methods: * `beginPriv` * `browseForDoc` * `endPriv` * `execDialog` * `launchURL` * `trustedFunction` * `trustPropagatorFunction` |
| `Dialog` object | methods: * `enable` * `end` * `load` * `store` |
| `Doc` object | properties: * `docID` Present in version 6.0, documented in version 7.0. * `dynamicXFAForm` * `external` * `hidden` * `mouseX` * `mouseY` * `noautocomplete` * `nocache (removed in version 9)`  `requiresFullSave`  methods: * `addWatermarkFromFile` * `addWatermarkFromText` * `embedDocAsDataObject` * `encryptUsingPolicy` * `getAnnot3D` * `getAnnots3D` * `getDataObjectContents` * `getOCGOrder` * `openDataObject` * `removeScript` * `setDataObjectContents` * `setOCGOrder` |
| [Doc.media](./doc.md#id178) object | methods: * `getOpenPlayers` |
| `Field` object | methods: * `signatureGetModifications` |
| `OCG` object | properties: * `constants` * `initState` * `locked`  methods: * `getIntent` * `setIntent` |
| `PlayerInfo` object | methods: * `honors` |
| `PrintParams` object | properties: * `nUpAutoRotate` * `nUpNumPagesH` * `nUpNumPagesV` * `nUpPageBorder` * `nUpPageOrder` |
| `search` object | properties: * `attachments` * `ignoreAccents` * `objectMetadata` * `proximityRange` |
| `security` object | security constants  methods: * `chooseSecurityPolicy` * `getSecurityPolicies` |
| `SecurityPolicy` object | SecurityPolicy properties |
| `SOAP` object | methods: * `queryServices` * `resolveService` * `streamDigest` |
| `util` object | methods: * `iconStreamFromIcon` * `streamFromString` * `stringFromStream` |
| `XMLData` object | methods: * `applyXPath` * `parse` |

<a id="modified-in-acrobat-7-0"></a>
<a id="id26"></a>
### Modified in Acrobat 7.0

The following properties and methods were changed or enhanced:

|  |  |
|---|---|
| `app` object | methods: * `addToolButton` * `execMenuItem` * `getPath` * `mailGetAddrs` * `openDoc` |
| `console` object | The console window is now available in Adobe Reader. |
| `Doc` object | methods: * `createTemplate` * `mailDoc` * `print` * `saveAs` * `submitForm` |
| `Field` object | methods: * `signatureSetSeedValue` |
| `Index` object | methods: * `build` |
| `OCG` object | properties: * `name` |
| `PrintParams` object | properties: * `pageHandling` |
| `search` object | properties: * `indexes` |
| `security` object | properties: * `handlers`  methods: * `getHandler` |
| `SecurityHandler` object | properties: * `digitalIDs`  methods: * `login` * `newUser` |
| `SOAP` object | methods: * `connect` * `request` |
| `spell` object | The `Spell` object is not available in Adobe Reader 7.0 or later.  methods: * `addWord` |
| `util` object | methods: * `printd` |

<a id="acrobat-6-0-changes"></a>
<a id="id27"></a>
## Acrobat 6.0 changes

The notion of a safe path was introduced for this version of Acrobat.

<a id="introduced-in-acrobat-6-0"></a>
<a id="id28"></a>
### Introduced in Acrobat 6.0

The following properties and methods were introduced in Acrobat 6:

|  |  |
|---|---|
| ADBC object | SQL types |
| `AlternatePresentation` object | properties: * `active` * `type`  methods: * `start` * `stop` |
| `Annotation` object | properties: * `borderEffectIntensity` * `borderEffectStyle` * `inReplyTo` * `richContents` * `toggleNoView`  methods: * `getStateInModel` * `transitionToState` |
| `app` object | properties: * `fromPDFConverters` * `printColorProfiles` * `printerNames` * `runtimeHighlight` * `runtimeHighlightColor` * `thermometer` * `viewerType`  methods: * `addToolButton` * `getPath` * `mailGetAddrs` * `newFDF` * `openFDF` * `popUpMenuEx` * `removeToolButton` |
| `Bookmark` object | methods: * `setAction` |
| `catalog` object | properties: * `isIdle` * `jobs`  methods: * `getIndex` * `remove` |
| `Certificate` object | properties: * `keyUsage` * `usage` |
| `Collab` object | methods: * `addStateModel` * `removeStateModel` |
| `console` object | methods: * `close` |
| `dbg` object | properties: * `bps`  methods: * `c` * `cb` * `q` * `sb` * `si` * `sn` * `so` * `sv` |
| `Directory` object | properties: * `info`  methods: * `connect` |
| `DirConnection` object | properties: * `canList` * `canDoCustomSearch` * `canDoCustomUISearch` * `canDoStandardSearch` * `groups` * `name` * `uiName`  methods: * `search` * `setOutputFields` |
| `Doc` object | properties: * `alternatePresentations` * `documentFileName` * `metadata` * `permStatusReady`  methods: * `addLink` * `addRecipientListCryptFilter` * `addRequirement` * `encryptForRecipients` * `exportAsText` * `exportXFAData` * `getLegalWarnings` * `getLinks` * `getOCGs` * `getPrintParams` * `importXFAData` * `newPage` * `removeLinks` * `setAction` * `setPageAction` * `setPageTabOrder` |
| `Error` object | properties: * `fileName` * `lineNumber` * `message` * `name`  methods: * `toString` |
| `event` object | properties: * `fieldFull` * `richChange` * `richChangeEx` * `richValue` |
| `FDF` object | properties: * `deleteOption` * `isSigned` * `numEmbeddedFiles`  methods: * `addContact` * `addEmbeddedFile` * `addRequest` * `close` * `mail` * `save` * `signatureClear` * `signatureSign` * `signatureValidate` |
| `Field` object | properties: * `buttonFitBounds` * `comb` * `commitOnSelChange` * `defaultStyle` * `radiosInUnison` * `richText` * `richValue` * `rotation`  methods: * `getLock` * `setLock` * `signatureGetSeedValue` * `signatureSetSeedValue` |
| `Index` object | methods: * `build` |
| `Link` object | properties: * `borderColor` * `borderWidth` * `highlightMode` * `rect`  methods: * `setAction` |
| `OCG` object | properties: * `name` * `state`  methods: * `setAction` |
| `PrintParams` object | properties: * `binaryOK` * `bitmapDPI` * `colorOverride` * `colorProfile` * `constants` * `downloadFarEastFonts` * `fileName` * `firstPage` * `flags` * `fontPolicy` * `gradientDPI` * `interactive` * `lastPage` * `pageHandling` * `pageSubset` * `printAsImage` * `printContent` * `printerName` * `psLevel` * `rasterFlags` * `reversePages` * `tileLabel` * `tileMark` * `tileOverlap` * `tileScale` * `transparencyLevel` * `usePrinterCRD` * `useT1Conversion` |
| `Report` object | properties: * `style` |
| `search` object | properties: * `docInfo` * `docText` * `docXMP` * `bookmarks` * `ignoreAsianCharacterWidth` * `jpegExif` * `legacySearch` * `markup` * `matchWholeWord` * `wordMatching` |
| `security` object | methods: * `chooseRecipientsDialog` * `getSecurityPolicies` * `importFromFile` |
| `SecurityHandler` object | properties: * `digitalIDs` * `directories` * `directoryHandlers` * `signAuthor` * `signFDF`  methods: * `newDirectory` |
| `SOAP` object | properties: * `wireDump`  methods: * `connect` * `request` * `response` * `streamDecode` * `streamEncode` * `streamFromString` * `stringFromStream` |
| `Span` object | properties: * `alignment` * `fontFamily` * `fontStretch` * `fontStyle` * `fontWeight` * `text` * `textColor` * `textSize` * `strikethrough` * `subscript` * `superscript` * `underline` |
| `spell` object | properties: * `languages` * `languageOrder`  methods: * `customDictionaryClose` * `customDictionaryCreate` * `customDictionaryExport` * `customDictionaryOpen` * `ignoreAll` |
| `Thermometer` object | properties: * `cancelled` * `duration` * `value` * `text`  methods: * `begin` * `end` |
| `util` object | methods: * `printd` * `spansToXML` * `xmlToSpans` |

<a id="modified-in-acrobat-6-0"></a>
<a id="id29"></a>
### Modified in Acrobat 6.0

The following properties and methods were changed or enhanced:

|  |  |
|---|---|
| `app` object | methods: * `addMenuItem` * `alert` * `listMenuItems` * `listToolbarButtons` * `response` |
| `Doc` object | properties: * `layout` * `zoomType`  methods: * `createDataObject` * `exportAsFDF` * `exportAsXFDF` * `exportDataObject` * `flattenPages` * `getField` (see Extended Methods)  `getURL` * `importDataObject` * `importIcon` * `print` * `saveAs` * `spawnPageFromTemplate` * `submitForm` |
| `event` object | properties: * `changeEx` |
| `Field` object | properties: * `name`  methods: * `buttonImportIcon` * `signatureInfo` * `signatureSign` * `signatureValidate` |
| `global` object | Persistent global data only applies to variables of type Boolean, Number or String. Acrobat 6.0 has reduced the maximum size of global persistent variables from 32 KB to 2-4 KB. Any data added to the string after this limit is dropped. |
| `search` object | methods: * `query` |
| `SecurityHandler` object | The following were introduced in Acrobat 5.0 as properties and methods of the PPKLite Signature Handler Object. In Acrobat 6.0, they are properties and methods of the `SecurityHandler` object. All of these have new descriptions, and some have additional parameters.  -  When signing using JavaScript methods, the user’s digital signature profile must be a `.pfx` file, not an `.apf`, as in earlier versions of Acrobat. To convert an `.apf` profile to the new `.pfx` type, use the UI (click Advanced > Manage Digital IDs > My Digital ID Files > Select My Digital ID File) to import the `.apf` profile.   properties: * `appearances` * `isLoggedIn` * `loginName` * `loginPath` * `name` * `signInvisible` * `signVisible` * `uiName`  methods: * `login` * `logout` * `newUser` * `setPasswordTimeout` |
| `Template` t object | methods:   `spawn` |

<a id="63660"></a>
**Extended Methods**

The Document `.getField` method was extended in Acrobat 6.0 so that it retrieves the Field object of individual widgets. See the `Field` object for a discussion of widgets and how to work with them.

<a id="deprecated-in-acrobat-6-0"></a>
<a id="id30"></a>
### Deprecated in Acrobat 6.0

|  |  |
|---|---|
| `search` object | properties:  soundex  thesaurus |
| `spell` object | methods: * `addDictionary` * `removeDictionary` |

<a id="30696"></a>
<a id="introduced-in-acrobat-6-0-2"></a>
<a id="id31"></a>
### Introduced in Acrobat 6.0.2

The following table lists the objects, properties and methods of the Multimedia plug-in. In Acrobat 6.0.2, multimedia JavaScript was documented in a separate document called the “Acrobat Multimedia JavaScript Reference”.

|  |  |
|---|---|
| `app` object | properties: * `media` * `monitors` |
| [app.media](./js-api-acrojs.md#19976) object | properties: * `align` * `canResize` * `closeReason` * `defaultVisible` * `ifOffScreen` * `layout` * `monitorType` * `openCode` * `over` * `pageEventNames` * `raiseCode` * `raiseSystem` * `renditionType` * `status` * `trace` * `version` * `windowType`  methods: * `addStockEvents` * `alertFileNotFound` * `alertSelectFailed` * `argsDWIM` * `canPlayOrAlert` * `computeFloatWinRect` * `constrainRectToScreen` * `createPlayer` * `getAltTextData` * `getAltTextSettings` * `getAnnotStockEvents` * `getAnnotTraceEvents` * `getPlayers` * `getPlayerStockEvents` * `getPlayerTraceEvents` * `getRenditionSettings` * `getURLData` * `getURLSettings` * `getWindowBorderSize` * `openPlayer` * `removeStockEvents` * `startPlayer` |
| `Doc` object | properties: * `innerAppWindowRect` * `innerDocWindowRect` * `media` * `outerAppWindowRect` * `outerDocWindowRect` * `pageWindowRect` |
| [Doc.media](./doc.md#id178) object | properties: * `canPlay`  methods: * `deleteRendition` * `getAnnot` * `getAnnots` * `getRendition` * `newPlayer` |
| `event` object | A new Screen type used with Multimedia along with associated event names. |
| `Events` object | methods: * `add` * `dispatch` * `remove` |
| `EventListener` object | methods: * `afterBlur` * `afterClose` * `afterDestroy` * `afterDone` * `afterError` * `afterEscape` * `afterEveryEvent` * `afterFocus` * `afterPause` * `afterPlay` * `afterReady` * `afterScript` * `afterSeek` * `afterStatus` * `afterStop` * `onBlur` * `onClose` * `onDestroy` * `onDone` * `onError` * `onEscape` * `onEveryEvent` * `onFocus` * `onGetRect` * `onPause` * `onPlay` * `onReady` * `onScript` * `onSeek` * `onStatus` * `onStop` |
| `Marker` object | properties: * `frame` * `index` * `name` * `time` |
| `Markers` object | properties: * `player`  methods: * `get` |
| `MediaOffset` object | properties: * `frame` * `marker` * `time` |
| `MediaPlayer` object | properties: * `annot` * `defaultSize` * `doc` * `events` * `hasFocus` * `id` * `innerRect`  i `isOpen`   `isPlaying` * `markers` * `outerRect` * `page` * `settings` * `uiSize` * `visible`  methods: * `close` * `open` * `pause` * `play` * `seek` * `setFocus` * `stop` * `triggerGetRect` * `where` |
| `MediaReject` object | properties: * `rendition` |
| `MediaSelection` object | properties: * `selectContext` * `players` * `rejects` * `rendition` |
| `MediaSettings` object | properties: * `autoPlay` * `baseURL` * `bgColor` * `bgOpacity` * `endAt` * `floating` * `duration` * `floating` * `layout` * `monitor` * `monitorType` * `page` * `palindrome` * `players` * `rate` * `repeat` * `showUI` * `startAt` * `visible` * `volume` * `windowType` |
| `Monitor` object | properties: * `colorDepth` * `isPrimary` * `rect` * `workRect` |
| `Monitors` object | methods: * `bestColor` * `bestFit` * `desktop` * `document` * `filter` * `largest` * `leastOverlap` * `mostOverlap` * `nonDocument` * `primary` * `secondary` * `select` * `tallest` * `widest` |
| `PlayerInfo` object | properties: * `id` * `mimeTypes` * `name` * `version`  methods: * `canPlay` * `canUseData` |
| `PlayerInfoList` object | methods: * `select` |
| `Rendition` object | properties: * `altText` * `doc` * `fileName` * `type` * `uiName`  methods: * `getPlaySettings` * `select` * `testCriteria` |
| `ScreenAnnot` object | properties: * `altText` * `alwaysShowFocus` * `display` * `doc` * `events` * `extFocusRect` * `innerDeviceRect` * `noTrigger` * `outerDeviceRect` * `page` * `player` * `rect`  methods: * `hasFocus` * `setFocus` |

<a id="acrobat-5-0-changes"></a>
<a id="id32"></a>
## Acrobat 5.0 changes

<a id="introduced-in-acrobat-5-0"></a>
<a id="id33"></a>
### Introduced in Acrobat 5.0

|  |  |
|---|---|
| ADBC object | methods:  getDataSourceList  newConnection |
| `AlternatePresentation` object | properties: * `alignment` * `AP` * `arrowBegin` * `arrowEnd` * `author` * `contents` * `doc` * `fillColor` * `hidden` * `modDate` * `name` * `noView` * `page` * `point` * `points` * `popupRect` * `print` * `rect` * `readOnly` * `rotate` * `strokeColor` * `textFont` * `type` * `soundIcon` * `width`  methods: * `destroy` * `getProps` * `setProps` |
| `app` object | properties: * `activeDocs` * `fs` * `plugIns` * `viewerVariation`  methods: * `addMenuItem` * `addSubMenu` * `clearInterval` * `clearTimeOut` * `listMenuItems` * `listToolbarButtons` * `newDoc` * `openDoc` * `popUpMenu` * `setInterval` * `setTimeOut` |
| `Bookmark` object | properties: * `children` * `color` * `doc` * `name` * `open` * `parent` * `style`  methods: * `createChild` * `execute` * `insertChild` * `remove` |
| `color` object | methods: * `convert` * `equal` |
| `console` object | methods: * `getColumnList` * `getTableList` * `console` |
| `Data` object | properties: * `creationDate` * `modDate` * `MIMEType` * `name` * `path` * `size` |
| `Doc` object | properties: * `bookmarkRoot` * `disclosed` (5.0.5)  `icons` * `info` * `layout` * `securityHandler` * `selectedAnnots` * `sounds` * `templates` * `URL`  methods: * `addAnnot` * `addField` * `addIcon` * `addThumbnails` * `addWeblinks` * `bringToFront` * `closeDoc` * `createDataObject` * `createTemplate` * `deletePages` * `deleteSound` * `exportAsXFDF` * `exportDataObject` * `extractPages` * `flattenPages` * `getAnnot` * `getAnnots` * `getDataObject` * `getIcon` * `getPageBox` * `getPageLabel` * `getPageNthWord` * `getPageNthWordQuads` * `getPageRotation` * `getPageTransition` * `getSound` * `importAnXFDF` * `importDataObject` * `importIcon` * `importSound` * `importTextData` * `insertPages` * `movePage` * `print` * `removeDataObject` * `removeField` * `removeIcon` * `removeTemplate` * `removeThumbnails` * `removeWeblinks` * `replacePages` * `saveAs` * `selectPageNthWord` * `setPageBoxes` * `setPageLabels` * `setPageRotations` * `setPageTransitions` * `submitForm` * `syncAnnotScan` |
| `event` object | properties: * `changeEx` * `keyDown` * `targetName` |
| `Field` object | properties: * `buttonAlignX` * `buttonAlignY` * `buttonPosition` * `buttonScaleHow` * `buttonScaleWhen` * `currentValueIndices` * `doNotScroll` * `doNotSpellCheck` * `exportValues` * `fileSelect` * `multipleSelection` * `rect` * `strokeColor` * `submitName` * `valueAsString`  methods: * `browseForFileToSubmit` * `buttonGetCaption` * `buttonGetIcon` * `buttonSetCaption` * `buttonSetIcon` * `checkThisBox` * `defaultIsChecked` * `isBoxChecked` * `isDefaultChecked` * `setAction` * `signatureInfo` * `signatureSign` * `signatureValidate` |
| `FullScreen` object | properties: * `backgroundColor` * `clickAdvances` * `cursor` * `defaultTransition` * `escapeExits` * `isFullScreen` * `loop` * `timeDelay` * `transitions` * `usePageTiming` * `useTimer` |
| `global` object | methods: * `subscribe` |
| `identity` object | properties: * `corporation` * `email` * `loginName` * `name` |
| `Index` object | properties: * `available` * `name` * `path` * `selected` |
| `PlayerInfo` object | properties: * `certified` * `loaded` * `name` * `path` * `version` |
| PPKLite Signature Handler Object (now listed under the\| `SecurityHandler` object) | properties: * `appearances` * `isLoggedIn` * `loginName` * `loginPath` * `name` * `signInvisible` * `signVisible` * `uiName`  methods: * `login` * `logout` * `newUser` * `setPasswordTimeout` |
| `Report` object | properties: * `absIndent` * `color` * `absIndent`  methods: * `breakPage` * `divide` * `indent` * `outdent` * `open` * `mail` * `writeText` * `save` * `writeText` |
| `search` object | properties: * `available` * `indexes` * `markup` * `maxDocs` * `proximity` * `refine` * soundex * `stem`  methods: * `addIndex` * `getIndexForPath` * `query` * `removeIndex` |
| `security` object | properties: * `handlers` * `validateSignaturesOnOpen`  methods: * `getHandler` |
| `spell` object | properties: * `available` * `dictionaryNames` * `dictionaryOrder` * `domainNames` s   methods: * `addDictionary` * `addWord` * `check` * `checkText` * `checkWord` * `removeDictionary` * `removeWord` * `userWords` |
| `TableInfo` object | properties: * `columnCount` * `rowCount`  methods: * `execute` * `getColumn` * `getColumnArray` * `getRow` * `nextRow` |
| `Template` object | properties: * `hidden` * `name`  methods: * `spawn` |

<a id="modified-in-acrobat-5-0"></a>
<a id="id34"></a>
### Modified in Acrobat 5.0

The console can act as an editor and can execute JavaScript code.

The following properties and methods have been changed or enhanced:

|  |  |
|---|---|
| `app` object | `language` \* `execMenuItem` |
| `Doc` object | - `exportAsFDF` * `print` * `submitForm` |
| `event` object | `type` |
| `Field` object | - `textFont` * `value` * `buttonImportIcon` * `getItemAt` |
| `util` object | `printd` |

The section related to `event` object has been greatly enhanced to facilitate better understanding of the Acrobat JavaScript Event model.

<a id="deprecated-in-acrobat-5-0"></a>
<a id="id35"></a>
### Deprecated in Acrobat 5.0

The following properties and methods have been deprecated:

|  |  |
|---|---|
| `app` object | - `fullscreen` * `numPlugIns` * `getNthPlugInName` |
| `Doc` object | - `author` * `creationDate` * `creationDate` * `keywords` * `modDate` * `numTemplates` * `producer` * `title` * `getNthTemplate` * `spawnPageFromTemplate` |
| `Field` object | `hidden` |
| `TTS` object | `soundCues` \* `speechCues` |

<a id="modified-in-acrobat-5-05"></a>
<a id="id36"></a>
### Modified in Acrobat 5.05

- A new symbol was added to the quick bar denoting which methods are missing from Acrobat Approval.
- In the `Doc` object, the property `disclosed` was added.

<a id="modified-in-adobe-reader-5-1"></a>
<a id="id37"></a>
### Modified in Adobe Reader 5.1

Access to the following properties and methods was changed for the Adobe 5.1 Reader:

|  |  |
|---|---|
| `Annotation` object | properties: * `alignment` * `AP` * `arrowBegin` * `arrowEnd` * `author` * `contents` * `doc` * `fillColor` * `hidden`  methods: * `destroy` * `getProps` * `setProps` * `modDate` * `name` * `noView` * `page` * `point` * `points` * `popupRect` * `print` * `rect` * `readOnly` * `rotate` * `strokeColor` * `textFont` * `type` * `soundIcon` * `width` |
| `Doc` object | properties: * `selectedAnnots`  methods: * `addAnnot` * `addField` * `exportAsFDF` * `exportAsXFDF` * `getAnnot` * `getAnnots` * `getNthTemplate` * `importAnFDF` * `importAnXFDF` * `importDataObject` * `mailDoc` * `mailForm` * `spawnPageFromTemplate` * `submitForm` * `syncAnnotScan` |
| `Template` object | methods: * `spawn` |
