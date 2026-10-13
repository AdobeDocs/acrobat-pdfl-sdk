# Security and Signature APIs

<a id="79993"></a>
<a id="security"></a>
<a id="id925"></a>
## security

The `security` object is a static JavaScript object that exposes security-related PDF functions such as encryption and digital signatures. Security functions are performed using a `SecurityHandler` object, which is obtained from the `security` object using the `getHandler` method.

> **Note**
>
> The `security` object is available without restriction, including in Adobe Reader. The methods and properties of the `security` object can only be executed during batch, console or application initialization events including in Adobe Reader, except where otherwise stated. See also priv. The event object contains a discussion of JavaScript events.

<a id="66342"></a>
<a id="security-constants"></a>
<a id="id926"></a>
### security constants

Beginning with Acrobat 7.0, several convenience strings are defined within the security object. The constants are held as properties of the wrapper objects listed below.

<a id="75621"></a>
**HandlerName object**

These are constants used when determining which handler to use.

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `StandardHandler` | String | R | This value can be specified in the `handler` property for a `SecurityPolicy` object that is based on the Standard (password-based) security handler. |
| `PPKLiteHandler` | String | R | This value can be specified in the `handler` property for a `SecurityPolicy` object that is based on the PPKLite (certificate-based) security handler. This value can also be passed to `security.getHandler` to create a new security context. |
| `APSHandler` | String | R | This the value specified in the `handler` property for a `SecurityPolicy` object that is based on the Adobe Policy Server security handler. This value can also be passed to `security.getHandler` to create a new security context. |

Example: The constant (string) `security.StandardHandler` is used to specify the `handler` property of the `SecurityPolicy` object.

```
security.getHandler(security.PPKLiteHandler, true);
```

<a id="60135"></a>
**EncryptTarget Object**

These constants are used when determining what data a policy is encrypting. They can be used in the `target` property of the `SecurityPolicy` object.

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `EncryptTargetDocument` | String | R | The Security Policy encrypts the entire document when applied. |
| `EncryptTargetAttachments` | String | R | The Security Policy encrypts only the file attachments embedded within the document. This means the document can be opened, but attachments cannot be opened without providing the correct security authentication. It is used for eEnvelope workflows. |

Example:

```
var filterOptions = { target: security.EncryptTargetAttachments };
security.chooseSecurityPolicy( { oOptions: filterOptions } );
```

<a id="security-properties"></a>
<a id="id927"></a>
### security properties

<a id="27159"></a>
<a id="handlers"></a>
<a id="id928"></a>
#### handlers

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Array | R |

An array containing the language-independent names of the available security handlers that can be used for encryption or signatures.

See also getSecurityPolicies.

The following information applies to different versions of Acrobat:

- Beginning with Acrobat 6.0, access to this property is unrestricted, to allow querying to see which handlers are available.
- In Acrobat 6.0, this call returned three handlers, Adobe.PPKLite, Adobe.PPKMS, and Adobe.AAB. Starting with Acrobat 7.0, all the functionality provided by Adobe.PPKMS has been rolled into Adobe.PPKLite, and Adobe.PPKMS is no longer available as a separate handler.
- Beginning with Acrobat 7.0, a new handler is available, Adobe.APS. This handler is used for authentication prior to calling any of the methods `encryptUsingPolicy`, `getSecurityPolicies`, or `chooseSecurityPolicy`. It has no other valid usage currently.
- Beginning with Acrobat 7.0, security constants are defined for each of the handlers. (Adobe.AAB is an exception. No constant was added because this handler will probably be deprecated in the near future.) These constants should be used when creating a new handler instance with `getHandler` or comparing against the handlers list.

Example: Get the list of security handlers available on this system:

```
for ( var i=0; i < security.handlers.length; i++ )

     console.println(security.handlers[i])
```

The output to the console might be

```
Adobe.APS
Adobe.PPKLite
Adobe.PPKMS
Adobe.AAB
```

<a id="78307"></a>
<a id="validatesignaturesonopen"></a>
<a id="id929"></a>
#### validateSignaturesOnOpen

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | Yes | Not allowed in Reader: Only available in Acrobat products | Boolean | R/W |

Gets or sets the user-level preference that causes signatures to be automatically validated when a document is opened.

> **Note**
>
> The property can be used to get in all situations, but can only set new values during a batch, console, or application initialization event. See priv.

<a id="security-methods"></a>
<a id="id930"></a>
### security methods

<a id="42796"></a>
<a id="chooserecipientsdialog"></a>
<a id="id931"></a>
#### chooseRecipientsDialog

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Opens a dialog box that allows a user to choose a list of recipients. Returns an array of generic Group objects that can be used when encrypting documents or data using either `encryptForRecipients` or `addRecipientListCryptFilter` methods of the Doc.

