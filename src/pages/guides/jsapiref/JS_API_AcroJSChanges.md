# Changes Across Versions

This section summarizes the new features and changes introduced in Acrobat and earlier.

## Acrobat XI changes

For more information on the following changes, see the JavaScript for Acrobat API Reference and Developing Acrobat Applications Using JavaScript.

### Changes to PrintParams object

The `colorOverride` property of the `PrintParams` object is no longer supported.

## Acrobat X changes

For more information on the following changes, see the JavaScript for Acrobat API Reference and Developing Acrobat Applications Using JavaScript.

### New JavaScript version

This release supports JavaScript version 1.8.

### Impact of Acrobat menu restructuring on JavaScript APIs

Starting Acrobat X, the number of top-level menu items has been reduced. The menu items available from Acrobat X onwards are: File, Edit, View, Window, and Help. If any of your previous scripts referred to a top-level menu item that no longer exists, the reference will not work.

Starting Acrobat X, the toolbar commands are available through the Tools pane on the right side of the display. Accordingly, methods and properties to customize the toolbar such as `app.addToolButton`, `hideToolBarButton`, and `removeToolButton`, now apply to the Tools pane area. For example, `app.addToolButton` adds a button to the Plugin Addon Tools panel in the Tools pane.

### New util method

The new `readFileIntoStream` util method loads an external file into a JavaScript stream, optionally encodes it as base64, and returns the content as a base64 encoded stream.

### Changes to search object

The following changes have been made to the “search” object properties

- The `thesaurus` and `soundex` properties have been removed
- The `legacySearch` property is now deprecated and always returns false.

### Changes to SearchExecuteQuery

The following have been removed from `nWordOptions` parameter of `SearchExecuteQuery` :

- `kWordOptionSoundsLike`
- `kWordOptionThesaurus`

### Function SearchIsLegacySearchAvailable deprecated

The function `SearchIsLegacySearchAvailable` has been deprecated and will always return false.

### Enhancements to PDFOptPDFVersion

The following have been added to `PDFOptPDFVersion` :

- `kPDFOptAcrobat9`
- `kPDFOptAcrobat10`

### Enhancements to Doc object

In this release, the following enhancements have been made to the `Doc` object:

#### Enhancements to the getDataObjectContents method

A `NotAllowedError` is thrown and the method fails if it attempts to access the content of an embedded file attachment for which any of the following conditions is true (all file name extension matching is case-insensitive):

- The attachment’s file name extension is “.SWF”. If a legitimate .SWF application or module run as part of Acrobat’s Rich Media Annotation or PDF Portfolio navigator is allowed access to the content bytes of .SWF embedded file attachments, it is possible that the legitimate .SWF will load a malicious .SWF.

> **Note**
>
> If you use the `Data.MIMEType` property to check whether a Data object represents a .SWF file, note that the MIME type for .SWF files is `application/x-shockwave-flash`.

- The attachment’s file name extension is “.GIF”, “.JPG”, “.JPEG”, or “.PNG” and the first three bytes of its content have the header signature of a .SWF file (“FWS” or “CWS”). The reason for this security restriction is that the same `ActionScriptflash.display.Loader class load()` method that can be used to load GIF, JPEG, and PNG images can also be used to load a SWF file. If a malicious SWF file’s extension has been altered to that of one of these image types, the SWF could be loaded.

#### Enhancements to the SaveAs Method

The following enhancements have been made to the `SaveAs` method of the `Doc` object:

##### New Values of cConvID

The following new values of cConvID have been added:

| Value | Valid Extension |
| --- | --- |
| `com.adobe.acrobat.docx` | `docx` |
| `com.adobe.acrobat.xlsx` | `xlsx` |

##### Deprecated Values of cConvID

The conversion IDs listed below are deprecated in Acrobat X. They are not registered but (only when used with the JavaScript `doc.saveAs` call) are internally mapped to valid, registered conversion IDs. Support for the deprecated conversion IDs will be fully removed in subsequent Acrobat releases.

| Deprecated cConvID | Equivalent Valid cConvID |
| --- | --- |
| `com.adobe.acrobat.html-3-20` | `com.adobe.acrobat.html` |
| `com.adobe.acrobat.htm l- 4-01-css-1-00` | `com.adobe.acrobat.html` |

#### New timestampSign and certifyInvisibleSign Doc methods

For more information on the new Doc methods `timestampSign and certifyInvisibleSign`, see the next section, Signature support for Emerging PAdES ETSI ESI standard.

<a id="84989"></a>
### Signature support for Emerging PAdES ETSI ESI standard