> **Note**
>
> Can be executed only during a console, menu, or application initialization event. See priv.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oOptions` | A `DisplayOptions` object containing the parameters for the display options. |

**Returns**

An array of `Group` objects.

See the Doc encryptForRecipients method for a description of the `Group` object.

<a id="67259"></a>
**DisplayOptions object**

The DisplayOptions object contains the following properties.

| Property | Description |
|----------|-------------|
| `bAllowPermGroups` | Controls whether permissions can be set for entries in the recipient list. Default value is `true`. |
| `bPlaintextMetadata` | If this property is specified, a check box is displayed to allow a user to select whether metadata is plaintext or encrypted. Its default value is the value of this property (`true` or `false`).   If this property is not specified, the check box is not shown. |
| `cTitle` | The title to be displayed in the dialog box. The default is “Choose Recipients”. |
| `cNote` | A note to be displayed in the dialog box. The default is not to show any note. |
| `bAllowImportFromFile` | Specifies whether the option is displayed that allows a user to import recipients from a file. The default value is `true`. |
| `bRequireEncryptionCert` | If `true`, recipients will be required to include an encryption certificate. The default value is `true`. |
| `bRequireEmail` | If `true`, recipients will be required to include an email address. The default value is `false`. |
| `bUserCert` | If `true`, the user will be prompted to provide his or her own certificate so that he or she can be included in the list of recipients. Setting this flag to `true` results in a prompt but does not require that the user provide a certificate. |

Example 1: Retrieve groups with permissions

```
var oOptions = {
    bAllowPermGroups: true,
    bPlaintextMetadata: false,
    cTitle: "Encrypt and Email",
    cNote: "Select recipients",
    bAllowImportFromFile: false,
    bRequireEncryptionCert: true,
    bRequireEmail: true
};
var groupArray = security.chooseRecipientsDialog( oOptions );
console.println("Full name = " + groupArray[0].userEntities[0].fullName);
```

Example 2: Get a list of recipients for which to encrypt data and email the document.

```
var oOptions = { bAllowPermGroups: false,
    cNote: "Select the list of recipients. "
    + "Each person must have both an email address and a certificate.",
    bRequireEmail: true,
    bUserCert: true
};
var oGroups = security.chooseRecipientsDialog( oOptions );
// Display the list of recipients in an alert
// Build an email "to" mailList
var numCerts = oGroups[0].userEntities.length;
var cMsg = "The document will be encrypted for the following:n";
var mailList = new Array;
for( var g=0; g<numCerts; ++g )
{
    var ue = oGroups[0].userEntities[g];
    var oCert = ue.defaultEncryptCert;
    if( oCert == null )
        oCert = ue.certificates[0];
    cMsg += oCert.subjectCN + ", " + ue.email + "n";
    var oRDN = oCert.subjectDN;
    if( ue.email )
    {
        mailList[g] = ue.email;
    }
    else
        if ( oRDN.e )
        {
            mailList[g] = oRDN.e;
        }
}
var result = app.alert( cMsg );
```

Example 3: List all the entries in an array of groups.

```
var  groups = security.chooseRecipientsDialog( oOptions );
for( g in groups ) {
    console.println( "Group No. " + g );
    // Permissions
    var perms = groups[g].permissions;
    console.println( "Permissions:" );
    for(p in perms) console.println( p + " = " + eval("perms." +p));
    // User Entities
    for( u in groups[i].userEntities ) {
    var user = groups[g].userEntities[u];
    console.println( "User No. " + u );
    for(i in user) console.println( i + " = " + eval("user." +i));
    }
}
```

<a id="20074"></a>
<a id="choosesecuritypolicy"></a>
<a id="id932"></a>
#### chooseSecurityPolicy

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | Not available in Reader |

Displays a dialog box to allow a user to choose from a list of security policies, filtered according to the options.

> **Note**
>
> Can be executed only during a batch, console, or application initialization event. See priv. This method will display UI.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oOptions` | (optional) A SecurityPolicyOptions object containing the parameters used for filtering the list of security policies returned. If not specified, all policies found are displayed. |

**Returns**

**Returns** a single SecurityPolicy object or `null` if the user cancelled the selection.

Example: Choose a policy and display the name.

```
var options = { cHandler: security.APSHandler };
var policy = security.chooseSecurityPolicy( options );
console.println("The policy chosen was: " + policy.name);
```

- `security.APSHandler` is one of the security constants.

<a id="82432"></a>
<a id="exporttofile"></a>
<a id="id933"></a>
#### exportToFile

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Exports a `Certificate` object to a local disk as a raw certificate file.

> **Note**
>
> Data being written must be data for a valid certificate; arbitrary data types cannot be written. This method will not overwrite an existing file.

See also `security.` importFromFile.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oObject` | The `Certificate` object that is to be exported to disk. |
| `cDIPath` | The device-independent save path.  -  The parameter `cDIPath` must be a safe path (see safe) and must end with the extension `.cer`. |

**Returns**

The path of the file that was written, if successful.

Example:

```
var outPath = security.exportToFile(oCert, "/c/outCert.cer");
```

<a id="71913"></a>
<a id="gethandler"></a>
<a id="id934"></a>
#### getHandler

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | All |

Obtains a `SecurityHandler` object. The caller can create as many new engines as desired and each call to `getHandler` creates a new engine. However, there is only one UI engine.

> **Note**
>
> This method is available from batch, console, and app initialization events. See priv.

**Backward Compatibility**: Because Adobe.PPKMS is no longer available as a separate handler starting with Acrobat 7.0, invoking `getHandler` with `cName` as “Adobe.PPKMS” returns the engine associated with Adobe.PPKLite handler.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The language-independent name of the security handler, as returned by the `handlers` property.  (Acrobat 7.0) Beginning with Acrobat 7.0, constant strings are defined for each of the valid handlers. See security constants, in particular the HandlerName object object. |
| `bUIEngine` | (optional) If `true`, the method returns the existing security handler instance that is associated with the Acrobat user interface (so that, for example, a user can log in through the user interface). If `false` (the default), returns a new engine. |

**Returns**

The `SecurityHandler` object specified by `cName`. If the handler is not present, returns a `null` object.

Example: Select the Adobe.PPKLite SecurityHandler.

```
// Validate signatures on open
security.validateSignaturesOnOpen = true;

// List all available signature handlers
var a = security.handlers;
for (var i = 0; i < a.length; i++)
    console.println("a["+i+"] = "+a[i]);

// Use "Adobe.PPKLite" handler engine for the UI
var ppklite = security.getHandler(
    security.PPKLiteHandler, true);
// Log in
ppklite.login("dps017", "/C/profiles/DPSmith.pfx");
```

See also the example following signatureSign for a continuation of this example.

<a id="45284"></a>
<a id="getsecuritypolicies"></a>
<a id="id935"></a>
#### getSecurityPolicies

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | Not available in Reader |

**Returns** the list of security policies currently available, filtered according to the options specified. The master list of security policies will be updated prior to filtering. The default `SecurityHandler` objects are used to retrieve the latest policies. If no policies are available or none meet the filtering restrictions, `null` will be returned.

> **Note**
>
> You may be able to retrieve more policies by calling `login` on the default SecurityHandler objects before calling this function.

Can be executed only during a console or application initialization event. Not available in Adobe Reader.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `bUI` | (optional) A flag controlling whether UI can be displayed.  Default value is `false`. |
| `oOptions` | (optional) A `SecurityPolicyOptions` object containing the parameters used for filtering the list of security policies returned. If not specified, all policies found are returned. |

**Returns**

An array of `SecurityPolicyOptions` objects or `null`.

<a id="95227"></a>
**SecurityPolicyOptions object**

The SecurityPolicyOptions object has the following properties:

| Property | Description |
|----------|-------------|
| `bFavorites` | If not passed, policies are not filtered based on whether a policy is a Favorite. If `true`, only policies that are Favorites are returned. If `false`, only policies that are not Favorites are returned. |
| `cHandler` | If not passed, policies are not filtered based on security filter. If defined, only policies that match the specified security filter are returned. The valid values are defined in security Constants (see the HandlerName object). Only a single value can be passed. |
| `cTarget` | If not defined, policies are not filtered based on the target. If defined, only policies that match the specified target are returned. The valid values are defined in the `EncryptTarget` object of security constants. Only a single value can be passed. |

Example 1: Retrieve the list of favorite PPKLite policies and display the names. This example uses `security.PPKLiteHandler` (see security constants).

```
var options = { bFavorites:true, cHandler:security.PPKLiteHandler };
var policyArray = security.getSecurityPolicies( { oOptions: options } );
for( var i = 0; i < policyArray.length; i++)
    console.println( policyArray[i].name );
```

Example 2: Force the login, retrieve the list of APS policies, and display the names. This example uses `security.APSHandler` (see security constants).

```
var aps = security.getHandler( security.APSHandler, true );
aps.login();
var options = { cHandler: security.APSHandler };
var policyArray = security.getSecurityPolicies({
    bUI: true,
    oOptions: options });
for(var i = 0; i < policyArray.length; i++)
    console.println( policyArray[i].name );
```

<a id="36368"></a>
<a id="importfromfile"></a>
<a id="id936"></a>
#### importFromFile

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Reads a raw data file and returns the data as an object with a type specified by `cType`. The file being imported must be a valid certificate. See also `security.` exportToFile

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cType` | The type of object to be returned by this method. The only supported type is “Certificate”. |
| `cDIPath` | (optional) When `bUI` is `false`, this parameter is required and specifies the device-independent path to the file to be opened.   If `bUI` is `true`, this is the seed path used in the open dialog box. |
| `bUI` | (optional) `true` if the user should be prompted to select the file that is to be imported. The default is `false`. |
| `cMsg` | (optional) If `bUI` is `true`, the title to use in the open dialog box. If `cMsg` is not specified, the default title is used. |

**Returns**

A `Certificate` object.

Example:

```
var oMyCert = security.importFromFile("Certificate", "/c/myCert.cer");
```

<a id="14320"></a>
<a id="importsettings"></a>
<a id="id937"></a>
#### importSettings

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 9.1 | No | Yes | Not available in Reader |

Allows limited functionality similar to Preferences > Security panel > Security Settings > Import, but it imports settings from an embedded file. This allows you to import digital IDs from an attached acrobat security settings file triggered by a button click from the containing document. Only digital IDs can be imported using this method, and other security settings, including trust settings, cannot be modified using this method. This method can only be triggered from a console, batch, or field mouse up event.

To create a file that can be embedded for this script, export the settings using Preferences > Security panel > Security Settings > Export. In the example below, if the script is attached to a button click event and the document represented by `this` is correctly formed, when the button is clicked it will bring up a simple import dialog for digital IDs.