The European Telecommunications Standards Institute (ETSI) has published a multi-part standard that defines a series of profiles for PAdES—Advanced Electronic Signatures for Portable Document Format (PDF) documents. For more information, see: [http://www.etsi.org/website/newsandevents/200909\_electronicsignature.aspx](http://www.etsi.org/website/newsandevents/200909_electronicsignature.aspx)

The standard includes a new feature to “timestamp the document”, which adds an invisible timestamp signature to a document. This release provides a corresponding JavaScript `Doc` method to do the same. Additionally, the release provides a `Doc` method to apply an invisible certification (this is already available as a menu item in Acrobat and is now supported in JavaScript as well). Both these methods take the same parameters as `field.signatureSign`, but are at the `Doc` level. These methods can only be executed during a batch, console, or application initialization event.

#### Adding an invisible timestamp

The new `timestampSign` Doc method adds an invisible timestamp to a document.

NOTE: This method is not available in Reader.

#### Adding an invisible Certification

The new `certifyInvisibleSign` Doc method adds an invisible certification to a document.

For more information on these methods, see the description of the `Doc` object in the JavaScript API reference.

### ADBC Support Removed from Documentation

ADBC is not supported since the previous release of Acrobat. In this release, the section on ADBC support has been removed from Acrobat SDK documentation.

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
| --- | --- |
| App object | methods:<br><br>- `newCollection` |
| Doc object | properties:<br><br>- `collection` |
| Data object | methods:<br><br>- `getFieldValue`<br>- `setFieldValue` |
| `Collection` object | properties:<br><br>- `fields`<br>- `initialDoc`<br>- `initialView`<br><br>methods:<br><br>- `addField`<br>- `getField`<br>- `removeField` |
| `collectionField` object | properties:<br><br>- `name`<br>- `order`<br>- `readOnly`<br>- `sort`<br>- `text`<br>- `type` |

Acrobat 6.0 (and Later) Compatible Media relies on the underlying operating system to locate and launch a multimedia player residing on the user’s system; however, Acrobat 9.0 natively supports Flash video (FLV) and Flash applications (SWF) which can be embedded in, or streamed to, a PDF document. Native support for Flash enables reliable cross-platform playback. No additional media player or specific codec is necessary.

Acrobat 6.0 (and Later) Compatible Media is superseded by the multimedia of Acrobat 9.0, which uses rich media annotations. Developers of PDFs with multimedia assets are, therefore, strongly encouraged to use the rich media annotations of Acrobat 9.

Below is a listing of the JavaScript API that support rich media annotations.

|  |  |
| --- | --- |
| Doc object | methods:<br><br>- `getAnnotRichMedia`<br>- `getAnnotsRichMedia` |
| `AnnotRichMedia` object | properties:<br><br>- `activated`<br>- `context3D`<br>- `name`<br>- `page`<br>- `rect`<br>- `subtype`<br><br>methods:<br><br>- `callAS` |

## Acrobat 8.1 changes

There are new security restrictions for the `search` object’s `addIndex`, `query`, and `removeIndex` methods, as well as the `spell` object’s `removeWord` method. For more information, see those method descriptions.

## Acrobat 8.0 changes

The JavaScript interpreter now supports E4X, ECMA-357. “EMCAScript for XML (E4X) Specification”, *http://www.ecma-international/publications/standards/Ecma-357.htm* , documents this specification. An example following `metadata` illustrates E4X usage.

The JavaScript category in the Preferences dialog box (Ctrl + K) has a new security check box, “Enable global object security policy”.

- When checked, the default, each time a global variable is written to, the origin which set it is remembered. Only origins that match can then access the variable. For files, this means only the file that set it, having the same path it had when the variable was set, can access the variable. For documents from URLs, it means only the web host which set it can access the variable.

There is an important exception to the restrictions described above. Global variables can be defined and accessed in a privileged context, in the console, in a batch sequence and in folder JavaScript.

- When not checked, documents from different origins are permitted to access the variable; this is the behavior previous to version 8.0.

See the section on the `global` object for additional details and examples.

There is a new restriction on the use of `app.execMenuItem` to a list of safe menu items. See the security note.

The following properties and methods are introduced in Acrobat 8.0:

|  |  |
| --- | --- |
| `Certificate` object | properties:<br><br>- `privateKeyValidityEnd`<br>- `privateKeyValidityStart`<br>- `validityEnd` (First introduced in version 7.0.5, but undocumented.)<br>- `validityStart` (First introduced in version 7.0.5, but undocumented.) |
| CertificateSpecifier Object | properties:<br><br>- `subjectDN`<br>- `keyUsage`<br>- `urlType`<br>- Expanded description of the `url` property.<br>- Added four new bit flags to the `flags` property: `subjectDN`, `issuerDN`, `keyUsage`, `url`. |
| `colorConvertAction` object | properties:<br><br>- `action`<br>- `alias`<br>- `colorantName`<br>- `convertIntent`<br>- `convertProfile`<br>- `embed`<br>- `isProcessColor`<br>- `matchAttributesAll`<br>- `matchAttributesAny`<br>- `matchIntent`<br>- `matchSpaceTypeAll`<br>- `matchSpaceTypeAny`<br>- `preserveBlack`<br>- `useBlackPointCompensation` |
| `Doc` object | properties:<br><br>- `xfa` (First introduced in version 6.0.2, but undocumented.)<br>- `XFAForeground`<br><br>methods:<br><br>- `colorConvertPage`<br>- `embedOutputIntent`<br>- `exportAsFDFStr`<br>- `exportAsXFDFStr`<br>- `getColorConvertAction` |
| `Net` object | properties:<br><br>- `SOAP`  (`Net.SOAP` has properties and methods aliased with `SOAP.wireDump`, `SOAP.connect`, `SOAP.request`, `SOAP.response`.)<br>- `Discovery`  (`Net.Discovery` has methods aliased with `SOAP.queryServices` and `SOAP.resolveService`.)<br>- `HTTP`<br><br>methods:<br>\* `streamDecode`<br>\* `streamDigest`<br>\* `streamEncode` |
| [Net.HTTP](JS_API_AcroJS.md#37414)  object | methods:<br><br>- `request` |
| `PrintParams` | properties:<br><br>- `booklet`<br>- `constants`. bookletBindings<br>- `constants`. bookletDuplexModes<br>- `constants`.handling.booklet ( See<br>- `pageHandling` for a description.) |
| `RDN` object | properties: Added 22 properties to the RDN object:  `businessCategory`, `countryOfCitizenship`, `countryOfResidence`, `dateOfBirth`, `dc`, `dnQualifier`, `gender`, `generationQualifier`, `givenName`, `initials`, `l`, `name`, `nameAtBirth`, `placeOfBirth`, `postalAddress`, `postalCode`, `pseudonym`, `serialNumber`, `sn`, `st`, `street`, `title` |
| `SecurityHandler` object | properties: The following three properties were previously undocumented.<br><br>- `docDecrypt`<br>- `docEncrypt`<br>- `validateFDF` |
| SeedValue Object | - Added three new flags: `legalAttestations`, `shouldAddRevInfo`, `digestMethod`.<br>- Change of behavior of the `reasons` property.<br>- Added the `digestMethod` property.<br>- Change in wording of the description of the `version` property.<br>- Added the `shouldAddRevInfo` property. |
| `SignatureInfo`  object | properties:  digestMethod |

The following properties and methods are modified in Acrobat 8.0:

|  |  |
| --- | --- |
| `app` object | methods:<br><br>- `openDoc` (`cDest` parameter added) |
| `Doc` object | methods:<br><br>- `addAnnot` (New default values for the `author` property.)<br>- `addRecipientListCryptFilter` (Added note for Acrobat 7.0.)<br>- `getLegalWarnings` (No longer dirties document. Return value changed.)<br>- `importTextData` (Can be only executed during a console or batch event.) |
| FDF object | methods:<br><br>- `addEmbeddedFile` (Updated description of the `nSaveOption` parameter for version 8.) |
| `Field` object | methods:<br><br>- `buttonImportIcon` (Can be executed only during a console or batch event) |
| `FullScreen`  object | properties:<br><br>- `escapeExits` (Can be set to `false` only during console and batch events) |
| LoginParameters Object | Modified wording of the `cURI` and `cUserId` properties. |
| `submitForm` method | The `cPassword` parameter can no longer be used. As of Acrobat 8.0, you cannot create password-encrypted FDF files. If this parameter is used, a form trying to submit a password-encrypted FDF will throw an `ESErrorInvalidArgs` exception and the form submission will not occur. |

## Acrobat 7.0.5 changes

Columns 5 and 6 of the quick bars have been removed.

The following properties and methods were introduced in Acrobat 7.0.5:

|  |  |
| --- | --- |
| `Collab` object | methods:<br><br>- `documentToStream` |
| `Data` object | properties:<br><br>- `description` |
| `Doc` object | properties:<br><br>- `hostContainer`<br>- `isModal`<br>- `viewState`<br><br>methods:<br><br>- `addRequirement`<br>- `removeRequirement` |
| Embedded PDF object | properties:<br><br>- `messageHandler`<br><br>method:  `postMessage` |
| `HostContainer` object | properties:<br><br>- `messageHandler`<br><br>methods:<br><br>- `postMessage` |
| `util` object | methods:<br><br>- `crackURL` |

The following properties and methods were modified in Acrobat 7.0.5:

|  |  |
| --- | --- |
| `SOAP` object | methods:<br><br>- `request` (`cRequestStyle` and `cContent` parameters added)<br>- `response` (`cRequestStyle` and `cContent` parameters added) |

## Acrobat 7.0 changes

The *Acrobat Multimedia JavaScript Reference* , which appeared as a separate document in version 6.0.2, was merged into the *Acrobat JavaScript Scripting Reference* , now named *JavaScript for Acrobat API Reference* . See the section [Introduced in Acrobat 6.0.2](JS_API_AcroJSChanges.md#30696) for a listing of all multimedia JavaScript objects, properties and methods.

Execution of JavaScript through a menu event is no longer privileged. There is now support for executing privileged code in a non-privileged context.

In versions of Acrobat earlier than 7.0, the JavaScript files `AForm.js`, `ADBC.js`, `Annots.js`, `AnWizard.js`, `media.js`, and `SOAP.js` resided in the App JavaScript folder. Beginning with Acrobat 7.0, these files are not shipped with Acrobat Pro, Acrobat Standard or Adobe Reader. In their place, a precompiled bytecode is used to improve performance. The `debugger.js` file in the App folder is not included in the bytecode.

Files in the User JavaScript folder are not included in the precompiled bytecode file.

It is recommended that users put their own `.js` files in the user JavaScript folder, the same place where `glob.js` resides. JavaScript code that sets up menu items ([addMenuItem](JS_API_AcroJS.md#52015) ) should be put in `config.js` in the User JavaScript folder. The location of this folder can be found programmatically by executing `app.getPath("user","javascript")` from the console.

Adobe Reader now has a console window. Under Edit > Preferences > JavaScript select Show Console on Errors and Messages. In addition to errors and exceptions, the console can also be opened programmatically with `console.show()`. See the `console` object for a few other details.

The debugging capability of the JavaScript Debugging window can be made available for Adobe Reader for the Windows and Mac OS platforms. To debug within Adobe Reader, the JavaScript file `debugger.js` must be installed, and the Windows registry must be edited appropriately.

<a id="38168"></a>
### Introduced in Acrobat 7.0

The following properties and methods were introduced in Acrobat 7.0.

|  |  |
| --- | --- |
| `Alerter` object | methods:<br><br>- `dispatch` |
| `Annotation` object | properties:<br><br>- `callout`<br>- `caretSymbol`<br>- Present in version 6.0, documented in version 7.0.  `creationDate`<br>- Present in version 6.0, documented in version 7.0.  `dash`<br>- Present in version 5.0, documented in version 7.0.  `delay`<br>- Present in version 5.0, documented in version 7.0.  `doCaption`<br>- `intent`<br>- `leaderExtend`<br>- `leaderLength`<br>- `lineEnding`<br>- `opacity`<br>- Present in version 5.0, documented in version 7.0.  `refType`<br>- `richDefaults`<br>- Present in version 6.0, documented in version 7.0.  `seqNum`<br>- Present in version 5.0, documented in version 7.0.  `state`<br>- Present in version 6.0, documented in version 7.0.  `stateModel`<br>- Present in version 6.0, documented in version 7.0.  `style`<br>- Present in version 6.0, documented in version 7.0. `subject` |
| `Annot3D` object | properties:<br><br>- `activated`<br>- `context3D`<br>- `innerRect`<br>- `name`<br>- `page`<br>- `rect` |
| `app` object | properties:<br><br>- `constants`<br><br>methods:<br><br>- `beginPriv`<br>- `browseForDoc`<br>- `endPriv`<br>- `execDialog`<br>- `launchURL`<br>- `trustedFunction`<br>- `trustPropagatorFunction` |
| `Dialog` object | methods:<br><br>- `enable`<br>- `end`<br>- `load`<br>- `store` |
| `Doc` object | properties:<br><br>- `docID` Present in version 6.0, documented in version 7.0.<br>- `dynamicXFAForm`<br>- `external`<br>- `hidden`<br>- `mouseX`<br>- `mouseY`<br>- `noautocomplete`<br>- `nocache (removed in version 9)`  `requiresFullSave`<br><br>methods:<br><br>- `addWatermarkFromFile`<br>- `addWatermarkFromText`<br>- `embedDocAsDataObject`<br>- `encryptUsingPolicy`<br>- `getAnnot3D`<br>- `getAnnots3D`<br>- `getDataObjectContents`<br>- `getOCGOrder`<br>- `openDataObject`<br>- `removeScript`<br>- `setDataObjectContents`<br>- `setOCGOrder` |
| [Doc.media](JS_API_AcroJS.md#69910) object | methods:<br><br>- `getOpenPlayers` |
| `Field` object | methods:<br><br>- `signatureGetModifications` |
| `OCG` object | properties:<br><br>- `constants`<br>- `initState`<br>- `locked`<br><br>methods:<br><br>- `getIntent`<br>- `setIntent` |
| `PlayerInfo` object | methods:<br><br>- `honors` |
| `PrintParams` object | properties:<br><br>- `nUpAutoRotate`<br>- `nUpNumPagesH`<br>- `nUpNumPagesV`<br>- `nUpPageBorder`<br>- `nUpPageOrder` |
| `search` object | properties:<br><br>- `attachments`<br>- `ignoreAccents`<br>- `objectMetadata`<br>- `proximityRange` |
| `security` object | security constants<br><br>methods:<br><br>- `chooseSecurityPolicy`<br>- `getSecurityPolicies` |
| `SecurityPolicy` object | SecurityPolicy properties |
| `SOAP` object | methods:<br><br>- `queryServices`<br>- `resolveService`<br>- `streamDigest` |
| `util` object | methods:<br><br>- `iconStreamFromIcon`<br>- `streamFromString`<br>- `stringFromStream` |
| `XMLData` object | methods:<br><br>- `applyXPath`<br>- `parse` |

### Modified in Acrobat 7.0

The following properties and methods were changed or enhanced:

|  |  |
| --- | --- |
| `app` object | methods:<br><br>- `addToolButton`<br>- `execMenuItem`<br>- `getPath`<br>- `mailGetAddrs`<br>- `openDoc` |
| `console` object | The console window is now available in Adobe Reader. |
| `Doc` object | methods:<br><br>- `createTemplate`<br>- `mailDoc`<br>- `print`<br>- `saveAs`<br>- `submitForm` |
| `Field` object | methods:<br><br>- `signatureSetSeedValue` |
| `Index` object | methods:<br><br>- `build` |
| `OCG` object | properties:<br><br>- `name` |
| `PrintParams` object | properties:<br><br>- `pageHandling` |
| `search` object | properties:<br><br>- `indexes` |
| `security` object | properties:<br><br>- `handlers`<br><br>methods:<br><br>- `getHandler` |
| `SecurityHandler` object | properties:<br><br>- `digitalIDs`<br><br>methods:<br><br>- `login`<br>- `newUser` |
| `SOAP` object | methods:<br><br>- `connect`<br>- `request` |
| `spell` object | The `Spell` object is not available in Adobe Reader 7.0 or later.<br><br>methods:<br><br>- `addWord` |
| `util` object | methods:<br><br>- `printd` |

## Acrobat 6.0 changes

The notion of a safe path was introduced for this version of Acrobat.

### Introduced in Acrobat 6.0

The following properties and methods were introduced in Acrobat 6:

|  |  |
| --- | --- |
| ADBC object | SQL types |
| `AlternatePresentation` object | properties:<br><br>- `active`<br>- `type`<br><br>methods:<br><br>- `start`<br>- `stop` |
| `Annotation` object | properties:<br><br>- `borderEffectIntensity`<br>- `borderEffectStyle`<br>- `inReplyTo`<br>- `richContents`<br>- `toggleNoView`<br><br>methods:<br><br>- `getStateInModel`<br>- `transitionToState` |
| `app` object | properties:<br><br>- `fromPDFConverters`<br>- `printColorProfiles`<br>- `printerNames`<br>- `runtimeHighlight`<br>- `runtimeHighlightColor`<br>- `thermometer`<br>- `viewerType`<br><br>methods:<br><br>- `addToolButton`<br>- `getPath`<br>- `mailGetAddrs`<br>- `newFDF`<br>- `openFDF`<br>- `popUpMenuEx`<br>- `removeToolButton` |
| `Bookmark` object | methods:<br><br>- `setAction` |
| `catalog` object | properties:<br><br>- `isIdle`<br>- `jobs`<br><br>methods:<br><br>- `getIndex`<br>- `remove` |
| `Certificate` object | properties:<br><br>- `keyUsage`<br>- `usage` |
| `Collab` object | methods:<br><br>- `addStateModel`<br>- `removeStateModel` |
| `console` object | methods:<br><br>- `close` |
| `dbg` object | properties:<br><br>- `bps`<br><br>methods:<br><br>- `c`<br>- `cb`<br>- `q`<br>- `sb`<br>- `si`<br>- `sn`<br>- `so`<br>- `sv` |
| `Directory` object | properties:<br><br>- `info`<br><br>methods:<br><br>- `connect` |
| `DirConnection` object | properties:<br><br>- `canList`<br>- `canDoCustomSearch`<br>- `canDoCustomUISearch`<br>- `canDoStandardSearch`<br>- `groups`<br>- `name`<br>- `uiName`<br><br>methods:<br><br>- `search`<br>- `setOutputFields` |
| `Doc` object | properties:<br><br>- `alternatePresentations`<br>- `documentFileName`<br>- `metadata`<br>- `permStatusReady`<br><br>methods:<br><br>- `addLink`<br>- `addRecipientListCryptFilter`<br>- `addRequirement`<br>- `encryptForRecipients`<br>- `exportAsText`<br>- `exportXFAData`<br>- `getLegalWarnings`<br>- `getLinks`<br>- `getOCGs`<br>- `getPrintParams`<br>- `importXFAData`<br>- `newPage`<br>- `removeLinks`<br>- `setAction`<br>- `setPageAction`<br>- `setPageTabOrder` |
| `Error` object | properties:<br><br>- `fileName`<br>- `lineNumber`<br>- `message`<br>- `name`<br><br>methods:<br><br>- `toString` |
| `event` object | properties:<br><br>- `fieldFull`<br>- `richChange`<br>- `richChangeEx`<br>- `richValue` |
| `FDF` object | properties:<br><br>- `deleteOption`<br>- `isSigned`<br>- `numEmbeddedFiles`<br><br>methods:<br><br>- `addContact`<br>- `addEmbeddedFile`<br>- `addRequest`<br>- `close`<br>- `mail`<br>- `save`<br>- `signatureClear`<br>- `signatureSign`<br>- `signatureValidate` |
| `Field` object | properties:<br><br>- `buttonFitBounds`<br>- `comb`<br>- `commitOnSelChange`<br>- `defaultStyle`<br>- `radiosInUnison`<br>- `richText`<br>- `richValue`<br>- `rotation`<br><br>methods:<br><br>- `getLock`<br>- `setLock`<br>- `signatureGetSeedValue`<br>- `signatureSetSeedValue` |
| `Index` object | methods:<br><br>- `build` |
| `Link` object | properties:<br><br>- `borderColor`<br>- `borderWidth`<br>- `highlightMode`<br>- `rect`<br><br>methods:<br><br>- `setAction` |
| `OCG` object | properties:<br><br>- `name`<br>- `state`<br><br>methods:<br><br>- `setAction` |
| `PrintParams` object | properties:<br><br>- `binaryOK`<br>- `bitmapDPI`<br>- `colorOverride`<br>- `colorProfile`<br>- `constants`<br>- `downloadFarEastFonts`<br>- `fileName`<br>- `firstPage`<br>- `flags`<br>- `fontPolicy`<br>- `gradientDPI`<br>- `interactive`<br>- `lastPage`<br>- `pageHandling`<br>- `pageSubset`<br>- `printAsImage`<br>- `printContent`<br>- `printerName`<br>- `psLevel`<br>- `rasterFlags`<br>- `reversePages`<br>- `tileLabel`<br>- `tileMark`<br>- `tileOverlap`<br>- `tileScale`<br>- `transparencyLevel`<br>- `usePrinterCRD`<br>- `useT1Conversion` |
| `Report` object | properties:<br><br>- `style` |
| `search` object | properties:<br><br>- `docInfo`<br>- `docText`<br>- `docXMP`<br>- `bookmarks`<br>- `ignoreAsianCharacterWidth`<br>- `jpegExif`<br>- `legacySearch`<br>- `markup`<br>- `matchWholeWord`<br>- `wordMatching` |
| `security` object | methods:<br><br>- `chooseRecipientsDialog`<br>- `getSecurityPolicies`<br>- `importFromFile` |
| `SecurityHandler` object | properties:<br><br>- `digitalIDs`<br>- `directories`<br>- `directoryHandlers`<br>- `signAuthor`<br>- `signFDF`<br><br>methods:<br><br>- `newDirectory` |
| `SOAP` object | properties:<br><br>- `wireDump`<br><br>methods:<br><br>- `connect`<br>- `request`<br>- `response`<br>- `streamDecode`<br>- `streamEncode`<br>- `streamFromString`<br>- `stringFromStream` |
| `Span` object | properties:<br><br>- `alignment`<br>- `fontFamily`<br>- `fontStretch`<br>- `fontStyle`<br>- `fontWeight`<br>- `text`<br>- `textColor`<br>- `textSize`<br>- `strikethrough`<br>- `subscript`<br>- `superscript`<br>- `underline` |
| `spell` object | properties:<br><br>- `languages`<br>- `languageOrder`<br><br>methods:<br><br>- `customDictionaryClose`<br>- `customDictionaryCreate`<br>- `customDictionaryExport`<br>- `customDictionaryOpen`<br>- `ignoreAll` |
| `Thermometer` object | properties:<br><br>- `cancelled`<br>- `duration`<br>- `value`<br>- `text`<br><br>methods:<br><br>- `begin`<br>- `end` |
| `util` object | methods:<br><br>- `printd`<br>- `spansToXML`<br>- `xmlToSpans` |

### Modified in Acrobat 6.0

The following properties and methods were changed or enhanced:

|  |  |
| --- | --- |
| `app` object | methods:<br><br>- `addMenuItem`<br>- `alert`<br>- `listMenuItems`<br>- `listToolbarButtons`<br>- `response` |
| `Doc` object | properties:<br><br>- `layout`<br>- `zoomType`<br><br>methods:<br><br>- `createDataObject`<br>- `exportAsFDF`<br>- `exportAsXFDF`<br>- `exportDataObject`<br>- `flattenPages`<br>- `getField` (see Extended Methods)  `getURL`<br>- `importDataObject`<br>- `importIcon`<br>- `print`<br>- `saveAs`<br>- `spawnPageFromTemplate`<br>- `submitForm` |
| `event` object | properties:<br><br>- `changeEx` |
| `Field` object | properties:<br><br>- `name`<br><br>methods:<br><br>- `buttonImportIcon`<br>- `signatureInfo`<br>- `signatureSign`<br>- `signatureValidate` |
| `global` object | Persistent global data only applies to variables of type Boolean, Number or String. Acrobat 6.0 has reduced the maximum size of global persistent variables from 32 KB to 2-4 KB. Any data added to the string after this limit is dropped. |
| `search` object | methods:<br><br>- `query` |
| `SecurityHandler` object | The following were introduced in Acrobat 5.0 as properties and methods of the PPKLite Signature Handler Object. In Acrobat 6.0, they are properties and methods of the `SecurityHandler` object. All of these have new descriptions, and some have additional parameters.  -  When signing using JavaScript methods, the user’s digital signature profile must be a `.pfx` file, not an `.apf`, as in earlier versions of Acrobat. To convert an `.apf` profile to the new `.pfx` type, use the UI (click Advanced > Manage Digital IDs > My Digital ID Files > Select My Digital ID File) to import the `.apf` profile.   properties:<br><br>- `appearances`<br>- `isLoggedIn`<br>- `loginName`<br>- `loginPath`<br>- `name`<br>- `signInvisible`<br>- `signVisible`<br>- `uiName`<br><br>methods:<br><br>- `login`<br>- `logout`<br>- `newUser`<br>- `setPasswordTimeout` |
| `Template` t object | methods:   `spawn` |

<a id="63660"></a>
**Extended Methods**

The Document `.getField` method was extended in Acrobat 6.0 so that it retrieves the Field object of individual widgets. See the `Field` object for a discussion of widgets and how to work with them.

### Deprecated in Acrobat 6.0

|  |  |
| --- | --- |
| `search` object | properties:  soundex  thesaurus |
| `spell` object | methods:<br><br>- `addDictionary`<br>- `removeDictionary` |

<a id="30696"></a>
### Introduced in Acrobat 6.0.2

The following table lists the objects, properties and methods of the Multimedia plug-in. In Acrobat 6.0.2, multimedia JavaScript was documented in a separate document called the “Acrobat Multimedia JavaScript Reference”.

|  |  |
| --- | --- |
| `app` object | properties:<br><br>- `media`<br>- `monitors` |
| [app.media](JS_API_AcroJS.md#19976) object | properties:<br><br>- `align`<br>- `canResize`<br>- `closeReason`<br>- `defaultVisible`<br>- `ifOffScreen`<br>- `layout`<br>- `monitorType`<br>- `openCode`<br>- `over`<br>- `pageEventNames`<br>- `raiseCode`<br>- `raiseSystem`<br>- `renditionType`<br>- `status`<br>- `trace`<br>- `version`<br>- `windowType`<br><br>methods:<br><br>- `addStockEvents`<br>- `alertFileNotFound`<br>- `alertSelectFailed`<br>- `argsDWIM`<br>- `canPlayOrAlert`<br>- `computeFloatWinRect`<br>- `constrainRectToScreen`<br>- `createPlayer`<br>- `getAltTextData`<br>- `getAltTextSettings`<br>- `getAnnotStockEvents`<br>- `getAnnotTraceEvents`<br>- `getPlayers`<br>- `getPlayerStockEvents`<br>- `getPlayerTraceEvents`<br>- `getRenditionSettings`<br>- `getURLData`<br>- `getURLSettings`<br>- `getWindowBorderSize`<br>- `openPlayer`<br>- `removeStockEvents`<br>- `startPlayer` |
| `Doc` object | properties:<br><br>- `innerAppWindowRect`<br>- `innerDocWindowRect`<br>- `media`<br>- `outerAppWindowRect`<br>- `outerDocWindowRect`<br>- `pageWindowRect` |
| [Doc.media](JS_API_AcroJS.md#69910) object | properties:<br><br>- `canPlay`<br><br>methods:<br><br>- `deleteRendition`<br>- `getAnnot`<br>- `getAnnots`<br>- `getRendition`<br>- `newPlayer` |
| `event` object | A new Screen type used with Multimedia along with associated event names. |
| `Events` object | methods:<br><br>- `add`<br>- `dispatch`<br>- `remove` |
| `EventListener` object | methods:<br><br>- `afterBlur`<br>- `afterClose`<br>- `afterDestroy`<br>- `afterDone`<br>- `afterError`<br>- `afterEscape`<br>- `afterEveryEvent`<br>- `afterFocus`<br>- `afterPause`<br>- `afterPlay`<br>- `afterReady`<br>- `afterScript`<br>- `afterSeek`<br>- `afterStatus`<br>- `afterStop`<br>- `onBlur`<br>- `onClose`<br>- `onDestroy`<br>- `onDone`<br>- `onError`<br>- `onEscape`<br>- `onEveryEvent`<br>- `onFocus`<br>- `onGetRect`<br>- `onPause`<br>- `onPlay`<br>- `onReady`<br>- `onScript`<br>- `onSeek`<br>- `onStatus`<br>- `onStop` |
| `Marker` object | properties:<br><br>- `frame`<br>- `index`<br>- `name`<br>- `time` |
| `Markers` object | properties:<br><br>- `player`<br><br>methods:<br><br>- `get` |
| `MediaOffset` object | properties:<br><br>- `frame`<br>- `marker`<br>- `time` |
| `MediaPlayer` object | properties:<br><br>- `annot`<br>- `defaultSize`<br>- `doc`<br>- `events`<br>- `hasFocus`<br>- `id`<br>- `innerRect`  i `isOpen`   `isPlaying`<br>- `markers`<br>- `outerRect`<br>- `page`<br>- `settings`<br>- `uiSize`<br>- `visible`<br><br>methods:<br><br>- `close`<br>- `open`<br>- `pause`<br>- `play`<br>- `seek`<br>- `setFocus`<br>- `stop`<br>- `triggerGetRect`<br>- `where` |
| `MediaReject` object | properties:<br><br>- `rendition` |
| `MediaSelection` object | properties:<br><br>- `selectContext`<br>- `players`<br>- `rejects`<br>- `rendition` |
| `MediaSettings` object | properties:<br><br>- `autoPlay`<br>- `baseURL`<br>- `bgColor`<br>- `bgOpacity`<br>- `endAt`<br>- `floating`<br>- `duration`<br>- `floating`<br>- `layout`<br>- `monitor`<br>- `monitorType`<br>- `page`<br>- `palindrome`<br>- `players`<br>- `rate`<br>- `repeat`<br>- `showUI`<br>- `startAt`<br>- `visible`<br>- `volume`<br>- `windowType` |
| `Monitor` object | properties:<br><br>- `colorDepth`<br>- `isPrimary`<br>- `rect`<br>- `workRect` |
| `Monitors` object | methods:<br><br>- `bestColor`<br>- `bestFit`<br>- `desktop`<br>- `document`<br>- `filter`<br>- `largest`<br>- `leastOverlap`<br>- `mostOverlap`<br>- `nonDocument`<br>- `primary`<br>- `secondary`<br>- `select`<br>- `tallest`<br>- `widest` |
| `PlayerInfo` object | properties:<br><br>- `id`<br>- `mimeTypes`<br>- `name`<br>- `version`<br><br>methods:<br><br>- `canPlay`<br>- `canUseData` |
| `PlayerInfoList` object | methods:<br><br>- `select` |
| `Rendition` object | properties:<br><br>- `altText`<br>- `doc`<br>- `fileName`<br>- `type`<br>- `uiName`<br><br>methods:<br><br>- `getPlaySettings`<br>- `select`<br>- `testCriteria` |
| `ScreenAnnot` object | properties:<br><br>- `altText`<br>- `alwaysShowFocus`<br>- `display`<br>- `doc`<br>- `events`<br>- `extFocusRect`<br>- `innerDeviceRect`<br>- `noTrigger`<br>- `outerDeviceRect`<br>- `page`<br>- `player`<br>- `rect`<br><br>methods:<br><br>- `hasFocus`<br>- `setFocus` |

## Acrobat 5.0 changes

### Introduced in Acrobat 5.0

|  |  |
| --- | --- |
| ADBC object | methods:  getDataSourceList  newConnection |
| `AlternatePresentation` object | properties:<br><br>- `alignment`<br>- `AP`<br>- `arrowBegin`<br>- `arrowEnd`<br>- `author`<br>- `contents`<br>- `doc`<br>- `fillColor`<br>- `hidden`<br>- `modDate`<br>- `name`<br>- `noView`<br>- `page`<br>- `point`<br>- `points`<br>- `popupRect`<br>- `print`<br>- `rect`<br>- `readOnly`<br>- `rotate`<br>- `strokeColor`<br>- `textFont`<br>- `type`<br>- `soundIcon`<br>- `width`<br><br>methods:<br><br>- `destroy`<br>- `getProps`<br>- `setProps` |
| `app` object | properties:<br><br>- `activeDocs`<br>- `fs`<br>- `plugIns`<br>- `viewerVariation`<br><br>methods:<br><br>- `addMenuItem`<br>- `addSubMenu`<br>- `clearInterval`<br>- `clearTimeOut`<br>- `listMenuItems`<br>- `listToolbarButtons`<br>- `newDoc`<br>- `openDoc`<br>- `popUpMenu`<br>- `setInterval`<br>- `setTimeOut` |
| `Bookmark` object | properties:<br><br>- `children`<br>- `color`<br>- `doc`<br>- `name`<br>- `open`<br>- `parent`<br>- `style`<br><br>methods:<br><br>- `createChild`<br>- `execute`<br>- `insertChild`<br>- `remove` |
| `color` object | methods:<br><br>- `convert`<br>- `equal` |
| `console` object | methods:<br><br>- `getColumnList`<br>- `getTableList`<br>- `console` |
| `Data` object | properties:<br><br>- `creationDate`<br>- `modDate`<br>- `MIMEType`<br>- `name`<br>- `path`<br>- `size` |
| `Doc` object | properties:<br><br>- `bookmarkRoot`<br>- `disclosed` (5.0.5)  `icons`<br>- `info`<br>- `layout`<br>- `securityHandler`<br>- `selectedAnnots`<br>- `sounds`<br>- `templates`<br>- `URL`<br><br>methods:<br><br>- `addAnnot`<br>- `addField`<br>- `addIcon`<br>- `addThumbnails`<br>- `addWeblinks`<br>- `bringToFront`<br>- `closeDoc`<br>- `createDataObject`<br>- `createTemplate`<br>- `deletePages`<br>- `deleteSound`<br>- `exportAsXFDF`<br>- `exportDataObject`<br>- `extractPages`<br>- `flattenPages`<br>- `getAnnot`<br>- `getAnnots`<br>- `getDataObject`<br>- `getIcon`<br>- `getPageBox`<br>- `getPageLabel`<br>- `getPageNthWord`<br>- `getPageNthWordQuads`<br>- `getPageRotation`<br>- `getPageTransition`<br>- `getSound`<br>- `importAnXFDF`<br>- `importDataObject`<br>- `importIcon`<br>- `importSound`<br>- `importTextData`<br>- `insertPages`<br>- `movePage`<br>- `print`<br>- `removeDataObject`<br>- `removeField`<br>- `removeIcon`<br>- `removeTemplate`<br>- `removeThumbnails`<br>- `removeWeblinks`<br>- `replacePages`<br>- `saveAs`<br>- `selectPageNthWord`<br>- `setPageBoxes`<br>- `setPageLabels`<br>- `setPageRotations`<br>- `setPageTransitions`<br>- `submitForm`<br>- `syncAnnotScan` |
| `event` object | properties:<br><br>- `changeEx`<br>- `keyDown`<br>- `targetName` |
| `Field` object | properties:<br><br>- `buttonAlignX`<br>- `buttonAlignY`<br>- `buttonPosition`<br>- `buttonScaleHow`<br>- `buttonScaleWhen`<br>- `currentValueIndices`<br>- `doNotScroll`<br>- `doNotSpellCheck`<br>- `exportValues`<br>- `fileSelect`<br>- `multipleSelection`<br>- `rect`<br>- `strokeColor`<br>- `submitName`<br>- `valueAsString`<br><br>methods:<br><br>- `browseForFileToSubmit`<br>- `buttonGetCaption`<br>- `buttonGetIcon`<br>- `buttonSetCaption`<br>- `buttonSetIcon`<br>- `checkThisBox`<br>- `defaultIsChecked`<br>- `isBoxChecked`<br>- `isDefaultChecked`<br>- `setAction`<br>- `signatureInfo`<br>- `signatureSign`<br>- `signatureValidate` |
| `FullScreen` object | properties:<br><br>- `backgroundColor`<br>- `clickAdvances`<br>- `cursor`<br>- `defaultTransition`<br>- `escapeExits`<br>- `isFullScreen`<br>- `loop`<br>- `timeDelay`<br>- `transitions`<br>- `usePageTiming`<br>- `useTimer` |
| `global` object | methods:<br><br>- `subscribe` |
| `identity` object | properties:<br><br>- `corporation`<br>- `email`<br>- `loginName`<br>- `name` |
| `Index` object | properties:<br><br>- `available`<br>- `name`<br>- `path`<br>- `selected` |
| `PlayerInfo` object | properties:<br><br>- `certified`<br>- `loaded`<br>- `name`<br>- `path`<br>- `version` |
| PPKLite Signature Handler Object (now listed under the\| `SecurityHandler` object) | properties:<br><br>- `appearances`<br>- `isLoggedIn`<br>- `loginName`<br>- `loginPath`<br>- `name`<br>- `signInvisible`<br>- `signVisible`<br>- `uiName`<br><br>methods:<br><br>- `login`<br>- `logout`<br>- `newUser`<br>- `setPasswordTimeout` |
| `Report` object | properties:<br><br>- `absIndent`<br>- `color`<br>- `absIndent`<br><br>methods:<br><br>- `breakPage`<br>- `divide`<br>- `indent`<br>- `outdent`<br>- `open`<br>- `mail`<br>- `writeText`<br>- `save`<br>- `writeText` |
| `search` object | properties:<br><br>- `available`<br>- `indexes`<br>- `markup`<br>- `maxDocs`<br>- `proximity`<br>- `refine`<br>- soundex<br>- `stem`<br><br>methods:<br><br>- `addIndex`<br>- `getIndexForPath`<br>- `query`<br>- `removeIndex` |
| `security` object | properties:<br><br>- `handlers`<br>- `validateSignaturesOnOpen`<br><br>methods:<br><br>- `getHandler` |
| `spell` object | properties:<br><br>- `available`<br>- `dictionaryNames`<br>- `dictionaryOrder`<br>- `domainNames` s   methods:<br>- `addDictionary`<br>- `addWord`<br>- `check`<br>- `checkText`<br>- `checkWord`<br>- `removeDictionary`<br>- `removeWord`<br>- `userWords` |
| `TableInfo` object | properties:<br><br>- `columnCount`<br>- `rowCount`<br><br>methods:<br><br>- `execute`<br>- `getColumn`<br>- `getColumnArray`<br>- `getRow`<br>- `nextRow` |
| `Template` object | properties:<br><br>- `hidden`<br>- `name`<br><br>methods:<br><br>- `spawn` |

### Modified in Acrobat 5.0

The console can act as an editor and can execute JavaScript code.

The following properties and methods have been changed or enhanced:

|  |  |
| --- | --- |
| `app` object | `language`<br>\* `execMenuItem` |
| `Doc` object | - `exportAsFDF`<br>- `print`<br>- `submitForm` |
| `event` object | `type` |
| `Field` object | - `textFont`<br>- `value`<br>- `buttonImportIcon`<br>- `getItemAt` |
| `util` object | `printd` |

The section related to `event` object has been greatly enhanced to facilitate better understanding of the Acrobat JavaScript Event model.

### Deprecated in Acrobat 5.0

The following properties and methods have been deprecated:

|  |  |
| --- | --- |
| `app` object | - `fullscreen`<br>- `numPlugIns`<br>- `getNthPlugInName` |
| `Doc` object | - `author`<br>- `creationDate`<br>- `creationDate`<br>- `keywords`<br>- `modDate`<br>- `numTemplates`<br>- `producer`<br>- `title`<br>- `getNthTemplate`<br>- `spawnPageFromTemplate` |
| `Field` object | `hidden` |
| `TTS` object | `soundCues`<br>\* `speechCues` |

### Modified in Acrobat 5.05

- A new symbol was added to the quick bar denoting which methods are missing from Acrobat Approval.
- In the `Doc` object, the property `disclosed` was added.

### Modified in Adobe Reader 5.1

Access to the following properties and methods was changed for the Adobe 5.1 Reader:

|  |  |
| --- | --- |
| `Annotation` object | properties:<br><br>- `alignment`<br>- `AP`<br>- `arrowBegin`<br>- `arrowEnd`<br>- `author`<br>- `contents`<br>- `doc`<br>- `fillColor`<br>- `hidden`<br><br>methods:<br><br>- `destroy`<br>- `getProps`<br>- `setProps`<br>- `modDate`<br>- `name`<br>- `noView`<br>- `page`<br>- `point`<br>- `points`<br>- `popupRect`<br>- `print`<br>- `rect`<br>- `readOnly`<br>- `rotate`<br>- `strokeColor`<br>- `textFont`<br>- `type`<br>- `soundIcon`<br>- `width` |
| `Doc` object | properties:<br><br>- `selectedAnnots`<br><br>methods:<br><br>- `addAnnot`<br>- `addField`<br>- `exportAsFDF`<br>- `exportAsXFDF`<br>- `getAnnot`<br>- `getAnnots`<br>- `getNthTemplate`<br>- `importAnFDF`<br>- `importAnXFDF`<br>- `importDataObject`<br>- `mailDoc`<br>- `mailForm`<br>- `spawnPageFromTemplate`<br>- `submitForm`<br>- `syncAnnotScan` |
| `Template` object | methods:<br><br>- `spawn` |