> **Note**
>
> Security settings files must be certified in order to be considered valid.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oDocObj` | The object that represents the document, usually denoted by `this` in the context of running a script. |
| `cFilename` | The file name of the embedded file in `oDocObj` that contains a security settings file. A practical limit on the length of the file name is enforced. If the name is too long the import will fail. |
| `bSimplifiedUI` | `true` if a simplified user interface is to be used (if possible), `false` otherwise. For digital IDs, a simplified user interface can be displayed if only a single ID is imported. If there is more than one ID or `bSimplifiedUI` is `false`, then a list of IDs is shown instead. |

**Returns**

The number of digital IDs installed, or -1 if cancelled.

Example:

```
security.importSettings(this, "ids.acrobatsecuritysettings", true);
```

<a id="25690"></a>
<a id="securityhandler"></a>
<a id="id938"></a>
## SecurityHandler

SecurityHandler objects are used to access security handler capabilities such as signatures, encryption, and directories. Different security handlers have different properties and methods. This section documents the full set of properties and methods that security objects may have. Individual SecurityHandler objects may or may not implement these properties and methods.

SecurityHandler objects can be obtained using the `security.getHandler` method.

The JavaScript interface for Adobe.PPKLite signatures was introduced in Acrobat 5.0, and the remainder of the JavaScript interface was introduced in Acrobat 6.0. Prior to Acrobat 6.0, there was no support in Acrobat to enable JavaScript in third-party security handlers.

Not all security handlers are JavaScript-enabled. Not all JavaScript enabled handlers are enabled for all security operations. Third-party public key security handlers may support JavaScript, but only if they use the new *PubSec* programming interface that was introduced in Acrobat 6.0.

JavaScript-enabled handlers provided by Adobe include:

- The Adobe.PPKLite security handler supports signatures and encryption. On the Windows operating system, it provides directory access through the Microsoft Active Directory Scripting Interface (ADSI).
- The Adobe.AAB security handler provides a local address book and support for directory operations.

> **Note**
>
> The Standard security handler, used for password encryption of documents, is not JavaScript-enabled in general. However, starting with Acrobat 7.0, encryption using Standard security is possible using predefined policies. See encryptUsingPolicy for more details.

Also starting with Acrobat 7.0, the Adobe.APS handler can be used for encryption with the `encryptUsingPolicy` method. This handler also makes a directory available through the directory services, but because no certificates are returned from this directory, it is of limited general use.

> **Note**
>
> SecurityHandler objects can only be created using the `Security` object `getHandler` method. This method is available only for batch, console, and application initialization events (see priv for details) and is available in Adobe Reader.

<a id="securityhandler-properties"></a>
<a id="id939"></a>
### SecurityHandler properties

<a id="84619"></a>
<a id="appearances"></a>
<a id="id940"></a>
#### appearances

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | Array | R |

An array containing the language-dependent names of the available user-configured appearances for the specified security handler. Appearances are used to create the on-page visual representation of a signature when signing a signature field. The name of an appearance can be specified as a signature info object property when signing a signature field using the Field object `signatureSign` method.

Acrobat provides a standard signature appearance module that is used by Adobe signature plug-ins and that can also be used by third-party signature plug-ins. This standard signature appearance module is preconfigured with one appearance and can be configured by users to contain more appearances. The name of the one pre-configured appearance, called *Standard Text* in the user interface, is not returned by this property.

If a security handler does not support selection of appearances, this property will return null.

<a id="69297"></a>
<a id="digitalids"></a>
<a id="id941"></a>
#### digitalIDs

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Object | R |

The certificates that are associated with the currently selected digital IDs for this security handler.

The return value is a generic object with the following properties:

| Property | Type | Version (Key) | Description |
|----------|------|---------------|-------------|
| `oEndUserSignCert` | `Certificate` object | 6.0 | The certificate that is associated with the currently selected digital IDs that is to be used by this SecurityHandler object when signing. The property is undefined if there is no current selection. |
| `oEndUserCryptCert` | `Certificate` object | 6.0 | The certificate that is associated with the currently selected digital IDs that is to be used when encrypting a document with this SecurityHandler object. The property is undefined if there is no current selection. |
| `certs` | Array of *Certificate* objects | 6.0 | An array of certificates corresponding to the list of all digital IDs that are available for this SecurityHandler object. |
| `stores` | Array of Strings | 6.0 | An array of strings, one for every `Certificate` object, identifying the store where the digital ID is stored. The string values are up to the security handler. For *Adobe.PPKLite* the valid values are ‘PKCS12’ and ‘MSCAPI’. |

The Adobe.PPKLite security handler returns all currently available digital IDs present in Password-protected digital ID files (both PKCS#12 and APF) and, on Windows, IDs present in the Windows (MSCAPI) store.

Both `oEndUserSignCert` and `oEndUserCryptCert` properties can be set using the user-interface. `oEndUserSignCert` can also be set using the `login` method. This means that `oEndUserCryptCert` will only be returned when using a Security Handler object that is obtained using the `getHandler` method with `bUIEngine` set to `true`.

Example: Export to a file the certificate that is associated with the currently selected digital IDs.

```
var sh = security.getHandler( "Adobe.PPKMS", true );
var ids = sh.digitalIDs;
var oCert = ids.oEndUserSignCert;
security.exportToFile( oCert, "/c/MySigningCert.cer" );
```

<a id="57042"></a>
<a id="directories"></a>
<a id="id942"></a>
#### directories

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Array | R |

An array of the available `Directory` objects for this Security Handler. New `Directory` objects can be created using the `newDirectory` method.

<a id="53498"></a>
<a id="directoryhandlers"></a>
<a id="id943"></a>
#### directoryHandlers

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Array | R |

An array containing the language-independent names of the available directory handlers for the specified security handler. For example, the Adobe.PPKMS security handler has a directory handler named Adobe.PPKMS.ADSI that supports queries using the *Microsoft Active Directory Script Interface* (ADSI). Valid directory handler names are required when activating a new `Directory` object using its `info` property.

<a id="33360"></a>
<a id="docdecrypt"></a>
<a id="id944"></a>
#### docDecrypt

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

**Returns** `true`, if the security handler is capable of decrypting PDF files.

<a id="32731"></a>
<a id="docencrypt"></a>
<a id="id945"></a>
#### docEncrypt

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

**Returns** `true`, if the security handler is capable of encrypting PDF files.

<a id="99723"></a>
<a id="isloggedin"></a>
<a id="id946"></a>
#### isLoggedIn

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | Boolean | R |

**Returns** `true` if currently logged into this `SecurityHandler` object. See the login method.

Different security handlers will have their own rules for determining the value of this property. The *Adobe.PPKLite* handler will return `true` if a user is logged in to a profile file (also called credential file, implemented as a PKCS#12 file). Adobe.PPKMS will always return `true`.

Example: Generic script to illustrate `isLoggedIn`.

```
var ppklite = security.getHandler("Adobe.PPKLite", true);
console.println( "Is logged in = " + ppklite.isLoggedIn ); // False
ppklite.login( "dps017", "/C/signatures/DPSmith.pfx");
console.println( "Is logged in = " + ppklite.isLoggedIn ); // True
```

<a id="43875"></a>
<a id="id947"></a>
<a id="id948"></a>
#### loginName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | String | R |

The name associated with the actively selected signing digital ID for the security handler. This may require that the `login` method be called to select a signing credential. The return value is `null` if a signing credential is not selected or if the security handler does not support this property.

<a id="63004"></a>
<a id="loginpath"></a>
<a id="id949"></a>
#### loginPath

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | String | R |

The device-independent path to the user’s profile file used to log in to the security handler. The return value is null if no one is logged in, if the security handler does not support this property, or if this property is irrelevant for the currently logged in user.

<a id="51304"></a>
<a id="id950"></a>
<a id="id951"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | String | R |

The language-independent name of the security handler. Example values for the Default Certificate, Windows Certificate, and Entrust Security Handlers are *Adobe.PPKLite*, Adobe.PPKMS, and *Entrust.PPKEF*. All security handlers must support this property.

<a id="42384"></a>
<a id="signauthor"></a>
<a id="id952"></a>
#### signAuthor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

Specifies whether the security handler is capable of generating certified documents. A certified document is signed with both a byte-range signature and an object signature. Object signatures, which are generated by traversing the document’s object tree, are used to detect and prevent modifications to a document. See the `mdp` property of the SignatureInfo object for details regarding modification detection and prevention (MDP) settings.

<a id="67664"></a>
<a id="signfdf"></a>
<a id="id953"></a>
#### signFDF

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

Indicates that the security handler is capable of signing FDF files.

<a id="18752"></a>
<a id="signinvisible"></a>
<a id="id954"></a>
#### signInvisible

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | Boolean | R |

Specifies whether the security handler is capable of generating invisible signatures.

<a id="44220"></a>
<a id="signvalidate"></a>
<a id="id955"></a>
#### signValidate

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

Indicates whether the security handler is capable of validating signatures.

<a id="31575"></a>
<a id="signvisible"></a>
<a id="id956"></a>
#### signVisible

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | Boolean | R |

Specifies whether the security handler is capable of generating visible signatures.

<a id="13603"></a>
<a id="id957"></a>
<a id="id958"></a>
#### uiName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | String | R |

The language-dependent string for the security handler. This string is suitable for user interfaces. All security handlers must support this property.

<a id="51812"></a>
<a id="validatefdf"></a>
<a id="id959"></a>
#### validateFDF

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

**Returns** `true`, if the security handler is capable of validating signatures over FDF files.

<a id="securityhandler-methods"></a>
<a id="id960"></a>
### SecurityHandler methods

<a id="75651"></a>
<a id="login"></a>
<a id="id961"></a>
#### login

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | All |

Provides a mechanism by which digital IDs can be accessed and selected for a particular Security Handler. Through the user interface, a default digital ID can be selected that persists either eternally or for as long as the application is running. If such a selection has been made through the UI, it might not be necessary to log into a Security Handler prior to using the digital ID.

**Parameters**  tend to be specific to a particular handler. The behavior for Adobe.PPKLite and Adobe.PPKMS handlers is specified below.

The parameters `cPassword` and `cDIPath` are provided for backward compatibility, or they can be included as properties of the `oParams` object. This latter method is the preferred calling convention beginning in Acrobat 6.0.

See also logout, newUser, and loginName.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cPassword` | (optional, Acrobat 5.0) The password necessary to access the password-protected digital ID. This parameter is supported by Adobe.PPKLite for accessing digital ID files and PKCS#11 devices. |
| `cDIPath` | (optional, Acrobat 5.0) A device-independent path to the password-protected digital ID file or a PKCS#11 library. This parameter is supported by Adobe.PPKLite. |
| `oParams` | (optional, Acrobat 6.0) A `LoginParameters` object with parameters that are specific to a particular `SecurityHandler` object. The common fields in this object are described below. These fields include the `cDIPath` and `cPassword` values, thus allowing the parameter list to be expressed in different ways. |
| `bUI` | (optional, Acrobat 6.0) Set to `true` if the user interface should be used to log the user in. If set to `false`, the default engine associated with the user interface is not used and the logged in state for the digital ID is not shown in the Security Settings dialog box. This attribute should be supported by all security handlers that support this method. |

**Returns** `true` if the login succeeded, `false` otherwise.

<a id="81900"></a>
**LoginParameters Object**

This generic JavaScript object contains parameters for the `login` method. It has the following properties:

| Property | Type | Version (Key) | Description |
|----------|------|---------------|-------------|
| `cDIPath` | String | 5.0 | The path to a file that contains the digital ID or a PKCS#11 library. Supported by Adobe.PPKLite security handler. |
| `cPassword` | String | 6.0 | A password that is used to authenticate the user. This password may be used to access a password-protected digital ID file or a PKCS#11 device. Supported by Adobe.PPKLite security handler. Note that Acrobat does not guarantee that this password is obfuscated in memory. |
| `cPFX` | String | 7.0 | (optional) A hex-encoded PFX to log in to. If this parameter is specified, it takes precedence over `cDIPath`.  This parameter is only used internally. Currently, there is no way to retrieve a hex encoded PFX file through JavaScript. |
| `oEndUserSignCert` | generic  object | 6.0 | Selects a digital ID for the purpose of performing end-user signing. The value of this property is a `Certificate` object (or a generic object with the same property names as a `Certificate` object), which defines the certificate that is being selected.  It may not be necessary to call this method for a particular handler. For example, if logged in to a PKCS#12 file containing one signing digital ID with Adobe.PPKLite, a signing credential does not need to be selected. All security handlers must be able to process the binary and SHA1Hash properties of this object. This object can be empty if `bUI` is `true`. |
| `cMsg` | String | 6.0 | A message to display in the login dialog box, if `bUI` is `true`. |
| `cURI` | String | 7.0 | URI used to connect to a server. Supported by Adobe.APS and Adobe.PPKLite handlers. In the case of Adobe.PPKLite, the URI specifies a Roaming Credential server. |
| `cUserId` | String | 7.0 | User name used when connecting to a server. Supported by the Adobe.APS and Adobe.PPKLite handlers. |
| `cDomain` | String | 7.0 | Domain name used when connecting to a server. Only supported by the Adobe.APS handler. |
| `iSlotID` | Integer | 7.0 | Specifies the slot ID of a PKCS#11 device to log into. This parameter is supported by the Adobe.PPKLite handler only. |
| `cTokenLabel` | String | 7.0 | Specifies the token label of a PKCS#11 device to log into. This parameter is supported by the Adobe.PPKLite handler only. |

Example 1: Log in and log out.

```
// Use the "Adobe.PPKLite" security handler object for the UI
var ppklite = security.getHandler( security.PPKLiteHandler, true );
var oParams = { cPassword: "dps017", cDIPath: "/C/DPSmith.pfx" }
ppklite.login( oParams );
<...
.. make a signature field and sign it ......>
ppklite.logout();
```

Use UI to select a credential, when already logged in.

```
ppklite.login(
{ oParams:
    { oEndUserSignCert: {},

     cMsg: "Select your Digital ID" },
    bUI : true
} );
```

Log in and select the signing credentials

```
var oCert = { SHA1Hash: "00000000" };
ppklite.login(
{ oParams:
    { cDIPath: "/C/test/DPSmith.pfx",

         cPassword: "dps017",
        oEndUserSignCert: oCert,
        cMsg: "Select your Digital ID"
    },

 bUI : true
});
```

Example 2: Use the “Adobe.PPKMS” security handler object, and select the credentials to use when signing.

```
var ppkms = security.getHandler( "Adobe.PPKMS" );
var oCert = myCerts[0];
ppkms.login( { oParams: { oEndUserSignCert: oCert } } );
```

Example 3: Use `security.APSHandler`, see security constants.

```
var aps = security.getHandler( security.APSHandler, true );
var oParams = { cUserName: "Acrobat", cPassword: "adobedon" };
aps.login( oParams );
<...
.. encrypt a document using this handle and a policy id .....>
aps.logout();
```

See signatureSign for details on signing a PDF document.

<a id="95399"></a>
<a id="logout"></a>
<a id="id962"></a>
#### logout

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | All |

Logs out for the `SecurityHandler` object. This method is used by Adobe.PPKLite, not by *Adobe.PPKMS*.

Also see the login method.

**Returns**

Beginning in Acrobat 6.0, returns `true` if the logout succeeded, `false` otherwise. Previous Acrobat releases did not generate a return value.

<a id="36849"></a>
<a id="newdirectory"></a>
<a id="id963"></a>
#### newDirectory

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | P | Yes | All |

**Returns** a new Directory object. This object must be activated using its `info` property before it is marked for persistence and before it can be used for searches. Existing directory objects can be discovered using the directories property.

**Returns**

A new `Directory` object

<a id="96919"></a>
<a id="newuser"></a>
<a id="id964"></a>
#### newUser

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | All |

Supports enrollment with Adobe.PPKLite and Adobe.PPKMS security handlers by creating a new self-sign credential.

> **Note**
>
> This method will not allow the user to overwrite an existing file.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cPassword` | (optional) The password necessary to access the password-protected digital ID file. This parameter is ignored by Adobe.PPKMS. |
| `cDIPath` | (optional) The device-independent path to the password-protected digital ID file. This parameter is ignored by Adobe.PPKMS.  -  Beginning with Acrobat 6.0, the parameter `cDIPath` must be a safe path (see safe) and end with the extension `.pfx`. |
| `oRDN` | The relative distinguished name (RDN) as an RDN object, containing the issuer or subject name for a certificate. The only required field is `cn`. If the country `c` is provided, it must be two characters, using the ISO 3166 standard (for example, “US”). |
| `oCPS` | (optional, Acrobat 6.0) A generic object containing certificate policy information that will be embedded in the Certificate Policy extension of the certificate. The object has these properties:  -  `oid` is required and indicates the certificate policy object identifier. -  `url` (optional) is a URL that points to detailed information about the policy under which the certificate has been issued -  `notice` (optional) is an abridged version of the information, embedded in the certificate. |
| `bUI` | (optional, Acrobat 6.0) If `true`, the user interface can be used to enroll. This parameter is supported by all security handlers that support this method. |
| `cStore` | (optional, Acrobat 7.0) A string identifying the store where the generated credential has to be stored. For the Adobe.PPKLite security handler, the valid store identifiers are “PKCS12” and “MSCAPI”. If this parameter is omitted and `cDIPath` is provided, the generated credential is stored in a PKCS#12 file, else it is stored in the CAPI store. |

**Returns**

`true` if successful, throws an exception if not successful.

Example 1: Create a new PPKLite self-sign credential (Acrobat 5.0 syntax)

```
var ppklite = security.getHandler(security.PPKLiteHandler);
var oRDN = { cn: "Fred NewUser", c: "US" };
var oCPS = {oid: "1.2.3.4.5",
    url: "http://www.example.com/mycps.html",
    notice: "This is a self generated certificate, hence the "
        + "recipient must verify it's authenticity through an out "
        + "of band mechanism" };
ppklite.newUser( "testtest", "/d/temp/FredNewUser.pfx", oRDN, oCPS);

// Alternate generic object syntax, allowing additional parameters
var oParams = {
    cPassword : "myPassword",
    cDIPath : "/d/temp/FredNewUser.pfx",
    oRDN : oRDN,
    oCPS : oCPS,
    bUI : false
};
ppklite.newUser( oParams );
```

Example 2: Use a certificate from an existing signed field to create the RDN

```
var f = this.getField( "mySignature" );
f.signatureValidate();
var sigInfo = f.signatureInfo();
var certs = sigInfo.certificates;
var oSubjectDN = certs[0].subjectDN;

ppklite.newUser({
    cPassword: "dps017",
    cDIPath: "/c/temp/DPSmith.pfx",
    oRDN: oSubjectDN
});
```

<a id="11628"></a>
<a id="setpasswordtimeout"></a>
<a id="id965"></a>
#### setPasswordTimeout

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | All |

Sets the number of seconds after which password should expire between signatures. This method is only supported by the Adobe.PPKLite security handler. For this handler the default timeout value for a new user is 0 (password always required).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cPassword` | The password needed to set the timeout value. |
| `iTimeout` | The timeout value, in seconds. Set to 0 for always expire (that is, password always required). Set to 0x7FFFFFFF for never expire. |

**Returns**

Throws an exception if the user has not logged in to the Adobe.PPKLite security handler, or unsuccessful for any other reason.

Example: This example logs in to the *PPKLite* security handler and sets the password timeout to 30 seconds. If the password timeout has expired—30 seconds in this example—the signer must provide a password. The password is not necessary if the password has not timed out.

```
var ppklite= security.getHandler( "Adobe.PPKLite" );
ppklite.login( "dps017", "/d/profiles/DPSmith.pfx" );

 ppklite.setPasswordTimeout( "dps017", 30 );
```

<a id="30747"></a>
<a id="securitypolicy"></a>
<a id="id966"></a>
## SecurityPolicy

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | Not available in Reader |

The Security Policy object represents a group of security settings used to apply encryption to a document. It is acquired as the return value of both `getSecurityPolicies` and `chooseSecurityPolicy`.

<a id="77960"></a>
<a id="securitypolicy-properties"></a>
<a id="id967"></a>
### SecurityPolicy properties

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `policyID` | String | R | A generated string that uniquely identifies the Security Policy. It is not intended to be human-readable.  This may be set to a known policy ID on a newly created SecurityPolicy object to force any method using this policy to retrieve the correct security settings before applying the policy. |
| `name` | String | R | The policy name used in the UI. It may be localized. |
| `description` | String | R | The policy description used in the UI. It may be localized. |
| `handler` | String | R | An enumerated value representing the security handler implementing this Security Policy. The possible values are defined in the `HandlerName` object in security constants. |
| `target` | String | R | An enumeration value representing the target data to be encrypted. The possible values are defined in the `EncryptTarget` object in security constants. |

<a id="51916"></a>
<a id="id968"></a>
<a id="id969"></a>
## SignatureInfo

A generic JavaScript object that contains the properties of a digital signature. Some properties are supported by all handlers, and additional properties can be supported.

The SignatureInfo object is returned by the Field object methods `signatureValidate` and `signatureInfo` and is passed to the `FDF` object methods `signatureSign` and `signatureValidate`.

Writable properties can be specified when signing the object.

<a id="signatureinfo-properties"></a>
<a id="id970"></a>
### SignatureInfo properties

All handlers define the following properties.

| Property | Type | Access | Version (Key) | Description |
|----------|------|--------|---------------|-------------|
| `buildInfo` | Object | R | 6.0 | An object containing software build and version information for the signature. The format of this object is described in the technical note *PDF Signature Build Dictionary Specification*. |
| `date` | Date  object | R | 5.0 | The date and time that the signature was created, returned as a JavaScript Date object. |
| `dateTrusted` | Boolean | R | 7.0 | A Boolean value that indicates whether the date is from a trusted source. If this value is not present, the date should be assumed to be from an untrusted source (for example, the signer’s computer system time). |
| `digestMethod` | String | R/W | 8.0 | The digest method to be used for signing. For Acrobat 8, the valid values are `SHA1`, `SHA256`, `SHA384`, `SHA512` and `RIPEMD160`. It is important that the caller knows that a particular signature handler can support this digest method. |
| `handlerName` | String | R | 5.0 | The language-independent name of the security handler that was specified as the Filter attribute in the signature dictionary. It is usually the name of the security handler that created the signature, but can also be the name of the security handler that the creator wants to be used when validating the signature. |
| `handlerUserName` | String | R | 5.0 | The language-dependent name corresponding to the security handler specified by `handlerName`. It is available only when the named security handler is available. |
| `handlerUIName` | String | R | 5.0 | The language-dependent name corresponding to the security handler specified by `handlerName`. It is available only when the named security handler is available. |
| `location` | String | R/W | 5.0 | Optional user-specified location when signing. It can be a physical location (such as a city) or hostname. |
| `mdp` | String | R/W | 6.0 | The Modification Detection and Prevention (MDP) setting that was used to sign the field or `FDF` object being read, or the MDP setting to use when signing. Values are:  *allowNone allowAll default defaultAndComments*  See [Modification Detection and Prevention (MDP) Values](./security-signature-apis.md#64083) for details. The value of `allowAll`, the default, means that MDP is not used for the signature, resulting in this not being an certification signature. |
| `name` | String | R | 5.0 | Name of the user that created the signature. |
| `numFieldsAltered` | Number | R | 5.0 only | Deprecated. The number of fields altered between the previous signature and this signature. Used only for signature fields.  Beginning in Acrobat 7.0, the functionality offered by the Field object method signatureGetModifications should be used instead. |
| `numFieldsFilledIn` | Number | R | 5.0 only | Deprecated. The number of fields filled-in between the previous signature and this signature. Used only for signature fields.  Beginning in Acrobat 7.0, the functionality offered by the Field object method signatureGetModifications should be used instead. |
| `numPagesAltered` | Number | R | 5.0 only | Deprecated. The number of pages altered between the previous signature and this signature. Used only for signature fields.  Beginning in Acrobat 7.0, the functionality offered by the Field object method signatureGetModifications should be used instead. |
| `numRevisions` | Number | R | 5.0 | The number of revisions in the document. Used only for signature fields. |
| `reason` | String | R/W | 5.0 | The user-specified reason for signing. |
| `revision` | Number | R | 5.0 | The signature revision to which this signature field corresponds. Used only for signature fields. |
| `sigValue` | String | R | 7.0 | Raw bytes of the signature, as a hex encoded string. |
| `status` | Number | R | 5.0 | The validity status of the signature, computed during the last call to `signatureValidate`.  See the return codes of the status property in the table status and idValidity properties. |
| `statusText` | String | R | 5.0 | The language-dependent text string, suitable for user display, denoting the signature validity status, computed during the last call to the `signatureValidate`. |
| `subFilter` | String | R/W | 6.0 | The format to use when signing. Consult the [PDF Reference](https://adobe.com/go/pdfreference) for a complete list of supported values. The known values used for public key signatures include adbe.pkcs7.sha1, adbe.pkcs7.detached, and adbe.x509.rsa\_sha1. It is important that the caller know that a particular signature handler can support  this format. |
| `timeStamp` | String | W | 7.0 | The URL of the server for time-stamping the signature. The only schemes and transport protocols supported for fetching time stamps are http or https.  This property is write-only. If the signature is time stamped, during verification the property `dateTrusted` will be set to `true` (provided the time stamp signature is trusted) and the `verifyDate` and the signing date will be the same. |
| `verifyDate` | Date  object | R | 7.0 | The date and time that the signature was either signed or verified (if the signature was verified).  If the signature is signed with a timestamp, `verifyDate` should be the signing date; if the signature is signed without a timestamp, `verifyDate` will be the verifying date.  The property returns a JavaScript Date object. |
| `verifyHandlerName` | String | R | 6.0 | The language-independent name of the security handler that was used to validate this signature. This will be `null` if the signature has not been validated (that is, if the `status` property has a value of 1). |
| `verifyHandlerUIName` | String | R | 6.0 | The language-dependent name corresponding to the security handler specified by `verifyHandlerName`. This will be null if the signature has not been validated, that is, if the `status` property has a value of 1). |

<a id="40445"></a>
<a id="signatureinfo-object-public-key-security-handler-properties"></a>
<a id="id972"></a>
#### SignatureInfo object public key security handler properties

Public key security handlers may define the following additional properties:

| Property | Type | Access | Version (Key) | Description |
|----------|------|--------|---------------|-------------|
| `appearance` | String | W | 5.0 | The name of the user-configured appearance to use when signing this field. PPKLite and PPKMS use the standard appearance handler. In this situation, the appearance names can be found in the signature appearance configuration dialog box of the Security user preferences.  The default, when not specified, is to use the Standard Text appearance. Used only for visible signature fields. |
| `certificates` | Array | R | 5.0 | Array containing a hierarchy of certificates that identify the signer. The first element in the array is the signer’s certificate. Subsequent elements include the chain of certificates up to the certificate authority that issued the signer’s certificate. For self-signed certificates this array will contain only one entry. |
| `contactInfo` | String | R/W | 5.0 | The user-specified contact information for determining trust. For example, it can be a telephone number that recipients of a document can use to contact the author. This is not recommended as a scalable solution for establishing trust. |
| `byteRange` | Array | R | 6.0 | An array of numbers indicating the bytes that are covered by this signature. |
| `docValidity` | Number | R | 6.0 | The validity status of the document byte range digest portion of the signature, computed during the last call to `signatureValidate`. All PDF document signature field signatures include a byte range digest.  See Validity Values for details of the return codes. |
| `idPrivValidity` | Number | R | 6.0 | The validity of the identity of the signer. This value is specific to the handler. See Private Validity Values for values supported by the Adobe.PPKLite and Adobe.PPKMS handlers.  This value is 0 unless the signature has been validated, that is, if the `status` property has a value of 1. |
| `idValidity` | Number | R | 6.0 | The validity of the identity of the signer as number.  See the return codes of the `idValidity` property in the table status and idValidity properties. |
| `objValidity` | Number | R | 6.0 | The validity status of the object digest portion of the signature, computed during the last call to `signatureValidate`. For PDF documents, signature field certification signatures and document-level application rights signatures include object digests. All FDF files are signed using object digests.  See Validity Values for details of the return codes. |
| `revInfo` | Object | R | 7.0 | A generic object containing two properties: `CRL` and `OCSP`. These properties are arrays of hex-encoded strings, where each string contains the raw bytes of the revocation information that was used to carry out revocation checking of a certificate.  For `CRL`, the strings represent CRLs. For `OCSP`, the strings represents OCSP responses. These properties are populated only if the application preference to populate them is turned on, because this data can potentially get very large. |
| `trustFlags` | Number | R | 6.0 | The bits in this number indicate what the signer is trusted for. The value is valid only when the value of the status property is 4. These trust settings are derived from the trust setting in the recipient’s trust database, for example, the Acrobat Address Book (Adobe.AAB). Bit assignments are: * *1*: Trusted for signatures * *2*: Trusted for certifying documents * *3*: Trusted for dynamic content such as multimedia * *4*: Adobe internal use * *5*: The JavaScript in the PDF file is trusted to operate outside the normal PDF restrictions |
| `password` | String | W | 5.0 | A password required as authentication when accessing a private key that is to be used for signing. This may or may not be required, dependent on the policies of the security handler. |

<a id="71840"></a>
<a id="status-and-idvalidity-properties"></a>
<a id="id973"></a>
#### status and idValidity properties

The following table list the codes returned by the SignatureInfo Object, `status` and `idValidity` properties.

| Status code | Description |
|-------------|-------------|
| -1 | Not a signature field. |
| 0 | Signature is blank or unsigned. |
| 1 | Unknown status. This occurs if the signature has not yet been validated; for example, if the document has not completed downloading over a network connection. |
| 2 | Signature is invalid. |
| 3 | Signature is valid but the identity of the signer could not be verified. |
| 4 | Signature is valid and the identity of the signer is valid. |

<a id="40865"></a>
<a id="validity-values"></a>
<a id="id974"></a>
#### Validity Values

The following codes are returned by the `docValidity` and `objValidity` properties. (See SignatureInfo object public key security handler properties). They provide a finer granularity of the validity of the signature than the `status` property.

| Status code | Description |
|-------------|-------------|
| `kDSSigValUnknown` | Validity not yet determined. |
| `kDSSigValUnknownTrouble` | Validity could not be determined because of errors encountered during the validation process. |
| `kDSSigValUnknownBytesNotReady` | Validity could not be determined because all bytes are not available, for example, when viewing a file in a web browser. Even when bytes are not immediately available, this value may not be returned if the underlying implementation blocks when bytes are not ready. Adobe makes no commitment regarding whether validation checks will block or not block. However, the implementation in Acrobat 6.0 will block when validating `docValidity` and not block when validating `objValidity`. |
| `kDSSigValInvalidTrouble` | Validity for this digest was not computed because there were errors in the formatting or information contained in this signature. There is sufficient evidence to conclude that the signature is invalid. |
| `kDSSigValUnused` | The validity for this digest is not used (for example, no document validity if no byte range). |
| `kDSSigValJustSigned` | The signature was just signed, so it is implicitly valid. |
| `kDSSigValFalse` | The digest or validity is invalid. |
| `kDSSigValTrue` | The digest or validity is valid. |

<a id="13196"></a>
<a id="private-validity-values"></a>
<a id="id975"></a>
#### Private Validity Values

Verification of the validity of the signer’s identity is specific to the handler that is being used to validate the identity. This value may contain useful information regarding an identity. The identity is returned in the `idPrivValidity` property. Values for Adobe.PPKMS and Adobe.PPKLite security handlers are shown here. This value is also mapped to an `idValidity` value that is common across all handlers.

| Status Code | idValidity  Mapping | Security Handler | Description |
|-------------|---------------------|------------------|-------------|
| `kIdUnknown` | 1 (unknown) | PPKMS, PPKLite | Validity not yet determined. |
| `kIdTrouble` | 1 (unknown) | PPKMS,  PPKLite | Could not determine validity because of errors, for example, internal errors, or could not build the chain, or could not check basic policy. |
| `kIdInvalid` | 2 (invalid) | PPKMS,  PPKLite | Certificate is invalid: not time nested, invalid signature, invalid/unsupported constraints, invalid extensions, chain is cyclic. |
| `kIdNotTimeValid` | 2 (invalid) | PPKMS,  PPKLite | Certificate is outside its time window (too early or too late). |
| `kIdRevoked` | 2 (invalid) | PPKMS | Certificate has been revoked. |
| `kIdUntrustedRoot` | 1 (unknown) | PPKMS,  PPKLite | Certificate has an untrusted root certificate. |
| `kIdBrokenChain` | 2 (invalid) | PPKMS,  PPKLite | Could not build a certificate chain up to a self-signed root certificate. |
| `kIdPathLenConstraint` | 2 (invalid) | PPKLite | Certificate chain has exceeded the specified length restriction. The restriction was specified in Basic Constraints extension of one of the certificates in the chain. |
| `kIdCriticalExtension` | 1 (unknown) | PPKMS | One of the certificates in the chain has an unrecognized critical extension. |
| `kIdJustSigned` | 4 (valid) | PPKMS,  PPKLite | Just signed by user (similar to kIdIsSelf) |
| `kIdAssumedValid` | 3 (idunknown) | PPKMS | Certificate is valid to a trusted root, but revocation could not be checked and was not required. |
| `kIdIsSelf` | 4 (valid) | PPKMS,  PPKLite | Certificate is my credential (no further checking was done). |
| `kIdValid` | 4 (valid) | PPKMS,  PPKLite | Certificate is valid to a trusted root (in the Windows or Acrobat Address Book). |
| `kIdRevocationUnknown` | ? | PPKMS,  PPKLite | Certificate is valid to a trusted root, but revocation could not be checked and was required by the user. |

<a id="64083"></a>
<a id="modification-detection-and-prevention-mdp-values"></a>
<a id="id976"></a>
#### Modification Detection and Prevention (MDP) Values

Modification detection and prevention (MDP) settings control which changes are allowed to occur in a document before the signature becomes invalid. Changes are recorded outside of the byte range, for signature fields, and can include changes that have been incrementally saved as part of the document or changes that have occurred in memory between the time that a document is opened and when the signature is validated. MDP settings may only be applied to the first signature in a document. Use of MDP will result in an certification signature. MDP has one of the following four values:

- *allowAll*: Allow all changes to a document without any of these changes invalidating the signature. This results in MDP not being used for the signature. This was the behavior for Acrobat 4.0 through 5.1.
- *allowNone*: Do not allow any changes to the document without invalidating the signature. Note that this will also lock down the author’s signature.
- *default*: Allow form field fill-in if form fields are present in the document. Otherwise, do not allow any changes to the document without invalidating the signature.
- *defaultAndComments*: Allow form field fill-in if form fields are present in the document and allow annotations (comments) to be added, deleted or modified. Otherwise, do not allow any changes to the document without invalidating the signature. Note that annotations can be used to obscure portions of a document and thereby affect the visual presentation of the document.
