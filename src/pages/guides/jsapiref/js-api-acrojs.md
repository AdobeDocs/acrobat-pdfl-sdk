<a id="javascript-apis"></a>
<a id="id1"></a>
# JavaScript APIs

* [Annotation APIs](./annotation-apis.md)
* [Security and Signature APIs](./security-signature-apis.md)
* [App APIs](./app-apis.md)
* [Event APIs](./event-apis.md)

<a id="53810"></a>
<a id="alerter"></a>
<a id="id2"></a>
## Alerter

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

The Acrobat multimedia plug-in displays error alerts under various conditions such as a missing media file. JavaScript code can customize these alerts, either for an entire document or for an individual media player.

In an alert situation, the internal function `app.media.alert` is called with parameters containing information about the alert. The `app.media.alert` method handles the alert by looking for alerter objects and calling their `dispatch` methods, in this order:

```
args.alerter
doc.media.alerter
doc.media.stockAlerter
```

To handle alerts for a specific player, provide an alerter object in `args.alerter` when you call `app.media.createPlayer` or `app.media.openPlayer`.

To handle alerts for an entire document, set `doc.media.alerter` to an alerter object.

All alerts can be suppressed for a player or document by setting `args.alerter` or `doc.media.alerter` to `null`.

`doc.media.stockAlerter` provides the default alerts that are used if a custom alerter is not specified. This property is initialized automatically by `app.media.alert`. Normally, `doc.media.stockAlerter` would not be referenced in developer code.

<a id="alerter-methods"></a>
<a id="id3"></a>
### Alerter methods

<a id="41501"></a>
<a id="dispatch"></a>
<a id="id4"></a>
#### dispatch

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Called by `app.media.alert` to handle alert situations.

**Parameters**

- `alert` An Alert object (see below).

**Returns**

A Boolean value, `true` to stop further alert processing, `false` to continue processing.

<a id="41949"></a>
**Alert object**

| Properties | Type | Description |
|------------|------|-------------|
| `type` | String | All alert types |
| `doc` | Doc object | All alert types |
| `fromUser` | Boolean | All alert types |
| `error` | Object | Available for the Exception type alert. The error object has a `message` property:  `error: { message: String }` |
| `errorText` | String | Available for the PlayerError type alert. |
| `fileName` | String | Available for the FileNotFound type alert. |
| `selection` | `MediaSelection` object | Available for the SelectFailed type alert. |

Example 1: Open a media player and suppress all alerts for this player.

```
app.media.openPlayer({ alerter: null });

// A more elaborate way to do the same thing
app.media.openPlayer(
{
    alerter:
    {
        dispatch() { return true; }
    }
});
```

Example 2: For all players in this document, log any alerts to a text field and allow the normal alert box to be displayed.

```
function logAlerts( doc )
{
    count = 0;
    doc.alerter =
    {
        dispatch( alert )
        {
            doc.getField("AlertLog").value += "Alert #"
                + ++count + ": " + alert.type + "n";
        }
    }
}
logAlerts( this );

// Another way to keep the counter
function logAlerts( doc )
{
    doc.alerter =
    {
        count = 0,
        dispatch( alert )
        {
            doc.getField("AlertLog").value += "Alert #"
                + ++this.count + ": " + alert.type + "n";
        }
    }
}
logAlerts( this );
```

Example  3: Handle the PlayerError alert here, with defaults for other alerts.

```
this.media.alerter =
{
    dispatch( alert )
    {
        switch( alert.type )
        {
            case "PlayerError":
            app.alert( "Player error: " + alert.errorText );
            return true;
        }
    }
}
```

<a id="15210"></a>
<a id="alternatepresentation"></a>
<a id="id5"></a>
## AlternatePresentation

This object provides an interface to the document’s particular alternate presentation. Use the Doc object method alternatePresentations to acquire an AlternatePresentation object.

See the [PDF Reference](https://adobe.com/go/pdfreference) for additional details on alternate presentations.

<a id="alternatepresentation-properties"></a>
<a id="id6"></a>
### AlternatePresentation properties

<a id="45263"></a>
<a id="active"></a>
<a id="id7"></a>
#### active

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | boolean | R |

This property is `true` if the presentation is currently active and `false` otherwise. When a presentation is active, it controls how the document that owns it is displayed.

Example: See the start method for an example.

<a id="39659"></a>
<a id="type"></a>
<a id="id8"></a>
#### type

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | string | R |

The type of the alternate presentation. Currently, the only supported type is “SlideShow”.

<a id="alternatepresentation-methods"></a>
<a id="id9"></a>
### AlternatePresentation methods

<a id="63957"></a>
<a id="start"></a>
<a id="id10"></a>
#### start

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Switches the document view into the alternate presentation mode and sets the `active` property to `true`. An exception is thrown if this or any other alternate presentation is already active.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cOnStop` | (optional) An expression to be evaluated by Acrobat when the presentation completes for any reason (as a result of a call to `stop`, an explicit user action, or the presentation logic itself). |
| `cCommand` | (optional) A command or script to pass to the alternate presentation.  -  This command is presentation-specific (not a JavaScript expression). |

Example: Assume there is a named presentation called “MySlideShow” within the document.

```
// oMySlideShow is an AlternatePresentation object
oMySlideShow = this.alternatePresentations.MySlideShow;
if (!oMySlideShow.active) oMySlideShow.start();
```

Note that `this.alternatePresentations` is used to access the specified presentation by property name.

<a id="40183"></a>
<a id="stop"></a>
<a id="id11"></a>
#### stop

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Stops the presentation and switches the document into normal (PDF) presentation. An exception is thrown if this presentation is not active.

Example: In this example, `oMySlideShow` is an AlternatePresentations object. See start for a related example.

```
// Stop the show if already active
if (oMySlideShow.active) oMySlideShow.stop();
```

<a id="49491"></a>
<a id="bookmark"></a>
<a id="id237"></a>
## Bookmark

A Bookmark object represents a node in the bookmark tree that appears in the bookmarks navigational panel. Bookmarks are typically used as a table of contents allowing the user to navigate quickly to topics of interest.

<a id="bookmark-properties"></a>
<a id="id238"></a>
### Bookmark properties

<a id="98065"></a>
<a id="children"></a>
<a id="id239"></a>
#### children

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Array  `null` | R |

An array of `Bookmark` objects that are the children of this bookmark in the bookmark tree. If there are no children of this bookmark, this property has a value of `null`.

See also the parent and bookmarkRoot properties.

Example: Dump all bookmarks in the document.

```
function DumpBookmark(bkm, nLevel)
{
    var s = "";
    for (var i = 0; i < nLevel; i++) s += " ";
    console.println(s + "+-" + bkm.name);
    if (bkm.children != null)
        for (var i = 0; i < bkm.children.length; i++)
            DumpBookmark(bkm.children[i], nLevel + 1);
}
console.clear(); console.show();
console.println("Dumping all bookmarks in the document.");
DumpBookmark(this.bookmarkRoot, 0);
```

<a id="71326"></a>
<a id="color"></a>
<a id="id240"></a>
#### color

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | Not available in Reader | Array | R/W (Adobe Reader: R only) |

Specifies the color for a bookmark. Values are defined by using gray, RGB or CMYK color. See Color arrays for information on defining color arrays and how values are used with this property. See also the style property.

Example: The following fun script colors the top-level bookmark red, green, and blue.

```
var bkm = this.bookmarkRoot.children[0];
bkm.color = color.black;
var C = new Array(1, 0, 0);
var run = app.setInterval(
    'bkm.color = ["RGB",C[0],C[1],C[2]]; C.push(C.shift());', 1000);
var stoprun=app.setTimeOut(
    "app.clearInterval(run); bkm.color=color.black",12000);
```

<a id="40682"></a>
<a id="id241"></a>
<a id="id242"></a>
#### doc

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Object | R |

The Doc that the bookmark resides in.

<a id="76081"></a>
<a id="id243"></a>
<a id="id244"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | Not available in Reader | String | R/W (Adobe Reader: R only) |

The text string for the bookmark that the user sees in the navigational panel.

Example: Put the top-level bookmark in bold.

```
var bkm = this.bookmarkRoot.children[0];
console.println( "Top-level bookmark name: " + bkm.name );
```

The example that follows the children property also uses the `name` property.

<a id="57280"></a>
<a id="open"></a>
<a id="id245"></a>
#### open

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | Not available in Reader | Boolean | R/W (Adobe Reader: R only) |

Determines whether the bookmark shows its children in the navigation panel (open) or whether the children subtree is collapsed (closed).

<a id="36697"></a>
<a id="parent"></a>
<a id="id246"></a>
#### parent

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Object  `null` | R |

The parent bookmark of the bookmark or `null` if the bookmark is the root bookmark. See also the children and bookmarkRoot properties.

<a id="86167"></a>
<a id="id247"></a>
<a id="id248"></a>
#### style

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | Not available in Reader | Integer | R/W (Adobe Reader: R only) |

Specifies the style for the bookmark’s font: 0 is normal, 1 is italic, 2 is bold, and 3 is bold-italic. See also the color property.

Example: The following code puts the top-level bookmark in bold.

```
var bkm = this.bookmarkRoot.children[0];
bkm.style = 2;
```

<a id="bookmark-methods"></a>
<a id="id249"></a>
### Bookmark methods

<a id="81576"></a>
<a id="createchild"></a>
<a id="id250"></a>
#### createChild

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | Not available in Reader |

Creates a new child bookmark at the specified location.

See also the children property and the insertChild and remove methods.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The name of the bookmark that the user sees in the navigation panel. |
| `cExpr` | (optional) An expression to be evaluated whenever the user clicks the bookmark. It is equivalent to creating a bookmark with a JavaScript action, as described in the [PDF Reference](https://adobe.com/go/pdfreference). The default is no expression. |
| `nIndex` | (optional) The 0-based index into the children array of the bookmark at which to create the new child. The default is 0. |

Example: Create a bookmark at the top of the bookmark panel that takes you to the next page in the document.

```
this.bookmarkRoot.createChild("Next Page", "this.pageNum++");
```

<a id="81661"></a>
<a id="execute"></a>
<a id="id251"></a>
#### execute

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Executes the action associated with this bookmark. This can have a variety of behaviors. See the [PDF Reference](https://adobe.com/go/pdfreference) for a list of common action types. See also the createChild method.

Example: Implement a simple search of the bookmarks. If successful, the action associated with the bookmark is executed.

```
// Document-level or folder-level JavaScript.
function searchBookmarks(bkm, nLevel, bkmName)
{
    if ( bkm.name == bkmName ) return bkm;
    if (bkm.children != null) {
        for (var i = 0; i < bkm.children.length; i++)
        {
            var bkMark = searchBookmarks(
                bkm.children[i], nLevel + 1, bkmName);
            if ( bkMark != null ) break;
        }
        return bkMark;
    }
    return null;
}
// Redefine this function for a more sophisticated compare.
function bmkCompare( name1, name2 )
{
        return ( name1 == name2 );
}
```

The following code initiates the search. This code could be executed as field-level JavaScript or be executed as a menu action.

```
var bkmName = app.response({
    cQuestion: "Enter the name of the bookmark to find",
    cTitle: "Bookmark Search and Execute"
});
if ( bkmName != null ) {
    var bkm = searchBookmarks(this.bookmarkRoot, 0, bkmName );
    if ( bkm != null ) bkm.execute();
    else app.alert("Bookmark not found");
}
```

<a id="61060"></a>
<a id="insertchild"></a>
<a id="id253"></a>
#### insertChild

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | Not available in Reader |

Inserts the specified bookmark as a child of this bookmark. If the bookmark already exists in the bookmark tree, it is unlinked before inserting it back into the tree. In addition, the insertion is checked for circularities and disallowed if one exists. This prevents users from inserting a bookmark as a child or grandchild of itself. See also the children property and the createChild and remove methods.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oBookmark` | A bookmark object to add as the child of this bookmark. |
| `nIndex` | (optional) The 0-based index into the children array of the bookmark at which to insert the new child. The default is 0. |

Example: Take the first child bookmark and move it to the end of the bookmarks.

```
var bm = bookmarkRoot.children[0];
bookmarkRoot.insertChild(bm, bookmarkRoot.children.length);
```

<a id="43068"></a>
<a id="remove"></a>
<a id="id254"></a>
#### remove

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | Not available in Reader |

Removes the bookmark and all its children from the bookmark tree. See also the children property and the createChild and insertChild methods.

Example: Remove all bookmarks from the document.

```
bookmarkRoot.remove();
```

<a id="52228"></a>
<a id="setaction"></a>
<a id="id255"></a>
#### setAction

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All but Reader |

Sets a JavaScript action for a bookmark.

See also the Doc addRequirement and setPageAction methods and the Field object setAction method.

> **Note**
>
> This method overwrites any action already defined for this bookmark.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cScript` | Defines the JavaScript expression that is to be executed whenever the user clicks the bookmark. |

Example: Attach an action to the topmost bookmark.

```
var bm = bookmarkRoot.children[0]
bm.setAction("app.beep(0);");
```

<a id="33812"></a>
<a id="catalog"></a>
<a id="id256"></a>
## catalog

A static object that accesses the functionality provided by the Acrobat Catalog plug-in. This plug-in must be installed to interface with the `catalog` object.

> **Note**
>
> The Catalog plug-in (and the `catalog` object) is available only in Acrobat Pro.

See also the Index object, which is used to invoke various indexing operations provided by the Catalog plug-in, and the CatalogJob object.

<a id="catalog-properties"></a>
<a id="id257"></a>
### catalog properties

<a id="59187"></a>
<a id="isidle"></a>
<a id="id258"></a>
#### isIdle

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Acrobat Pro only | Boolean | R |

**Returns** `true` when Catalog is not busy with an indexing job.

<a id="22300"></a>
<a id="jobs"></a>
<a id="id259"></a>
#### jobs

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Acrobat Pro only | Array | R |

Gets information about the Catalog jobs. Catalog maintains a list of its pending, in-progress, and completed jobs for each Acrobat session. Returns an array of `CatalogJob` objects.

<a id="catalog-methods"></a>
<a id="id260"></a>
### catalog methods

<a id="87258"></a>
<a id="getindex"></a>
<a id="id261"></a>
#### getIndex

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Acrobat Pro only |

Uses a specified path of a Catalog index to get an `Index` object. The returned object can be used to perform various indexing operations such as building or deleting an index.

**Parameters**

| Property | Description |
|----------|-------------|
| `cDIPath` | The device-independent path of a Catalog index. |

**Returns**

The `Index` object.

<a id="37233"></a>
<a id="id262"></a>
<a id="id263"></a>
#### remove

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Acrobat Pro only |

Removes the specified `CatalogJob` object from Catalog’s job list. Catalog maintains a list of pending, in-progress, and completed jobs for each Acrobat session.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oJob` | The `CatalogJob` object to remove, as returned by the `jobs` property and various methods of the `Index` object. |

Example: Delete all jobs that are pending and need complete rebuild.

```
if (typeof catalog != undefined)  {
    for (var i=0; i<catalog.jobs.length; i++){
        var job = catalog.jobs[i];
        console.println("Index: ", job.path);

        if (job.status == "Pending" && job.type == "Rebuild")
            catalog.remove(job);
    }
}
```

<a id="13857"></a>
<a id="catalogjob"></a>
<a id="id264"></a>
## CatalogJob

This generic JavaScript object provides information about a job submitted to Catalog. It is returned by the `build` method of the `Index` object and the `catalog.jobs` property, and passed to `catalog.remove.`

<a id="catalogjob-properties"></a>
<a id="id265"></a>
### CatalogJob properties

<a id="49309"></a>
<a id="path"></a>
<a id="id266"></a>
#### path

Device-independent path of the index associated with the job

| Type | Access |
|------|--------|
| String | R |

<a id="58696"></a>
<a id="id267"></a>
<a id="id268"></a>
#### type

Type of indexing operation associated with the job.

| Type | Access |
|------|--------|
| String | R |

Possible values are:

```
Build
Rebuild
Delete
```

<a id="20317"></a>
<a id="id269"></a>
<a id="id270"></a>
#### status

The status of the indexing operation.

| Type | Access |
|------|--------|
| String | R |

Possible values are:

```
Pending
Processing
Completed
CompletedWithErrors
```

<a id="44855"></a>
<a id="certificate"></a>
<a id="id271"></a>
## Certificate

The Certificate object provides read-only access to the properties of an X.509 public key certificate.

Related objects and methods are:

- `security` object: importFromFile and getSecurityPolicies
- `DirConnection` object: search

Field object: signatureInfo
\* `FDF` object: signatureValidate
\* RDN object

- Usage Object

> **Note**
>
> There are no security restrictions on this object.

<a id="certificate-properties"></a>
<a id="id272"></a>
### Certificate properties

<a id="96257"></a>
<a id="binary"></a>
<a id="id273"></a>
#### binary

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

The raw bytes of the certificate, as a hex encoded string.

<a id="20527"></a>
<a id="issuerdn"></a>
<a id="id274"></a>
#### issuerDN

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | `RDN` object | R |

The distinguished name of the issuer of the certificate, returned as an `RDN` object.

<a id="87992"></a>
<a id="keyusage"></a>
<a id="id275"></a>
#### keyUsage

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array of Strings | R |

An array of strings indicating the value of the certificate key usage extension. Possible values are

```
kDigitalSignature    kDataEncipherment    kCRLSign
kNonRepudiation      kKeyAgreement        kEncipherOnly
kKeyEncipherment     kKeyCertSign         kDecipherOnly
```

<a id="40392"></a>
<a id="md5hash"></a>
<a id="id276"></a>
#### MD5Hash

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

The MD5 digest of the certificate, represented as a hex-encoded string. This provides a unique fingerprint for this certificate.

<a id="62254"></a>
<a id="privatekeyvalidityend"></a>
<a id="id277"></a>
#### privateKeyValidityEnd

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | Date object | R |

The date before which it’s legal to use the private key associated with this certificate. If the PKUP extension is not present or this property isn’t present in the extension, this represents the validity end date of the certificate itself. Before a digital ID can be used for signing, Acrobat ensures that the signing time is prior to the `privateKeyValidityEnd` date.

<a id="63122"></a>
<a id="privatekeyvaliditystart"></a>
<a id="id278"></a>
#### privateKeyValidityStart

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | Date object | R |

The date after which it’s legal to use the private key associated with this certificate. If the Private Key Usage Period (PKUP) certificate extension is not present, this represents the validity start date of the certificate itself. Before a digital ID can be used for signing, Acrobat ensures that the signing time is more recent than the `privateKeyValidityStart` date.

<a id="34510"></a>
<a id="sha1hash"></a>
<a id="id279"></a>
#### SHA1Hash

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

The SHA1 digest of the certificate, represented as a hex-encoded string. This provides a unique fingerprint for this certificate.

<a id="68894"></a>
<a id="serialnumber"></a>
<a id="id280"></a>
#### serialNumber

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

A unique identifier for this certificate, used in conjunction with `issuerDN`.

<a id="31991"></a>
<a id="subjectcn"></a>
<a id="id281"></a>
#### subjectCN

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

The common name of the signer.

<a id="23415"></a>
<a id="subjectdn"></a>
<a id="id282"></a>
#### subjectDN

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | `RDN` object | R |

The distinguished name of the signer, returned as an RDN object.

<a id="50891"></a>
<a id="ubrights"></a>
<a id="id283"></a>
#### ubRights

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Rights object | R |

The application rights that can be enabled by this certificate, returned as a generic `Rights` object.

<a id="36240"></a>
**Rights Object**

A `Rights` object has the following properties.

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `mode` | String | R | Possible values are: * *Evaluation*: Rights enabled by this certificate for this document are valid as long as this certificate is valid. * *Production*: Rights enabled by this certificate for this document are valid for eternity.  Currently, this value is not used by Adobe’s PDF viewer. |
| `rights` | Array of Strings | R | Array of strings indicating the application rights that can be enabled by this certificate. Possible values are: * *FormFillInAndSave*: The right to fill in forms, excluding signature fields, and to save the modified file. * *FormImportExport*: The right to import and export form data. * *FormAddDelete*: The right to add or delete a form field. * *SubmitStandalone*: The right to submit a document outside a browser. * *SpawnTemplate*: The right to spawn page templates. * *Signing*: The right to sign existing form fields in a document. * *AnnotModify*: The right to create, delete, and modify comments. * *AnnotImportExport*: The right to import and export annotations. * *BarcodePlaintext*: The right to encode the appearance of a form field as a plain text barcode. * *AnnotOnline*: Allow online commenting. Enables uploading of any annotations in the document to a server and downloading of annotations from a server. Does not enable the addition of these annotations into the document. * *FormOnline*: Enable forms-specific online mechanisms such as SOAP or Active Data Object. * *EFModify*: The right to create, delete, modify, and import named embedded files. Does not apply to file attachment annotations. |

<a id="81656"></a>
<a id="usage"></a>
<a id="id284"></a>
#### usage

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Usage object | R |

The purposes for which this certificate may be used within the Acrobat environment returned as a `Usage` object.

<a id="87917"></a>
**Usage Object**

This generic JavaScript object represents a certificate usage value in the `certificate.usage` property. It has the following properties.

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `endUserSigning` | Boolean | R | `true` if the certificate is usable for end-user signing. |
| `endUserEncryption` | Boolean | R | `true` if the certificate is usable for end-user encryption. |

Example: Encrypt the currently open document for everyone in the address book. Address book entries that contain sign-only certificates, CA certificates, no certificates, or are otherwise unsuitable for encryption, are not included in the final recipient list.

```
var eng = security.getHandler( "Adobe.AAB" );
var dc = eng.directories[0].connect();
var recipients = dc.search();

var filteredRecipients = new Array();
for( i = 0; i < recipients.length; ++i ) {
    if( recipients[i].defaultEncryptCert &&
        recipients[i].defaultEncryptCert.usage.endUserEncryption ) {
        filteredRecipients[filteredRecipients.length] = recipients[i];
        continue;
    }
    if(recipients[i].certificates) {
        for( j = 0; j < recipients[i].certificates.length; ++j )
            if( recipients[i].certificates[j].usage.endUserEncryption ) {
                filteredRecipients[filteredRecipients.length]

                     = recipients[i];
                continue;
            }
    }
}
this.encryptForRecipients({
    oGroups:[{userEntities: filteredRecipients}]
});
```

<a id="74572"></a>
<a id="validityend"></a>
<a id="id285"></a>
#### validityEnd

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.05 | No | No | All | Date object | R |

The validity end date of the certificate. Before a digital ID can be used for signing, Acrobat ensures that the signing time is prior to the `validityEnd` date.

<a id="55071"></a>
<a id="validitystart"></a>
<a id="id286"></a>
#### validityStart

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.05 | No | No | All | Date object | R |

The validity start date of the certificate. Before a digital ID can be used for signing Acrobat, ensures that the signing time is more recent than the `validityStart` date.

<a id="29350"></a>
<a id="collab"></a>
<a id="id287"></a>
## Collab

This static object represents the collaboration functionality.

<a id="collab-methods"></a>
<a id="id288"></a>
### Collab methods

<a id="49904"></a>
<a id="addstatemodel"></a>
<a id="id289"></a>
#### addStateModel

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Adds a new state model to Acrobat. A state model describes the valid states that an annotation using the model can have (see the Annotation object for details about getting and setting the state of an annotation). State models can be used to describe the workflow that a document review goes through and can be used for review management.

See also removeStateModel, getStateInModel, and transitionToState.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | A unique, language-independent identifier for the State Model. |
| `cUIName` | The display name of the state model used in the user interface. The value should be a localized string. |
| `oStates` | The states in the state model, described by a `States` object. |
| `cDefault` | (optional) One of the states in the model to be used as a default state if no other state is set. The default is for there to be no default state. |
| `bHidden` | (optional) Specifies whether the state model should be hidden in the state model user interface. The default is `false` (the State Model is shown). |
| `bHistory` | (optional) Specifies whether an audit history is maintained for the state model. Keeping an audit history requires more space in the file. The default is `true`. |

<a id="10552"></a>
**States object**

This generic object represents a set of states in a state model and is passed as the `oStates` parameter. The elements in the object literal are the unique state identifiers and the values are objects having the following properties:

| Property | Description |
|----------|-------------|
| `cUIName` | The UI (display name) for the state. |
| `oIcon` | (optional) An `Icon Stream` object that is displayed in the UI for the state. |

Example: Add a new state model with a unique name of “ReviewStates”:

```
Collab.addStateModel({
    cName: "ReviewStates",
    cUIName: "My Review",

     oStates:
    {
        "initial": {cUIName: "Haven't reviewed it"},
        "approved": {cUIName: "I approve"},
        "rejected": {cUIName: "Forget it"},
        "resubmit": {cUIName: "Make some changes"}
    },
    cDefault: "initial"
});
```

A state model can be removed with `Collab.removeStateModel`.

<a id="77375"></a>
<a id="documenttostream"></a>
<a id="id290"></a>
#### documentToStream

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0.5 | No | Yes | All |

Saves a copy of a Doc and returns the contents as a stream object.

The document `dirty` property is preserved after this method is called and the original document is not modified.

**Parameters**

| Property | Description |
|----------|-------------|
| `oDocument` | The Doc. |

**Returns**

A `ReadStream` object.

<a id="90340"></a>
<a id="removestatemodel"></a>
<a id="id291"></a>
#### removeStateModel

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Removes a state model that was previously added by calling `addStateModel`. Removing a state model does not remove the state information associated with individual annotations. If the model is removed and added again, all of the state information for the annotations is still available.

See also addStateModel, getStateInModel, and transitionToState.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | A unique, language-independent identifier for the state model that was used in `addStateModel`. |

Example: Continuing the example in `addStateModel`, remove the state model “ReviewStates”:

```
// Remove the state model
Collab.removeStateModel("ReviewStates");
```

<a id="37083"></a>
<a id="id292"></a>
<a id="id293"></a>
## color

The `color` object is a convenience static object that defines the basic colors. Use this object to set a property or call a method that requires a color array.

<a id="98898"></a>
<a id="color-arrays"></a>
<a id="id294"></a>
### Color arrays

A color is represented in JavaScript as an array containing 1, 2, 4, or 5 elements corresponding to a Transparent, Gray, RGB, or CMYK color space, respectively. The first element in the array is a string denoting the color space type. The subsequent elements are numbers that range between zero and one inclusive. For example, the color red can be represented as `["RGB", 1, 0, 0]`.

Invalid strings or insufficient elements in a color array cause the color to be interpreted as the color black.

| Color space | String | Number of additional elements | Description |
|-------------|--------|-------------------------------|-------------|
| Transparent | “T” | 0 | A *transparent* color space indicates a complete absence of color and allows those portions of the document underlying the current field to show through. |
| Gray | “G” | 1 | Colors are represented by a single value—the intensity of achromatic light. In this color space, 0 is black, 1 is white, and intermediate values represent shades of gray. For example,.5 represents medium gray. |
| RGB | “RGB” | 3 | Colors are represented by three values: the intensity of the *red*, *green*, and *blue* components in the output. RGB is commonly used for video displays, which are generally based on red, green, and blue phosphors. |
| CMYK | “CMYK” | 4 | Colors are represented by four values, the amounts of the cyan, magenta, yellow, and black components in the output. This color space is commonly used for color printers, where they are the colors of the inks used in four-color printing. Only cyan, magenta, and yellow are necessary, but black is generally used in printing because black ink produces a better black than a mixture of cyan, magenta, and yellow inks and because black ink is less expensive than the other inks. |

<a id="color-properties"></a>
<a id="id295"></a>
### color properties

The `color` object defines the following colors.

| Color object | Keyword | Equivalent JavaScript | Version |
|--------------|---------|-----------------------|---------|
| Transparent | `color.transparent` | `[ "T" ]` |  |
| Black | `color.black` | `[ "G", 0 ]` |  |
| White | `color.white` | `[ "G", 1 ]` |  |
| Red | `color.red` | `[ "RGB", 1,0,0 ]` |  |
| Green | `color.green` | `[ "RGB", 0,1,0 ]` |  |
| Blue | `color.blue` | `[ "RGB", 0, 0, 1 ]` |  |
| Cyan | `color.cyan` | `[ "CMYK", 1,0,0,0 ]` |  |
| Magenta | `color.magenta` | `[ "CMYK", 0,1 0,0 ]` |  |
| Yellow | `color.yellow` | `[ "CMYK", 0,0,1,0 ]` |  |
| Dark Gray | `color.dkGray` | `[ "G", 0.25 ]` | 4.0 |
| Gray | `color.gray` | `[ "G", 0.5 ]` | 4.0 |
| Light Gray | `color.ltGray` | `[ "G", 0.75 ]` | 4.0 |

Example: This example sets the text color of the field to red if the value of the field is negative, or to black if the field value is nonnegative.

```
var f = event.target; /* field that the event occurs at */
f.target.textColor = event.value < 0 ? color.red : color.black;
```

<a id="color-methods"></a>
<a id="id296"></a>
### color methods

- convert
- equal

<a id="16408"></a>
<a id="convert"></a>
<a id="id297"></a>
#### convert

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Converts the color space and color values specified by the `color` object to the specified color space:

- Conversion to the gray color space is lossy (in the same fashion that displaying a color TV signal on a black-and-white TV is lossy).
- The conversion of RGB to CMYK does not take into account any black generation or undercolor removal parameters.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `colorArray` | Array of color values. See Color arrays. |
| `cColorspace` | The color space to which to convert. |

**Returns**

A color array.

Example: The return value of the code line below is the array `["CMYK", 0, 1, 1, 0]`.

```
color.convert(["RGB",1,0,0], "CMYK");
```

<a id="10606"></a>
<a id="equal"></a>
<a id="id298"></a>
#### equal

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Compares two `Color Arrays` to see if they are the same. The routine performs conversions, if necessary, to determine if the two colors are indeed equal (for example, `["RGB",1,1,0]` is equal to `["CMYK",0,0,1,0]`).

**Parameters**

| Property | Description |
|----------|-------------|
| `colorArray1` | The first color array for comparison. |
| `colorArray2` | The second color array for comparison. |

**Returns**

`true` if the arrays represent the same color, `false` otherwise.

Example:

```
var f = this.getField("foo");
if (color.equal(f.textColor, f.fillColor))
    app.alert("Foreground and background color are the same!");
```

<a id="40112"></a>
<a id="colorconvertaction"></a>
<a id="id299"></a>
## colorConvertAction

This object describes a single color conversion action.

You can obtain colorConvertAction object from the Doc object method getColorConvertAction. The returned object can then be modified. A color conversion action is divided into a “match” section and an “action” section. The “match” section describes what sorts of objects can match this action. The Doc object method colorConvertPage, accepts an array of these actions, against which matches are attempted until a match is found.

<a id="colorconvertaction-properties"></a>
<a id="id300"></a>
### colorConvertAction properties

<a id="60292"></a>
<a id="action"></a>
<a id="id301"></a>
#### action

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Integer | R/W |

Describes the action to perform if a match occurs.

The value of `action` is accessed through the `constants.actions` object of the colorConvertAction object as the following constants:

**constants.actions object**

| Name | Description |
|------|-------------|
| `Preserve` | Do nothing but handle ink aliases. |
| `Convert` | Convert to target space. |
| `Decalibrate` | Convert calibrated space to device. |
| `DownConvert` | Downconvert NChannel to DeviceN. |

<a id="95592"></a>
<a id="alias"></a>
<a id="id302"></a>
#### alias

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | String | R/W |

If this action is an ink action then this describes the ink’s alias.

<a id="66014"></a>
<a id="colorantname"></a>
<a id="id303"></a>
#### colorantName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | String | R/W |

If this action is an ink action then this describes the colorant name.

See the related property isProcessColor.

<a id="41068"></a>
<a id="convertintent"></a>
<a id="id304"></a>
#### convertIntent

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Integer | R/W |

Defines the rendering intent used to color convert the object. For a detailed description of rendering intents, please see Table 4.20 of the [PDF Reference](https://adobe.com/go/pdfreference).

The value of convertIntent is accessed through the [constants.renderingIntents object](./js-api-acrojs.md#56390) of the colorConvertAction object.

<a id="84007"></a>
<a id="convertprofile"></a>
<a id="id305"></a>
#### convertProfile

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | String | R/W |

Describes the color profile to which matching objects should be converted if the action is `Convert`. A list of available color profiles can be obtained from the printColorProfiles property of the `app` object

<a id="29705"></a>
<a id="embed"></a>
<a id="id306"></a>
#### embed

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Boolean | R/W |

If the matched object is to be converted and `embed` is `true`, the resulting object will have a color profile embedded in the file. Otherwise, the object will be stored as the corresponding device color space for the profile to which the object was converted.

<a id="85716"></a>
<a id="isprocesscolor"></a>
<a id="id307"></a>
#### isProcessColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Boolean | R/W |

If this action is an ink action and if `isProcessColor` is `true`, the ink represents a process color, and the `colorantName` should be one of `Cyan`, `Magenta`, `Yellow`, `Black`, `Red`, `Green` or `Blue`.

<a id="68063"></a>
<a id="matchattributesall"></a>
<a id="id308"></a>
#### matchAttributesAll

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Integer | R/W |

The value of the `matchAttributesAll` property is a bitmap containing object attributes (flags) to be matched. A match occurs if all flags match, i.e. if there is a complete match.

The flags are accessed through the `constants.objectFlags` object of the colorConvertAction object and are defined as follows:

<a id="47626"></a>
**constants.objectFlags object**

| Flag name | Description |
|-----------|-------------|
| `ObjImage` | Object is an image. |
| `ObjJPEG` | Object is a JPEG image. |
| `ObjJPEG2000` | Object is a JPEG2000 Image. |
| `ObjLossy` | Image in a lossy space. |
| `ObjNonLossy` | Image in a non-lossy space. |
| `ObjText` | Object is text. |
| `ObjLineArt` | Object is line-art (fill or stroke). |
| `ObjShade` | Object is a smooth shade. |
| `ObjTransparent` | Object is not opaque. |
| `ObjOverprinting` | Object overprints. |
| `ObjOverprintMode` | OPM is set to 1. |

> **Note**
>
> The value of `matchAttributesAll` can be set by using the bitwise operators with the bit flags of `constants.objectFlags`.

Example: Match images that overprint.

```
var action = this.getColorConvertAction();
action.matchAttributesAll = action.constants.objFlags.ObjImage
               action.constants.objFlags.ObjOverprinting;
```

<a id="55787"></a>
<a id="matchattributesany"></a>
<a id="id309"></a>
#### matchAttributesAny

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Integer | R/W |

The value of the `matchAttributesAny` property is a bitmap containing object attributes to be matched. A match occurs if any of the flags match.

The flags are accessed through the [constants.objectFlags object](./js-api-acrojs.md#47626) of the colorConvertAction object.

> **Note**
>
> The value of `matchAttributesAny` can be set by using the bitwise operators with the bit flags of `constants.objectFlags`.

<a id="23732"></a>
<a id="matchintent"></a>
<a id="id310"></a>
#### matchIntent

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Integer | R/W |

Matches the rendering intent used for the object. For a detailed description of rendering intents, please see Table 4.20 of the [PDF Reference](https://adobe.com/go/pdfreference).

The value of `matchIntent` is accessed through the `constants.renderingIntents` object of the colorConvertAction object and are defined as follows:

<a id="56390"></a>
**constants.renderingIntents object**

| Name | Description |
|------|-------------|
| `AbsoluteColorimetric` | Absolute colorimetric rendering intent. |
| `RelativeColorimetric` | Relative colorimetric rendering intent. |
| `Saturation` | Saturation rendering intent |
| `Perceptual` | Perceptual rendering intent |
| `Any` | Match any of the above rendering intents |
| `Document` | Use the rendering intent specified by the current graphics state in which the matched object is rendered (used by convertIntent only). |

<a id="45157"></a>
<a id="matchspacetypeall"></a>
<a id="id311"></a>
#### matchSpaceTypeAll

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Integer | R/W |

The value of the `matchSpaceTypeAll` property is a bitmap containing color space attributes (flags) to be matched. A match occurs if all flags match, i.e. if there is a complete match.

These two fields are bitmaps containing color space attributes to be matched. The first field will only match if all flags match, i.e. if there is a complete match. The second field will match if any of the flags match.

The flags are accessed through the `constants.spaceFlags` object of the colorConvertAction object and are defined as follows:

<a id="76159"></a>
**constants.spaceFlags object**

| Flag name | Description |
|-----------|-------------|
| `DeviceSpace` | Color space is one of DeviceRGB, DeviceCMYK, or DeviceGray. |
| `CalibratedSpace` | Color space is ICCBased, CalRGB, CalGray, or Lab. |
| `AlternateSpace` | This color space is the alternate space of a DeviceN, Separation, or ICCBased. |
| `BaseSpace` | This color space is the base space of an Indexed space. |
| `IndexedSpace` | This color space is an indexed space. |
| `SeparationSpace` | This color space is a Separation color space. |
| `DeviceNSpace` | This color space is a DeviceN color space. |
| `NChannelSpace` | This color space is a DeviceN color space with NChannel attributes. |
| `RGBSpace` | This space is RGB. This flag should only be used in combination with `DeviceSpace` or `CalibratedSpace`. |
| `CMYKSpace` | This space is CMYK. This flag should only be used in combination with `DeviceSpace` or `CalibratedSpace`. |
| `GraySpace` | This space is Grayscale. This flag should only be used in combination with `DeviceSpace` or `CalibratedSpace`. |
| `LabSpace` | This space is CIELAB. This flag should only be used in combination with *DeviceSpace* or `CalibratedSpace`. |

> **Note**
>
> The value of `matchSpaceTypeAll` can be set by using the bitwise operators with the bit flags of `constants.spaceFlags`.

<a id="78757"></a>
<a id="matchspacetypeany"></a>
<a id="id312"></a>
#### matchSpaceTypeAny

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Integer | R/W |

The value of the `matchSpaceTypeAny` property is a bitmap containing color space attributes (flags) to be matched. A match occurs if any of the flags match.

The flags are accessed through the [constants.spaceFlags object](./js-api-acrojs.md#76159) of the colorConvertAction object.

> **Note**
>
> The value of `matchSpaceTypeAny` can be set by using the bitwise operators with the bit flags of `constants.spaceFlags`.

<a id="36011"></a>
<a id="preserveblack"></a>
<a id="id313"></a>
#### preserveBlack

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Boolean | R/W |

If the matched object is to be converted and `preserveBlack` is `true`, the conversion will be done using a “black-preserving” transform, in which text or line art objects are handled specially. If a CMYK color is (0.0, 0.0, 0.0, 1.0), an RGB color is (0.0, 0.0, 0.0) or a gray color is (0.0), and `preserveBlack` is `true`, that color is considered special-case black, and is converted straight to black without using the conversion profile. The resulting color will be as described for the matching black color for the corresponding profile target color space, for example, if the convert profile is RGB, the resulting color will be (0.0, 0.0, 0.0) no matter what the color profile says.

<a id="66694"></a>
<a id="useblackpointcompensation"></a>
<a id="id314"></a>
#### useBlackPointCompensation

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | Acrobat Pro only | Boolean | R/W |

If `useBlackPointCompensation` is true, `use` black point compensation for all color conversions. The effect of this flag depends on the color management method (CMM) being used, but if the Adobe CMM is being used, colorimetric transforms are scaled such that black remains black no matter what the media black point of the source profile.

<a id="26749"></a>
<a id="collection"></a>
<a id="id315"></a>
## Collection

A collection object is obtained from the Doc. collection property. Doc. `collection` returns a `null` value when there is no PDF collection (also called PDF package and PDF portfolio).

The collection object is used to set the initial document in the collection, set the initial view of the collection, and to get, add, and remove collection fields (or categories).

<a id="collection-properties"></a>
<a id="id316"></a>
### Collection properties

<a id="67804"></a>
<a id="fields"></a>
<a id="id317"></a>
#### fields

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | Array | R/W |

The `fields` property is an array of collectionField objects in the collection.

Example: Enumerate all the `collectionFields` in a collection.

```
for (var i in collection.fields)
```

console.println(i);

<a id="10634"></a>
<a id="initialdoc"></a>
<a id="id318"></a>
#### initialDoc

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | String | R/W |

Use the `initialDoc` property to specify the document in the collection that is initially viewed when the collection is opened. The value of `initialDoc` is the name property of the Data object of the initial document, or `null` if no initial document is specified.

Example: Set the initial document to the third file in the collection.

```
this.collection.initialDoc = this.dataObjects[2].name;
```

<a id="11002"></a>
<a id="initialview"></a>
<a id="id319"></a>
#### initialView

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | String | R/W |

A string describing the initial collection view. Possible values include `Tile`, `Details`, `Hidden`, `Custom`, or `null`. The values of `Tile` and `Details` are built-in views, while `Custom` indicates that a document-based Navigator is preferred.

Example: Set the initial view to `Details`.

```
this.collection.initialView = "Details";
```

<a id="collection-methods"></a>
<a id="id320"></a>
### Collection methods

<a id="23829"></a>
<a id="addfield"></a>
<a id="id321"></a>
#### addField

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 9.0 | No | No | All |

Adds a new field (or category) to the collection schema. The method throws an exception if the field already exits.

| `name` | A string that is the name of the field of the collectionField object to be added. |
|--------|-----------------------------------------------------------------------------------|
| `text` | The text of this field that is displayed to the user in the user interface. |
| `type` | (Optional) A string that specifices the type of data associated with the field. Possible values are are listed below.  `S`, a string type. A field with a string value.   `D`, a date type. A field with a date value.   `N`, a numeric type. A field with a numeric value.   The following values identify the types of file-related fields:  `F`, a field reserved for the file name of a member of the collection.   `Desc`, a field reserved for a description string of a member of the collection.   `Size`, a ield reserved for the file size of a member of the collection.   `ModDate`, a field reserved for the modification date of a member of the collection.   `CreationDate`, a field reserved for the creation date of a member of the collection.   `CompressedSize`, a field reserved for the compressed file size of a member of the collection.   The default is `"S"`, a string type. |
| `order` | (Optional) An integer that indicates the order of the field in the display of the collection in the user interface. If this parameter is not specified, the new field is listed last. |
| `visible` | (Optional) A Boolean value that indicates the visibility of the field. The field is visible if the the value is `true` ; not visible if `false`. The default is `true`. |
| `readOnly` | (Optional) A Boolean value, the field is read only if `true`. The default is `false`.   If a field is read only, the user is not allowed to change the value of this field through the user interface. |

**Returns**

The collectionField object of the newly created field.

Example: Create a new field in the collection called `"to"` using object literal techniques.

```
this.collection.addField({name:"to", order:3, text:"To", type:"S"});

// The same example as above, but using ordered parameters.
this.collection.addField("to", "To", "S", 3);
```

<a id="87286"></a>
<a id="getfield"></a>
<a id="id322"></a>
#### getField

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 9.0 | No | No | All |

The `getField` method returns the collectionField object corresponding to the `name` of a collection field.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `name` | A string that is the name of the field of the `collectionField` object to be retrieved. |

**Returns**

A `collectionField` object, or `null` if the field is not found.

Example: Get the collectionField object of the `"from"` field.

```
var f = this.collection.getField("from");
```

<a id="70653"></a>
<a id="removefield"></a>
<a id="id323"></a>
#### removeField

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 9.0 | No | No | All |

Remove a field from the collection schema.

**Parameters**

| Property | Description |
|----------|-------------|
| `name` | A string that is the name of the field to be removed. |

Example: Remove the `"from"` field from the collection schema.

```
this.collection.removeField("from");
```

<a id="31572"></a>
<a id="collectionfield"></a>
<a id="id324"></a>
## collectionField

The properties of the `collectionField` object are the fields (or categories) used by the collection. The text property (see below) is the (display) string the user sees in the user-interface with viewing a listing of the files files in the collection. Use the `collectionField` object to set the order the fields are listed in the user-interface, the sort order of the listing of the files, or to set a field as read only.

The collection field values for embedded files in the collection can be got or set through getFieldValue and setFieldValue methods of the Data object.

<a id="collectionfield-properties"></a>
<a id="id325"></a>
### collectionField properties

<a id="50349"></a>
<a id="id326"></a>
<a id="id327"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | String | R |

The string that specifies the name of the field.

<a id="70457"></a>
<a id="order"></a>
<a id="id328"></a>
#### order

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | Integer | R/W |

Specifies the order the field is listed in relation to other fields. Field order is 0-based. When changing the value, if needed, the order of other fields will be incremented to prevent duplicates.

<a id="30423"></a>
<a id="id329"></a>
<a id="id330"></a>
#### readOnly

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | Boolean | R/W |

A Boolean value that specifies whether the user may change values of the field in the user interface. When readonly is `true`, no changes are allowed.

<a id="94450"></a>
<a id="sort"></a>
<a id="id331"></a>
#### sort

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | Integer | R/W |

The value of `sort` specifies how this field contributes to the ordering of files in the collection.

If the value is 0, this field is not used to sort the files. If the absolute value is 1, this field is the primary sort field. If the absolute value is 2, the field is the secondary sort field (used to break ties on the primary sort field), and so on. Additionally, the sign of value indicates the direction in which the files should be sorted. Positive values indicate that the files are sorted in ascending order, and negative values indicate that files are sorted in descending order.

Example: To illustrate the sorting scheme, consider a simple set of 4 fields that describe an email inbox: `From`, `Subject`, `To`, and `Received`. Each file in the collection represents a single email message. Set the sort order for each of these fields as indicated below:

- `From`: `0`
- `To`: `0`
- `Subject`: `1`
- `Received`: `-2`

The above sort order indicates that the primary sort field is `"Subject"` (the absolute value of the field is 1) and that files should be sorted in ascending order (the sign is positive). If two files have the same subject, the secondary sort field is consulted. In this case, the secondary sort field is `"Received"` (the absolute value of the field is 2) and it is specified to sort in descending order. The files are sorted by `Subject` in ascending order. Any files that have identical `Subjects` will be sorted in a subgroup by their `Received` field, but in descending order. The other fields do not contribute to the sort, since they are 0.

<a id="56468"></a>
<a id="text"></a>
<a id="id332"></a>
#### text

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | String | R/W |

The value of `text` specifies the display text used by the field in the user-interface.

<a id="20646"></a>
<a id="id333"></a>
<a id="id334"></a>
#### type

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 9.0 | No | No | All | String | R/W |

A text string that specifies the type of data stored in the field. Possible values include:

- `S`, the value of this field is a string type.
- `D`, the value of this field is a date type.
- `N`, the value of this field is a number type.
- `F`, the value of this field is the file name of a member of the collection.
- `Desc`, the value of this field is a description string of a member of the collection.
- `Size`, the value of this field is the file size of a member of the collection.
- `ModDate`, the value of this field is the modification date of a member of the collection.
- `CreationDate`, the value of this field is the creation date of a member of the collection.
- `CompressedSize`, the value of this field is the compressed file size of a member of the collection.

The value of this property cannot be changed for a field that already exists. When a new field is created using the addField method, the `type` can be set.

Example: Modify and examine the properties of user-defined field `"from".`

```
var f = this.collection.getField("from");
f.visible = true;
f.order = 1;
f.text = "From";
console.println("Field name: " + f.name);
console.println("Field type: " + f.type);
```

<a id="78269"></a>
<a id="column"></a>
<a id="id335"></a>
## Column

This generic JavaScript object contains the data from every row in a column. A column object is returned by the `getColumn` and `getColumnArray` methods of the `Statement` object. See also the ColumnInfo object.

<a id="column-properties"></a>
<a id="id336"></a>
### Column properties

<a id="53313"></a>
<a id="columnnum"></a>
<a id="id337"></a>
#### columnNum

START HERE

The number identifying the column.

| Type | Access |
|------|--------|
| Number | R |

<a id="16818"></a>
<a id="id338"></a>
<a id="id339"></a>
#### name

The name of the column.

| Type | Access |
|------|--------|
| String | R |

<a id="15970"></a>
<a id="id340"></a>
<a id="id341"></a>
#### type

One of the `SQL Types` for the data in the column.

| Type | Access |
|------|--------|
| Number | R |

<a id="45830"></a>
<a id="typename"></a>
<a id="id342"></a>
#### typeName

The name of the type of data the column contains.

| Type | Access |
|------|--------|
| String | R |

<a id="56665"></a>
<a id="value"></a>
<a id="id343"></a>
#### value

The value of the data in the column, in the format in which the data was originally retrieved.

| Type | Access |
|------|--------|
| various | R/W |

<a id="73870"></a>
<a id="columninfo"></a>
<a id="id344"></a>
## ColumnInfo

This generic JavaScript object contains basic information about a column of data. It is returned by the `getColumnList` method of the `Connection` object. See also the Column object.

<a id="columninfo-properties"></a>
<a id="id345"></a>
### ColumnInfo properties

<a id="87257"></a>
<a id="id346"></a>
<a id="id347"></a>
#### name

A string that represents the identifying name of a column. This string can be used in a call to the `getColumn` method of the `Statement` object identify the associated column.

| Type | Access |
|------|--------|
| String | R |

<a id="33941"></a>
<a id="description"></a>
<a id="id348"></a>
#### description

A string that contains database-dependent information about the column.

| Type | Access |
|------|--------|
| String | R |

<a id="62088"></a>
<a id="id349"></a>
<a id="id350"></a>
#### type

A numeric value identifying one of the `ADBC SQL Types` that applies to the data contained in the column associated with the `ColumnInfo` object.

| Type | Access |
|------|--------|
| Number | R |

<a id="22487"></a>
<a id="id351"></a>
<a id="id352"></a>
#### typeName

| Type | Access |
|------|--------|
| String | R |

A string identifying the type of the data contained in the associated column. It is not one of the `SQL Types` (see `type` above), but a database-dependent string representing the data type. This property may give useful information about user-defined data types.

<a id="92099"></a>
<a id="console"></a>
<a id="id353"></a>
## console

The `console` object is a static object that enables access to the Acrobat JavaScript Console for executing JavaScript and displaying debug messages.

This object does not function in Adobe Reader versions earlier than 7.0. Beginning with version 7.0, Adobe Reader has a console window. Its primary function is to report errors and messages. This capability is controlled by the JavaScript preference Show Console on Errors and Messages. Though the console is not interactive, the methods of the `console` object function as they do in Acrobat.

The debugging capability of the Acrobat JavaScript Debugging window can be made available for Adobe Reader for the Windows and Mac OS platforms. To debug within Adobe Reader, the JavaScript file debugger.js must be installed and the Windows registry must be edited appropriately. See the [JavaScript Developer Guide](../jsdevguide/index.md) for technical details.

See also the dbg object.

<a id="console-methods"></a>
<a id="id354"></a>
### console methods

<a id="68659"></a>
<a id="clear"></a>
<a id="id355"></a>
#### clear

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Clears the console windows buffer of any output.

<a id="70690"></a>
<a id="hide"></a>
<a id="id356"></a>
#### hide

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | No | No | All |

Closes the console window.

<a id="92823"></a>
<a id="println"></a>
<a id="id357"></a>
#### println

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Prints a string value to the console window with an accompanying carriage return.

**Parameters**

| Property | Description |
|----------|-------------|
| `cMessage` | A string message to print. |

Example 1: This example prints the value of a field to the console window. The script could be executed during a mouse-up event.

```
var f = this.getField("myText");
console.clear(); console.show();
console.println("Field value = " + f.value);
```

Example 2: The console can be used as a debugging tool. For example, you can write values of variables to the console. The following script is at the document level:

```
var debugIsOn = true;
function myFunction ( n, m )
{
    if (debugIsOn)
    {
        console.println("Entering function: myFunction");
        console.println(" Parameter 1: n = " + n);
        console.println(" Parameter 2: m = " + m);
    }
    ....
    ....
    if (debugIsOn) console.println(" Return value: rtn = " + rtn);
    return rtn;
}
```

Beginning with Acrobat 6.0, debugging can also be accomplished with the JavaScript Debugger. See the dbg object.

<a id="54323"></a>
<a id="show"></a>
<a id="id358"></a>
#### show

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Shows the console window.

Example: Clear and show the console window:

```
console.clear();
console.show();
```

<a id="69212"></a>
<a id="data"></a>
<a id="id359"></a>
## Data

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

The Data object is the representation of an embedded file or data stream that is stored in the document. See the [PDF Reference](https://adobe.com/go/pdfreference) for details.

Using Data objects is a good way to associate and embed source files, metadata, and other associated data with a document. Data objects can be inserted from the external file system, queried, and extracted.

See the following Doc properties and methods:

- createDataObject, dataObjects, exportDataObject, getDataObject, importDataObject, removeDataObject, openDataObject, getDataObjectContents, and setDataObjectContents.

The following objects, properties and methods support PDF portfolios (also called PDF collections or PDF packages):

- `app.newCollection`, Doc. collection, Collection object, and collectionField object

> **Note**
>
> The Data object methods were implemented in Acrobat 5.0. However, the ability to use them in Adobe Reader with additional usage rights only became available in Adobe Reader 6.0.

<a id="data-properties"></a>
<a id="id361"></a>
### Data properties

<a id="35317"></a>
<a id="id362"></a>
<a id="id363"></a>
#### creationDate

The creation date of the file that was embedded.

| Type | Access |
|------|--------|
| Date | R |

<a id="89891"></a>
<a id="id364"></a>
<a id="id365"></a>
#### description

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.05 | No | No | All | String | R/W |

The description associated with this data object.

<a id="45643"></a>
<a id="id366"></a>
<a id="id367"></a>
#### MIMEType

The MIME type associated with this data object.

| Type | Access |
|------|--------|
| String | R |

<a id="17649"></a>
<a id="id368"></a>
<a id="id369"></a>
#### modDate

The modification date of the file that was embedded.

| Type | Access |
|------|--------|
| Date | R |

<a id="27704"></a>
<a id="id370"></a>
<a id="id371"></a>
#### name

The name associated with this data object.

| Type | Access |
|------|--------|
| String | R |

Example: Display the names of file attachments to this document.

```
console.println("Dumping all data objects in the document.");
var d = this.dataObjects;
for (var i = 0; i < d.length; i++)
    console.println("DataObject[" + i + "]=" + d[i].name);
```

<a id="11291"></a>
<a id="id372"></a>
<a id="id373"></a>
#### path

The file name and extension of the file that was embedded.

| Type | Access |
|------|--------|
| String | R |

<a id="68523"></a>
<a id="id374"></a>
<a id="id375"></a>
#### size

The size, in bytes, of the uncompressed data object.

| Type | Access |
|------|--------|
| Number | R |

<a id="data-methods"></a>
<a id="id376"></a>
### Data methods

<a id="72277"></a>
<a id="getfieldvalue"></a>
<a id="id377"></a>
#### getFieldValue

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 9.0 | No | No | All |

Get the value of the field as specified by the `name` parameter for this embedded file. When attempting to get a field value that is not defined in the collection schema, `null` is returned.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `name` | A string that identifies the field of interest. |
| `includePrefix` | (Optional) A Boolean value indicating whether the prefix should be included with the returned string. If `true`, the prefix is included with the return string. The default is `false`. |

**Returns**

The value of the field, or `null` if field is not present in schema.

<a id="16110"></a>
<a id="setfieldvalue"></a>
<a id="id378"></a>
#### setFieldValue

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 9.0 | No | No | All |

Type conversion is performed when setting field values. The type conversion is determined by the collectionField in the schema. When attempting to set a field value that is not defined in the schema, an exception is raised.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `name` | A string that identifies the field of interest. An exception raised if `name` not present in schema. |
| `value` | A string, a number, or a date that specifies the value of the field. The value will be type-coerced to match the schema. |
| prefix | (Optional) A string that specifies the field value prefix. |

**Returns**

The value of the field, or `null` if field is not present in schema.

Example: Get and set field values of the first data object in this collection.

```
var d = this.dataObjects[0];
d.setFieldValue("subject", "New laptop!", "RE: ");

// Now get the same field value we just set. Here s = "RE: New laptop!"
var s = d.getFieldValue({ name:"subject", includePrefix:true });

// Get the same field value, with includePrefix set to false, the default
// Now the value of s is "New laptop!".
s = d.getFieldValue("subject");

// Sets subject to "A. C. Robat" and clears prefix
d.setFieldValue("subject", "A. C. Robat");
```

<a id="80986"></a>
<a id="datasourceinfo"></a>
<a id="id379"></a>
## DataSourceInfo

This generic JavaScript object contains basic information about a database. The `ADBC.getDataSourceList` method returns an array of these objects.

<a id="datasourceinfo-properties"></a>
<a id="id380"></a>
### DataSourceInfo properties

<a id="59989"></a>
<a id="id381"></a>
<a id="id382"></a>
#### name

A string that represents the identifying name of a database. This string can be passed to `newConnection` to establish a connection to the database that the `DataSourceInfo` object is associated with.

| Type | Access |
|------|--------|
| String | R |

<a id="21861"></a>
<a id="id383"></a>
<a id="id384"></a>
#### description

A string that contains database-dependent information about the database.

| Type | Access |
|------|--------|
| String | R |

<a id="65262"></a>
<a id="dbg"></a>
<a id="id385"></a>
## dbg

The `dbg` object is a static object that can be used to control the JavaScript Debugger from a command-line console. Its methods provide the same functionality as the buttons in the JavaScript Debugger dialog box toolbar. In addition, breakpoints can be created, deleted, and inspected using the `dbg` object.

The `dbg` object and the JavaScript Debugger are only available in Acrobat Pro.

> **Note**
>
> If the viewer locks up during a debugging session, pressing Esc may resolve the problem.

Debugging is not possible with a modal dialog box open; for example, when debugging a batch sequence.

Debugging a script with a running event initiated by either `app.setInterval` or `app.setTimeOut` may cause recurring alert boxes to appear. Use Esc after the modal dialog box is dismissed to resolve the problem.

(Acrobat 7.0) While the Debugger is open and a debugging session is under way, the Acrobat application is unavailable.

<a id="dbg-properties"></a>
<a id="id386"></a>
### dbg properties

<a id="45894"></a>
<a id="bps"></a>
<a id="id387"></a>
#### bps

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | P | Array | R |

An array of *breakpoint generic objects* corresponding to breakpoints set in the debugger. This object contains the following properties and methods.

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `fileName` | string | R | A string that identifies the script in the debugger. |
| `condition` | string | R | A JavaScript expression evaluated by the debugger to decide to whether to stop at a breakpoint. Used to create conditional breakpoints. The default value for this property is the string “true”. |
| `lineNum` | number | R | The line number in the script for which the breakpoint is set. |

| Method | Parameters | Returns | Description |
|--------|------------|---------|-------------|
| `toString` | none | String | A string describing the breakpoint. |

Example: List all currently active breakpoints.

```
var db = dbg.bps
for ( var i = 0; i < db.length; i++ )
{
    for ( var o in db[i] ) console.println(o + ": " + db[i][o]);
    console.println("------------------------------------");
}
```

See sb for another example of usage.

<a id="dbg-methods"></a>
<a id="id388"></a>
### dbg methods

<a id="24979"></a>
<a id="c"></a>
<a id="id389"></a>
#### c

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Acrobat Pro only |

The `c` (continue) method resumes execution of a program stopped in the debugger. The JavaScript program may either stop again, depending on where the breakpoints are set, or reach execution end.

<a id="54263"></a>
<a id="cb"></a>
<a id="id390"></a>
#### cb

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | No | Acrobat Pro only |

The `cb` (clear breakpoint) method clears a breakpoint in the debugger. The `dbg.cb` method dirties the document only if breakpoints are stored in the document, as set through the user preferences, Edit > Preferences > JavaScript.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `fileName` | The name of the script from where the breakpoint is going to be deleted. |
| `lineNum` | The line number for the breakpoint that is going to be cleared in the script. |

<a id="14994"></a>
<a id="q"></a>
<a id="id391"></a>
#### q

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | No | Acrobat Pro only |

The `q` (quit) method quits debugging and executing the current JavaScript. It additionally dismisses the debugger dialog box.

<a id="85448"></a>
<a id="sb"></a>
<a id="id392"></a>
#### sb

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | No | Acrobat Pro only |

The `sb` (set breakpoint) method sets a new breakpoint in the debugger. The `dbg.sb` method dirties the document only if breakpoints are stored in the document, as set through the user preferences, Edit > Preferences > JavaScript.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `fileName` | The name of the script where the breakpoint is to be set. |
| `lineNum` | The line number in the script to create the breakpoint. |
| `condition` | (optional) a JavaScript expression to be evaluated when the debugger reaches the breakpoint. If the expression evaluates to `true`, the debugger stops at the breakpoint. If the expression evaluates to `false`, the debugger continues executing the script and does not stop at the breakpoint. The default value is `true`. |

Example 1: Some script is run and an exception is thrown due to some error. A breakpoint is programmatically set using the information given in the error message.

```
SyntaxError: missing ; before statement 213:Document-Level: myDLJS
// now set a breakpoint using the console
dbg.sb({
    fileName: "Document-Level: myDLJS",
    lineNum: 213,
    condition: "true"
});
```

Example 2: Simulate the functionality of the Store Breakpoints in PDF File check box in the JavaScript user preferences.

```
// Save breakpoints in PDF file
this.addScript("myBreakpoints", "var myBPS = " + dbg.bps.toSource());

// Now reset the breakpoints
for ( var i = 0; i < myBPS.length; i++ ) dbg.sb( myBPS[i] );
```

Example 3: Set a conditional break. Consider the following code, which is a mouse-up action.

```
for (var i=0; i<100; i++)
    myFunction(i);          // defined at document level

// In the console, set a conditional break. Here, we break when the

 // index of the loop is greater than 30.
dbg.sb({
    fileName:"AcroForm:Button1:Annot1:MouseUp:Action1",
    lineNum:2,
    condition:"i > 30"
})
```

<a id="70905"></a>
<a id="si"></a>
<a id="id393"></a>
#### si

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Acrobat Pro only |

The `si` (step in) method advances the program pointer to the next instruction in the JavaScript program, entering each function call for which there is a script defined. (Native JavaScript calls cannot be stepped into.)

<a id="67180"></a>
<a id="sn"></a>
<a id="id394"></a>
#### sn

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Acrobat Pro only |

The `sn` (step instruction) method advances the program pointer to the next bytecode in the JavaScript program. (Each JavaScript instruction is made up of several bytecodes as defined by the JavaScript interpreter.)

<a id="47502"></a>
<a id="so"></a>
<a id="id395"></a>
#### so

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Acrobat Pro only |

The `so` (step out) method executes the program until it exits the current function. Execution stops at the instruction immediately following the call to the current function. If the scope currently under debug is the top-level scope, the program either continues executing until it ends or stops again when it reaches a breakpoint.

<a id="92782"></a>
<a id="sv"></a>
<a id="id396"></a>
#### sv

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Acrobat Pro only |

The `sv` (step over) method advances the program pointer to the next instruction in the JavaScript program. If a function call is encountered, the debugger does not step into the instructions defined inside that function.

<a id="26032"></a>
<a id="dialog"></a>
<a id="id397"></a>
## Dialog

An instance of this object is passed as a parameter to dialog box handlers (see Dialog box handlers). These handlers include the `initialize`, `validate`, `commit`, `destroy` and *ItemID* methods of the dialog box descriptor object literal that is passed to `app.execDialog`. The Dialog object allows the current state of the Dialog to be queried and set.

<a id="dialog-methods"></a>
<a id="id398"></a>
### Dialog methods

<a id="83122"></a>
<a id="enable"></a>
<a id="id399"></a>
#### enable

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Enables or disables various dialog box elements using the object literal passed in.

Typically, `enable` is called in the `initialize` method (see Dialog box handlers) of the object literal passed to `app.execDialog` to preset whether various dialog box elements are enabled or not.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| object literal | For each dialog box item to modify, there should be an entry in the object literal with the Dialog *ItemID* as the label and a Boolean value as the value indicating if it is enabled or not. |

Example: See the examples following `app.` execDialog.

<a id="99912"></a>
<a id="end"></a>
<a id="id400"></a>
#### end

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Terminates a currently executing dialog box (as if the Cancel button had been pressed). This method takes an optional parameter of the *ItemID*, a string, of the dialog box element that will be reported as dismissing the dialog. This *ItemID* will be the return value of the `app.execDialog` call that created the dialog.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| String | (optional) The *ItemID* of the dialog box element that will be reported as dismissing the dialog. |

Example: See the examples following `app.` execDialog.

<a id="32700"></a>
<a id="load"></a>
<a id="id401"></a>
#### load

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Sets the values of dialog box elements using the object literal passed in. Dialog box items are identified by an *ItemID* which is a unique 4-character string.

Typically, `load` is called in the `initialize` method (see Dialog box handlers) of the object literal passed to `app.execDialog` to preset the value of various dialog box elements.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| object literal | For each dialog box item to be modified, there should be an entry in the object literal with the *ItemID* as the label and the dialog box element setting as the contents. If the dialog box element takes multiple values (for example, a `list_box` or a `popup`), the value should be an object literal consisting of the displayed entry as the label and a numeric value as the contents. Similarly, if the dialog box element is hierarchical in nature (for example, a `hier_list_box`), the value should be a set of nested object literals. If the numeric value is greater than 0, the item is selected, otherwise it is not selected. |

Example: See the examples following `app.` execDialog.

<a id="63111"></a>
<a id="store"></a>
<a id="id402"></a>
#### store

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Gets the values of dialog box elements as an object literal returned. Dialog box items are identified by an *ItemID*, which is a unique 4-character string. For each dialog box element, there will be an entry in the object literal with the *ItemID* as the label and the dialog box element setting as the contents. If the dialog box element takes multiple values (for example, a `list_box` or a `popup`), the value should be an object literal consisting of the displayed entry as the label and a numeric value as the contents. If the numeric value is greater than 0, the item was selected, otherwise it was not selected.

Typically, `store` is called in the `commit` method (see Dialog box handlers) of the object literal passed to `app.execDialog` to extract the value of various dialog box elements.

**Returns**

object literal

<a id="70131"></a>
<a id="dirconnection"></a>
<a id="id403"></a>
## DirConnection

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | All |

This object represents an open connection to a directory: a repository of user information, including public-key certificates. Directory connections are opened using the `Directory` object `connect` method. A directory with a particular name can have more than one connection open at a time. All DirConnection objects must support all properties and methods listed here, unless otherwise specified.

> **Note**
>
> This object can only be obtained from a `Directory` object and is thus governed by the security restrictions of the `Directory` object. The `DirConnection` object is therefore available only for batch, console and application initialization, including in Adobe Reader. See also priv.

<a id="dirconnection-properties"></a>
<a id="id404"></a>
### DirConnection properties

<a id="61351"></a>
<a id="canlist"></a>
<a id="id405"></a>
#### canList

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

Indicates whether the directory connection is capable of listing all of its entries. Some directories may contain too many entries for this operation to be practical.

Example: The AAB directory allows listing of the local trusted identity list.

```
var sh = security.getHandler( "Adobe.AAB" );
var dc = sh.directories[0].connect();
console.println( "CanList = " + dc.canList );
```

<a id="54768"></a>
<a id="candocustomsearch"></a>
<a id="id406"></a>
#### canDoCustomSearch

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

Specifies whether the directory connection supports searching using directory-specific search parameter attributes. For example, directory-specific attributes for an LDAP directory include o (organization), c (country), cn (common name), givenname, sn (surname), uid, st, postalcode, mail, and telephonenumber.

<a id="19446"></a>
<a id="candocustomuisearch"></a>
<a id="id407"></a>
#### canDoCustomUISearch

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

Specifies whether the directory connection supports searching using its own custom user interface to collect the search parameters.

<a id="64521"></a>
<a id="candostandardsearch"></a>
<a id="id408"></a>
#### canDoStandardSearch

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Boolean | R |

Specifies whether the directory connection supports search using standard search parameter attributes. The standard attributes are

```
firstName
lastName
fullName
email
certificates
```

Some directory database implementations may not support these attributes, but directory handlers are free to translate these attributes to names understood by the directory.

<a id="38818"></a>
<a id="groups"></a>
<a id="id409"></a>
#### groups

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Array | R |

An array of language-dependent names for groups that are available through this connection.

<a id="68524"></a>
<a id="id410"></a>
<a id="id411"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | String | R |

The language-independent name of the directory that this object is connected to. An example of this would be `Adobe.PPKMS.ADSI.dir0`. All `DirConnection` objects must support this property.

<a id="66947"></a>
<a id="uiname"></a>
<a id="id412"></a>
#### uiName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | String | R |

The language-dependent string of the directory this object is connected to. This string is suitable for user interfaces. All `DirConnection` objects must support this property.

<a id="dirconnection-methods"></a>
<a id="id413"></a>
### DirConnection methods

<a id="65566"></a>
<a id="search"></a>
<a id="id414"></a>
#### search

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | All |

Searches the directory and returns an array of UserEntity objects that match the search parameters. A `UserEntity` object is a generic object that contains properties for all attributes that were requested by the `setOutputFields` method. If the `setOutputFields` method is not called prior to a search, it would return a `UserEntity` object containing no entries.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oParams` | (optional) A generic object containing an array of key-value pairs consisting of search attribute names and their corresponding strings. If `oParams` is not provided and `canList` is `true` for this directory, all entries in the directory will be returned. If `oParams` is not provided and `canList` is `false`, an exception occurs. |
| `cGroupName` | (optional) The name of a group (not to be confused with `Group` objects). If specified, the search will be restricted to this group. |
| `bCustom` | (optional) If `false` (the default), `oParams` contains standard search attributes. If `true`, `oParams` contains directory-specific search parameters. If the `canDoCustomSearch` property is not `true`, an exception occurs. |
| `bUI` | (optional) If `true`, the handler displays the user interface to allow collection of search parameters. The results of the search are returned by this method. `canDoCustomUISearch` must also be `true` if `bUI` is `true`, or an exception will occur. If `bUI` is specified, `bCustom` must also be specified, though its value is ignored. |

**Returns**

An array of `UserEntity` objects.

Example 1: Directory search.

```
var sh = security.getHandler( "Adobe.PPKMS" );
var dc= sh.directories[0].connect();
dc.setOutputFields( {oFields:["certificates","email"]} )
var retVal = dc.search({oParams:{lastName:"Smith"}});
if( retVal.length )
console.println( retVal[0].email );
```

Example 2: List all entries in a local Acrobat Address Book. The script searches the directory and returns an array of users, along with their certificate information.

```
var sh = security.getHandler( "Adobe.AAB" );
var dc = sh.directories[0].connect();
if( dc.canList ) {
    var x = dc.search();
    for( j=0; j<x.length; ++j ) {
        console.println("Entry[" + j + "] = " + x[j].fullName + ":");
        for(i in x[j]) console.println("  " + i + " = " + x[j][i]);
    }
}
```

<a id="45615"></a>
**UserEntity object**

A generic JavaScript object that describes a user in a directory and the user’s associated certificates. It contains standard properties that have a specific meaning for all directory handlers. Directory handlers translate these entries to the ones that are specific to them when required. An array of these objects is returned by the `search` method of the `DirConnection` object.

It has the following properties

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `firstName` | String | R/W | The first name of the user. |
| `lastName` | String | R/W | The last name of the user. |
| `fullName` | String | R/W | The full name of the user. |
| `certificates` | Array of `Certificate` objects | R/W | An array of certificates that belong to this user. To find a certificate that is to be used for a particular use, the caller should inspect the certificate’s `keyUsage` property. |
| `defaultEncryptCert` | Array of `Certificate` objects | R/W | The preferred certificate to use when encrypting documents for this user entity. Routines that process user entity objects will look first to this property when choosing an encryption certificate. If this property is not set, the first valid match in the certificates property will be used. |

<a id="89710"></a>
<a id="setoutputfields"></a>
<a id="id415"></a>
#### setOutputFields

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Defines the list of attributes that should be returned when executing the `search` method.

> **Note**
>
> This method is not supported by the Adobe.AAB directory handler. Custom options are not supported by the Adobe.PPKMS.ADSI directory handler.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oFields` | An array of strings containing the names of attributes that should be returned from the directory when calling the search method. The names in this array must either be names of standard attributes that can be used for all directory handlers or custom attributes that are defined for a particular directory. The standard attributes are the property names defined for the `UserEntity` object. Directory handlers can, when needed, translate standard attribute names to names that it understands. |
| `bCustom` | (optional) A Boolean value indicating that the names in `oFields` are standard output attribute names. If `true`, the names represent directory-specific attributes that are defined for a particular directory handler. The default is `false`. |

**Returns**

An array of strings, containing the names of attributes from `oFields` that are not supported by this directory. An empty array is returned if the `oFields` array is empty.

Example: In this example, `dc.setOutputFields` returns the array of strings `["x", "y"]`.

```
var sh = security.getHandler("Adobe.PPKMS");
var dc = sh.directories[0].connect();
var w = dc.setOutputFields( [ "certificates", "email", "x", "y"] );
console.println( w );
```

See also the examples that follow the `DirConnection.search` method.

<a id="60701"></a>
<a id="directory"></a>
<a id="id416"></a>
## Directory

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | All |

Directories are a repository of user information, including public-key certificates. Directory objects provide directory access and are obtained using the `directories` property or the `newDirectory` method of the `SecurityHandler` object.

Acrobat 6.0 and later provides several directories. The Adobe.AAB Security Handler has a single directory named Adobe.AAB.AAB. This directory provides access to the local Acrobat Address Book, also called the *trusted identity store*. On Windows, the Adobe.PPKMS Security Handler provides access through the Microsoft Active Directory Script Interface (ADSI) to as many directories as have been created by the user. These directories are created sequentially with names `Adobe.PPKMS.ADSI.dir0`, `Adobe.PPKMS.ADSI.dir1`, and so on.

> **Note**
>
> This object can only be obtained from a `SecurityHandler` object and is thus governed by the security restrictions of the `SecurityHandler` object. The Directory object is therefore available only for batch, console and application initialization, including in Adobe Reader. See also priv.

<a id="directory-properties"></a>
<a id="id417"></a>
### Directory properties

<a id="53347"></a>
<a id="info"></a>
<a id="id418"></a>
#### info

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | All | Object | R/W |

The value of this property is a `DirectoryInformation` object, a generic object used to set and get the properties for this `Directory` object.

Example:

```
// Create and activate a new directory
var oDirInfo = { dirStdEntryID: "dir0",
    dirStdEntryName: "Employee LDAP Directory",
    dirStdEntryPrefDirHandlerID: "Adobe.PPKMS.ADSI",
    dirStdEntryDirType: "LDAP",
    server: "ldap0.example.com",
    port: 389 };
var sh = security.getHandler( "Adobe.PPKMS" );
var newDir = sh.newDirectory();
newDir.info = oDirInfo;
```

<a id="56624"></a>
**DirectoryInformation object**

A directory information object is a generic object representing the properties for a directory and has the following standard properties.

| Property | Type | Access | Required | Description |
|----------|------|--------|----------|-------------|
| `dirStdEntryID` | String | R/W | Yes | A unique, language-independent name for the directory. Must be alphanumeric and can include underscores, periods and hyphens. For new directory objects, it is suggested that the ID not be provided, in which case a new unique name will be automatically generated. |
| `dirStdEntryName` | String | R/W | Yes | A user-friendly name for the directory. |
| `dirStdEntryPrefDirHandlerID` | String | R/W | No | The name of the directory handler to be used by this directory. Security handlers can support multiple directory handlers for multiple directory types (for example, local directories and LDAP directories). |
| `dirStdEntryDirType` | String | R/W | No | The type of directory. Examples of this are LDAP, ADSI, and WINNT. |
| `dirStdEntryVersion` | String | R | No | The version of the data. The default value is 0 if this is not set by the directory. The value for Acrobat 6.0 directories for the Adobe.AAB and Adobe.PPKMS.ADSI directory handlers is `0x00010000`. |

Directory information objects can include additional properties that are specific to a particular directory handler. The Adobe.PPKMS.ADSI directory handler includes the following additional properties:

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `server` | String | R/W | The server that hosts the data. For example, addresses.employees.example.com. |
| `port` | Number | R/W | The port number for the server. The standard LDAP port number is 389. |
| `searchBase` | String | R/W | Narrows the search to a particular section of the directory. An example of this is  o=XYZ Systems,c=US. |
| `maxNumEntries` | Number | R/W | The maximum number of entries to be retrieved in a single search. |
| `timeout` | Number | R/W | The maximum time allowed for a search. |

Example 1: Create and activate a new directory.

```
var oDirInfo = { dirStdEntryID: "dir0",
    dirStdEntryName: "Employee LDAP Directory",
    dirStdEntryPrefDirHandlerID: "Adobe.PPKMS.ADSI",
    dirStdEntryDirType: "LDAP",
    server: "ldap0.example.com",
    port: 389
};
var sh = security.getHandler( "Adobe.PPKMS" );
var newDir = sh.newDirectory();
newDir.info = oDirInfo;
```

Example 2: Get information for an existing directory.

```
var sh = security.getHandler("Adobe.PPKMS");
var dir0 = sh.directories[0];
// Get directory info object just once for efficiency
var dir0Info = dir0.info;
console.println( "Directory " + dir0Info.dirStdEntryName );
console.println( "address " + dir0Info.server + ":" + dir0Info.port );
```

<a id="directory-methods"></a>
<a id="id419"></a>
### Directory methods

<a id="36168"></a>
<a id="connect"></a>
<a id="id420"></a>
#### connect

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | All |

**Returns** a `DirConnection` object that is a connection to the directory with the specified name. There can be more than one active connection for a directory.

See also the DirConnection object and the `SecurityHandler` object’s directories property.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oParams` | (optional) A generic object that can contain parameters that are necessary to create the connection. Properties of this object are dependent on the particular directory handler and can include `userid` and `password`. |
| `bUI` | (optional) A Boolean value whose default is `false`. It specifies whether the directory handler can bring its UI, if required for establishing the connection. |

**Returns**

A `DirConnection` object, or `null` if there is no directory with the specified name.

Example: Enumerate available directories and connect.

```
var sh = security.getHandler( "Adobe.PPKMS" );
var dirList = sh.directories;
for ( var i=0; i< dirList.length; i++)
    for ( var o in dirList[i].info )
        console.println( o + " = " + dirList[i].info[o]);
var dirConnection = dirList[0].connect();
```

<a id="92005"></a>
<a id="embedded-pdf"></a>
<a id="id421"></a>
## Embedded PDF

This object describes an API exposed to the object model of a container application that allows sending and receiving messages from an embedded PDF document. For example, when a PDF document is embedded in an HTML document using the `<OBJECT>` tag, the PDF object is scripted in the browser scripting context.

The `HostContainer` object provides the corresponding interface in the PDF scripting model. Both the container and PDF document must explicitly allow this communication to occur for security reasons.

<a id="embedded-pdf-properties"></a>
<a id="id422"></a>
### Embedded PDF properties

<a id="71300"></a>
<a id="messagehandler"></a>
<a id="id423"></a>
#### messageHandler

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0.5 | No | No | All | Object | R/W |

This property allows a script running in the web browser scripting context to register a notification object that will be called if a script in the PDF document calls the Doc `hostContainer.postMessage` method.

The value of this property is an object that may expose the following methods.

| Method | Description |
|--------|-------------|
| `onMessage` | If present, this method will be called in response to the Doc `hostContainer.postMessage` method. The message is delivered asynchronously. The method is passed a single array parameter containing the array passed to the `postMessage` method. |
| `onError` | If present, this method will be called in response to an error. It is passed an Error object and an array of strings corresponding to the message that caused the error. If an error occurs and this property is undefined, the error will not be delivered (unlike messages, errors are not queued).  The `name` property of the `Error` object will be set to one of the following strings:  -  “MessageGeneralError”: A general error occurred. -  “MessageNotAllowedError”: The operation failed for security reasons. -  “MessageDocNotDisclosedError”: The document has not been configured for disclosure to the host container. The `hostContainer.messageHandler.onDisclose` property of the Doc must be initialized correctly. -  “MessageDocRefusedDisclosureError”: The document has refused to disclose itself to the host container based on the URL because the `hostContainer.messageHandler.onDisclose` method returned `false`. |

When the methods are invoked, the `this` object will be the `messageHandler` instance that the method is being called on. Properties on the `messageHandler` property that begin with `on` are reserved for future use as notification methods.

If the PDF document has had the `postMessage` method called on it prior to this method being registered, all of the queued messages will subsequently be passed to the `messageHandler` object once it is set.

Messages are guaranteed to be delivered in the order in which they are posted and errors are guaranteed to be delivered in the order in which they occurred. However, there is no correspondence between the delivery order of messages and errors.

**Exceptions** thrown from within the handler methods will be discarded. Messages and errors will not be delivered while inside an `onMessage` / onError `handler`.

> **Note**
>
> This property is not implemented on the Mac OS platform.

<a id="embedded-pdf-methods"></a>
<a id="id424"></a>
### Embedded PDF methods

<a id="48590"></a>
<a id="postmessage"></a>
<a id="id425"></a>
#### postMessage

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0.5 | No | No | All |

Sends a message asynchronously to the PDF document message handler if the PDF document has disclosed itself by returning `true` from the `onDisclosed` method of the `HostContainer` object `messageHandler` property.

The message is passed to the `onMessage` method of the `messageHandler`.

If the PDF document does not disclose itself to the host container, an error will be passed to the `onError` method of the `messageHandler` property at some later point after `postMessage` has returned. If the PDF document has not registered to receive events by setting the Doc `hostContainer.messageHandler` property, the events will be queued until the PDF document sets the property.

The messages will be submitted to a queue of messages until they are delivered. If the queue size exceeds a maximum, an error will be thrown until some of the messages in the queue have been delivered.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `aMessage` | An array of one or more strings that will be passed to `onMessage`. |

> **Note**
>
> This method is not implemented on the Mac OS platform.

<a id="13935"></a>
<a id="error"></a>
<a id="id426"></a>
## Error

Error objects are dynamically created whenever an exception is thrown from methods or properties implemented in JavaScript. Several subclasses of the Error object can be thrown by core JavaScript (`EvalError`, `RangeError`, `SyntaxError`, `TypeError`, `ReferenceError`, `URLError`). They all have the Error object as prototype. JavaScript can throw some of these exceptions, or implement subclasses of the Error object at its convenience. If your scripts are using the mechanism of `try/catch` error handling, the object thrown should be one of the types listed in the following table.

| Error object | Brief description |
|--------------|-------------------|
| `RangeError` | Argument value is out of valid range. |
| `TypeError` | Wrong type of argument value. |
| `ReferenceError` | Reading a variable that does not exist. |
| `MissingArgError` | Missing required argument. |
| `NumberOfArgsError` | Invalid number of arguments to a method. |
| `InvalidSetError` | A property set is not valid or possible. |
| `InvalidGetError` | A property get is not valid or possible. |
| `OutOfMemoryError` | Out of memory condition occurred. |
| `NotSupportedError` | Functionality not supported in this configuration (for example, Adobe Reader). |
| `NotSupportedHFTError` | HFT is not available (a plug-in may be missing). |
| `NotAllowedError` | Method or property is not allowed for security reasons. |
| `GeneralError` | Unspecified error cause. |
| `RaiseError` | Acrobat internal error. |
| `DeadObjectError` | Object is dead. |
| `HelpError` | User requested for help with a method. |

Error object types implemented by JavaScript inherit properties and methods from the core Error object. Some JavaScript objects may implement their own specific types of exception. A description of the Error subclass (with added methods and properties, if any) should be provided in the documentation for the particular object.

Example: Print all properties of the Error object to the console.

```
try {
    app.alert(); // one argument is required for alert
} catch(e) {
    for (var i in e)
    console.println( i + ": " + e[i])
}
```

<a id="error-properties"></a>
<a id="id427"></a>
### Error properties

<a id="50406"></a>
<a id="filename"></a>
<a id="id428"></a>
#### fileName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

The name of the script that caused the exception to be thrown.

<a id="67199"></a>
<a id="linenumber"></a>
<a id="id429"></a>
#### lineNumber

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R |

The offending line number from where an exception was thrown in the JavaScript code.

<a id="43381"></a>
<a id="extmessage"></a>
<a id="id430"></a>
#### extMessage

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | String | R |

A message providing additional details about the exception.

<a id="71361"></a>
<a id="message"></a>
<a id="id431"></a>
#### message

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

The error message providing details about the exception.

<a id="24685"></a>
<a id="id432"></a>
<a id="id433"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R/W |

The name of the `Error` object subclass, indicating the type of the `Error` object instance.

<a id="error-methods"></a>
<a id="id434"></a>
### Error methods

<a id="69913"></a>
<a id="tostring"></a>
<a id="id435"></a>
#### toString

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Gets the error message that provides details about the exception.

**Returns**

The error message string. (See the message property.)

<a id="43659"></a>
<a id="fdf"></a>
<a id="id538"></a>
## FDF

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | All |

This object corresponds to a PDF-encoded data exchange file. Typically, FDF files contain forms data that is exported from a PDF file. However, FDF files can also be used as general purpose data files and it is for this latter purpose that the FDF object exists.

All security methods and properties are available only during batch, console, and application initialization events. See priv.

<a id="fdf-properties"></a>
<a id="id539"></a>
### FDF properties

<a id="61881"></a>
<a id="deleteoption"></a>
<a id="id540"></a>
#### deleteOption

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | Yes | Not available in Reader | Integer | R/W |

Indicates whether the FDF file should be automatically deleted after it is processed. This value may or may not be used, depending on the content of the FDF file and how it is processed. It is used for embedded files beginning in Acrobat 6.0. Allowed values are

- *0*: (default) Acrobat will automatically delete the FDF file after processing
- *1*: Acrobat will not delete the FDF file after processing (however, a web or email browser may still delete the file).
- *2*: Acrobat will prompt the user to determine whether to delete the FDF file after processing (however, a web or email browser may still delete the file).

<a id="83309"></a>
<a id="issigned"></a>
<a id="id541"></a>
#### isSigned

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All but Reader | Boolean | R |

**Returns** `true` if the FDF data file is signed.

Example: See if the fdf is signed.

```
var fdf = app.openFDF("/C/temp/myDoc.fdf");
console.println( "It is "+ fdf.isSigned + " that this FDF is signed");
fdf.close();
```

See a more complete example following signatureSign.

<a id="69469"></a>
<a id="numembeddedfiles"></a>
<a id="id542"></a>
#### numEmbeddedFiles

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All but Reader | Integer | R |

The number of files embedded in the FDF file. If the `FDF` object is a valid FDF file, no exceptions will be thrown.

A file may be embedded in an FDF file with the addEmbeddedFile method.
Example: Create a new FDF object, embed a PDF doc, save the FDF, open the FDF again, and count the number of embedded files.

```
var fdf = app.newFDF();
fdf.addEmbeddedFile("/C/myPDFs/myDoc.pdf");
fdf.save("/c/temp/myDocWrapper.fdf");
fdf = app.openFDF("/c/temp/myDocWrapper.fdf");
console.println("The number of embedded files = "
    + fdf.numEmbeddedFiles);
fdf.close();
```

<a id="fdf-methods"></a>
<a id="id543"></a>
### FDF methods

<a id="59252"></a>
<a id="addcontact"></a>
<a id="id544"></a>
#### addContact

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | Yes | Not allowed in Reader: Only available in Acrobat products |

Adds a contact to the FDF file.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oUserEntity` | An `UserEntity` object that list the contact to be added to the FDF file. |

**Returns**

Throws an exception on failure.

Example:

```
var oEntity={firstName:"Fred", lastName:"Smith", fullName:"Fred Smith"};
var f = app.newFDF();
f.addContact( oEntity );
f.save( "/c/temp/FredCert.fdf" );
```

<a id="10402"></a>
<a id="addembeddedfile"></a>
<a id="id545"></a>
#### addEmbeddedFile

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Add the specified file to the end of the array of embedded files in the FDF file. Anyone opening the FDF file will be instructed to save the embedded file or files according to `nSaveOption`. If the embedded file is a PDF file, it is opened and displayed. If the embedded file is an FDF file, the file is opened for processing.

FDF files containing embedded files have been supported beginning with Acrobat 4.05. An example use for embedding PDF files is when these files are hosted on an HTTP server and the user should click to download and save the PDF file, rather than viewing the file in the browser. There is no relationship between these embedded files and files that are associated with forms data that is stored in an FDF file.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cDIPath` | (optional) A device-independent absolute path to a file on the user’s hard drive. If not specified, the user is prompted to locate a file. |
| `nSaveOption` | (optional) Specifies how the embedded file will be presented to the user opening this FDF file, where the file will be saved, and whether the file will be deleted after it is saved. Values are: * *0*: The file will be saved to the Acrobat document folder. In Acrobat 8, the user will see a confirmation dialog which must be agreed to before the file will be saved to the disk * *1*: (the default) The user will be prompted for a file name to which to save the embedded file. * *2*: Should not be used. * *3*: The file will be automatically saved as a temporary file and deleted during cleanup (when Acrobat is closed).  In Acrobat 4.05 through 5.05, for values of `0` and `3`, the user is prompted for the location of the save folder if they have not already set this value.   For all values of `nSaveOption`, if the file is a PDF or FDF file, it is automatically opened by Acrobat after it is saved. |

**Returns**

Throws an exception if this operation could not be completed, otherwise returns the number of embedded files that are now in the FDF file.

Example: Create a new FDF, embed a PDF doc, then save.

```
var fdf = app.newFDF();
fdf.addEmbeddedFile("/C/myPDFs/myDoc.pdf");
fdf.save("/c/temp/myDocs.fdf");
```

<a id="71568"></a>
<a id="addrequest"></a>
<a id="id546"></a>
#### addRequest

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Adds a request to the FDF file. There can be only one request in an FDF file. If the FDF file already contains a request, it is replaced with this new request.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cType` | What is being requested. Currently the only valid value is the string “CMS”, which is a request for contact information. |
| `cReturnAddress` | The return address string for the request. This must begin with  `mailto:, http: or https:` and be of the form `"http://www.example.com/cgi.pl"` or `"mailto:jdoe@example.com"`. |
| `cName` | (optional) The name of the person or organization that has generated the request. |

**Returns**

Throws an exception if there is an error.

Example:

```
var f = app.newFDF();
f.addRequest( "CMS", "http://www.example.com/cgi.pl", "Acme Corp" );
f.save( "/c/tmp/request.fdf" );
```

<a id="49024"></a>
<a id="close"></a>
<a id="id547"></a>
#### close

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Immediately closes the FDF file.

**Returns**

Throws an exception if there is an error.

See the `FDF` object save method, which also closes an FDF file.

Example: See example following the addEmbeddedFile method.

<a id="38284"></a>
<a id="mail"></a>
<a id="id548"></a>
#### mail

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Saves the `FDF` object as a temporary FDF file and mails this file as an attachment to all recipients, with or without user interaction. The temporary file is deleted after it is no longer needed.

See also `a` pp. mailGetAddrs, `app.` mailMsg, the Doc methods mailDoc and mailForm, and the `Report` object method mail.

> **Note**
>
> On Windows, the client computer must have its default mail program configured to be MAPI enabled to use this method.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `bUI` | (optional) Specifies whether to display a user interface. If `true` (the default), the rest of the parameters are used to seed a compose-new-message window that is displayed to the user. If `false`, the `cTo` parameter is required and all others are optional.   -  (Acrobat 7.0) When this method is executed in a non-privileged context, the `bUI` parameter is not honored and defaults to `true`. See priv. |
| `cTo` | (optional) A semicolon-separated list of recipients for the message. |
| `cCc` | (optional) A semicolon-separated list of CC recipients for the message. |
| `cBcc` | (optional) A semicolon-separated list of BCC recipients for the message. |
| `cSubject` | (optional) The subject of the message. The length limit is 64 KB. |
| `cMsg` | (optional) The content of the message. The length limit is 64 KB. |

**Returns**

Throws an exception if there is an error.

Example:

```
var fdf = app.openFDF( "/c/temp/myDoc.fdf" );
/* This opens the compose new message window */
fdf.mail();

/* This will send out the mail with the attached FDF file to fun1@example.com

 and fun2@example.com */
fdf.mail( false, "fun1@example.com", "fun2@example.com", "",
    "This is the subject", "This is the body.");
```

<a id="72930"></a>
<a id="save"></a>
<a id="id549"></a>
#### save

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Save the `FDF` object as a file. A save will always occur. The file is closed when it is saved and the `FDF` object no longer contains a valid object reference.

See the close method, which also closes a FDF file.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cDIPath` | The device-independent path of the file to be saved.  -  `cDIPath` must be a safe path (see safe) and must have an extension of `.fdf`. |

**Returns**

Throws an exception if there is an error.

Example: Create a new FDF, embed a PDF doc, then save.

```
var fdf = app.newFDF()
fdf.addEmbeddedFile("/C/myPDFs/myDoc.pdf");
fdf.save("/c/temp/myDocs.fdf");
```

<a id="98207"></a>
<a id="signatureclear"></a>
<a id="id550"></a>
#### signatureClear

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

If the `FDF` object is signed, clears the signature and returns `true` if successful. Does nothing if the `FDF` object is not signed. Does not save the file.

**Returns**

`true` on success.

<a id="33751"></a>
<a id="signaturesign"></a>
<a id="id551"></a>
#### signatureSign

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Sign the `FDF` object with the specified security object. `FDF` objects can be signed only once. The `FDF` object is signed in memory and is not automatically saved as a file to disk. Call save to save the `FDF` object after it is signed. Call signatureClear to clear FDF signatures.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oSig` | The `SecurityHandler` object that is to be used to sign. Security objects normally require initialization before they can be used for signing. Check the documentation for your security handler to see if it is able to sign FDF files. The `signFDF` property of the SecurityHandler object will indicate whether a particular security object is capable of signing FDF files. |
| `oInfo` | (optional) A `SignatureInfo` object containing the writable properties of the signature. |
| `nUI` | (optional) The type of dialog box to show when signing. Values are: * *0*: Show no dialog box. * *1*: Show a simplified dialog box with no editable fields (fields can be provided in `oInfo`). * *2*: Show a more elaborate dialog box that includes editable fields for reason, location, and contact information.  The default is `0`. |
| `cUISignTitle` | (optional) The title to use for the sign dialog box. It is used only if `nUI` is non-zero. |
| `cUISelectMsg` | (optional) A message to display when a user must select a resource for signing, such as selecting a credential. It is used only when `nUI` is non-zero. |

**Returns**

`true` if the signature was applied successfully, `false` otherwise.

Example: Open an existing FDF data file and sign.

```
var eng = security.getHandler( "Adobe.PPKLite" );
eng.login("myPassword","/c/test/Acme.pfx");
var myFDF = app.openFDF( "/c/temp/myData.fdf" );
if( !myFDF.isSigned ) {
    myFDF.signatureSign({
        oSig: eng,
        nUI: 1,
        cUISignTitle: "Sign Embedded File FDF",
        cUISelectMsg: "Please select a Digital ID to use to "
            + "sign your embedded file FDF."
    });
    myFDF.save( "/c/temp/myData.fdf" );
};
```

<a id="81915"></a>
<a id="signaturevalidate"></a>
<a id="id552"></a>
#### signatureValidate

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All but Reader |

Validate the signature of an `FDF` object and return a `SignatureInfo` object specifying the properties of the signature.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oSig` | (optional) The security handler to be used to validate the signature. Can be either a `SecurityHandler` object or a generic object with the following properties: * *oSecHdlr*: The `SecurityHandler` object to use to validate this signature. * *bAltSecHdlr*: A Boolean value. If `true`, an alternate security handler, selected based on user preference settings, may be used to validate the signature. The default is `false`, meaning that the security handler returned by the signature’s `handlerName` property is used to validate the signature. This parameter is not used if `oSecHdlr` is provided.   If `oSig` is not supplied, the security handler returned by the signature’s `handlerName` property is used to validate the signature. |
| bUI | (optional) If `true`, allow the UI to be shown, if necessary, when validating the data file. The UI may be used to select a validation handler, if none is specified. |

**Returns**

A `SignatureInfo` object. The signature status is described in `status` property.

Example: Open an FDF file, if signed, validate it the signature and return information to the console.

```
fdf = app.openFDF("/c/temp/myDoc.fdf");
eng = security.getHandler( "Adobe.PPKLite" );
if (fdf.isSigned)
{
    var oSigInfo = fdf.signatureValidate({
        oSig: eng,
        bUI: true
    });
    console.println("Signature Status: " + oSigInfo.status);
    console.println("Description: " + oSigInfo.statusText);
} else {
    console.println("FDF not signed");
}
```

<a id="36795"></a>
<a id="field"></a>
<a id="id553"></a>
## Field

This object represents an Acrobat form field (that is, a field created using the Acrobat form tool or the Doc `addField` method). In the same manner that a form author can modify an existing field’s properties, such as the border color or font, the JavaScript user can use the Field object to perform the same modifications.

Before a field can be accessed, it must be bound to a JavaScript variable through a method provided by the Doc. More than one variable may be bound to a field by modifying the field’s object properties or accessing its methods. This affects all variables bound to that field.

```
var f = this.getField("Total");
```

This example allows the script to manipulate the form field “Total” by means of the variable `f`.

Fields can be arranged hierarchically within a document. For example, form fields with names like “FirstName” and “LastName” are called *flat names* and there is no association between them. By changing the field names, a hierarchy of fields within the document can be created.

For example, “Name.First” and “Name.Last” forms a tree of fields. The period (‘.’) separator in Acrobat forms denotes a hierarchy shift. “Name” in these fields is the parent; “First” and “Last” are the children. Also, the field “Name” is an *internal* field because it has no visible appearance. “First” and “Last” are *terminal* fields that appear on the page.

Acrobat form fields that share the same name also share the same value. Terminal fields can have different presentations of that data. For example, they can appear on different pages, be rotated differently, or have a different font or background color, but they have the same value. Therefore, if the value of one presentation of a terminal field is modified, all others with the same name are updated automatically.

Each presentation of a terminal field is referred to as a *widget*. An individual widget does not have a name but is identified by index (0-based) within its terminal field. The index is determined by the order in which the individual widgets of this field were created (and is unaffected by tab-order).

You can determine the index for a specific widget by using the Fields navigation tab in Acrobat. The index is the number that follows the ‘#’ sign in the field name shown. (In Acrobat 6.0 or later, the widget index is displayed only if the field has more than one widget.) You can double-click an entry in the Fields panel to go to the corresponding widget in the document. Alternatively, if you select a field in the document, the corresponding entry in the Fields panel is highlighted.

Beginning with Acrobat 6.0, `getField` can be used to retrieve the Field object of one individual widget of a field. This notation consists of appending a “.” (period) followed by the widget index to the field name passed. When this approach is used, the Field object returned by `getField` encapsulates only one individual widget. You can use the Field objects returned this way anywhere you would use a Field object returned by passing the unaltered field name. However, the set of nodes that are affected may vary, as shown in the following table.

Beginning with Acrobat 8.0, the LiveCycle Reader Extensions Field right is checked for `Field` objects only if the JavaScript code is executed outside the PDF file (from the JavaScript console, through batch execution, or through `JSObject`).

| Action | Field object that represents all  widgets | Field object that represents one specific widget |
|--------|-------------------------------------------|--------------------------------------------------|
| Get a widget property | Gets the property of widget # 0. | Gets the property of the widget. |
| Set a widget property | Sets the property of all widgets that are children of that field.  (The `rect` property and the `setFocus` method are exceptions that apply to widget # 0. See example below.) | Sets the property of the widget. |
| Get a field property | Gets the property of the field. | Gets the property of the parent field. |
| Set a field property | Sets the property of the field. | Sets the property of the parent field. |

The following example changes the `rect` property of the second radio button (the first would have index 0) of the field “my radio”.

```
var f = this.getField("my radio.1");
f.rect = [360, 677, 392, 646];
```

<a id="54526"></a>
<a id="field-versus-widget-attributes"></a>
<a id="id554"></a>
### Field versus widget attributes

Some properties of the Field object, such as `value`, apply to all widgets that are children of that field. Other properties, such as `rect`, are specific to individual widgets.

The following field properties and methods affect field-level attributes:

```
calcOrderIndex, charLimit, comb, currentValueIndices,defaultValue,

 doNotScroll, doNotSpellCheck, delay, doc, editable, exportValues,

 fileSelect, multiline, multipleSelection, name, numItems,page, password,

 readonly, required,submitName, type, userName, value, valueAsString,

 clearItems, browseForFileToSubmit, deleteItemAt, getItemAt, insertItemAt,

 setAction, setItems,signatureInfo, signatureSign, and signatureValidate.
```

The following field properties and methods affect widget-level attributes:

```
alignment, borderStyle, buttonAlignX, buttonAlignY, buttonPosition,

 buttonScaleHow, buttonScaleWhen, display, fillColor, hidden, highlight,

 lineWidth, print, rect, strokeColor, style, textColor, textFont, textSize,

 buttonGetCaption, buttonGetIcon, buttonImportIcon, buttonSetCaption,

 buttonSetIcon, checkThisBox, defaultIsChecked, isBoxChecked,

 isDefaultChecked, setAction, and setFocus.
```

> **Note**
>
> The `setAction` method can apply at the field or widget level, depending on the event. The `Keystroke`, `Validate`, `Calculate`, and `Format` events apply to fields. The `MouseUp`, `MouseDown`, `MouseEnter`, `MouseExit`, `OnFocus`, and `OnBlur` events apply to widgets.

The `checkThisBox`, `defaultIsChecked`, `isBoxChecked`, and `isDefaultChecked` methods take a widget index, `nWidget`, as a parameter. If you invoke these methods on a Field object `f` that represents one specific widget, the `nWidget` parameter is optional (and is ignored if passed) and the method acts on the specific widget encapsulated by `f`.

<a id="field-properties"></a>
<a id="id555"></a>
### Field properties

In general, field properties correspond to those stored in field and annotation dictionaries in the PDF document (see the [PDF Reference](https://adobe.com/go/pdfreference)).

Some property values are stored in the PDF document as names, while others are stored as strings (see the [PDF Reference](https://adobe.com/go/pdfreference)). For a property that is stored as a name, there is a 127-character limit on the length of the string.

**Examples** of properties that have a 127-character limit include `value` and `defaultValue` for check boxes and radio buttons. The [PDF Reference](https://adobe.com/go/pdfreference) documents all Annotation properties as well as how they are stored.

<a id="47052"></a>
<a id="id559"></a>
<a id="id560"></a>
#### alignment

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | String | R/W |

Controls how the text is laid out within the text field. Values are

```
left
center
right
```

**Fields**

`text`

Example:

```
var f = this.getField("MyText");
f.alignment = "center";
```

<a id="18616"></a>
borderStyle

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | String | R/W |

The border style for a field. Valid border styles are

```
solid
dashed
beveled
inset
underline
```

The border style determines how the border for the rectangle is drawn. The `border` object is a static convenience constant that defines all the border styles of a field, as shown in the following table:

| Type | Keyword | Description |
|------|---------|-------------|
| `solid` | `border.s` | Strokes the entire perimeter of the rectangle with a solid line. |
| `beveled` | `border.b` | Equivalent to the `solid` style with an additional beveled (pushed-out appearance) border applied inside the solid border. |
| `dashed` | `border.d` | Strokes the perimeter with a dashed line. |
| `inset` | `border.i` | Equivalent to the `solid` style with an additional inset (pushed-in appearance) border applied inside the solid border. |
| `underline` | `border.u` | Strokes the bottom portion of the rectangle’s perimeter. |

**Fields**

All

Example: The following example shows how to set the border style of a field to `solid` :

```
var f = this.getField("MyField");
f.borderStyle = border.s; /* border.s evaluates to "solid" */
```

<a id="40106"></a>
<a id="buttonalignx"></a>
<a id="id561"></a>
#### buttonAlignX

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Integer | R/W |

Controls how space is distributed from the left of the button face with respect to the icon. It is expressed as a percentage between 0 and 100, inclusive. The default value is 50.

If the icon is scaled anamorphically (which results in no space differences), this property is not used.

**Fields**

`button`

<a id="41863"></a>
<a id="buttonaligny"></a>
<a id="id562"></a>
#### buttonAlignY

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Integer | R/W |

Controls how unused space is distributed from the bottom of the button face with respect to the icon. It is expressed as a percentage between 0 and 100, inclusive. The default value is 50.

If the icon is scaled anamorphically (which results in no space differences), this property is not used.

**Fields**

`button`

Example: This example is an elevator animation. The field “myElevator” is a button form field that has small width and large height. An icon is imported as the appearance face.

```
function MoveIt()
{
    if ( f.buttonAlignY == 0 ) {
        f.buttonAlignY++;
        run.dir = true;
        return;
    }
    if ( f.buttonAlignY == 100 ) {
        f.buttonAlignY--;
        run.dir = false;
        return;
    }
    if (run.dir) f.buttonAlignY++;
    else f.buttonAlignY--;
}
var f = this.getField("myElevator");
f.buttonAlignY=0;
run = app.setInterval("MoveIt()", 100);
run.dir=true;
toprun = app.setTimeOut(
    "app.clearInterval(run); app.clearTimeOut(toprun)", 2*20000+100);
```

<a id="13558"></a>
<a id="buttonfitbounds"></a>
<a id="id563"></a>
#### buttonFitBounds

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | F | Boolean | R/W |

If `true`, the extent to which the icon may be scaled is set to the bounds of the button field. The additional icon placement properties are still used to scale and position the icon within the button face.

In previous versions of Acrobat, the width of the field border was always taken into consideration when scaling an icon to fit a button face, even when no border color was specified. Setting this property to `true` when a border color has been specified for the button will cause an exception to be raised.

**Fields**

`button`

<a id="23056"></a>
<a id="buttonposition"></a>
<a id="id564"></a>
#### buttonPosition

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Integer | R/W |

Controls how the text and the icon of the button are positioned with respect to each other within the button face. The convenience `position` object defines all of the valid alternatives.

| Icon/text placement | Keyword |
|---------------------|---------|
| Text Only | `position.textOnly` |
| Icon Only | `position.iconOnly` |
| Icon top, Text bottom | `position.iconTextV` |
| Text top, Icon bottom | `position.textIconV` |
| Icon left, Text right | `position.iconTextH` |
| Text left, Icon right | `position.textIconH` |
| Text in Icon (overlaid) | `position.overlay` |

**Fields**

`button`

<a id="36156"></a>
<a id="buttonscalehow"></a>
<a id="id565"></a>
#### buttonScaleHow

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Integer | R/W |

Controls how the icon is scaled (if necessary) to fit inside the button face. The convenience `scaleHow` object defines all of the valid alternatives:

| How is icon scaled | Keyword |
|--------------------|---------|
| Proportionally | `scaleHow.proportional` |
| Non-proportionally | `scaleHow.anamorphic` |

**Fields**

`button`

<a id="36367"></a>
<a id="buttonscalewhen"></a>
<a id="id566"></a>
#### buttonScaleWhen

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Integer | R/W |

Controls when an icon is scaled to fit inside the button face. The convenience `scaleWhen` object defines all of the valid alternatives:

| When is icon scaled | Keyword |
|---------------------|---------|
| Always | `scaleWhen.always` |
| Never | `scaleWhen.never` |
| If icon is too big | `scaleWhen.tooBig` |
| If icon is too small | `scaleWhen.tooSmall` |

**Fields**

`button`

<a id="20477"></a>
<a id="calcorderindex"></a>
<a id="id567"></a>
#### calcOrderIndex

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | Integer | R/W |

Changes the calculation order of fields in the document. When a computable `text` or combo box field is added to a document, the field’s name is appended to the calculation order array. The calculation order array determines in what order the fields are calculated. The `calcOrderIndex` property works similarly to the Calculate tab used by the Acrobat Form tool.

**Fields**

`combobox`, `text`

Example:

```
var a = this.getField("newItem");
var b = this.getField("oldItem");
a.calcOrderIndex = b.calcOrderIndex + 1;
```

In this example, the “newItem” field was added after the “oldItem” field. The script changes the `calcOrderIndex` property of the “newItem” field so that it is calculated before the “oldItem” field.

<a id="42060"></a>
<a id="charlimit"></a>
<a id="id568"></a>
#### charLimit

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | Integer | R/W |

Limits the number of characters that a user can type into a text field.

See `event.` fieldFull to detect when the maximum number of characters is reached.

**Fields**

`text`

Example: Set a limit on the number of characters that can be typed into a field.

```
var f = this.getField("myText");
f.charLimit = 20;
```

<a id="64322"></a>
<a id="comb"></a>
<a id="id569"></a>
#### comb

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | F | Boolean | R/W |

If set to `true`, the field background is drawn as series of boxes (one for each character in the value of the field) and each character of the content is drawn within those boxes. The number of boxes drawn is determined from the `charLimit` property.

It applies only to text fields. The setter will also raise if any of the following field properties are also set `multiline`, `password`, and `fileSelect`. A side-effect of setting this property is that the `doNotScroll` property is also set.

**Fields**

`text`

Example: Create a comb field in the upper left corner of a newly created document.

```
var myDoc = app.newDoc();                 // Create a blank doc
var Bbox = myDoc.getPageBox("Crop");      // Get crop box
var inch = 72;

// Add a text field at the top of the document
var f = myDoc.addField("Name.Last", "text", 0,
    [ inch, Bbox[1]-inch, 3*inch, Bbox[1]- inch - 14 ] );
// Add some attributes to this text field
f.strokeColor = color.black;
f.textColor = color.blue;
f.fillColor = ["RGB",1,0.66,0.75];

f.comb = true;                            // Declare this is a comb field
f.charLimit = 10;                         // Max number of characters
```

<a id="74343"></a>
<a id="commitonselchange"></a>
<a id="id570"></a>
#### commitOnSelChange

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | F | Boolean | R/W |

Controls whether a field value is committed after a selection change:

- If `true`, the field value is committed immediately when the selection is made.
- If `false`, the user can change the selection multiple times without committing the field value. The value is committed only when the field loses focus, that is, when the user clicks outside the field.

**Fields**

`combobox`, `listbox`

<a id="52225"></a>
<a id="currentvalueindices"></a>
<a id="id571"></a>
#### currentValueIndices

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Integer  Array | R/W |

Reads and writes single or multiple values of a list box or combo box.

**Read**

**Returns** the options-array indices of the strings that are the value of a list box or combo box field. These indices are 0-based. If the value of the field is a single string, it returns an integer. Otherwise, it returns an array of integers sorted in ascending order. If the current value of the field is not a member of the set of offered choices (as could happen in the case of an editable combo box) it returns -1.

**Write**

Sets the value of a list box or combo box. It accepts a single integer or array of integers as an argument. To set a single string as the value, pass an integer that is the 0-based index of that string in the options array. Note that in the case of an editable combo box, if the desired value is not a member of the set of offered choices, you must set the value instead. Except for this case, `currentValueIndices` is the preferred way to set the value of a list box or combo box.

To set a multiple selection for a list box that allows it, pass an array as argument to this property, containing the indices (sorted in ascending order) of those strings in the options array. If passed an array like this: `Field.value=["item1", "item3"]`, it also selects the items. The ability for a list box to support multiple selections can be set through multipleSelection.

**Related methods** and properties include numItems, getItemAt, insertItemAt, deleteItemAt and setItems.

**Fields**

`combobox`, `listbox`

**Example (Read)**

A mouse-up action of a button. The script gets the current value of a list box.

```
var f = this.getField("myList");
var a = f.currentValueIndices;
if (typeof a == "number")     // A single selection
    console.println("Selection: " + f.getItemAt(a, false));
else {     // Multiple selections
    console.println("Selection:");
    for (var i = 0; i < a.length; i ++)
        console.println("   " + f.getItemAt(a[i], false));
}
```

**Example (Write)**

The following code, selects the second and fourth (0-based index values, 1 and 3, respectively) in a list box.

```
var f = this.getField("myList");
f.currentValueIndices = [1,3];
```

<a id="14483"></a>
<a id="defaultstyle"></a>
<a id="id572"></a>
#### defaultStyle

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | F | `Span` object | R/W |

This property defines the default style attributes for the form field. If the user clicks an empty field and begins entering text without changing properties using the property toolbar, these are the properties that will be used. This property is a single `Span` object without a `text` property. Some of the properties in the default style span mirror the properties of the Field object. Changing these properties also modifies the `defaultStyle` property for the field and vice versa.

The following table details the properties of the Field object that are also in the default style and any differences between their values.

| Field properties | defaultStyle  (Span properties) | Description |
|------------------|---------------------------------|-------------|
| `alignment` | `alignment` | The `alignment` property has the same values for both the default style and the Field object. |
| `textFont` | `fontFamily`  `fontStyle`  `fontWeight` | The value of this field property is a complete font name that represents the font family, weight, and style. In the default style property, each property is represented separately. If an exact match for the font properties specified in the default style cannot be found, a similar font will be used or synthesized. |
| `textColor` | `textColor` | The `textColor` property has the same values for both the default style and the Field object. |
| `textSize` | `textSize` | The `textSize` property has the same values for both the default style and the Field object. |

> **Note**
>
> When a field is empty, `defaultStyle` is the style used for newly entered text. If a field already contains text when `defaultStyle` is changed, the text will not pick up any changes to `defaultStyle`. Newly entered text uses the attributes of the text it is inserted into (or specified with the toolbar).

When pasting rich text into a field, unspecified attributes in the pasted rich text are filled with those from `defaultStyle`.

Superscript and Subscript are ignored in `defaultStyle`.

**Fields**

`rich text`

Example: Change the default style for a text field.

```
var style = this.getField("Text1").defaultStyle;
style.textColor = color.red;
style.textSize = 18;

// if Courier Std is not found, use a monospace font
style.fontFamily = ["Courier Std", "monospace" ];

this.getField("Text1").defaultStyle = style;
```

<a id="36634"></a>
<a id="defaultvalue"></a>
<a id="id573"></a>
#### defaultValue

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | String | R/W |

The default value of a field—that is, the value that the field is set to when the form is reset. For combo boxes and list boxes, either an export or a user value can be used to set the default. A conflict can occur, for example, when the field has an export value and a user value with the same value but these apply to different items in the list. In such cases, the export value is matched against first.

**Fields**

all except `button`, `signature`

Example:

```
var f = this.getField("Name");
f.defaultValue = "Enter your name here.";
```

<a id="30113"></a>
<a id="donotscroll"></a>
<a id="id574"></a>
#### doNotScroll

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Boolean | R/W |

If `true`, the text field does not scroll and the user, therefore, is limited by the rectangular region designed for the field. Setting this property to `true` or `false` corresponds to checking or unchecking the Scroll Long Text field in the Options tab of the field.

**Fields**

`text`

<a id="73181"></a>
<a id="donotspellcheck"></a>
<a id="id575"></a>
#### doNotSpellCheck

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Boolean | R/W |

If `true`, spell checking is not performed on this editable text field. Setting this property to `true` or `false` corresponds to unchecking or checking the Check Spelling attribute in the Options tab of the Field Properties dialog box.

**Fields**

`combobox` (editable), `text`

<a id="29401"></a>
<a id="id576"></a>
<a id="id577"></a>
#### delay

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | F | Boolean | R/W |

Delays the redrawing of a field’s appearance. It is generally used to buffer a series of changes to the properties of the field before requesting that the field regenerate its appearance. Setting the property to `true` forces the field to wait until `delay` is set to `false`. The update of its appearance then takes place, redrawing the field with its latest settings.

There is a corresponding Doc delay flag if changes are being made to many fields at once.

**Fields**

all

Example: Change the appearance of a check box. Set `delay` to `true`, makes changes, and sets `delay` to `false`.

```
// Get the myCheckBox field
var f = this.getField("myCheckBox");
// Set the delay and change the fields properties
// to beveled edge and medium thickness line.
f.delay = true;
f.borderStyle = border.b;
.
..        // A number of other changes
f.strokeWidth = 2;
f.delay = false; // Force the changes now
```

<a id="10117"></a>
<a id="display"></a>
<a id="id578"></a>
#### display

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | D | No | All | Integer | R/W |

Controls whether the field is hidden or visible on screen and in print. The values for the `display` property are listed in the table below.

| Effect | Keyword |
|--------|---------|
| Field is visible on screen and in print | `display.visible` |
| Field is hidden on screen and in print | `display.hidden` |
| Field is visible on screen but does not print | `display.noPrint` |
| Field is hidden on screen but prints | `display.noView` |

This property supersedes the older `hidden` and `print` properties.

**Fields**

all

Example:

```
// Set the display property
var f = getField("myField");
f.display = display.noPrint;

// Test whether field is hidden on screen and in print
if (f.display == display.hidden) console.println("hidden");
```

<a id="15139"></a>
<a id="id579"></a>
<a id="id580"></a>
#### doc

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | object | R |

**Returns** the Doc of the document to which the field belongs.

**Fields**

all

<a id="36583"></a>
<a id="editable"></a>
<a id="id581"></a>
#### editable

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | Boolean | R/W |

Controls whether a combo box is editable. If `true`, the user can type in a selection. If `false`, the user must choose one of the provided selections.

**Fields**

`combobox`

Example:

```
var f = this.getField("myComboBox");
f.editable = true;
```

<a id="58250"></a>
<a id="exportvalues"></a>
<a id="id582"></a>
#### exportValues

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D |  | F | Array | R/W |

An array of strings representing the export values for the field. The array has as many elements as there are annotations in the field. The elements are mapped to the annotations in the order of creation (unaffected by tab-order).

For radio button fields, this property is required to make the field work properly as a group. The button that is checked at any time gives its value to the field as a whole.

For check box fields, unless an export value is specified, “Yes” (or the corresponding localized string) is the default when the field is checked. “Off” is the default when the field is unchecked (the same as for a radio button field when none of its buttons are checked).

**Fields**

`checkbox`, `radiobutton`

Example: Create a radio button field and sets its export values.

```
var d = 40;
var f = this.addField("myRadio","radiobutton",0,  [200, 510, 210, 500]);
this.addField("myRadio","radiobutton",0,  [200+d, 510-d, 210+d, 500-d]);
this.addField("myRadio","radiobutton",0,  [200, 510-2*d, 210, 500-2*d]);
this.addField("myRadio","radiobutton",0,  [200-d, 510-d, 210-d, 500-d]);
f.strokeColor = color.black;
// Now give each radio field an export value
f.exportValues = ["North", "East", "South", "West"];
```

<a id="69226"></a>
<a id="fileselect"></a>
<a id="id583"></a>
#### fileSelect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | Yes | F | Boolean | R/W |

If `true`, sets the file-select flag in the Options tab of the text field (Field is Used for File Selection). This indicates that the value of the field represents a path of a file whose contents may be submitted with the form.

The path may be entered directly into the field by the user, or the user can browse for the file. (See the browseForFileToSubmit method.)

> **Note**
>
> The file select flag is mutually exclusive with the `multiline`, `charLimit`, `password`, and `defaultValue` properties. Also, on the Mac OS platform, when setting the file select flag, the field gets treated as read-only. Therefore, the user must browse for the file to enter into the field. (See browseForFileToSubmit.)

This property can only be set during a batch or console event. See priv. The event object contains a discussion of JavaScript events.

**Fields**

`text`

<a id="16464"></a>
<a id="id584"></a>
<a id="id585"></a>
#### fillColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | D | No | F | Array | R/W |

Specifies the background color for a field. The background color is used to fill the rectangle of the field. Values are defined by using `transparent`, `gray`, `RGB` or `CMYK` color. See Color arrays for information on defining color arrays and how values are used with this property.

In older versions of this specification, this property was named `bgColor`. The use of `bgColor` is now discouraged, although it is still valid for backward compatibility.

**Fields**

all

Example: Change the background color of a text field. If the current color is red, it changes to blue, otherwise it changes to yellow.

```
var f = this.getField("myField");
if (color.equal(f.fillColor, color.red))
    f.fillColor = color.blue;
else
    f.fillColor = color.yellow;
```

<a id="29686"></a>
<a id="id586"></a>
<a id="id587"></a>
#### hidden

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| deprecated | No | No | D | boolean | R/W |

> **Note**
>
> This property has been superseded by the `display` property and its use is discouraged.

If the value is `false`, the field is visible to the user; if `true`, the field is invisible. The default value is `false`.

**Fields**

all

<a id="12328"></a>
<a id="highlight"></a>
<a id="id588"></a>
#### highlight

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | String | R/W |

Defines how a button reacts when a user clicks it. The four highlight modes supported are:

- *none*: No visual indication that the button has been clicked.
- *invert*: The region encompassing the button’s rectangle inverts momentarily.
- *push*: The down face for the button (if any) is displayed momentarily.
- *outline*: The border of the rectangleinverts momentarily.
- The convenience `highlight` object defines each state, as follows:

| Type | Keyword |
|------|---------|
| `none` | `highlight.n` |
| `invert` | `highlight.i` |
| `push` | `highlight.p` |
| `outline` | `highlight.o` |

**Fields**

`button`

Example: Set the highlight property of a button to “invert”.

```
var f = this.getField("myButton");
f.highlight = highlight.i;
```

<a id="98518"></a>
lineWidth

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | D | No | F | Integer | R/W |

Specifies the thickness of the border when stroking the perimeter of a field’s rectangle. If the stroke color is transparent, this parameter has no effect except in the case of a beveled border. Values are:

- *0*: none
- *1*: thin
- *2*: medium
- *3*: thick

In older versions of this specification, this property was `borderWidth`. The use of `borderWidth` is now discouraged, although it is still valid for backward compatibility.

The default value for `lineWidth` is 1 (thin). Any integer value can be used; however, values beyond 5 may distort the field’s appearance.

**Fields**

all

Example: Change the border width of the Text Box to medium thickness

```
f.lineWidth = 2
```

<a id="79716"></a>
<a id="multiline"></a>
<a id="id589"></a>
#### multiline

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | Boolean | R/W |

Controls how text is wrapped within the field. If `false` (the default), the text field can be a single line only. If `true`, multiple lines are allowed and they wrap to field boundaries.

**Fields**

`text`

Example: See the Doc getField method.

<a id="72810"></a>
<a id="multipleselection"></a>
<a id="id590"></a>
#### multipleSelection

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Boolean | R/W |

If `true`, indicates that a list box allows a multiple selection of items.

See also type, value, and currentValueIndices.

**Fields**

`listbox`

<a id="13887"></a>
<a id="id591"></a>
<a id="id592"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | String | R |

This property returns the fully qualified field name of the field as a string object.

Beginning with Acrobat 6.0, if the Field object represents one individual widget, the returned name includes an appended ‘.’ followed by the widget index.

**Fields**

all

Example: Get a Field object and write the `name` of the field to the console.

```
var f = this.getField("myField");

// Displays "myField" in the console window
console.println(f.name);
```

<a id="16920"></a>
<a id="numitems"></a>
<a id="id593"></a>
#### numItems

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Integer | R |

The number of items in a combo box or list box.

**Fields**

`combobox`, `listbox`

Example: Get the number of items in a list box.

```
var f = this.getField("myList");
console.println("There are " + f.numItems + " in this list box");
```

Face names and values of a combo box or list box can be accessed through the getItemAt method. See that method for an additional example of `numItems`.

<a id="40237"></a>
<a id="id594"></a>
<a id="id595"></a>
#### page

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Integer  Array | R |

The page number or an array of page numbers of a field. If the field has only one appearance in the document, the `page` property returns an integer representing the 0-based page number of the page on which the field appears. If the field has multiple appearances, it returns an array of integers, each member of which is a 0-based page number of an appearance of the field. The order in which the page numbers appear in the array is determined by the order in which the individual widgets of this field were created (and is unaffected by tab-order). If an appearance of the field is on a hidden template page, `page` returns a value of -1 for that appearance.

**Fields**

all

Example 1: Determine whether a particular field appears on one page, or more than one page.

```
var f = this.getField("myField");
if (typeof f.page == "number")
    console.println("This field only occurs once on page " + f.page);
else
    console.println("This field occurs " + f.page.length + " times);
```

**Example 2 (Acrobat 6.0)**

The `page` property can be used to get the number of widgets associated with a field name. This example gets the number of radio buttons in a radio button field.

```
var f = this.getField("myRadio");
if ( typeof f.page == "object" )
    console.println("There are " + f.page.length
        + " radios in this field.");
```

<a id="16278"></a>
<a id="password"></a>
<a id="id596"></a>
#### password

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | Boolean | R/W |

Specifies whether the field should display asterisks when data is entered in the field. (Upon submission, the actual data entered is sent.) If this property is `true`, data in the field is not saved when the document is saved to disk.

**Fields**

`text`

<a id="38471"></a>
<a id="id597"></a>
<a id="id598"></a>
#### print

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| deprecated | No | No | D, F | boolean | R/W |

> **Note**
>
> This property has been superseded by the `display` property and its use is discouraged.

If `true`, the field appears when the user prints the document. If `false`, the field does not appear when printing. This property can be used to hide control buttons and other fields that are not useful on the printed page.

**Fields**

all

<a id="54850"></a>
<a id="radiosinunison"></a>
<a id="id599"></a>
#### radiosInUnison

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | F | Boolean | R/W |

If `false`, even if a group of radio buttons have the same name and export value, they behave in a mutually exclusive fashion, like HTML radio buttons. The default for new radio buttons is `false`.

If `true`, if a group of radio buttons have the same name and export value, they turn on and off in unison, as in Acrobat 4.0.

**Fields**

`radiobutton`

<a id="27391"></a>
<a id="id600"></a>
<a id="id601"></a>
#### readonly

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | Boolean | R/W |

The read-only characteristic of a field. If a field is read-only, the user can see the field but cannot change it.

**Fields**

all

Example: Get a field and make it read-only.

```
var f = this.getField("myTextField");
f.value = "You can't change this message!";
f.readonly = true;
```

<a id="91364"></a>
<a id="id602"></a>
<a id="id603"></a>
#### rect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | Array | R/W |

An array of four numbers in rotated user space that specify the size and placement of the form field. These four numbers are the coordinates of the bounding rectangle and are listed in the following order: upper-left *x*, upper-left *y*, lower-right *x* and lower-right *y*.

> **Note**
>
> The `Annotation` object also has a `rect` property. However, the coordinates are not in rotated user space and they are in a different order than in the Field object `rect` property.

**Fields**

all

Example 1: Lay out a 2-inch-wide text field just to the right of the field “myText”.

```
var f = this.getField("myText");  // Get the Field object
var myRect = f.rect;              // and get its rectangle
myRect[0] = f.rect[2];            // The ulx for new = lrx for old
myRect[2] += 2 * 72;               // Move two inches for lry
f = this.addField("myNextText", "text", this.pageNum, myRect);
f.strokeColor = color.black;
```

Example 2: Move an existing button field 10 points to the right.

```
var b = this.getField("myButton");
var aRect = b.rect;   // Make a copy of b.rect
aRect[0] += 10;       // Increment first x coordinate by 10
aRect[2] += 10;       // Increment second x coordinate by 10
b.rect = aRect;       // Update the value of b.rect
```

<a id="28273"></a>
<a id="required"></a>
<a id="id604"></a>
#### required

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | Boolean | R/W |

Specifies whether a field requires a value. If `true`, the field’s value must be non-`null` when the user clicks a submit button that causes the value of the field to be posted. If the field value is `null`, the user receives a warning message and the submit does not occur.

**Fields**

all except `button`

Example: Make “myField” into a required field.

```
var f = this.getField("myField");
f.required = true;
```

<a id="87647"></a>
<a id="richtext"></a>
<a id="id605"></a>
#### richText

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | F | Boolean | R/W |

If `true`, the field allows rich text formatting. The default is `false`.

**Fields**

`text`

Related objects and properties are richValue, defaultStyle, `event.` richValue, `event.` richChange, `event.` richChangeEx, the `Annotation` object richContents property, and the Span object.

Example 1: Get a Field object and set it for rich text formatting.

```
var f = this.getField("Text1");
f.richText = true;
```

See richValue for a more complete example.

<a id="55711"></a>
Example 2: Count the number of rich text fields in the document.

```
var count = 0;
for ( var i = 0; i < this.numFields; i++)
{
    var fname = this.getNthFieldName(i);
    var f = this.getField(fname);
    if ( f.type == "text" && f.richText ) count++
}
console.println("There are a total of "+ count + " rich text fields.");
```

<a id="88243"></a>
<a id="id606"></a>
<a id="id607"></a>
#### richValue

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | F | Array of `Span` objects | R/W |

This property specifies the text contents and formatting of a rich text field. For field types other than rich text, this property is `undefined`. The rich text contents are represented as an array of `Span` objects containing the text contents and formatting of the field.

**Fields**

rich text

Related objects and properties are richText, defaultStyle, `event.` richValue, `event.` richChange, `event.` richChangeEx, the `Annotation` object richContents property, and the Span object.

Example 1: Turn all bold text into red underlined text.

```
var f = this.getField("Text1");
var spans = f.richValue;
for ( var i = 0; i < spans.length; i++ )
{
    if( spans[i].fontWeight >= 700 )
    {
        spans[i].textColor = color.red;
        spans[i].underline = true;
    }
}
f.richValue = spans;
```

<a id="48009"></a>
2

Create a text field, marks it for rich text formatting, and inserts rich text.

```
var myDoc = app.newDoc();                  // Create a blank doc
var Bbox = myDoc.getPageBox("Crop");       // Get crop box
var inch = 72;

// Add a text field at the top of the document
var f = myDoc.addField("Text1", "text", 0,
    [72, Bbox[1]-inch, Bbox[2]-inch, Bbox[1]-2*inch ] );
// Add some attributes to this text field
f.strokeColor = color.black;
f.richText = true;                         // Rich text
f.multiline = true;                        // Multiline

// Now build up an array of Span objects
var spans = new Array();
spans[0] = new Object();
spans[0].text = "Attention:r";
spans[0].textColor = color.blue;
spans[0].textSize = 18;

spans[1] = new Object();
spans[1].text = "Adobe Acrobat 6.0r";
spans[1].textColor = color.red;
spans[1].textSize = 20;
spans[1].alignment = "center";

spans[2] = new Object();
spans[2].text = "will soon be here!";
spans[2].textColor = color.green;
spans[2].fontStyle = "italic";
spans[2].underline = true;
spans[2].alignment = "right";

// Now give the rich field a rich value
f.richValue = spans;
```

<a id="35949"></a>
<a id="rotation"></a>
<a id="id608"></a>
#### rotation

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | Not available in Reader | Integer | R/W |

The rotation of a widget in counterclockwise increments. Valid values are 0, 90, 180, and 270.

**Fields**

all

Example: Create a rotated text field on each page and fill it with text.

```
for ( var i=0; i < this.numPages; i++) {
    var f = this.addField("myRotatedText"+i,"text",i,[6, 6+72, 18, 6]);
    f.rotation = 90; f.value = "Confidential";
    f.textColor = color.red; f.readonly = true;
}
```

<a id="20562"></a>
<a id="id609"></a>
<a id="id610"></a>
#### strokeColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | D | No | F | Array | R/W |

Specifies the stroke color for a field that is used to stroke the rectangle of the field with a line as large as the line width. Values are defined by using `transparent`, `gray`, `RGB` or `CMYK` color. See Color arrays for information on defining color arrays and how values are used with this property.

In older versions of this specification, this property was `borderColor`. The use of `borderColor` is now discouraged, although it is still valid for backward compatibility.

**Fields**

all

Example: Change the stroke color of each text field in the document to red.

```
   for ( var i=0; i < this.numFields; i++) {
       var fname = this.getNthFieldName(i);
       var f = this.getField(fname);
       if ( f.type == "text" ) f.strokeColor = color.red;
}
```

<a id="51110"></a>
<a id="id611"></a>
<a id="id612"></a>
#### style

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | String | R/W |

Allows the user to set the glyph style of a check box or radio button. The glyph style is the graphic used to indicate that the item has been selected.

The style values are associated with keywords as follows.

| Style | Keyword |
|-------|---------|
| check | `style.ch` |
| cross | `style.cr` |
| diamond | `style.di` |
| circle | `style.ci` |
| star | `style.st` |
| square | `style.sq` |

**Fields**

`checkbox`, `radiobutton`

Example: This example sets the glyph style to circle.

```
var f = this.getField("myCheckbox");
f.style = style.ci;
```

<a id="19265"></a>
<a id="submitname"></a>
<a id="id613"></a>
#### submitName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | F | String | R/W |

If nonempty, used during form submission instead of name. Only applicable if submitting in HTML format (that is, URL-encoded).

**Fields**

all

<a id="74886"></a>
<a id="textcolor"></a>
<a id="id614"></a>
#### textColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | D | No | F | Array | R/W |

The foreground color of a field. It represents the text color for text, button, or list box fields and the check color for check box or radio button fields. Values are defined the same as the `fillColor`. See Color arrays for information on defining color arrays and how values are set and used with this property.

In older versions of this specification, this property was `fgColor`. The use of `fgColor` is now discouraged, although it is still valid for backward compatibility.

> **Note**
>
> An exception is thrown if a transparent color space is used to set `textColor`.

**Fields**

all

Example: This example sets the foreground color to red.

```
var f = this.getField("myField");
f.textColor = color.red;
```

<a id="11104"></a>
<a id="id615"></a>
<a id="id616"></a>
#### textFont

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | String | R/W |

The font that is used when laying out text in a text field, combo box, list box or button. Valid fonts are defined as properties of the `font` object. Beginning with Acrobat 5.0, arbitrary fonts can also be used. See fonts.

**Fields**

`button`, `combobox`, `listbox`, `text`

<a id="45386"></a>
**font Object**

| Text font | Keyword |
|-----------|---------|
| Times-Roman | `font.Times` |
| Times-Bold | `font.TimesB` |
| Times-Italic | `font.TimesI` |
| Times-BoldItalic | `font.TimesBI` |
| Helvetica | `font.Helv` |
| Helvetica-Bold | `font.HelvB` |
| Helvetica-Oblique | `font.HelvI` |
| Helvetica-BoldOblique | `font.HelvBI` |
| Courier | `font.Cour` |
| Courier-Bold | `font.CourB` |
| Courier-Oblique | `font.CourI` |
| Courier-BoldOblique | `font.CourBI` |
| Symbol | `font.Symbol` |
| ZapfDingbats | `font.ZapfD` |

<a id="34606"></a>
Use of arbitrary fonts

Beginning with Acrobat 5.0, an arbitrary font can be used when laying out a text field, combo box, list box or button by setting the value of `textFont` to the PDSysFont font name, as returned by PDSysFontGetName. (See the [Acrobat and PDF Library API Reference](./API_References/Acrobat_API_Reference/index.md).)

1. To find the PDSysFont font name of a font:
2. Create a text field in a PDF document. Using the UI, set the text font for this field to the desired font.
3. Open the JavaScript Debugger Console and execute the script

```
this.getField("Text1").textFont
```

The above code assumes the name of the field is `Text1`.

1. The string returned to the console is the font name needed to programmatically set the text font.

Example: Set the font to Helvetica.

```
var f = this.getField("myField");
f.textFont = font.Helv;
```

**Example (Acrobat 5.0)**

Set the font of myField to Viva-Regular.

```
var f = this.getField("myField");
f.textFont = "Viva-Regular";
```

<a id="35479"></a>
<a id="id617"></a>
<a id="id618"></a>
#### textSize

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | Number | R/W |

Specifies the text size (in points) to be used in all controls. In check box and radio button fields, the text size determines the size of the check. Valid text sizes range from 0 to 32767, inclusive. A value of zero means the largest point size that allows all text data to fit in the field’s rectangle.

**Fields**

all

Example: Set the text size of “myField” to 28 points.

```
this.getField("myField").textSize = 28;
```

<a id="27024"></a>
<a id="id619"></a>
<a id="id620"></a>
#### type

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | String | R |

**Returns** the type of the field as a string. Valid types are:

```
button
checkbox
combobox
listbox
radiobutton
signature
text
```

**Fields**

all

Example: Count the number of text fields in the document.

```
var count = 0;
for ( var i=0; i<this.numFields; i++) {
    var fname = this.getNthFieldName(i);
    if ( this.getField(fname).type == "text" ) count++; }
console.println("There are " + count + " text fields.");
```

<a id="38544"></a>
<a id="username"></a>
<a id="id621"></a>
#### userName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | String | R/W |

The user name (short description string) of the field. It is intended to be used as tooltip text whenever the cursor enters a field. It can also be used as a user-friendly name, instead of the field name, when generating error messages.

**Fields**

all

Example: Add a tooltip to a button field.

```
var f = this.getField("mySubmit");
f.userName = "Press this button to submit your data.";
```

<a id="22606"></a>
<a id="id622"></a>
<a id="id623"></a>
#### value

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | D | No | F | various | R/W |

The value of the field data that the user has entered. Depending on the `type` of the field, may be a String, Date, or Number. Typically, the `value` is used to create calculated fields.

Beginning with Acrobat 6.0, if a field contains rich text formatting, modifying this property will discard the formatting and regenerate the field value and appearance using the `defaultStyle` and plain text value. To modify the field value and maintain formatting use the `richValue` property.

> **Note**
>
> For signature fields, if the field has been signed, a non-`null` string is returned as the value.

For Acrobat 5.0 or later, if the field is a list box that accepts multiple selections (see multipleSelection), you can pass an array to set the `value` of the field, and `value` returns an array for a list box with multiple values currently selected.

The `currentValueIndices` of a list box that has multiple selections is the preferred and most efficient way to get and set the value of this type of field.

See also valueAsString and `event.` type.

**Fields**

all except `button`

Example: In this example, the `value` of the field being calculated is set to the sum of the “Oil” and “Filter” fields and multiplied by the state sales tax.

```
var oil = this.getField("Oil");
var filter = this.getField("Filter");
event.value = (oil.value + filter.value) * 1.0825;
```

<a id="74707"></a>
<a id="valueasstring"></a>
<a id="id624"></a>
#### valueAsString

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | All | String | R |

**Returns** the value of a field as a JavaScript string.

It differs from `value`, which attempts to convert the contents of a field contents to an accepted format. For example, for a field with a value of “020”, `value` returns the integer 20, while `valueAsString` returns the string “020”.

**Fields**

all except `button`

<a id="field-methods"></a>
<a id="id625"></a>
### Field methods

<a id="60961"></a>
<a id="browseforfiletosubmit"></a>
<a id="id626"></a>
#### browseForFileToSubmit

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

If invoked on a text field for which the `fileSelect` flag is set (checked), opens a standard file-selection dialog box. The path entered through the dialog box is automatically assigned as the value of the text field.

If invoked on a text field in which the `fileSelect` flag is clear (unchecked), an exception is thrown.

Example: The following code references a text field with the file select flag checked. It is a mouse-up action of a button field.

```
var f = this.getField("resumeField");
f.browseForFileToSubmit();
```

<a id="21910"></a>
<a id="buttongetcaption"></a>
<a id="id627"></a>
#### buttonGetCaption

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Gets the caption associated with a button.

Use `buttonSetCaption` to set the caption.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nFace` | (optional) If specified, gets a caption of the given type: * *0*: (default) normal caption * *1*: down caption * *2*: rollover caption |

**Returns**

The caption string associated with the button.

Example: This example places pointing arrows to the left and right of the caption on a button field with icon and text.

```
// A mouse enter event
event.target.buttonSetCaption("=> "+ event.target.buttonGetCaption()
    +" <=");

// A mouse exit event
var str = event.target.buttonGetCaption();
str = str.replace(/=>  <=/g, "");
event.target.buttonSetCaption(str);
```

The same effect can be created by having the same icon for rollover and the same text, with the arrows inserted, for the rollover caption. This approach would be slower and cause the icon to flicker. The above code gives a very fast and smooth rollover effect because only the caption is changed, not the icon.

<a id="41330"></a>
<a id="buttongeticon"></a>
<a id="id628"></a>
#### buttonGetIcon

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Gets the `Icon` object of a specified type associated with a button.

See also the buttonSetIcon method for assigning an icon to a button.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nFace` | (optional) If specified, gets an icon of the given type: * *0*: (default) normal icon * *1*: down icon * *2*: rollover icon |

**Returns**

The `Icon` object.

Example:

```
// Swap two button icons.
var f = this.getField("Button1");
var g = this.getField("Button2");
var temp = f.buttonGetIcon();
f.buttonSetIcon(g.buttonGetIcon());
g.buttonSetIcon(temp);
```

See also buttonSetIcon and buttonImportIcon.

<a id="27194"></a>
<a id="buttonimporticon"></a>
<a id="id629"></a>
#### buttonImportIcon

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | Yes | Not available in Reader |

Imports the appearance of a button from another PDF file. If neither optional parameter is passed, the user is prompted to select a file.

See also buttonGetIcon, buttonSetIcon, addIcon, getIcon, importIcon, and removeIcon.

> **Note**
>
> (Acrobat 8.0) If `cPath` is specified, this method can only be executed during batch and console events. See priv. The event object contains a discussion of JavaScript events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cPath` | (optional, Acrobat 5.0) The device-independent path for the file.  Beginning with Acrobat 6.0, Acrobat first attempts to open `cPath` as a PDF file. On failure, Acrobat tries to convert the file to PDF from one of the known graphics formats (BMP, GIF, JPEG, PCX, PNG, TIFF) and then import the converted file as a button icon. |
| `nPage` | (optional, Acrobat 5.0) The 0-based page number from the file to turn into an icon. The default is 0. |

**Returns**

An integer, as follows:

- *1*: The user cancelled the dialog
- *0*: No error
- *-1*: The selected file could not be opened
- *-2*: The selected page was invalid

**Example (Acrobat 5.0)**

It is assumed that we are connected to an employee information database. We communicate with the database using the `ADBC` object and related objects. An employee’s record is requested and three columns are utilized, *FirstName*, *SecondName*, and *Picture*. The *Picture* column, from the database, contains a device-independent path to the employee’s picture, stored in PDF format. The script might look like this:

```
var f = this.getField("myPicture");
f.buttonSetCaption(row.FirstName.value + " " + row.LastName.value);
if (f.buttonImportIcon(row.Picture.value) != 0)
    f.buttonImportIcon("/F/employee/pdfs/NoPicture.pdf");
```

The button field “myPicture” has been set to display both icon and caption. The employee’s first and last names are concatenated to form the caption for the picture. Note that if there is an error in retrieving the icon, a substitute icon can be imported.

<a id="22265"></a>
<a id="buttonsetcaption"></a>
<a id="id630"></a>
#### buttonSetCaption

|  |  |  |  |
|---|---|---|---|
| 5.0 | D |  |  |

Sets the caption associated with a button.

Use `buttonGetCaption` to get the current caption.

See buttonAlignX, buttonAlignY, buttonFitBounds, buttonPosition, buttonScaleHow, and buttonScaleWhen for details on how the icon and caption are placed on the button face.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cCaption` | The caption associated with the button. |
| `nFace` | (optional) If specified, sets a caption of the given type: * *0*: (default) normal caption * *1*: down caption * *2*: rollover caption |

Example:

```
var f = this.getField("myButton");
f.buttonSetCaption("Hello");
```

<a id="39147"></a>
<a id="buttonseticon"></a>
<a id="id631"></a>
#### buttonSetIcon

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | All |

Sets the icon associated with a button.

See buttonAlignX, buttonAlignY, buttonFitBounds, buttonPosition, buttonScaleHow, and buttonScaleWhen for details on how the icon and caption are placed on the button face.

Use either `buttonGetIcon` or `doc.getIcon` to get an `Icon` object that can be used for the `oIcon` parameter of this method.

> **Note**
>
> This method must be executed from script embedded within the document. Executing script containing `buttonSetIcon` in the console of the Adobe Reader, for example, will throw a `NotAllowedError` exception.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oIcon` | The `Icon` object associated with the button. |
| `nFace` | (optional) If specified, sets an icon of the given type: * *0*: (default) normal icon * *1*: down icon * *2*: rollover icon |

Example: This example takes every named icon in the document and creates a list box using the names. Selecting an item in the list box sets the icon with that name as the button face of the field “myPictures”. What follows is the mouse-up action of the button field “myButton”.

```
var f = this.getField("myButton")
var aRect = f.rect;
aRect[0] = f.rect[2];             // Place list box relative to the
aRect[2] = f.rect[2] + 144;        // position of "myButton"
var myIcons = new Array();
var l = addField("myIconList", "combobox", 0, aRect);
l.textSize = 14;
l.strokeColor = color.black;
for (var i = 0; i < this.icons.length; i++)
    myIcons[i] = this.icons[i].name;
l.setItems(myIcons);
l.setAction("Keystroke",
    'if (!event.willCommit) {rt'
    + 'var f = this.getField("myPictures");rt'
    + 'var i = this.getIcon(event.change);rt'
    + 'f.buttonSetIcon(i);r'
    + '}');
```

The named icons themselves can be imported into the document through an interactive scheme, such as the example given in `addIcon` or through a batch sequence.

See also buttonGetCaption for a more extensive example.

<a id="20167"></a>
<a id="checkthisbox"></a>
<a id="id632"></a>
#### checkThisBox

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | F |

Checks or unchecks the specified widget.

Only check boxes can be unchecked. A radio button cannot be unchecked using this method, but if its default state is unchecked (see defaultIsChecked) it can be reset to the unchecked state using the `resetForm`. method of the Doc.

> **Note**
>
> For a set of radio buttons that do not have duplicate export values, you can set the `value` to the export value of the individual widget that should be checked (or pass an empty string if none should be).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nWidget` | The 0-based index of an individual check box or radio button widget for this field. The index is determined by the order in which the individual widgets of this field were created (and is unaffected by tab-order).  Every entry in the Fields panel has a suffix giving this index; for example, MyField #0. |
| `bCheckIt` | (optional) Specifies whether the widget should be checked. The default is `true`. |

Example: Check a check box.

```
var f = this.getField("ChkBox");
f.checkThisBox(0,true);
```

<a id="34371"></a>
<a id="clearitems"></a>
<a id="id633"></a>
#### clearItems

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | D | No | F |

Clears all the values in a list box or combo box.

**Related methods** and properties include numItems, getItemAt, deleteItemAt, currentValueIndices, insertItemAt and setItems.

Example: Clear the field “myList” of all items.

```
this.getField("myList").clearItems();
```

<a id="29663"></a>
<a id="defaultischecked"></a>
<a id="id634"></a>
#### defaultIsChecked

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | All |

Sets the specified widget to be checked or unchecked by default.

> **Note**
>
> For a set of radio buttons that do not have duplicate export values, you can set the `defaultValue` to the export value of the individual widget that should be checked by default (or pass an empty string if none should be checked).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nWidget` | The 0-based index of an individual radio button or check box widget for this field. The index is determined by the order in which the individual widgets of this field were created (and is unaffected by tab-order).  Every entry in the Fields panel has a suffix giving this index (for example, MyField #0). |
| `bIsDefaultChecked` | (optional) If `true` (the default), the widget should be checked by default (for example, when the field gets reset). If `false`, it should be unchecked by default. |

**Returns**

`true` on success.

Example: Change the default of “ChkBox” to checked, then reset the field to reflect the default value.

```
var f = this.getField("ChkBox");
f.defaultIsChecked(0,true);
this.resetForm(["ChkBox"]);
```

<a id="22922"></a>
<a id="deleteitemat"></a>
<a id="id635"></a>
#### deleteItemAt

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | D | No | F |

Deletes an item in a combo box or a list box.

For a list box, if the current selection is deleted, the field no longer has a current selection. If this method is invoked again on the same field and no parameter is specified, unexpected behavior can result because there is no current selection to delete. Therefore, it is important to make a new selection (such as by using the `currentValueIndices` method) for the method to behave as documented.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nIdx` | (optional) The 0-based index of the item in the list to delete. If not specified, the currently selected item is deleted. |

Example: Delete the current item in the list, then select the top item in the list.

```
var a = this.getField("MyListBox");
a.deleteItemAt();              // Delete current item, and...
a.currentValueIndices = 0;     // select top item in list
```

<a id="20956"></a>
<a id="getarray"></a>
<a id="id636"></a>
#### getArray

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Gets the array of terminal child fields (that is, fields that can have a value) for this Field object, the parent field.

**Returns**

An array of Field objects

Example: Make a calculation of the values of the child fields of the parent field.

```
// f has 3 children: f.v1, f.v2, f.v3
var f = this.getField("f");
var a = f.getArray();
var v = 0.0;
for (j =0; j < a.length; j++) v += a[j].value;
// v contains the sum of all the children of field "f"
```

<a id="14076"></a>
<a id="getitemat"></a>
<a id="id637"></a>
#### getItemAt

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Gets the internal value of an item in a combo box or a list box.

The number of items in a list can be obtained from `numItems`. See also insertItemAt, deleteItemAt, clearItems, currentValueIndices and setItems.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nIdx` | The 0-based index of the item in the list or -1 for the last item in the list. |
| `bExportValue` | (optional, Acrobat 5.0) Specifies whether to return an export value:  -  If `true` (the default), if the item has an export value, it is returned. If there is no export value, the item name is returned. -  If `false`, the method returns the item name. |

**Returns**

The export value or name of the specified item.

Example: In the two examples that follow, assume there are three items on “myList”: “First”, with an export value of 1; “Second”, with an export value of 2; and “Third”, with no export value.

```
// Returns value of first item in list, which is 1
var f = this.getField("myList");
var v = f.getItemAt(0);
```

The following example shows the use of the second optional parameter. By setting it to `false`, the item name (face value) can be obtained, even if there is an export value.

```
for (var i=0; i < f.numItems; i++)
    console.println(f.getItemAt(i,true) + ":  " + f.getItemAt(i,false));
```

The output to the console reads:

```
1:            First
2:            Second
Third:        Third
```

<a id="28478"></a>
<a id="getlock"></a>
<a id="id638"></a>
#### getLock

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Gets a `Lock` object, a generic object that contains the lock properties of a signature field.

See also setLock.

**Returns**

The `Lock` object for the field.

<a id="48393"></a>
<a id="insertitemat"></a>
<a id="id639"></a>
#### insertItemAt

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | D | No | F |

Inserts a new item into a combo box or a list box.

**Related methods** and properties include numItems, getItemAt, deleteItemAt, clearItems, currentValueIndices and setItems.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The item name that will appear in the form. |
| `cExport` | (optional) The export value of the field when this item is selected. If not provided, the `cName` is used as the export value. |
| `nIdx` | (optional) The index in the list at which to insert the item. If 0 (the default), the new item is inserted at the top of the list. If –1, the new item is inserted at the end of the list. |

Example:

```
var l = this.getField("myList");
l.insertItemAt("sam", "s", 0); /* inserts sam to top of list l */
```

<a id="49604"></a>
<a id="isboxchecked"></a>
<a id="id640"></a>
#### isBoxChecked

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Determines whether the specified widget is checked.

> **Note**
>
> For a set of radio buttons that do not have duplicate export values, you can get the `value`, which is equal to the export value of the individual widget that is currently checked (or returns an empty string, if none is).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nWidget` | The 0-based index of an individual radio button or check box widget for this field. The index is determined by the order in which the individual widgets of this field were created (and is unaffected by tab-order).  Every entry in the Fields panel has a suffix giving this index, for example, MyField #0. |

**Returns**

`true` if the specified widget is currently checked, `false` otherwise.

Example: Determine the state of the check box and report back with an alert box.

```
var f = this.getField("ChkBox");
var cbStatus = (f.isBoxChecked(0)) ? " " : " not ";
app.alert("The box is" + cbStatus + "checked");
```

<a id="74380"></a>
<a id="isdefaultchecked"></a>
<a id="id641"></a>
#### isDefaultChecked

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Determines whether the specified widget is checked by default (for example, when the field gets reset).

> **Note**
>
> For a set of radio buttons that do not have duplicate export values, you can get the `defaultValue`, which is equal to the export value of the individual widget that is checked by default (or returns an empty string, if none is).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nWidget` | The 0-based index of an individual radio button or check box widget for this field. The index is determined by the order in which the individual widgets of this field were created (and is unaffected by tab-order).  Every entry in the Fields panel has a suffix giving this index, for example, MyField #0. |

**Returns**

`true` if the specified widget is checked by default, `false` otherwise.

Example: Determine if the specified check box is checked by default.

```
var f = this.getField("ChkBox");
var cbStatus = (f.isDefaultChecked(0)) ? "Checked" : "Unchecked";
app.alert("The Default: " + cbStatus);
```

<a id="37472"></a>
<a id="id642"></a>
<a id="id643"></a>
#### setAction

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | Not available in Reader |

Sets the JavaScript action of the field for a given trigger.

**Related methods** are the `Bookmark` object setAction method and the Doc methods setAction, addScript, and setPageAction.

> **Note**
>
> This method will overwrite any action already defined for the chosen trigger.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cTrigger` | A string that sets the trigger for the action. Values are:  *MouseUp MouseDown MouseEnter MouseExit OnFocus OnBlur Keystroke Validate Calculate Format*  For a list box, use the `Keystroke` trigger for the Selection Change event. |
| `cScript` | The JavaScript code to be executed when the trigger is activated. |

Example: Set up a button field with `addField`, add some properties, and a mouse-up action using `setAction`.

```
var f = this.addField("actionField", "button", 0, [20, 100, 100, 20]);
f.setAction("MouseUp", "app.beep(0);");
f.delay = true;
    f.fillColor = color.ltGray;
    f.buttonSetCaption("Beep");
    f.borderStyle = border.b;
    f.lineWidth = 3;
    f.strokeColor = color.red;
    f.highlight = highlight.p;
f.delay = false;
```

<a id="34701"></a>
<a id="setfocus"></a>
<a id="id644"></a>
#### setFocus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.05 | No | No | All |

Sets the keyboard focus to this field. This can involve changing the page that the user is currently on or causing the view to scroll to a new position in the document. This method brings the document in which the field resides to the front, if it is not already there.

See also bringToFront.

Example: Search for a certain open document, then focus on the field of interest. This script uses `app.activeDocs`, which requires the `disclosed` property of the documents to be `true`, or the script to be run during console, batch or menu events.

```
var d = app.activeDocs;
for (var i = 0; i < d.length; i++) {
    if (d[i].info.Title == "Response Document") {
        d[i].getField("name").value="Enter your name here: "
        // also brings the doc to front.
        d[i].getField("name").setFocus();
        break;
    }
}
```

<a id="90526"></a>
<a id="setitems"></a>
<a id="id645"></a>
#### setItems

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | D | No | F |

Sets the list of items for a combo box or a list box.

**Related methods** and properties include numItems, getItemAt, deleteItemAt, currentValueIndices and clearItems.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oArray` | An array in which each element is either an object convertible to a string or another array:  -  For an element that can be converted to a string, the user and export values for the list item are equal to the string. -  For an element that is an array, the array must have two subelements convertible to strings, where the first is the user value and the second is the export value. |

**Examples**

Get various fields (combo or list) and set items in the list using various techniques.

```
var l = this.getField("ListBox");
l.setItems(["One", "Two", "Three"]);

var c = this.getField("StateBox");
c.setItems([["California", "CA"],["Massachusetts", "MA"],
    ["Arizona", "AZ"]]);

var c = this.getField("NumberBox");
c.setItems(["1", 2, 3, ["PI", Math.PI]]);
```

<a id="73832"></a>
<a id="setlock"></a>
<a id="id646"></a>
#### setLock

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | Yes | Not allowed in Reader: Only available in Acrobat products |

Controls which fields are to be locked when a signature is applied to this signature field. No modifications can be made to locked fields. If the signature is cleared, all fields that were locked become unlocked. The property settings can be obtained using `getLock`.

> **Note**
>
> The method can be executed during a batch, application initialization, or console event. See priv.

This method cannot be applied to a field that is in a document that is already signed.

**Parameters**

| Property | Description |
|----------|-------------|
| `oLock` | A `Lock` object containing the lock properties. |

**Returns**

`true` if successful, otherwise `false` or throws an exception.

<a id="26269"></a>
**Lock Object**

A generic JavaScript object containing lock properties. This object is passed to `setLock` and returned by `getLock` for a signature field. It contains the following properties.

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `action` | String | R/W | The language-independent name of the action. Values are: * *All*: All fields in the document are to be locked. * *Include*: Only the fields specified in fields are to be locked. * *Exclude*: All fields except those specified in fields are to be locked. |
| `fields` | Array of Strings | R/W | An array of strings containing the field names. Required if the value of action is `Include` or `Exclude`. |

<a id="63549"></a>
<a id="signaturegetmodifications"></a>
<a id="id647"></a>
#### signatureGetModifications

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

**Returns** an object containing information on modifications that have been made to the document after the signature field was signed. The information includes only the difference between the current and signed state of the document. Transient objects, such as objects added after the signature but then subsequently deleted, are not reported.

**Returns**

An object containing modification information. The object has the following properties:

| Property | Type | Description |
|----------|------|-------------|
| `formFieldsCreated` | Array of Field objects | Array of form fields created after signing. |
| `formFieldsDeleted` | Array of Generic objects | Array of form fields deleted after signing. Each generic object in the array is a string of the form `name: type`. |
| `formFieldsFilledIn` | Array of Field objects | Array of form fields filled in after signing. |
| `formFieldsModified` | Array of Field objects | Array of form fields modified after signing. In this context, form field fill-in does not constitute modification. |
| `annotsCreated` | Array of `Annotation`  objects | Array of annotations created after signing. If the annotation is transient (for example, a dynamically created pop-up), the corresponding element of the array is a string of the form `author: name: type`. |
| `annotsDeleted` | Array of Generic objects | Array of annotations deleted after signing. Each generic object in the array is of the form `author: name: type`. |
| `annotsModified` | Array of `Annotation`  objects | Array of annotations modified after signing. If the annotation is transient (for example, a dynamically created pop-up), the corresponding element of the array is a string of the form `author: name: type`. |
| `numPagesCreated` | Integer | Number of pages added after signing. |
| `numPagesDeleted` | Integer | Number of pages deleted after signing. |
| `numPagesModified` | Integer | Number of pages whose content has been modified after signing (add/delete/modify of annotations/form fields are not considered as page modification for this purpose). |
| `spawnedPagesCreated` | Array of Strings | List of pages spawned after signing. For each spawned page, the name of the source template is provided. |
| `spawnedPagesDeleted` | Array of Strings | List of spawned pages deleted after signing. For each spawned page, the name of the source template is provided. |
| `spawnedPagesModified` | Array of Strings | List of spawned pages modified after signing. For each spawned page, the name of the source template is provided. |

Example: Write modification information back to the console.

```
var sigField = this.getField( "mySignature" );
var sigMods = sigField.signatureGetModifications();

var formFieldsCreated = sigMods.formFieldsCreated;
for( var i = 0; i < formFieldsCreated.length; i++ )
    console.println( formFieldsCreated[i].name );

var formFieldsDeleted = sigMods.formFieldsDeleted;
for( var i = 0; i < formFieldsDeleted.length; i++ )
    console.println( formFieldsDeleted[i].name );

var formFieldsFilledIn = sigMods.formFieldsFilledIn;
for( var i = 0; i < formFieldsFilledIn.length; i++ )
    console.println( formFieldsFilledIn[i].name );

var formFieldsModified = sigMods.formFieldsModified;
for( var i = 0; i < formFieldsModified.length; i++ )
    console.println( formFieldsModified[i].name );

var spawnedPages = sigMods.spawnedPagesCreated;
for( var i = 0; i < spawnedPages.length; i++ )
    console.println( spawnedPages[i] );

console.println( sigMods.numPagesDeleted );
```

<a id="10692"></a>
<a id="signaturegetseedvalue"></a>
<a id="id648"></a>
#### signatureGetSeedValue

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a `SeedValue` object that contains the seed value properties of a signature field. Seed values are used to control properties of the signature, including the signature appearance, reasons for signing, and the person.

See signatureSetSeedValue.

**Returns**

A `SeedValue` object.

Example: Access the seed value for a signature field.

```
var f = this.getField( "sig0" );
var seedValue = f.signatureGetSeedValue();
// displays the seed value filter and flags
console.println( "Filter name:" + seedValue.filter);
console.println( "Flags:" + seedValue.flags);
// displays the certificate seed value constraints
var certSpec = seedValue.certspec;
console.println( "Issuer:" + certspec.issuer);
```

<a id="89499"></a>
<a id="signatureinfo"></a>
<a id="id649"></a>
#### signatureInfo

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

**Returns** a `SignatureInfo` object that contains the properties of the signature. The object is a snapshot of the signature at the time that this method is called. A security handler may specify additional properties that are specific to the security handler.

> **Note**
>
> There are no restrictions on when this method can be called. However, the specified security handler, `oSig`, may not always be available. See the `security.` getHandler method for details.

Some properties of a signature handler, for example, `certificates` (a property of the `SignatureInfo` object), may return a `null` value until the signature is validated. Therefore, `signatureInfo` should be called again after `signatureValidate`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oSig` | (optional) The `SecurityHandler` object to use to retrieve the signature properties. If not specified, the security handler is determined by the user preferences. (It is usually the handler that was used to create the signature.) |

**Returns**

A `SignatureInfo` object that contains the properties of the signature. This type of object is also used when signing signature fields, signing FDF objects, or with the `FDF` object `signatureValidate` method.

Example: Access SignatureInfo object properties.

```
// Get all info
var f = getField( "Signature1" );
f.signatureValidate();
var s = f.signatureInfo();
console.println( "Signature Attributes:" );
for(i in s) console.println( i + " = " + s[i] );

// Get particular info
var f = this.getField("Signature1"); // uses the ppklite sig handler
var Info = f.signatureInfo();
// Some standard signatureInfo properties
console.println("name = " + Info.name);
console.println("reason = " + Info.reason);
console.println("date = " + Info.date);

// Additional signatureInfo properties from PPKLite
console.println("contact info = " + Info.contactInfo);

// Get the certificate; first (and only) one
var certificate = Info.certificates[0];

// Common name of the signer
console.println("subjectCN = " +  certificate.subjectCN);
console.println("serialNumber = " +  certificate.serialNumber);

// Display some information about the distinguished name of signer
console.println("subjectDN.cn = " + certificate.subjectDN.cn);
console.println("subjectDN.o = " +  certificate.subjectDN.o);
```

<a id="65475"></a>
<a id="signaturesetseedvalue"></a>
<a id="id650"></a>
#### signatureSetSeedValue

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | Yes | Not allowed in Reader: Only available in Acrobat products |

Sets properties that are used when signing signature fields. The properties are stored in the signature field and are not altered when the field is signed, the signature is cleared, or when `resetForm` is called. Use `signatureGetSeedValue` to obtain the property settings.

When setting seed values, keep in mind the following:

- Seed values should not be set on signed documents and cannot be set on certified documents. They are primarily used to configure fields on documents that are not yet signed.
- Setting a seed value often causes Acrobat not to display or not to use its default settings. For example, preset reasons are stored in the registry and specifying a signing reason causes the application to ignore the registry list so that only the custom reasons are displayed.

> **Note**
>
> The method can be executed during a batch, application initialization or console event. See priv.

Certifying signatures are signatures with a `SignatureInfo` object `mdp` property value of `allowNone`, `default`, or `defaultAndComments`.

Not allowed in Adobe Reader.

Refer to the *Acrobat 8.0 Security Feature User Reference* to obtain a deeper understanding of the use of signature seed values.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oSigSeedValue` | A `SeedValue` object containing the signature seed value properties. |

<a id="64991"></a>
**SeedValue Object**

A generic JavaScript object, passed to `signatureSetSeedValue` and returned by `signatureGetSeedValue`, which represents a signature seed value. It has the following properties:

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `appearanceFilter` | String | R/W | (Acrobat 9.0) A string corresponding to the named appearance that the AppearanceFilter seed value should match. |
| `certspec` | object | R/W | A seed value `CertificateSpecifier` object. see CertificateSpecifier Object for a listing of the properties of this object. |
| `digestMethod` | Array of strings | R/W | (Acrobat 8) An array of acceptable digest methods to use while signing. The valid string values are `SHA1`, `SHA256`, `SHA384`, `SHA512`, `MD5`, and `RIPEMD160`. |

> **Note**
>
> This is only applicable if the DigitalID contains RSA public/private keys. If they contain DSA public/private keys, then the value is always `SHA1`.
>
> The `flags` property indicates whether this is a required constraint.
>
> - - `filter`
>   - String
>   - R/W
>   - The language-independent name of the security handler to be used when signing.
>     If `filter` is specified and the `flags` property indicates this entry is a required constraint, then the signature handler specified by this entry must be used when signing; otherwise, signing must not take place. If `flags` indicates that this is an optional constraint, then this handler should be used if it is available. If it is not available, a different handler can be used instead.
> - - `flags`
>   - Number
>   - R/W
>   - A set of bit flags controlling which of the following properties of this object are required. The value is the logical OR of the following values, which are set if the corresponding property is required:
>     - 1: filter
>     - 2: subFilter
>     - 4: version
>     - 8: reasons
>     - 16: legalAttestations
>     - 32: shouldAddRevInfo
>     - 64: digestMethod\*
>     - 128: lockDocument
>     - 256: appearanceFilter
>     Usage: 1 specifies filter, 3 specifies filter and sub-filter, and 11 specifies filter, sub-filter, and reasons. If this field is not present, all properties are optional.
> - - `legalAttestations`
>   - Array of Strings
>   - R/W
>   - (Acrobat 7.0) A list of legal attestations that the user can use when creating an Modification Detection and Prevention (MDP) (certified) signature.
>     The value of the corresponding flag in the `flags` property indicates whether this is a required or optional constraint.
> - - `lockDocument`
>   - String
>   - R/W
>   - (Acrobat 9.0) A string corrresponding to one of the three LockDocument seed value states. Values are
>     - auto
>     - true
>     - false
>     Any other value will not be set.
> - - `mdp`
>   - String
>   - R/W
>   - (Acrobat 7.0) The MDP setting to use when signing the field. Values are
>     *allowNone
>     default
>     defaultAndComments*
>     While `allowAll` is a legal value, it cancels out the effect of MDP and no certification signature can be used for this field, resulting in the signature being an approval signature, not an certification signature.
>     Values are unique identifiers and are described in the table titled [Modification Detection and Prevention (MDP) Values](./security-signature-apis.md#64083).
> - - `reasons`
>   - Array of Strings
>   - R/W
>   - A list of reasons that the user is allowed to use when signing.
>     (Acrobat 8.0) If this array has a single element and that element is a single period ‘.’ and if the `reasons` are marked as required by the `flags` property, then Acrobat 8 will suppress the UI for specifying a reason during signing. This overrides the users preference.
>     If this array is empty and `reasons` are marked as required, an exception will be thrown.
> - - `shouldAddRevInfo`
>   - Boolean
>   - R/W
>   - (Acrobat 8) If set to `true`, instructs the application to carry out revocation checking of the certificate (and the corresponding chains) used to sign, and include all the revocation information within the signature.
>     Only relevant if `subFilter` is `adbe.pkcs7.detached` or `adbe.pkcs7.sha1`, and it is not applicable for `adbe.x509.rsa_sha1`. Hence, if the `subFilter` is `adbe.x509.rsa_sha1` and it’s required that revocation information be added, then the signing operation fails.
>     If `shouldAddRevInfo` is `true` and the `flags` property indicates this is a required constraint, then the tasks described above must be performed. If they cannot be performed, then signing must fail.
>     The default value is `false`.
> - - `subFilter`
>   - Array of Strings
>   - R/W
>   - An array of acceptable formats to use for the signature. Refer to the Signature Info object’s `subFilter` property for a list of known formats.
>     The first name in the array that matches an encoding supported by the signature handler should be the encoding that is actually used for signing. If `subFilter` is specified and the `flags` property indicates that this entry is a required constraint, then the first matching encodings must be used when signing; otherwise, signing must not take place. If the `flags` property indicates that this is an optional constraint, then the first matching encoding should be used if it is available. If it is not available, a different encoding can be used.
> - - `timeStampspec`
>   - Object
>   - R/W
>   - (Acrobat 7.0) A Seed Value timeStamp Specifier object. It uses the `url` and `flags` properties to specify a timestamp server. See Seed value timeStamp specifier object.
> - - `version`
>   - Number
>   - R/W
>   - The minimum required version number of the signature handler to be used to sign the signature field. Valid values are 1 and 2. A value of 1 specifies that the parser must be able to recognize all seed value dictionary entries specified in PDF 1.5. A value of 2 specifies that it must be able to recognize all seed value dictionary entries specified in PDF 1.7 and earlier.
>     The `flags` property indicates whether this is a required constraint.

> **Note**
>
> The [PDF Reference](https://adobe.com/go/pdfreference) version 1.6 and earlier, erroneously indicates that the `V` entry (the key that corresponds to the `version` parameter) is of type integer. This entry is of type real.

<a id="83422"></a>
**CertificateSpecifier Object**

This generic JavaScript object contains the certificate specifier properties of a signature seed value. Used in the `certSpec` property of the `SeedValue` object. This object contains the following properties:

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `flags` | Number | R/W | A set of bit flags controlling which of the following properties of this object are required. The value is the logical OR of the following values, which are set if the corresponding property is required: * 1: subject * 2: issuer * 4: oid * 8: subjectDN * 16: Reserved * 32: keyUsage * 64: url\*  If this field is not present, all properties are optional. |
| `issuer` | Array of `Certificate` objects | R/W | An array of `Certificate` objects that are acceptable for signing. If specified, the signing certificate must be issued by a certificate that is an exact match with one of the certificates in this array.  The value of the corresponding flag in the `flags` property indicates whether this is a required or optional constraint. |
| `keyUsage` | Object | R/W | (Acrobat 8.0) Array of integers, where each integer specifies the acceptable key-usage extension that must be present in the signing certificate.  Each integer is constructed as follows:  There are two bits used for each key-usage type (defined in RFC 3280) starting from the least significant bit: * digitalSignature(bits 2,1), * nonRepudiation(4,3) * keyEncipherment(6,5) * dataEncipherment(8,7) * keyAgreement(10,9) * keyCertSign(12,11) * cRLSign(14,13) * encipherOnly(16,15) * decipherOnly(18,17) * The value of the two bits have the following semantics: * 00: the corresponding keyUsage must not be set * 01: the corresponding keyUsage must be set * 10 and 11: the state of the corresponding `keyUsage` doesn’t matter.  For example, if it is required that the key-usage type digitalSignature be set and the state of all other key-usage types do not matter, then the corresponding integer would be 0x7FFFFFFD. That is, to represent digitalSignature, set 01 for bits 2 and 1 respectively, and set 11 for all other key-usage types.  The value of the corresponding flag in the `flags` property indicates whether this is a required constraint. |
| `oid` | Array of  Strings | R/W | An array of strings that contain Policy OIDs that must be present in the signing certificate. This property is only applicable if the `issuer` property is present.  The value of the corresponding flag in the `flags` property indicates whether this is a required or optional constraint. |
| `subject` | Array of `Certificate` objects | R/W | An array of `Certificate` objects that are acceptable for signing. If specified, the signing certificate must be an exact match with one of the certificates in this array.  The value of the corresponding flag in the `flags` property indicates whether this is a required or optional constraint. |
| `subjectDN` | Array of objects | R/W | (Acrobat 8.0) Array of objects, where each object specifies a Subject Distinguished Name (DN) that is acceptable for signing. A signing certificate satisfies a DN requirement if it at least contains all the attributes specified in the DN (it can therefore contain additional DN attributes). If this entry is specified, the signing certificate must satisfy at least one of the DNs in the array.  DN attribute restrictions are specified in this object by adding them as properties. The properties’ key names can either be the corresponding attributes’ friendly names or OIDs (as defined in RFC 3280). The properties’ value must be of type string.  The value of the corresponding flag in the `flags` property indicates whether this is a required or optional constraint.  Example 1: `{cn:"Alice", ou:"Engineering", o:"Acme Inc"}`. The friendly names for the DN attributes (`cn`, `o`, `ou`, and so on) are the ones defined in RDN (see RDN).  Example 2: `{cn:"Joe Smith", ou:"Engineering", "2.5.4.43":"JS"}`, where OID `2.5.4.43` is used to carry out matching for the “Initials” attribute. The following is sample code to define the above DN:  `var subjectDN = {cn:"Joe Smith", ou:"Engineering"}; subjectDN["2.5.4.43"] = "JS";`  Attributes whose value is of type DirectoryString or IA5String can be specified as shown in the example above, whereas for all other value types, for example, `dateOfBirth` whose value is of type GeneralizedTime, the values need to be specified as a hex-encoded binary string.  For more information about the various attributes and their types, refer to RFC 3280. |
| url | String | R/W | A URL that can be used to enroll for a new credential if a matching credential is not found.  A degenerate use of this property is when the URL points to a web service that is a DigitalID store (such as a signature web service that can be used for server-based signing). In that case, the URL indicates that as long as the signer has a DigitalID from that web service, it is acceptable for signing.  The value of the corresponding flag in the `flags` property indicates whether this is a required or optional constraint. |
| `urlType` | String | R/W | (Acrobat 8.0) String indicating the type of URL specified by the `url` property. These are the valid values for Acrobat 8.0: * `"HTML"`: The URL points to an HTML website and Acrobat will use the web browser to display its contents. The the value of the `url` bit of the `flags` property is ignored. * `"ASSP"`: The URL references a signature web service that can be used for server-based signing. If the `url` bit of the `flags` property indicates that this is a required constraint, this implies that the credential used when signing must come from this server.  If this attribute isn’t present, it’s assumed that the URL points to a HTML site. |

<a id="44704"></a>
**Seed value timeStamp specifier object**

The properties of the seed value timeStamp specifier object are as follows:

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `url` | String | R/W | URL of the timeStamp server providing an RFC 3161 compliant timeStamp. |
| `flags` | Number | R/W | A bit flag controlling whether the time stamp is required (1) or not required (0). The default is 0. |

Example 1: Seed the signature field, which has yet to be signed, with MDP, legal attestations, and permitted reasons for signing.

```
// Obtain the signature Field object:
var f = this.getField("mySigField");
f.signatureSetSeedValue({
    mdp: "defaultAndComments",
    legalAttestations: ["Trust me and be at ease.",
        "You can surely trust the author."],
    reasons: ["This is a reason", "This is a better reason"],
    flags: 8
})
```

Example 2: Sets the signing handler as PPKMS and the format as “adbe.pkcs7.sha1”.

```
   var f = this.getField( "mySigField" );

   f.signatureSetSeedValue({
       filter: "Adobe.PPKMS",
       subFilter: ["adbe.pkcs7.sha1"],
       flags: 3
});
```

Example 3: Sets the signing handler as PPKLite and the issuer of the signer’s certificate as caCert. Both are mandatory seed values and signing will fail if either constraint is not met.

```
var caCert = security.importFromFile("Certificate", "/C/temp/CA.cer");
f.signatureSetSeedValue({
    filter: "Adobe.PPKLite",
    certspec: {
        issuer: [caCert],
        url: "http://www.example.com/enroll.html",
        flags : 2
    },
    flags: 1
});
```

<a id="20782"></a>
<a id="id652"></a>
<a id="id653"></a>
#### signatureSign

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | Yes | Requires digital signature rights |

Signs the field with the specified security handler. See also `security.` getHandler and `securityHandler.` login.

> **Note**
>
> This method can only be executed during a batch, console, or application initialization event. See priv. The `event` object contains a discussion of JavaScript events.

Signature fields cannot be signed if they are already signed. Use `resetForm` to clear signature fields.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oSig` | Specifies the `SecurityHandler` object to be used for signing. Throws an exception if the specified handler does not support signing operations. Some security handlers require that the user be logged in before signing can occur. If `oSig` is not specified, this method selects a handler based on user preferences or by prompting the user if `bUI` is `true`. |
| `oInfo` | (optional) A `SignatureInfo` object specifying the writable properties of the signature. See also signatureInfo. |
| `cDIPath` | (optional) The device-independent path to the file to save to following the application of the signature. If not specified, the file is saved back to its original location. |
| `bUI` | (optional, Acrobat 6.0) A Boolean value specifying whether the security handler should show the user interface when signing. If `true`, `oInfo` and `cDIPath` are used as default values in the signing dialog boxes. If `false` (the default), the signing occurs without a user interface. |
| `cLegalAttest` | (optional, Acrobat 6.0) A string that can be provided when creating an certification signature.  Certification signatures are signatures where the `mdp` property of the `SignatureInfo` object has a value other than `allowAll`. When creating an certification signature, the document is scanned for legal warnings and these warnings are embedded in the document. A caller can determine what legal warnings are found by first calling the Doc `getLegalWarnings` method. If warnings are to be embedded, an author may provide an attestation as to why these warnings are being applied to a document. |

**Returns**

`true` if the signature was applied successfully, `false` otherwise.

Example 1: Sign the “Signature” field with the PPKLite signature handler:

```
var myEngine = security.getHandler( "Adobe.PPKLite" );
myEngine.login( "dps017", "/c/profile/dps.pfx" );
var f = this.getField("Signature");

// Sign the field
f.signatureSign( myEngine,
    {   password: "dps017",             // provide password
        location: "San Jose, CA",       // .
        .. see note below
        reason: "I am approving this document",
        contactInfo: "dpsmith@example.com",
        appearance: "Fancy"});
```

> **Note**
>
> In the above example, a password was provided. This may or may not have been necessary depending whether the `Password Timeout` had expired. The `Password Timeout` can be set programmatically by `securityHandler.setPasswordTimeout`.

Example 2: Sign an certification signature field.

```
var myEngine = security.getHandler( "Adobe.PPKLite" );
myEngine.login( "dps017", "/c/profile/dps.pfx" );

var f = this.getField( "AuthorSigFieldName" );
var s = { reason: "I am the author of this document",
        mdp: "allowNone" };
f.signatureSign({
    oSig: myEngine,
    oInfo: s,
    bUI: false,
    cLegalAttest: "To reduce file size, fonts are not embedded."
});
```

<a id="95248"></a>
<a id="id654"></a>
<a id="id655"></a>
#### signatureValidate

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Validates and returns the validity status of the signature in a signature field. This routine can be computationally expensive and take a significant amount of time depending on the signature handler used to sign the signature.

> **Note**
>
> There are no restrictions on when this method can be called. However, the parameter `oSig` is not always available. See `security.` getHandler for details.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oSig` | (optional) The security handler to be used to validate the signature. Its value is either a `SecurityHandler` object or a `SignatureParameters` object. If this handler is not specified, the method uses the security handler returned by the signature’s `handlerName` property. |
| `bUI` | (optional, Acrobat 6.0) If `true`, allows the UI to be shown when validating, if necessary. The UI may be used to select a validation handler if none is specified. The default is `false`. |

**Returns**

The validity status of the signature. Validity values are:

- *-1*: Not a signature field
- *0*: Signature is blank
- *1*: Unknown status
- *2*: Signature is invalid
- *3*: Signature of document is valid, identity of signer could not be verified
- *4*: Signature of document is valid and identity of signer is valid.

See the `signVisible` and `statusText` properties of the SignatureInfo object.

<a id="91834"></a>
**SignatureParameters object**

A generic object with the following properties that specify which security handlers are to be used for validation by `signatureValidate` :

| `oSecHdlr` | The security handler object to use to validate this signature. |
|------------|----------------------------------------------------------------|
| `bAltSecHdlr` | If `true`, an alternate security handler, selected based on user preference settings, may be used to validate the signature. The default is `false`, which means that the security handler returned by the signature’s `handlerName` property is used to validate the signature. This parameter is not used if `oSecHdlr` is provided. |

Example: Validate a signature, then report to the console.

```
var f = this.getField("Signature1") // Get signature field
var status = f.signatureValidate();
var sigInfo = f.signatureInfo();
if ( status < 3 )
     var msg = "Signature not valid! " + sigInfo.statusText;
else
    var msg = "Signature valid! " + sigInfo.statusText;
app.alert(msg);
```

<a id="16267"></a>
<a id="id656"></a>
<a id="id657"></a>
## FullScreen

The interface to fullscreen (presentation mode) preferences and properties. To acquire a `fullScreen` object, use `app.fs`.

<a id="fullscreen-properties"></a>
<a id="id658"></a>
### FullScreen properties

<a id="95727"></a>
<a id="backgroundcolor"></a>
<a id="id659"></a>
#### backgroundColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | No | All | Color Array | R/W |

The background color of the screen in full screen mode. See Color arrays for details.

Example:

```
app.fs.backgroundColor = color.ltGray;
```

<a id="12908"></a>
<a id="clickadvances"></a>
<a id="id660"></a>
#### clickAdvances

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | No | All | Boolean | R/W |

Specifies whether a mouse click anywhere on the page causes the page to advance.

<a id="43744"></a>
<a id="cursor"></a>
<a id="id661"></a>
#### cursor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | No | All | Number | R/W |

Determines the behavior of the pointer in full screen mode. The convenience `cursor` object defines all the valid cursor behaviors:

| Cursor Behavior | Keyword |
|-----------------|---------|
| Always hidden | `cursor.hidden` |
| Hidden after delay | `cursor.delay` |
| Visible | `cursor.visible` |

Example:

```
app.fs.cursor = cursor.visible;
```

<a id="46194"></a>
<a id="defaulttransition"></a>
<a id="id662"></a>
#### defaultTransition

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | No | All | String | R/W |

The default transition to use when advancing pages in full screen mode. Use `transitions` to obtain list of valid transition names supported by the viewer.

“No Transition” is equivalent to `app.fs.defaultTransition = "";`

Example: Put the document into presentation mode.

```
app.fs.defaultTransition = "WipeDown";
app.fs.isFullScreen = true;
```

<a id="54221"></a>
<a id="escapeexits"></a>
<a id="id663"></a>
#### escapeExits

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | Yes | All | Boolean | R/W |

A Boolean value specifying the escape key can be used to exit full screen mode.

> **Note**
>
> (Version 8.0) This property can only set to `false` during batch and console events. See priv. The `event` object contains a discussion of JavaScript events.

<a id="11586"></a>
<a id="isfullscreen"></a>
<a id="id664"></a>
#### isFullScreen

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Boolean | R/W |

If `true`, the viewer is in full screen mode rather than regular viewing mode, which is possible only if one or more documents are open for viewing.

> **Note**
>
> A PDF document being viewed from within a web browser cannot be put into full screen mode.

Example:

```
app.fs.isFullScreen = true;
```

In the above example, the viewer is set to full screen mode. If `isFullScreen` was previously `false`, the default viewing mode would be set. (The default viewing mode is defined as the original mode the Acrobat application was in before full screen mode was initiated.)

<a id="70106"></a>
<a id="loop"></a>
<a id="id665"></a>
#### loop

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | No | All | Boolean | R/W |

Specifies whether the document will loop around to the beginning of the document in response to a page advance (whether generated by mouse click, keyboard, or timer) in full screen mode.

<a id="11728"></a>
<a id="timedelay"></a>
<a id="id666"></a>
#### timeDelay

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | No | All | Number | R/W |

The default number of seconds before the page automatically advances in full screen mode. See useTimer to activate or deactivate automatic page turning.

Example: Set full screen properties, then go into full screen mode.

```
app.fs.timeDelay = 5;          // Delay 5 seconds
app.fs.useTimer = true;        // Activate automatic page turning
app.fs.usePageTiming = true;   // Allow page override
app.fs.isFullScreen = true;    // Go into full screen
```

<a id="85692"></a>
<a id="transitions"></a>
<a id="id667"></a>
#### transitions

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Array | R |

An array of strings representing valid transition names implemented in the viewer. `No Transition` is equivalent to setting `defaultTransition` to the empty string:

```
app.fs.defaultTransition = "";
```

Example: Produce a listing of the currently supported transition names.

```
console.println("[" + app.fs.transitions + "]");
```

<a id="70905"></a>
<a id="usepagetiming"></a>
<a id="id668"></a>
#### usePageTiming

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | No | All | Boolean | R/W |

Specifies whether automatic page turning will respect the values specified for individual pages in full screen mode. Set transition properties of individual pages using setPageTransitions.

<a id="88396"></a>
<a id="usetimer"></a>
<a id="id669"></a>
#### useTimer

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | P | No | All | Boolean | R/W |

Specifies whether automatic page turning is enabled in full screen mode. Use `timeDelay` to set the default time interval before proceeding to the next page.

<a id="12440"></a>
<a id="global"></a>
<a id="id670"></a>
## global

This is a static JavaScript object that allows you to share data between documents and to have data be persistent across sessions. Such data is called *persistent global data*. Global data-sharing and notification across documents is done through a subscription mechanism, which allows you to monitor global data variables and report their value changes across documents.

> **Note**
>
> Beginning with version 8.0, the access to global variables has changed somewhat, the details are described below:

The JavaScript category in the Preferences dialog box (Ctrl + K) has a new security check box: Enable Global Object Security Policy.

- When checked, the default, each time a global variable is written to, the origin which set it is remembered. Only origins that match can then access the variable.
- For files, this means only the file that set it, having the same path it had when the variable was set, can access the variable.
- For documents from URLs it means only the host which set it can access the variable.

There is an important exception to the restrictions described above, global variables can be defined and accessed in a privileged context, in the console, in a batch sequence and in folder JavaScript. For more information on privileged contexts, see priv.

- When not checked, documents from different origins are permitted to access the variable; this is the behavior previous to version 8.0.

For examples, see section Global object security policy.

<a id="creating-global-properties"></a>
<a id="id671"></a>
### Creating global properties

You can specify global data by adding properties to the global object. The property type can be a String, a Boolean value, or a Number.

For example, to add a variable called `radius` and to allow all document scripts to have access to this variable (provided “Enable global object security policy” is not checked), the script defines the property:

```
global.radius = 8;
```

The global variable `radius` is now known across documents throughout the current viewer session. Suppose two files, `A.pdf` and `B.pdf`, are open and the global declaration is made in `A.pdf`. From within either file (`A.pdf` *or* `B.pdf`), you can calculate the volume of a sphere using `global.radius`.

```
var V = (4/3) * Math.PI * Math.pow(global.radius, 3);
```

In either file, you obtain the same result, 2144.66058. If the value of `global.radius` changes and the script is executed again, the value of `V` changes accordingly.

<a id="deleting-global-properties"></a>
<a id="id672"></a>
### Deleting global properties

To delete a variable or a property from the `global` object, use the `delete` operator to remove the defined property. Information on the reserved JavaScript keyword `delete` can be found in the JavaScript 1.5 documentation.

For example, to remove the `global.radius` property, call the following script:

```
delete global.radius
```

<a id="66001"></a>
<a id="global-object-security-policy"></a>
<a id="id673"></a>
### Global object security policy

The new global security policy places restrictions on document access to global variables. For more information and exceptions, see the Note in global.

In a document, named `docA.pdf`, execute the following script in a non-privileged context (mouse-up button):

```
global.x = 1
global.setPersistent("x", true);
```

The path for `docA.pdf` is the origin saved with the `global.x` variable; consequently, `docA.pdf` can access this variable:

```
console.println("global.x = " + global.x);
```

To set this global from `docA.pdf`, we execute `global.x = 3`, for example, in any context.

To have a document with a different path get and set this global variable, the getting and setting must occur in a trusted context, with a raised level of privilege. The following scripts are folder JavaScript.

```
myTrustedGetGlobal = app.trustedFunction ( function()
{
    app.beginPriv();
    var y = global.x;
    return y
    app.endPriv();
});
myTrustedSetGlobal = app.trustedFunction ( function(value)
{
    app.beginPriv();
    global.x=value;
    app.endPriv();
});
```

Another document, `docB.pdf` can access the `global.x` variable through the above trusted functions:

```
// Mouse up button action from doc B
console.println("The value of global.x is " + myTrustedGetGlobal());
```

The global can also be set from `docB.pdf:`

```
// Set global.x from docB.pdf
myTrustedSetGlobal(2);
```

Once `global.x` has been set from `docB.pdf,` the origin is changed; `docA.pdf` cannot access `global.x` directly unless it is through a trusted function:

```
// Execute a mouse up button action from docA.pdf
console.println("The value of global.x is " + myTrustedGetGlobal());
```

<a id="global-methods"></a>
<a id="id674"></a>
### global methods

<a id="42685"></a>
<a id="setpersistent"></a>
<a id="id675"></a>
#### setPersistent

|  |  |  |  |
|---|---|---|---|
| 3.01 |  |  |  |

Controls whether a specified variable is persistent across invocations of Acrobat.

Persistent global data only applies to variables of type Boolean, Number, or String.

Upon application exit, persistent global variables are stored in the `glob.js` file located in the user’s folder for folder-level scripts and re-loaded at application start. For Acrobat 6.0 or later, there is a 2-4 KB limit on the size of this file. Any data added to the string after this limit is dropped.

When specifying persistent global variables, you should use a naming convention. For example, you can give your variables the form `myCompany_variableName`. This prevents collisions with other persistent global variable names throughout the documents.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cVariable` | The variable (global property) for which to set persistence. |
| `bPersist` | If `true`, the property will exist across Acrobat viewer sessions. If `false` (the default) the property will be accessible across documents but not across the Acrobat viewer sessions. |

Example: Make the `radius` property persistent and accessible for other documents.

```
global.radius = 8;                      // Declare radius to be global
global.setPersistent("radius", true);   // Now say it's persistent
```

The volume calculation, defined above, will now yield the same result across viewer sessions, or until the value of `global.radius` is changed.

<a id="28547"></a>
<a id="subscribe"></a>
<a id="id676"></a>
#### subscribe

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Allows you to automatically update fields when the value of a global variable changes. If the specified property `cVariable` is changed, even in another document, the specified function `fCallback` is called. Multiple subscribers are allowed for a published property.

**Parameters**

| Property | Description |
|----------|-------------|
| `cVariable` | The global property. |
| `fCallback` | The function to call when the property is changed. |

The syntax of the callback function is as follows:

```
function fCallback(newval) {
// newval is the new value of the global variable you
// have subscribed to.
    < code to process the new value of the global variable >
}
```

The callback will be terminated when the document from which the script was originally registered is closed, or the (global) property deleted.

Example: In this example, it is assumed that Enable Global Object Security Policy is not checked. There are two files, `setRadius.pdf` and `calcVolume.pdf`, open in Acrobat or Adobe Reader:

`setRadius.pdf` has a single button with the code

```
global.radius = 2;
```

The `calcVolume.pdf` has a document-level JavaScript named `subscribe` :

```
global.subscribe("radius", RadiusChanged);
function RadiusChanged(x)  // callback function
{
    var V = (4/3) * Math.PI * Math.pow(x,3);
    this.getField("MyVolume").value = V;  // Put value in text field
}
```

With both files open, clicking on the button in `setRadius.pdf` immediately gives an update in the text field “MyVolume” in `calcVolume.pdf` of 33.51032 (as determined by `global.radius = 2`).

<a id="29659"></a>
<a id="hostcontainer"></a>
<a id="id677"></a>
## HostContainer

This object manages communication between a PDF document and a corresponding host container that the document is contained within, such as an HTML page. The host container for a document is specified by the Doc `hostContainer` property.

The `Embedded PDF` object provides the corresponding API for the object model of the container application.

<a id="hostcontainer-properties"></a>
<a id="id678"></a>
### HostContainer properties

<a id="85023"></a>
<a id="id679"></a>
<a id="id680"></a>
#### messageHandler

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.05 | No | No | All | Object | R/W |

A notification object that is called if a script in the host container calls the `postMessage` method. This object may expose the following methods and properties:

| Method/Property | Description |
|-----------------|-------------|
| `onMessage` | (Optional) A method that is called in response to `postMessage`. The message is delivered asynchronously. The method is passed a single array parameter containing the array that was passed to `postMessage`. |
| `onError` | (Optional) A method that is called in response to an error. The method is passed an `Error` object and an array of strings corresponding to the message that caused the error.  The `name` property of the `Error` object is set to one of these: * `"MessageGeneralError"`: A general error occurred. * `"MessageNotAllowedError"`: The operation failed for security reasons.  If an error occurs and this property is undefined, the error will not be delivered (unlike messages, errors are not queued). |
| `onDisclose` | A required method that is called to determine whether the host application is permitted to send messages to the document. This allows the PDF document author to control the conditions under which messaging can occur for security reasons. The method should be set during the `Doc/Open` event. The method is passed two parameters: * *cURL*: The URL indicating the location of the host container (for example, the URL of an HTML page using an `<OBJECT>` tag). * *cDocumentURL*: The URL of the PDF document that disclosure is being checked for.  If the method returns `true`, the host container is permitted to post messages to the message handler. |
| `allowDeliverWhileDocIsModal` | A Boolean value indicating whether messages and errors will be delivered while the document is in a modal state. By default (`false`), messages and errors are queued and not delivered to the `onMessage` and `onError` handlers if the application is currently displaying a modal dialog. The `app.isModal` property can be used to detect this case. |

> **Note**
>
> Instead of specifying a method, `onDisclose` may specify the value `HostContainerDisclosurePolicy.SameOriginPolicy`, which means that the document will be disclosed to the host container if they both originate from the same location. In this case, the origination is determined by the scheme, server, and port. The scheme must be `http`, `https`, or `ftp` for the document to be disclosed.

When these methods are invoked, the `this` object will be the `messageHandler` instance that the method is being called on.

Other methods and properties can be added to `messageHandler` provided that they do not begin with `on`.

If `messageHandler` is set to `null` or an object without an `onMessage` method, messages sent by `postMessage` are queued until the property is set to a valid `messageHandler` instance.

Messages are guaranteed to be delivered in the order in which they are posted and errors are guaranteed to be delivered in the order in which they occurred. However, there is no correspondence between the delivery order of messages and errors.

**Exceptions** thrown from within the handler methods will be discarded. If an exception is thrown from within `onDisclose`, the function will be treated as a failure. Messages and errors will not be delivered while inside an `onMessage` / `onError` / `onDisclose` handler.

Example: A generic host container message handler.

```
this.hostContainer.messageHandler =
{
    onMessage: function(aMessage)
    {
        for(var i = 0; i < aMessage.length; i++)
         console.println("Recv'd Msg[ " + i + "]: " + aMessage[i]);
    },
    onError: function(error, aMessage){ },
    onDisclose: HostContainerDisclosurePolicy.SameOriginPolicy
};
```

<a id="hostcontainer-methods"></a>
<a id="id681"></a>
### HostContainer methods

<a id="90555"></a>
<a id="id682"></a>
<a id="id683"></a>
#### postMessage

|  |  |  |  |
|---|---|---|---|
| 7.0.5 |  |  |  |

Sends a message asynchronously to the message handler for the host container of the PDF document. For this message to be delivered, the host container (for example, an `<OBJECT>` element in an HTML page) must have registered for notification by setting its `messageHandler` property. The message is passed to the `onMessage` method of the `messageHandler`.

The messages are submitted to a queue until they are delivered. If the queue exceeds a maximum number of messages, a parameter error is thrown until some of the messages in the queue have been delivered.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `aMessage` | An array of one or more strings that are passed to the `onMessage` method of the `messageHandler` property. |

Example:

```
var aMessage = ["MyMessageName", "Message Body"];
this.hostContainer.postMessage(aMessage);
```

<a id="73868"></a>
<a id="icon"></a>
<a id="id684"></a>
## Icon

This generic JavaScript object is an opaque representation of a Form XObject appearance stored in the Doc `icons` property. It is used with Field objects of type `button`. The `icon` object contains the following property:

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `name` | string | R | The name of the icon. An icon has a name if it exists in the document-level named icons tree. |

<a id="48588"></a>
<a id="icon-stream"></a>
<a id="id685"></a>
## Icon Stream

This generic JavaScript object represents an icon stream. It is used by `app.addToolButton` and `collab.addStateModel`. It has the following properties:

| Property | Description |
|----------|-------------|
| `read(nBytes)` | A function that takes the number of bytes to read and returns a hex-encoded string. The data should be the icon representation as 32 bits per pixel with 4 channels (ARGB) or 8 bits per channel with the channels interleaved. If the icon has multiple layers, the function may return the pixels for the topmost layer, followed by the next layer behind it, and so on. |
| `width` | The icon width in pixels. |
| `height` | The icon height in pixels. |

The `util.iconStreamFromIcon` method can be used to convert an `Icon` object to an `Icon Stream` object.

<a id="68797"></a>
<a id="identity"></a>
<a id="id686"></a>
## identity

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | All |

This is a static object that identifies the current user of the application.

> **Note**
>
> The `identity` object properties are only accessible during batch, console and application initialization events to protect the privacy of the user. See priv.

<a id="identity-properties"></a>
<a id="id687"></a>
### identity properties

<a id="69829"></a>
<a id="corporation"></a>
<a id="id688"></a>
#### corporation

| Type | Access |
|------|--------|
| String | R/W |

The corporation name that the user has entered in the Identity preferences panel.

<a id="33868"></a>
<a id="email"></a>
<a id="id689"></a>
#### email

| Type | Access |
|------|--------|
| String | R/W |

The email address that the user has entered in the Identity preferences panel.

<a id="98507"></a>
<a id="loginname"></a>
<a id="id690"></a>
#### loginName

| Type | Access |
|------|--------|
| String | R |

The login name as registered by the operating system.

<a id="95607"></a>
<a id="id691"></a>
<a id="id692"></a>
#### name

| Type | Access |
|------|--------|
| String | R/W |

The user name that the user entered in the Identity preferences panel.

Example: The following can be executed in the console, or, perhaps, a folder-level JavaScript.

```
console.println("Your name is " + identity.name);
console.println("Your e-mail is " + identity.email);
```

<a id="95590"></a>
<a id="index"></a>
<a id="id693"></a>
## Index

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

An object that represents a Catalog-generated index. It is non-creatable and returned by various methods of the `search` object and `catalog` object. You use this object to perform various indexing operations using Catalog. You can find the status of the index with a search.

<a id="index-properties"></a>
<a id="id694"></a>
### Index properties

<a id="32844"></a>
<a id="available"></a>
<a id="id695"></a>
#### available

| Type | Access |
|------|--------|
| Boolean | R |

Specifies whether the index is available for selection and searching. An index may be unavailable if a network connection is down or a CD-ROM is not inserted, or if the index administrator has brought the index down for maintenance purposes.

<a id="21497"></a>
<a id="id696"></a>
<a id="id697"></a>
#### name

| Type | Access |
|------|--------|
| String | R |

The name of the index as specified by the index administrator at indexing time.

See `search.` indexes, which returns an array of the Index objects currently accessed by the search engine.

Example: This example enumerates all of the indexes and writes their names to the console.

```
for (var i = 0; i < search.indexes.length; i++) {
    console.println("Index[" + i + "] = " + search.indexes[i].name);
}
```

<a id="46342"></a>
<a id="id698"></a>
<a id="id699"></a>
#### path

| Type | Access |
|------|--------|
| String | R |

The device-dependent path where the index resides. See the [PDF Reference](https://adobe.com/go/pdfreference) for exact syntax of the path.

<a id="35848"></a>
<a id="selected"></a>
<a id="id701"></a>
#### selected

| Type | Access |
|------|--------|
| Boolean | R/W |

Specifies whether the index participates in the search. If `true`, the index is searched as part of the query. If `false` it is not searched. Setting or unsetting this property is equivalent to checking the selection status in the index list dialog box.

<a id="index-methods"></a>
<a id="id702"></a>
### Index methods

<a id="15721"></a>
<a id="build"></a>
<a id="id703"></a>
#### build

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Acrobat Pro only |

Builds the index associated with the Index object using the Catalog plug-in. This method does not build a new index.

The index is built at the same location as the index file. If the index already exists, the included directories are scanned again for changes and the index is updated. If the index does not exist, a new index can be defined and built through the user interface.

If Catalog is idle, the index build is started immediately; otherwise, it gets queued with Catalog.

> **Note**
>
> (Acrobat 7.0) This method can only be executed during a batch or console event. See priv. The event object contains a discussion of JavaScript events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cExpr` | (optional) An expression to be evaluated after the build operation on the index is complete. The default is no expression. See the [PDF Reference](https://adobe.com/go/pdfreference) for more details. |
| `bRebuildAll` | (optional) If `true`, a clean build is performed. The index is first deleted and then built. The default is `false`. |

**Returns**

A `CatalogJob` object that can be used to check the job parameters and status.

Example:

```
/* Building an index */
if (typeof catalog != "undefined")  {
    var idx = catalog.getIndex("/c/mydocuments/index.pdx");
    var job = idx.build("Done()", true);
    console.println("Status : ", job.status);
}
```

<a id="48288"></a>
<a id="link"></a>
<a id="id705"></a>
## Link

This object is used to set and get the properties and to set the JavaScript action of a link.

Link objects can be obtained from the Doc methods `addLink` or `getLinks`. (See also removeLinks.)

<a id="link-properties"></a>
<a id="id706"></a>
### Link properties

<a id="38599"></a>
<a id="bordercolor"></a>
<a id="id707"></a>
#### borderColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | Yes | Not available in Reader | Array | R/W |

The border color of a Link object. See Color arrays for information on defining color arrays and how colors are used with this property.

<a id="89645"></a>
<a id="borderwidth"></a>
<a id="id708"></a>
#### borderWidth

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | Not available in Reader | Integer | R/W |

The border width of the Link object.

<a id="41034"></a>
<a id="highlightmode"></a>
<a id="id709"></a>
#### highlightMode

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | Not available in Reader | String | R/W |

The visual effect to be used when the mouse button is pressed or held down inside an active area of a link. The valid values are:

```
None
Invert
Outline
Push
```

The default is `Invert`.

<a id="29424"></a>
<a id="id710"></a>
<a id="id711"></a>
#### rect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | Not available in Reader | Array | R/W |

The rectangle in which the link is located on the page. Contains an array of four numbers, the coordinates in rotated user space of the bounding rectangle, listed in the following order: upper-left *x*, upper-left *y*, lower-right *x* and lower-right *y*.

<a id="link-methods"></a>
<a id="id712"></a>
### Link methods

<a id="91831"></a>
<a id="id713"></a>
<a id="id714"></a>
#### setAction

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | D | No | Not available in Reader |

Sets the specified JavaScript action for the MouseUp trigger for the Link object.

> **Note**
>
> This method will overwrite any action already defined for this link.

**Parameters**

| Property | Description |
|----------|-------------|
| `cScript` | The JavaScript action to use. |

<a id="86741"></a>
<a id="monitor"></a>
<a id="id715"></a>
## Monitor

A Monitor object represents an individual display monitor. A Monitor object can be obtained from `app.monitors`, which returns an array of all monitors connected to the system. `app.monitors` is a `Monitors` object so the methods of the Monitors object can be used to select or filter out monitors from a multiple monitor system based on different criteria. See the Monitors `object` for details.

The Monitor object and the `Monitors` object are used in the MediaSettings `monitor` property.

<a id="monitor-properties"></a>
<a id="id716"></a>
### Monitor properties

<a id="17958"></a>
<a id="colordepth"></a>
<a id="id717"></a>
#### colorDepth

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Number | R |

The color depth of the monitor; that is, the number of bits per pixel.

<a id="32631"></a>
Example: Get the primary monitor and check its color depth. The `Monitors.primary` method is use to select the primary monitor.

```
var monitors = app.monitors.primary();
console.println( "Color depth of primary monitor is "

     + monitors[0].colorDepth );
```

<a id="30012"></a>
<a id="isprimary"></a>
<a id="id718"></a>
#### isPrimary

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R |

A Boolean value that is `true` for the primary monitor, `false` for all other monitors.

<a id="24432"></a>
Example: Get the widest monitor and determine if it is the primary monitor.

```
var monitors = app.monitors.widest();
var isIsNot = (monitors[0].isPrimary) ? "is" : "is not";
console.println("The widest monitor "+isIsNot+" the primary monitor.");
```

<a id="62397"></a>
<a id="id719"></a>
<a id="id720"></a>
#### rect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Rectangle | R |

A rectangle specifying the boundaries of the monitor in virtual desktop coordinates:

- The origin of the virtual desktop is the top left corner of the primary monitor. Therefore, the primary monitor’s bounds are always in the form \[ 0, 0, right, bottom \].
- Secondary monitors may have positive or negative values in their bounds arrays, depending on where they are positioned relative to the primary monitor.

<a id="48528"></a>
<a id="workrect"></a>
<a id="id721"></a>
#### workRect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Rectangle | R |

A rectangle representing a monitor’s workspace boundaries in virtual desktop coordinates. See rect for information about these coordinates.

The workspace is the area of a monitor that is normally used for applications, omitting any items such as docked toolbars or taskbars. For example, running Windows on a single 800x600 display, `rect` is \[ 0, 0, 800, 600 \]. With a standard Windows taskbar 30 pixels high and always visible at the bottom of the screen, `workRect` is \[ 0, 0, 800, 570 \].

<a id="57963"></a>
<a id="id722"></a>
<a id="id723"></a>
## Monitors

A Monitors object is equivalent to a read-only array of `Monitor` objects, each one representing a single monitor. Elements can be accessed using the usual array notation and the `length` property.

The `app.monitors` property returns a Monitors object that includes every monitor connected to the user’s system. JavaScript code can loop through this array to get information about the available monitors and select one for a full screen or pop-up media player.

> **Note**
>
> The Monitors object returned by `app.monitors` is unsorted (the monitors are not listed in any particular order).

The Monitors object has a number of filter methods that select one or more monitors based on various criteria. All of the monitor selection options provided in the PDF file format are implemented as calls to these filter methods.

None of the filter methods modify the original Monitors object. They each return a new Monitors object, which normally contains one or more Monitor objects. If a single monitor matches the filtering criterion better than any other, the result Monitors object contains that monitor. If more than one monitor satisfies the filtering criterion equally (for example, for the `bestColor` method, if more than one monitor has the same greatest color depth), the result contains all of those monitors.

Several of the filter methods have an optional minimum or required parameter. If this parameter is specified and no monitor meets that minimum requirement, the result Monitors object is empty. Otherwise, if the original Monitors object was not empty, the result always contains at least one monitor.

Wherever a filter method refers to height, width, or area, the dimensions are in pixels.

Example:

```
var monitors = app.monitors;
for ( var i = 0; i< monitors.length; i++)
console.println("monitors["+i+"].colorDepth = "+monitors[i].colorDepth);
```

`Monitors.length` contains the number of elements in the Monitors object. For the Monitors object returned by `app.monitors`, this is the number of monitors in the user’s system. For a Monitors object returned by one of the filter methods, this number may be smaller.

<a id="monitors-methods"></a>
<a id="id724"></a>
### Monitors methods

<a id="59721"></a>
<a id="bestcolor"></a>
<a id="id725"></a>
#### bestColor

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered to include the monitor or monitors with the greatest color depth.

If `nMinColor` is specified, returns an empty Monitors array if the best color depth is less than `nMinColor`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nMinColor` | (optional) The minimal color depth required for the monitor. |

**Returns**

A `Monitors` object

Example:

```
var monitors = app.monitors.bestColor(32);
if (monitors.length == 0 )
    console.println("Cannot find the required monitor.");
else
    console.println("Found at least one monitor.");
```

<a id="85937"></a>
<a id="bestfit"></a>
<a id="id726"></a>
#### bestFit

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered to include only the smallest monitor or monitors with at least the specified `nWidth` and `nHeight` in pixels.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nWidth` | Minimum width of the best fit monitor. |
| `nHeight` | Minimum height of the best fit monitor. |
| `bRequire` | (optional) Specifies what to return if no monitors have at least the specified width and height. If `true`, the method returns an empty Monitors array. If `false` or omitted, a Monitors array containing the largest monitor or monitors is returned. |

**Returns**

A `Monitors` object

<a id="31310"></a>
<a id="desktop"></a>
<a id="id727"></a>
#### desktop

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Creates a new `Monitors` object containing one `Monitor` object that represents the entire virtual desktop. The `rect` property is the union of every `rect` in the original Monitors object, the `workRect` property is the union of every `workRect` in the original Monitors object, and `colorDepth` is the minimum `colorDepth` value found in the original Monitors object.

**Returns**

A `Monitors` object

> **Note**
>
> The `desktop` method is normally called directly on a Monitors object returned by `app.monitors`. If that Monitors object is first filtered by any of its other methods, the `desktop` method does the same calculations listed above with that subset of the monitors.

<a id="17611"></a>
<a id="document"></a>
<a id="id728"></a>
#### document

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Returns a copy of the `Monitors` object, filtered to include the monitor or monitors that display the greatest amount of the document, as specified by the Doc parameter `doc`.

If the document does not appear on any of the monitors in the original Monitors object, the method returns an empty Monitors array if `bRequire` is `true` or a Monitors array containing at least one arbitrarily chosen monitor from the original array if `bRequire` is `false` or omitted.

**Parameters**

| Property | Description |
|----------|-------------|
| `doc` | The Doc of the document |
| `bRequire` | (optional) A Boolean value. See the description above. |

**Returns**

A `Monitors` object

<a id="60526"></a>
<a id="filter"></a>
<a id="id729"></a>
#### filter

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered by calling a ranker function for each monitor in the list. The ranker function takes a Monitor parameter and returns a numeric rank. The return value from `filter` is a Monitors array containing the monitors that had the highest rank (either a single monitor, or more than one if there was a tie).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `fnRanker` | A (ranker) function that takes a Monitor parameter and returns a numeric rank |
| `nMinRank` | (optional) If `nMinRank` is undefined, `filter` always includes at least one monitor from the original list (unless the original list was empty). If `nMinRank` is specified, `filter` returns an empty Monitors array if no monitors had at least that rank according to the ranker function. |

**Returns**

A `Monitors` object

> **Note**
>
> Most of the other Monitors filtering functions are implemented as `filter` calls.

Example: This script implements `Monitors.bestColor( minColor)`. It returns a `Monitors` object containing the monitor or monitors that have the greatest color depth. If `minColor` is specified, returns an empty Monitors array if the best color depth is less than `minColor`.

```
bestColor: function( minColor )
{
    return this.filter(
        function( m ) { return m.colorDepth; }, minColor );
}
```

<a id="99555"></a>
<a id="largest"></a>
<a id="id730"></a>
#### largest

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered to include the monitor or monitors with the greatest area in pixels.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nMinArea` | (optional) If the optional parameter `nMinArea`, a number, is specified, `largest()` returns an empty Monitors array if that greatest area is less than that value. |

**Returns**

A `Monitors` object

<a id="73436"></a>
<a id="leastoverlap"></a>
<a id="id731"></a>
#### leastOverlap

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered to include the monitor or monitors that contain the smallest amount of the rectangle, as specified by the `rect` parameter.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `rect` | A rectangle, an array of four numbers in screen coordinates. |
| `maxOverlapArea` | (optional) If `maxOverlapArea` is specified, the result Monitors array contains only those monitors that contain at least that much area of the rectangle, or an empty Monitors array if no monitors contain that much area of the rectangle. |

**Returns**

A `Monitors` object

<a id="36907"></a>
<a id="mostoverlap"></a>
<a id="id732"></a>
#### mostOverlap

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered to include the monitor or monitors that contain the largest amount of the rectangle, as specified by the `rect` parameter.

If there is no monitor with at least that much overlapping area, the method returns an empty Monitors array if `minOverlapArea` is specified, or a Monitors array containing at least one arbitrarily chosen monitor from the original array if `minOverlapArea` is omitted.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `rect` | A rectangle, an array of four numbers in screen coordinates. |
| `minOverlapArea` | (optional) A Boolean value; see description above. |

**Returns**

A `Monitors` object

<a id="74274"></a>
<a id="nondocument"></a>
<a id="id733"></a>
#### nonDocument

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered to include the monitor or monitors that display none of, or the least amount of, the document.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `doc` | The Doc of the target document |
| `bRequire` | (optional) `bRequire` is a Boolean value that determines the return value when there is no monitor that is completely clear of the document. If `true`, `nonDocument` returns an empty, or if false or omitted, `nonDocument` returns a Monitors array containing at least one arbitrarily chosen monitor from the original Monitors array. |

**Returns**

A `Monitors` object

<a id="20098"></a>
<a id="primary"></a>
<a id="id734"></a>
#### primary

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered by removing all secondary monitors, leaving only the primary monitor if it was present in the original list.

If the primary monitor was not present in the original list, returns a Monitors array containing at least one arbitrarily chosen monitor from the original list.

**Returns**

A `Monitors` object

<a id="27587"></a>
Example: Get the primary monitor and check its color depth.

```
var monitors = app.monitors.primary();
// Recall that each element in a monitors object is a monitor object
// This code uses monitor.colorDepth
console.println( "Color depth of primary monitor is "

     + monitors[0].colorDepth );
```

<a id="90658"></a>
<a id="secondary"></a>
<a id="id735"></a>
#### secondary

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered by removing the primary monitor, returning only secondary monitors.

If the original `Monitors` object contained only the primary monitor and no secondary monitors, returns the original list.

**Returns**

A `Monitors` object

<a id="32009"></a>
<a id="select"></a>
<a id="id736"></a>
#### select

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered according `nMonitor`, a monitor selection value as used in PDF and enumerated in `app.media.monitorType`.

The `doc` is required when `nMonitor` is `app.media.monitorType.document` or `app.media.monitorType.nonDocument` and ignored for all other `nMonitor` values.

These selection values correspond directly to the various Monitors filter methods. `select` calls the corresponding filter method and then, in most cases, also filters with `primary` as a tie-breaker in case more than one monitor matches the main filter.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nMonitor` | The monitor type, a number from `app.media.monitorType`. |
| `doc` | A Doc. The parameter is required if `nMonitor` is either `app.media.monitorType.document` or `app.media.monitorType.nonDocument`, ignored otherwise. |

**Returns**

A `Monitors` object.

Example: These two equivalent methods are for filtering monitors.

```
settings.monitor =
app.monitors().select( app.media.monitorType.document, doc );
settings.monitor = app.monitors().document(doc).primary();
```

<a id="30414"></a>
<a id="tallest"></a>
<a id="id737"></a>
#### tallest

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered to include only the monitor or monitors with the greatest height in pixels.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nMinHeight` | (optional) If `nMinHeight` is specified and no monitor has at least that height, the return value is an empty Monitors array. |

**Returns**

A `Monitors` object

<a id="46128"></a>
<a id="widest"></a>
<a id="id738"></a>
#### widest

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the `Monitors` object, filtered to include only the monitor or monitors with the greatest width in pixels.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nMinWidth` | (optional) If nMinWidth is specified and no monitor has at least that width, the return value is an empty Monitors array. |

**Returns**

A `Monitors` object

<a id="78835"></a>
<a id="net"></a>
<a id="id739"></a>
## Net

The `Net` object allows for the discovery and access to networking services through a variety of protocols.

The `Net` object forms a namespace for the networking services that currently exist in the global namespace (SOAP). The existing objects will be maintained for backwards-compatibility however any new services should use the new namespace.

<a id="83901"></a>
<a id="net-properties"></a>
<a id="id740"></a>
### Net properties

<a id="63722"></a>
<a id="soap"></a>
<a id="id741"></a>
#### SOAP

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | Object | R |

The `Net.SOAP` object allows for communication with network services that use the SOAP Messaging Protocol. The `Net.SOAP` object has one property and three method. See the referenced link for full documentation.

| Name | Short Description |
|------|-------------------|
| Net.SOAP properties |  |
| wireDump | If `true`, synchronous SOAP requests will cause the XML Request and Response to be dumped to the JavaScript Console. This is useful for debugging SOAP problems. |
| Net.SOAP methods |  |
| connect | Converts the URL of a WSDL document to a JavaScript object with callable methods corresponding to the web service. |
| request | Initiates a remote procedure call (RPC) or sends an XML message to a SOAP HTTP endpoint. The method either waits for the endpoint to reply (synchronous processing) or calls a method on the notification object (asynchronous processing). |
| response | Initiates a remote procedure call (RPC) or sends an XML message to a SOAP HTTP endpoint without waiting for a reply. |

<a id="17451"></a>
<a id="discovery"></a>
<a id="id742"></a>
#### Discovery

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | Object | R |

The `Discovery` object allows for the dynamic discovery of network services. The `Net.Discovery` object has two methods. See the referenced link for full documentation.

| Net.Discovery method | Short Description |
|----------------------|-------------------|
| queryServices | Locates network services that have published themselves using DNS Service Discovery (DNS-SD). |
| resolveService | Allows a service name to be bound to a network address and port in order for a connection to be made. |

<a id="85823"></a>
<a id="http"></a>
<a id="id743"></a>
#### HTTP

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | Object | R |

The `Net.HTTP` object allows access to web services that use HTTP. These methods allow communication with a wider variety of services than the `Net.SOAP` object. The `HTTP` object can be used to implement any messaging protocol that utilizes HTTP, for example, WebDAV or the ATOM Publishing Protocol.

See [Net.HTTP](./js-api-acrojs.md#37414) for full documentation of the methods of the `HTTP` object.

<a id="24131"></a>
<a id="net-methods"></a>
<a id="id744"></a>
### Net methods

The `Net` object has three methods. See the referenced link for full documentation.

| Net method | Short Description |
|------------|-------------------|
| streamDecode | Allows a stream object to be decoded with the specified encoding type. |
| streamDigest | Allows a stream object to be digested with the specified encoding type. |
| streamEncode | Encodes a stream object. |

<a id="37414"></a>
<a id="net-http"></a>
<a id="id745"></a>
## Net.HTTP

The `Net.HTTP` object allows access to web services that use HTTP. These methods allow communication with a wider variety of services than the `Net.SOAP` object. The `HTTP` object can be used to implement any messaging protocol that utilizes HTTP, for example, WebDAV or the ATOM Publishing Protocol.

<a id="net-http-methods"></a>
<a id="id746"></a>
### Net.HTTP methods

<a id="99486"></a>
<a id="request"></a>
<a id="id747"></a>
#### request

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 8.0 | No | Yes | F |

The `request` method asynchronously invokes an HTTP Web Service. This method allows connecting to a wider set of web services than the `Net.SOAP.request` (`SOAP.request`) method and with finer control over the HTTP method, headers and / or body. This method allows the creation of more complicated networking protocols such as WebDAV or the Atom Publishing Protocol.

> **Note**
>
> This method can only be made outside the context of a document (for example, in a folder level JavaScript).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cVerb` | A string that specifies the HTTP verb to use. The verb must be one of the following (Messaging protocol > Parameter value): * HTTP (RFC 1945, 2616): GET, POST, PUT, DELETE, OPTIONS, HEAD * WebDAV (RFC 2518):     PROPFIND, PROPPATCH, MKCOL, LOCK, UNLOCK, COPY, MOVE, ACL, SEARCH * WebDAV Versioning Extensions (RFC 3253):       CHECKIN, CHECKOUT, UNCHECKOUT, MERGE, VERSION-CONTROL, REPORT, KWORKSPACE, UPDATE, LABEL, MERGE, MKACTIVITY * CalDAV Calendaring Extensions: MKCALENDAR |
| `cURL` | A string that specifies the network endpoint location of the web service to connect to. The scheme of the URL *must* be either HTTP or HTTPS. |
| `aHeaders` | (optional) An array that specifies HTTP headers to be sent with the request. Some headers such as Content-length cannot be set explicitly. Each element in the array is an object describing the header with the following properties: * `name`: The name of the header to use, this must be a valid HTTP Header name. * `value`: The value for the HTTP header, this must be a valid HTTP Header value string. |
| `oRequest` | (optional) A Stream object that specifies the request body of the method. No encoding of the message body is done prior to sending it. |
| `oHandler` | (optional) An object that handles the response from the service. The `oHandler` object will have the response method invoked with the following parameters: * `oRequest`: The response body as a stream object on success. * `cURL`: The request URL that was used when this request was invoked. * `oException`: An exception object if the method was not successful. The exception object has the following properties: * `error`: The HTTP status code that was returned. * `msg`: An error message associated with the failure. * `aHeaders`: An array of response headers returned from the server. See the aHeaders parameter of the Net.HTTP.request method for a description of the format. |
| `oAuthenticate` | (optional) An object that specifies how to handle HTTP authentication or specifies credentials to use. The default is to present a user interface to the user to handle HTTP authentication challenges for BASIC and DIGEST authentication modes. The `oAuthenticate` object can have the following properties: * `Username`: A string containing the username to use for authentication. * `Password`: A string containing the authentication credential to use. * `UsePlatformAuth`: A Boolean indicating that platform authentication should be used. If platform authentication is enabled, the Username and Password are ignored and the underlying platform networking code is used. This may cause an authentication UI to be shown to the user and/or the credentials of the currently logged in user to be used. The default is false and is only supported on the Windows platform. |

**Exceptions**

The method throws an exception if the URL is invalid or the same, origin requirement is not satisfied.

Example: Create a collection at the URL specified.

```
CreateWebDAVCollection = function(cURL)
{
   var params =
   {
       cVerb: "MKCOL",
       cURL: cURL,
       oHandler:
       {
           response: function(msg, uri, e)
               {
                   // HTTP 405 - Can't MKCOL if it exists!
                   if(e != undefined && e.error != 405) {
                       app.alert("Failed to MKCOL: "+ e);
                   } else app.alert("Created collection");
               }
           }
       };
       Net.HTTP.request(params);
} // CreateWebDAVCollection
```

<a id="66402"></a>
<a id="ocg"></a>
<a id="id748"></a>
## OCG

An OCG object represents an *optional content group* in a PDF file. Content in the file can belong to one or more optional content groups. Content belonging to one or more OCGs is referred to as optional content and its visibility is determined by the states (ON or OFF) of the OCGs to which it belongs. In the simplest case, optional content belongs to a single OCG, with the content being visible when the OCG is on and hidden when the OCG is off. More advanced visibility behavior can be achieved by using multiple OCGs and different visibility mappings.

Use the Doc `getOCGs` method to get an array of OCG objects for a PDF document.

The Doc methods `addWatermarkFromFile` and `addWatermarkFromText` add watermarks in an OCG.

See the [PDF Reference](https://adobe.com/go/pdfreference) for additional details on optional content groups.

<a id="ocg-properties"></a>
<a id="id750"></a>
### OCG properties

<a id="78529"></a>
<a id="id751"></a>
<a id="id752"></a>
#### constants

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Each instance of an OCG object inherits this property, which is a wrapper object for holding various constant values.

<a id="68717"></a>
**intents Object**

An OCG’s intent array can contain arbitrary strings, but those contained in this object are the only ones recognized by Acrobat.

| Property | Description |
|----------|-------------|
| `design` | Designates a design intent in an OCG object. |
| `view` | Designates a view intent in an OCG object. |

<a id="73206"></a>
**states Object**

The `states` object is used to set the initial state of the OCG (see initState).

| Property | Description |
|----------|-------------|
| `on` | Designates an OCG state of ON. |
| `off` | Designates an OCG state of OFF. |

<a id="34918"></a>
<a id="initstate"></a>
<a id="id753"></a>
#### initState

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | All | Boolean | R/W (Adobe Reader: R only) |

This property is used to determine whether this OCG is on or off by default. See the states Object for possible values.

Example: Set an initial state of an OCG to off.

```
var ocgs = this.getOCGs();
ocgs[0].initState.constants.states.off;
```

<a id="16397"></a>
<a id="locked"></a>
<a id="id754"></a>
#### locked

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | D | No | All | Boolean | R/W (Adobe Reader: R only) |

This property is used to determine whether this OCG is locked. If an OCG is locked, its on/off state cannot be toggled through the UI.

<a id="90593"></a>
<a id="id755"></a>
<a id="id756"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | All | String | R/W (Adobe Reader: R only) |

The text string seen in the UI for this OCG. It can be used to identify OCGs, although it is not necessarily unique.

> **Note**
>
> In Acrobat 6.0, the `name` is read-only; for Acrobat 7.0, it is read/write.

Example: A function that toggle all Watermark OCGs.

```
function ToggleWatermark(doc)
{
    var ocgArray = doc.getOCGs();
    for (var i=0; i < ocgArray.length; i++) {
        if (ocgArray[i].name == "Watermark") {
            ocgArray[i].state = !ocgArray[i].state;
        }
    }
}
```

<a id="24633"></a>
<a id="id757"></a>
<a id="id758"></a>
#### state

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Represents the current on/off state of this OCG.

Changing the state of an OCG does not dirty the document, the OCGs revert to their initial state when the document is loaded again.

Example: Turn on all the OCGs in the given document.

```
function TurnOnOCGsForDoc(doc)
{
    var ocgArray = doc.getOCGs();
    for (var i=0; i < ocgArray.length; i++)
        ocgArray[i].state = true;
}
```

<a id="ocg-methods"></a>
<a id="id759"></a>
### OCG methods

<a id="71160"></a>
<a id="getintent"></a>
<a id="id760"></a>
#### getIntent

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

**Returns** this OCG’s intent array.

An OCG will affect the visibility of content only if it has `onstants.intents.view` as an intent.

See also setIntent and the intents Object.

**Returns**

An array of strings. See constants.intents for possible values.

<a id="39535"></a>
<a id="id761"></a>
<a id="id762"></a>
#### setAction

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Not available in Reader |

Registers a JavaScript expression to be evaluated after every state change for this OCG.

Setting an action for an OCG does not dirty the document, therefore, the assignment of action must be made when the document is first opened, as document level script, or dynamically through user interaction.

> **Note**
>
> This method will overwrite any action already defined for this OCG.

**Parameters**

| Property | Description |
|----------|-------------|
| `cExpr` | The expression to be evaluated after the OCG state changes. |

Example: The function below is used to assign a beep sound to an OCG passed to it. The script that follows the function definition assigns a beeping action to the first OCG, as listed in the array returned by the `getOCGs` method.

```
/* Beep when the given ocg is changed */
function BeepOnChange(ocg)
{
    ocg.setAction("app.beep()");
}
var ocgs = this.getOCGs();
BeepOnChange(ocgs[0]);
```

<a id="15064"></a>
<a id="setintent"></a>
<a id="id763"></a>
#### setIntent

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | D | No | Not available in Reader |

Sets this OCG’s intent array. An OCG should only affect the visibility of content if this array contains constants.intents.view. See the intents Object for possible values.

See also getIntent and the intents Object.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `aIntentArray` | An array of strings to be used as this OCG’s intent array. |

Example: Set the intent of all OCGs in the document to both View and Design.

```
var ocgs = this.getOCGs();
for (i=0; i < ocgs.length; i++) {
    ocgs[i].setIntent( [ocgs[i].constants.intents.view,
    ocgs[i].constants.intents.design]);
}
```

<a id="58967"></a>
PlayerInfo

A PlayerInfo object represents a media player that is available for media playback. The `app.media.getPlayers` method returns a `PlayerInfoList` object, which is a collection of PlayerInfo objects.

<a id="playerinfo-properties"></a>
<a id="id764"></a>
### PlayerInfo properties

<a id="26289"></a>
<a id="id"></a>
<a id="id765"></a>
#### id

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

Represents a media player plug-in and associated media player. This string is not localized and is not intended for display to the user. This string may be used in the `MediaPlayer.settings.players` array when creating a MediaPlayer, and it is also found in the `MediaPlayer.id property` after opening a player.

Example: List player information for all media players that play “video/mpeg”.

```
var playerInfoList = app.media.getPlayers("video/mpeg");

for ( var i=0; i < playerInfoList.length; i++) {
    console.println("id: " + playerInfoList[i].id)
    console.println("name: " + playerInfoList[i].name)
    console.println("version: " + playerInfoList[i].version)
}
```

<a id="22221"></a>
<a id="mimetypes"></a>
<a id="id766"></a>
#### mimeTypes

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array of String | R |

An array of strings listing the MIME types that this media player supports.

Example:

```
var qtinfo = app.media.getPlayers().select({id: /quicktime/i })[0];
console.println( qtinfo.mimeTypes );
```

<a id="49721"></a>
<a id="id767"></a>
<a id="id768"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

The name of the media player. This string is localized according to the current language as found in app.language. It is suitable for display in list boxes and the like, but not for direct comparisons in JavaScript code.

<a id="24800"></a>
<a id="id769"></a>
<a id="id770"></a>
#### version

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

A string containing the version number of the media player. For most players, it is the version number of the underlying media player that is installed on the user’s system. This string is in dotted decimal format, for example, 7.4.030.1170.

<a id="playerinfo-methods"></a>
<a id="id771"></a>
### PlayerInfo methods

<a id="76833"></a>
<a id="canplay"></a>
<a id="id772"></a>
#### canPlay

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Checks to see if the media player can be used for playback, taking the user’s security settings into account.

If the parameter `bRejectPlayerPrompt` is `true`, the method returns `false` if using this player would result in a security prompt. Otherwise the method returns `true` if playback is allowed either with or without a security prompt. (This method itself never triggers a security prompt, but a later attempt to create a media player may.)

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oDoc` | A Doc |
| `bRejectPlayerPrompt` | A Boolean value whose default is `false`. If `true`, the method returns `false` if using this player would result in a security prompt. If `false`, the method returns `true` if playback is allowed either with or without a security prompt. |

**Returns**

Boolean

<a id="82266"></a>
<a id="canusedata"></a>
<a id="id773"></a>
#### canUseData

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Tells whether the player can use the specified data, as passed by its parameter `oData`, for playback. Returns `true` if the data can be used for playback and `false` otherwise.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oData` | A MediaData object (see `MediaSettings.data` for a description of this object). This object is obtained in several ways, from `app.media.getAltTextData`, `app.media.getURLData`, or indirectly by `Rendition.getPlaySettings`. |

**Returns**

Boolean

<a id="54413"></a>
<a id="honors"></a>
<a id="id774"></a>
#### honors

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Asks a player plug-in whether it can honor all of the settings, methods, and events listed in the `args` parameter. The answer is not guaranteed to be correct, but is a best guess without opening a media player. For example, if `args.URL` is provided, the scheme (such as `"http://"`) is checked, but `honors` does not try to actually open the URL.

> **Note**
>
> Compatibility: `honors` is supported only on Acrobat 7.0 and above. The Acrobat SDK provides JavaScript source code that can be copied into a PDF to provide compatibility with both Acrobat 6.0 and Acrobat 7.0. This code uses hard-coded tests for Acrobat 6.0 and calls `honors` on newer versions of Acrobat. See the playerHonors Function for details.

- `honors` and the HonorsArgs object are similar to the MH (“must honor”) entries in the PDF format, some of which can be set in the Playback Requirements panel of the Rendition Settings for a multimedia rendition. The `honors` method provides a way to choose a player that meets playback requirements dynamically in JavaScript code instead of statically in the PDF file.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `args` | The `HonorsArgs` object to be tested. The `HonorsArgs` object is very similar to the parameter, `PlayerArgs Object`, used by the `app.media.openPlayer` method. In fact, any PlayerArgs object can be used as an HonorsArgs. HonorsArgs also allows a few other options that are used only with `honors`. |

**Returns**

A Boolean value which is `true` if the player plug-in can honor everything in the `args` object.

<a id="26457"></a>
Example: Play a media clip using a player that supports specific features.

```
function playWithRequirements( args )
{
    var plugins = app.media.getPlayers( args.mimeType )
    if( plugins )
    {
        for (var plugin in plugins)
        {
            if( plugin.honors(args) )
            {
                args.players = [plugin];
                return app.media.openPlayer( args );
            }
        }
    }
}
```

Play using a media player that has these capabilities for an AVI file on an http URL: It can turn off autoplay, supports the pause method, the seek method and startAt setting using a marker+time offset, and supports the Ready and Close events.

```
playWithRequirements({
    mimeType: 'video/avi',
    URL: 'http://www.example.com/bar.avi',
    settings:
    {
        autoPlay: false,
        startAt: { marker: 'test', time: 1 },
    },
    methods:
    {
        pause:[],
        seek[ { marker: 'test', time: 1 } ],
    },
    events:
    {
        afterReady: doAfterReady( e ),
        onClose: doOnClose( e ),
    },
});
```

<a id="90332"></a>
**HonorsArgs object**

The HonorsArgs object lists settings, methods, and events that are used in a call to the `honors` method of the `PlayerInfo` object or the `playerHonors` function. In this discussion, `PlayerInfo.honors` refers to both.

Any `PlayersArgs` object (as used in a call to `app.media.openPlayer`) may be used as an HonorsArgs object, or an HonorsArgs object can be created to be used in a `PlayerInfo.honors` call.

If the same object is used in `app.media.openPlayer` and `PlayerInfo.honors`, be aware that the two functions interpret unknown `args` differently. `app.media.openPlayer` ignores settings or events that it does not know about, but `PlayerInfo.honors` returns `false` if there are any settings, methods, or events it does not recognize.

For example, `{` `settings:` `{` `upsideDown: true` `}` `}` would be allowed in an `app.media.openPlayer` call. There is no such setting as “upsideDown”, so the setting is ignored. But in a call to `PlayerInfo.honors`, this unknown setting returns `false`.

Below is a complete list of the properties allowed in the HonorsArgs object. This illustration is loosely in the form of a JavaScript object literal, but it shows the type or description of each property instead of an actual property value:

```
args =
{
    mimeType: string,
    URL: string,
    settings:
    {
        autoPlay: boolean,
        baseURL: string,
        bgColor: Acrobat color array,
        duration: number,
        endAt: MediaOffset,
        layout: number,
        palindrome: boolean,
        rate: number,
        repeat: number,
        showUI: boolean,
        startAt: MediaOffset,
        visible: boolean,
        volume: number,
    },
    methods:
    {
        pause: [],
        play: [],
        seek: [ MediaOffset ],
        stop: [],
        where: [],
    },
    events:
    {
        Done: anything, onDone: anything, afterDone: anything,
        Error: anything, onError: anything, afterError: anything,
        Escape: anything, onEscape: anything, afterEscape: anything,
        Pause: anything, onPause: anything, afterPause: anything,
        Play: anything, onPlay: anything, afterPlay: anything,
        Ready: anything, onReady: anything, afterReady: anything,
        Script: anything, onScript: anything, afterScript: anything,
        Seek: anything, onSeek: anything, afterSeek: anything,
        Status: anything, onStatus: anything, afterStatus: anything,
        Stop: anything, onStop: anything, afterStop: anything,
    },
}
```

Additional comments on the above listing.

- The `mimeType`, `URL`, and `settings` properties are identical to the corresponding properties in PlayerArgs. The `mimeType` property is required; the `honors` method does not try to determine the MIME type from the URL’s file extension. `URL` can be a real URL or a fictitious one, as long as it is in the correct URL format. See MediaSettings object for a description of these properties.
- The `methods` property lists the MediaPlayer methods that the player must support for the given MIME type. The value of each `methods` property is an array containing the arguments that would be passed into a call to that method. In Acrobat 7.0, the only player method that has any arguments is `seek`, which takes a single MediaOffset argument. See MediaPlayer object for a description of these properties.

If you use the same object as a PlayerArgs and an HonorsArgs, it can have a `methods` property, even though a PlayerArgs normally does not have that property. Anywhere a PlayerArgs is used, the unknown property is ignored.

- The `events` property lists the events that the player must support. As shown above, each event can be named with the `on` or `after` prefix or no prefix. All three mean the same thing. If a player supports a particular on event, it always supports the corresponding `after` event (because the `after` events are generated in the same way for all players). See EventListener object for a description of these properties.

The notation `anything` means literally that: in the HonorsArgs, these values are just placeholders. So, the events object from a PlayerArgs works in an HonorsArgs:

```
events:
{
    afterReady: doAfterReady( e ),
    onClose: doOnClose( e ),
},
```

Or, if you are creating an HonorsArgs, you can simplify the notation as follows:

```
events: { Ready: true, Close: true },
```

<a id="29870"></a>
**playerHonors Function**

This function is provided as JavaScript source code that can be copied into a PDF file as a document script. It performs the same tests as the `honors` method in Acrobat 7.0, but it works on Acrobat 6.0 as well.

When running on Acrobat 6.0, `playerHonors` uses hard-coded tests that match the capabilities of the media players shipped with Acrobat 6.0.

When running on Acrobat 7.0 and later, `playerHonors` calls `honors`.

**Parameters**

| Property | Description |
|----------|-------------|
| `doc` | A Doc. |
| `info` | A `PlayerInfo` object. |
| `args` | The `HonorsArgs` object to be tested. |

**Returns**

A Boolean value which is `true` if the player plug-in can honor everything in the `args` object.

Example: This example is the same as shown for the `honors` method of the `PlayerInfo` object, but using the `playerHonors` JavaScript function. This works on both Acrobat 6.0 and 7.0, provided a copy of the `playerHonors` source code is placed into the target PDF.

```
function playWithRequirements( args ) {
    var plugins = app.media.getPlayers( 'video/avi' )
    if( plugins ) {
        for (var plugin in plugins) {
            if( playerHonors( doc, plugin, args ) ) {
                args.players = [plugin];
                return app.media.openPlayer( args );
            }
        }
    }
}
```

<a id="14162"></a>
<a id="playerinfolist"></a>
<a id="id775"></a>
## PlayerInfoList

This object is equivalent to an array of `PlayerInfo` objects. The individual elements (the `PlayerInfo` objects) can be accessed using the usual array notation. The number of elements can be obtained from the `length` property.

This object is returned by the `app.media.getPlayers` method.

When a media player is created using `app.media.createPlayer`, the `settings.players` property of the `PlayerArgs` object passed to the method may contain a PlayerInfoList. The created player is restricted to those in the list.

<a id="playerinfolist-methods"></a>
<a id="id776"></a>
### PlayerInfoList methods

<a id="59419"></a>
<a id="id777"></a>
<a id="id778"></a>
#### select

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a copy of the PlayerInfoList, filtered to include only the players that match selection criteria. If no players match, an empty array is returned.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `object` | (optional) An object that contains any of the properties `id`, `name`, or `version`. The values of these properties may be strings or regular expressions. Specified properties are required to match. Omitted properties can match any player. |

**Returns**

`PlayerInfoList` object

Example 1: Use QuickTime to view the media clip.

```
var playerList = app.media.getPlayers().select({ id: /quicktime/i });
// QuickTime supports palindrome, so let's try it.
var settings = { players: playerList, palindrome: true };
var player = app.media.openPlayer({ settings: settings });
```

Example 2: Choose the Flash player by using a pattern match on its player ID.

```
var player = app.media.createPlayer();
player.settings.players = app.media.getPlayers().select({ id:/flash/i});
player.open();
```

<a id="48754"></a>
<a id="plugin"></a>
<a id="id779"></a>
## PlugIn

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This object gives access to information about the plug-in it represents. A PlugIn object is obtained using `app.plugIns`.

<a id="plugin-properties"></a>
<a id="id780"></a>
### PlugIn properties

<a id="41150"></a>
<a id="certified"></a>
<a id="id781"></a>
#### certified

If `true`, the plug-in is certified by Adobe. Certified plug-ins have undergone extensive testing to ensure that breaches in application and document security do not occur. The user can configure the viewer to only load certified plug-ins.

| Type | Access |
|------|--------|
| Boolean | R |

Example: Get the number of uncertified plug-ins.

```
var j=0; aPlugins = app.plugIns;
for (var i=0; i < aPlugins.length; i++)
    if (!aPlugins[i].certified) j++;
console.println("Report: There are "+j+" uncertified plug-ins loaded.");
```

<a id="99810"></a>
<a id="loaded"></a>
<a id="id782"></a>
#### loaded

If `true`, the plug-in was loaded.

| Type | Access |
|------|--------|
| Boolean | R |

<a id="25279"></a>
<a id="id783"></a>
<a id="id784"></a>
#### name

The name of the plug-in.

| Type | Access |
|------|--------|
| String | R |

Example: Get the number of plug-ins, and list them in the console.

```
// Get an array of PlugIn Objects
var aPlugins = app.plugIns;
// Get the number of plug-ins
var nPlugins = aPlugins.length;
// Enumerate the names of all plug-ins
for (var i = 0; i < nPlugins; i++)
    console.println("Plugin #" + i + " is " + aPlugins[i].name);
```

<a id="94716"></a>
<a id="id785"></a>
<a id="id786"></a>
#### path

The device-independent path to the plug-in.

| Type | Access |
|------|--------|
| String | R |

<a id="92542"></a>
<a id="id787"></a>
<a id="id788"></a>
#### version

The version number of the plug-in. The integer part of the version number indicates the major version, and the decimal part indicates the minor and update versions. For example, 5.11 would indicate that the plug-in has major version 5, minor version 1, and update version 1.

| Type | Access |
|------|--------|
| Number | R |

<a id="43354"></a>
<a id="printparams"></a>
<a id="id789"></a>
## PrintParams

This is a generic object that controls printing parameters that affect any document printed using JavaScript. Changing this object does not change the user preferences or make any permanent changes to the document.

In Acrobat 6.0, the Doc `print` method takes a PrintParams object as its argument. You can obtain a PrintParams object from the Doc `getPrintParams` method. The returned object can then be modified.

Many of the PrintParams properties take integer constants as values, which you can access using the `constants` property. For example:

```
// Get the printParams object of the default printer
var pp = this.getPrintParams();
// Set some properties
pp.interactive = pp.constants.interactionLevel.automatic;
// Print
this.print(pp);
```

The `constants` properties are all integers allowing read access only.

<a id="printparams-properties"></a>
<a id="id790"></a>
### PrintParams properties

<a id="39494"></a>
<a id="binaryok"></a>
<a id="id791"></a>
#### binaryOK

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

`true` if a binary channel to the printer is supported. The default is `true`.

<a id="72759"></a>
<a id="bitmapdpi"></a>
<a id="id792"></a>
#### bitmapDPI

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | Integer | R/W |

The dots per inch (DPI) to use when producing bitmaps or rasterizing transparency. The valid range is 1 to 9600. If the document protections specify a maximum printing resolution, the lower of the two values is used. The default is 300. Illegal values are treated as 300. See also gradientDPI.

<a id="75229"></a>
<a id="booklet"></a>
<a id="id793"></a>
#### booklet

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | object | R/W |

An object used to set the parameters for booklet printing. The properties of the `booklet` object are listed in the table below.

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `binding` | Integer | R/W | When printing a booklet, the `binding` property determines the paper binding direction and the page arrange order. The value of `binding` is set through the constants `bookletBindings` object, given below. The default is `Left`. |
| `duplexMode` | Integer | R/W | When printing a booklet, the `duplexMode` property determines the duplex printing mode. The value of `duplexMode` property is set through the constants `duplexMode` object, given below. The default is `BothSides`. When the output device doesn’t support automatic duplex functionality, a manual duplex can be performed by two separated printings of front and back sides. |
| `subsetFrom` | Integer | R/W | When printing a booklet, `subsetFrom` determines the first booklet sheet to be printed. Independently from the general page range selection, only a subset of the final booklet result is printed by this option.  Valid sheet numbers start from 0, which is the first sheet. The default value is 0.  The special value of -1 represents the last sheet. More generally, the negative integer -N represents the sheet that is (N-1) from the last sheet. Thus, -2 is the sheet just before the last sheet, -3 is the sheet that is 2 sheets from the last one.  See the additional note below on booklet subsetting. |
| `subsetTo` | Integer | R/W | When printing a booklet, `subsetTo` determines the last booklet sheet to be printed. Independently from the general page range selection, only a subset of the final booklet result is printed by this option.  Valid sheet numbers start from 0, but the value -1 represents the last sheet. The default value is -1.  The negative integer -N represents the sheet that is (N-1) from the last sheet. Thus, -2 is the sheet just before the last sheet, -3 is the sheet that is 2 sheets from the last one.  See the additional note below on booklet subsetting. |

The `bookletBindings` object has properties used to set the value of `booklet.binding`.

**constants.bookletBindings object**

| Property | Description |
|----------|-------------|
| `Left` | Left-side binding for Western-style left-to-right reading direction. The paper is folded on the short side. |
| `Right` | Right-side binding for text with right-to-left reading direction or Japanese-style vertical writing. The paper is folded on the short side. |
| `LeftTall` | Left-side binding for Western-style left-to-right reading direction. The paper is folded on the long side producing long and narrow pages. |
| `RightTall` | Right-side binding for text with right-to-left reading direction or Japanese-style vertical writing. The paper is folded on the long side producing long and narrow pages. |

The `bookletDuplexModes` object has properties used to set the value of `booklet.duplexMode`.

<a id="53154"></a>
**constants.bookletDuplexModes object**

| Property | Description |
|----------|-------------|
| `BothSides` | Automatically prints both sides of the paper. The selected printer must support automatic duplex printing. |
| `FrontSideOnly` | Only prints all pages that appear on the front side of the paper. Reinsert the printed pages and print again with `BacksideOnly` mode to complete a manual duplex printing. |
| `BackSideOnly` | Only prints all pages that appear on the back side of the paper. |

> **Note**
>
> (Booklet subsetting using `subsetFrom` and `subsetTo`) Since the booklet output can change by the source page range (by setting firstPage and lastPage properties of the PrintParams object), the same effect cannot be achieved easily by changing these page range properties. For example. the first (2-side) sheet of an 8-page booklet job has a page number sequence of \[8, 1, 2, 7\] while the first sheet of 16-page booklet job has a page number sequence of \[16, 1, 2, 15\]. The `subsetFrom` and `subsetTo` properties are useful for printing certain pages of a booklet document with different devices or media. A typical example would be printing the cover and the inside cover in color while rest of the document is in black and white. Another common example is printing the cover page on thicker colored paper.

**Example 1 (binding)**

Set up booklet printing for right-side binding of text, and print.

```
var pp = this.getPrintParams();
pp.pageHandling = pp.constants.handling.booklet;
pp.booklet.binding = pp.constants.bookletBindings.Right;
this.print(pp);
```

**Example 2 (duplexMode)**

Print booklet in duplex mode, printing only the front pages.

```
var pp = this.getPrintParams();
pp.pageHandling = pp.constants.handling.booklet;
pp.booklet.duplexMode = pp.constants.bookletDuplexModes.FrontSideOnly;
this.print(pp);
```

**Example 3 (subsetFrom and subsetTo)**

Set up booklet printing to print the second sheet only and print.

```
var pp = this.getPrintParams();
pp.pageHandling = pp.constants.handling.booklet;
pp.booklet.subsetFrom = 1;
pp.booklet.subsetTo = 1;
this.print(pp);
```

Set booklet printing from the second sheet to the last sheet.

```
pp.booklet.subsetFrom = 1;
pp.booklet.subsetTo = -1;
```

Set booklet printing to print last sheet only.

```
pp.booklet.subsetFrom = -1;
pp.booklet.subsetTo = -1;
```

Set booklet printing to print last sheet two sheets.

```
pp.booklet.subsetFrom = -2;
pp.booklet.subsetTo = -1;
```

Set booklet printing to print all pages except the last two.

```
pp.booklet.subsetFrom = 0;
pp.booklet.subsetTo = -3;
```

<a id="78256"></a>
<a id="colorprofile"></a>
<a id="id794"></a>
#### colorProfile

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | String | R/W |

The color profile to use. A list of available color spaces can be obtained from `printColorProfiles`. The default is “Printer/PostScript Color Management”.

<a id="12065"></a>
<a id="id795"></a>
<a id="id796"></a>
#### constants

| Version (Key) | Save-Prefs | Security | Product | Type | Accessibility |
|---------------|------------|----------|---------|------|---------------|
| 6.0 | No | No | All | object | R |

Each instance of a PrintParams object inherits this property, which is a wrapper that holds various constant values. The values are all integers allowing read access only. They are used as option values of some of the other properties of the PrintParams object, and their values are listed with the properties to which they apply.

| Constant object | Contains constant values for this property |
|-----------------|--------------------------------------------|
| `bookletBindings` | booklet |
| `bookletDuplexModes` | booklet |
| `duplexTypes` | DuplexType |
| `fontPolicies` | fontPolicy |
| `handling` | pageHandling |
| `interactionLevel` | interactive |
| `nUpPageOrders` | nUpPageOrder |
| `printContents` | printContent |
| `flagValues` | flags |
| `rasterFlagValues` | rasterFlags |
| `subsets` | pageSubset |
| `tileMarks` | tileMark |
| `usages` | usePrinterCRD  useT1Conversion |

<a id="57970"></a>
<a id="downloadfareastfonts"></a>
<a id="id797"></a>
#### downloadFarEastFonts

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

If `true` (the default), send Far East fonts to the printer if needed. Set this property to `false` if the printer has Far East fonts but incorrectly reports that it needs them.

<a id="24870"></a>
<a id="duplextype"></a>
<a id="id798"></a>
#### DuplexType

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | Integer | R/W |

Sets the printing duplex mode to simplex, duplex long edge, or duplex short edge feed. This property appears as DuplexMode under the Advanced tab of the Document Properties dialog box.

**constants.duplexTypes Object**

The duplex options are accessed through the `constants.duplexType` object. The properties of this object are listed in the table that follows.

| Property | Description |
|----------|-------------|
| Simplex | Prints on one side of the paper. |
| DuplexFlipLongEdge | Prints on both sides of the paper; the paper flips along the long edge. |
| DuplexFlipShortEdge | Prints on both sides of the paper; the paper flips along the short edge. |

The selected printer should support duplex printing, if either DuplexFlipLongEdge or DuplexFlipShortEdge is used.

Example: Set printing to duplex short edge feed and print.

```
var pp = this.getPrintParams();
pp.DuplexType = pp.constants.duplexTypes.DuplexFlipShortEdge;
this.print(pp);
```

<a id="22668"></a>
<a id="id799"></a>
<a id="id800"></a>
#### fileName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R/W |

The device-independent path for a file name to be used instead of sending the print job to the printer (Print to File). The path may be relative to the location of the current document. When printing to a file, if the interaction level (see interactive) is set to `full`, it is lowered to `automatic`.

The default value is the empty string (no file name).

> **Note**
>
> Printing to a file produces output suitable for the printer, for example, Postscript or GDI commands.

When `printerName` is an empty string and `fileName` is specified, the current document is saved as a PostScript file.

Example:

```
var pp = this.getPrintParams();
pp.fileName = "/c/print/myDoc.prn";
this.print(pp);
```

Example 2: Save the current document as a PostScript file.

```
var pp = this.getPrintParams();
pp.fileName = "/c/temp/myDoc.ps";
pp.printerName = "";
this.print(pp);
```

<a id="95550"></a>
<a id="firstpage"></a>
<a id="id801"></a>
#### firstPage

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

The first page number of the document to print. The number is 0-based. The first page of any document is 0, regardless of page number labels. The default value is 0, and values that are out of the document’s page range are treated as 0.

See also lastPage.

Example:

```
var pp = this.getPrintParams();
pp.firstPage = 0;
pp.lastPage = 9;
this.print(pp);
```

<a id="37069"></a>
<a id="flags"></a>
<a id="id802"></a>
#### flags

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

A bit field of flags to control printing. These flags can be set or cleared using bitwise operations through the `constants` `flagValues` object.

Zero or more flags can be set; unsupported flags are ignored. The flags default to those set by user preferences.

**constants.flagValues object**

The table below lists the properties of the flagValues object; unless otherwise noted, these properties are not available in Adobe Reader.

| Property | Description |
|----------|-------------|
| `applyOverPrint` | Do overprint preview when printing. Turn off if overprinting is natively supported. |
| `applySoftProofSettings` | Use the soft proofing settings before doing color management. |
| `applyWorkingColorSpaces` | Apply working color spaces when printing. |
| `emitHalftones` | Emit the halftones specified in the document. |
| `emitPostScriptXObjects` | PostScript only, do include PostScript XObjects’ content in output. |
| `emitFormsAsPSForms` | Converts Form XObjects to PS forms. The default is off. |
| `maxJP2KRes` | Use the maximum resolution of JPeg2000 images instead of the best matching resolution. |
| `setPageSize` | Enable setPageSize. Choose the paper tray by the PDF page size. Available in Adobe Reader. |
| `suppressBG` | Do not emit the BlackGeneration in the document. |
| `suppressCenter` | Do not center the page. Available in Adobe Reader. |
| `suppressCJKFontSubst` | Suppress CJK Font Substitution on Printer—does not apply when `kAVEmitFontAllFonts` is used. |
| `suppressCropClip` | Do not emit the cropbox page clip. Available in Adobe Reader. |
| `suppressRotate` | Do not rotate the page. Available in Adobe Reader. |
| `suppressTransfer` | Do not emit the transfer functions in the document. |
| `suppressUCR` | Do not emit UnderColorRemovals in the document. |
| `useTrapAnnots` | Print TrapNet and PrinterMark annotations, even if the print setting is “document only”. |
| `usePrintersMarks` | Print PrinterMark annotations, even if the print setting is “document only”. Available in Acrobat Pro only. |

Example 1: In the Output options section of the Advanced Print Setup dialog box, check the Apply Output Preview Settings check box.

```
pp = getPrintParams();
fv = pp.constants.flagValues;
// or pp.flags = fv.applySoftProofSettings;;
pp.flags = pp.flags  fv.applySoftProofSettings;
this.print(pp);
```

Example 2: Uncheck Auto-Rotate and Center (checked by default) in the Print dialog box.

```
pp = getPrintParams();
fv = pp.constants.flagValues;
pp.flags = (fv.suppressCenter  fv.suppressRotate);
this.print(pp);
```

Example 3: In the PostScript options section of the Advanced Print Setup dialog box, check the Emit Undercolor Removal/Black Generation check box.

```
pp = getPrintParams();
fv = pp.constants.flagValues;
pp.flags &= ~(fv.suppressBG  fv.suppressUCR)
this.print(pp)
```

<a id="11931"></a>
<a id="fontpolicy"></a>
<a id="id803"></a>
#### fontPolicy

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Sets the font policy. The value of the `fontpolicy` property is set through the `constants` `fontPolicies` object. The default is `pageRange`.

**constants.fontPolicies object**

| Property | Description |
|----------|-------------|
| `everyPage` | Emit needed fonts before every page and free all fonts after each page. This produces the largest, slowest print jobs, but requires the least amount of memory from the printer. |
| `jobStart` | Emit needed fonts at the beginning of the print job and free them at the end of the print job. This produces the smallest, fastest print jobs, but requires the most memory from the printer. |
| `pageRange` | (Default) Emit fonts before the first page that uses them and free them after the last page that uses them. This also produces the smallest and fastest print jobs and can use less memory. However, the print job must be printed as produced because of page ordering.  -  `pageRange` can be a good compromise between speed and memory. However, do not use it if the PostScriptcript pages will be programmatically reordered afterwards. |

<a id="64020"></a>
<a id="gradientdpi"></a>
<a id="id804"></a>
#### gradientDPI

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | Integer | R/W |

The dots per inch to use when rasterizing gradients. This value can generally be set lower than `bitmapDPI` because it affects areas to which the eye is less sensitive. It must be set from 1 to 9600. Illegal values are treated as 150. If the document protections specify a maximum printing resolution, the lower of the two values will be used. The default value is 150.

<a id="91914"></a>
<a id="interactive"></a>
<a id="id805"></a>
#### interactive

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Specifies the level of interaction between the user and the print job. The value of this property is set through the `constants` `interactionLevel` object. The default is `full`.

> **Note**
>
> (Acrobat 7.0) Non-interactive printing can only be executed during batch, console, and menu events. Printing is made non-interactive by setting `bUI` to `false` when calling the Doc `print` method or by setting the `interactive` property to `silent`, for example,

```
var pp = this.getPrintParams();
pp.interactive = pp.constants.interactionLevel.silent;
```

Outside of batch, console, and menu events, the values of `bUI` and of `interactive` are ignored, and a print dialog box will always be presented.

See also priv.

**constants.interactionLevel Object**

| Property | Description |
|----------|-------------|
| `automatic` | No print dialog box is displayed. During printing, a progress monitor and cancel dialog box are displayed and removed automatically when printing is complete. |
| `full` | Displays the print dialog box, allowing the user to change print settings and requiring the user to press OK to continue. During printing, a progress monitor and cancel dialog box is displayed and removed automatically when printing is complete. |
| `silent` | No print dialog box is displayed. No progress or cancel dialog box is displayed. Even error messages are not displayed. |

Example:

```
var pp = this.getPrintParams();
pp.interactive = pp.constants.interactionLevel.automatic;
pp.printerName = "Adobe PDF";
this.print(pp);
```

<a id="49783"></a>
<a id="lastpage"></a>
<a id="id806"></a>
#### lastPage

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

The last 0-based page number of the document to print. The term “0-based” means the first page of any document is 0, regardless of page number labels. If the value is less than `firstPage` or outside the legal range of the document, this reverts to the default value. The default value is the number of pages in the document less one.

See firstPage for an example.

<a id="87255"></a>
<a id="nupautorotate"></a>
<a id="id807"></a>
#### nUpAutoRotate

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Boolean | R/W |

A Boolean value that if `true`, automatically rotates each page to match the page orientation to the available paper area during Multiple Pages Per Sheet printing. The default is `false`, but `nUpAutoRotate` obeys the print settings.

Multiple Pages Per Sheet is obtained by setting `pageHandling` to `nUp`.

<a id="90256"></a>
<a id="nupnumpagesh"></a>
<a id="id808"></a>
#### nUpNumPagesH

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Integer | R/W |

The number of pages to lay out in the horizontal direction when printing Multiple Pages Per Sheet. The default is 2, but `nUpNumPagesH` obeys the print settings.

Multiple Pages Per Sheet is obtained by setting `pageHandling` to `nUp`.

Example: Perform Multiple Pages Per Sheet printing on this document, set up parameters, and print.

```
pp = this.getPrintParams();
pp.pageHandling = pp.constants.handling.nUp;
pp.nUpPageOrders = pp.constants.nUpPageOrders.Vertical;
pp.nUpNumPagesH = 3;
pp.nUpNumPagesV = 3;
pp.nUpPageBorder=true;
pp.nUpAutoRotate=true;
this.print(pp);
```

<a id="27311"></a>
<a id="nupnumpagesv"></a>
<a id="id809"></a>
#### nUpNumPagesV

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Integer | R/W |

The number of pages to be laid out in the vertical direction when printing Multiple Pages Per Sheet. The default is 2, but `nUpNumPagesV` obeys the print settings.

Multiple Pages Per Sheet is obtained by setting `pageHandling` to `nUp`.

See nUpNumPagesH for an example.

<a id="90998"></a>
<a id="nuppageborder"></a>
<a id="id810"></a>
#### nUpPageBorder

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Boolean | R/W |

A Boolean value that if `true`, draws and prints a page boundary around each of the pages during Multiple Pages Per Sheet printing. The default is `false`, but `nUpPageBorder` obeys the print settings.

Multiple Pages Per Sheet is obtained by setting `pageHandling` to `nUp`.

See nUpNumPagesH for an example.

<a id="93690"></a>
<a id="nuppageorder"></a>
<a id="id811"></a>
#### nUpPageOrder

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Integer | R/W |

When printing multiple pages per sheet, the `nUpPageOrder` property determines how the multiple pages are laid out on the sheet. The value of the `nUpPageOrder` property is set through the `constants` `nUpPageOrders` object. The default is `Horizontal`, but `nUpPageOrder` obeys the print settings.

Multiple Pages Per Sheet is obtained by setting `pageHandling` to `nUp`.

**constants.nUpPageOrders Object**

| Property | Description |
|----------|-------------|
| `Horizontal` | Pages are placed from left to right, from top to bottom. |
| `HorizontalReversed` | Pages are placed from right to left, from top to bottom. |
| `Vertical` | Pages are placed from top to bottom, from left to right. |

Example: Perform Multiple Pages Per Sheet printing on this document, set the parameters, and print.

```
pp = this.getPrintParams();
pp.pageHandling = pp.constants.handling.nUp;
pp.nUpPageOrders = pp.constants.nUpPageOrders.Horizontal;
pp.nUpNumPagesH = 2;
pp.nUpNumPagesV = 2;
pp.nUpPageBorder=true;
this.print(pp);
```

<a id="58768"></a>
<a id="numcopies"></a>
<a id="id812"></a>
#### NumCopies

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 8.0 | No | No | All | Integer | R/W |

Sets the number of copies to be printed for this print job.

Example: Set print job for duplex printing with two copies.

```
var pp = this.getPrintParams();
pp.DuplexType = pp.constants.duplexTypes.DuplexFlipShortEdge;
pp.NumCopies = 2;
this.print(pp);
```

<a id="89810"></a>
<a id="pagehandling"></a>
<a id="id813"></a>
#### pageHandling

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Takes one of seven values specified by the constants `handling` object. If set to an illegal value, it is treated as `shrink`. The default is `shrink`.

**constants.handling Object**

| Property | Reader | Description |
|----------|--------|-------------|
| `none` |  | No page scaling is applied. |
| `fit` |  | Pages are enlarged or shrunk to fit the printer’s paper. |
| `shrink` |  | Small pages are printed small, and large pages are shrunk to fit on the printer’s paper. |
| `tileAll` | No | All pages are printed using tiling settings. This can be used to turn a normal-sized page into a poster by setting the `tileScale` property greater than 1. |
| `tileLarge` | No | Small or normal pages are printed in the original size and large pages are printed on multiple sheets of paper. |
| `nUp` |  | (Version 7.0) Pages are rescaled to print multiple pages on each printer page.  Properties related to Multiple Pages Per Sheet printing are nUpAutoRotate, nUpNumPagesH, nUpNumPagesV, nUpPageBorder and nUpPageOrder. |
| `booklet` |  | (Version 8.0) Prints multiple pages on the same sheet of paper in the order required to read correctly when folded. The properties of the booklet object are used to set the parameters for booklet printing. |

Example 1:

```
var pp = this.getPrintParams();
pp.pageHandling = pp.constants.handling.shrink;
this.print(pp);
```

Example 2: Perform Multiple Pages Per Sheet printing on this document, set the parameters and print.

```
pp = this.getPrintParams();
pp.pageHandling = pp.constants.handling.nUp;
pp.nUpPageOrders = pp.constants.nUpPageOrders.Horizontal;
pp.nUpNumPagesH = 2;
pp.nUpNumPagesV = 2;
pp.nUpPageBorder=true;
this.print(pp);
```

**Example 3 (Version 8.0)**

Print document as a booklet, taking all the default settings.

```
var pp = this.getPrintParams();
pp.pageHandling = pp.constants.handling.booklet;
this.print(pp);
```

<a id="51148"></a>
<a id="pagesubset"></a>
<a id="id814"></a>
#### pageSubset

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Select even, odd, or all the pages to print. The value of `pageSubset` is set through the `constants` `subsets` object. The default is `all`.

**constants.subsets Object**

| Property | Description |
|----------|-------------|
| `all` | Print all pages in the page range. |
| `even` | Print only the even pages. Page labels are ignored, and the document is treated as if it were numbered 1 through n, the number of pages. |
| `odd` | Print only the odd pages. |

Example:

```
var pp = this.getPrintParams();
pp.pageSubset = pp.constants.subsets.even;
this.print(pp);
```

<a id="72914"></a>
<a id="printasimage"></a>
<a id="id815"></a>
#### printAsImage

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Set to `true` to send pages as large bitmaps. This can be slow and more jagged looking but can work around problems with a printer’s PostScript interpreter. Set `bitmapDPI` to increase or decrease the resolution of the bitmap. If interaction (see interactive) is `full`, the user’s printer preferences for `printAsImage` will be used. The default is `false`.

<a id="95227"></a>
<a id="printcontent"></a>
<a id="id816"></a>
#### printContent

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Sets the contents of the print job. The value of the `printContents` property is set through the `constants` `printContents` object. The default is `doc`.

**constants.printContents Object**

| Property | Description |
|----------|-------------|
| `doc` | Print the document contents, not comments. |
| `docAndComments` | Print the document contents and comments. |
| `formFieldsOnly` | Print the contents of form fields only. Useful for printing onto pre-preprinted forms. |

Example: Set printer to silently print form fields only.

```
var pp = this.getPrintParams();
pp.interactive = pp.constants.interactionLevel.silent;
pp.printContent = pp.constants.printContents.formFieldsOnly;
this.print(pp);
```

<a id="84668"></a>
<a id="printrange"></a>
<a id="id817"></a>
#### printRange

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 11.0 | No | No | All | Array | R/W |

Use the `printRange` property to print multiple sets of pages, each having a different page range. The parameter format is an array of pairs (`nStart`, `nEnd`), where `nStart` and `nEnd` are 0-based index pages of the PDF document.

**Exceptions**

The `ESErrorInvalidArgs` exception occurs when:

- the format of the specified parameters is invalid
- the `startPage` and `endPage` values are less than 0.
- the `startPage` and `endPage` values are greater than or equal to `totalPages` in the PDF.

Example 1:

```
var pp = this.getPrintParams();
pp.interactive = pp.constants.interactionLevel.full;
pp.printRange=[[1, 1], [3, 4]];
this.print(pp);
```

<a id="92611"></a>
<a id="printername"></a>
<a id="id818"></a>
#### printerName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R/W |

The name of the destination printer. This property is a Windows and, beginning with version 9.0, a Mac OS feature.

By default, `printerName` is set to the name of the default printer. If `printerName` is set to an empty string, the printer used is either the last printer used by Acrobat/Adobe Reader (if printing occurred during the current session) or the System Default printer. When `printerName` is an empty string and `fileName` is a nonempty string, the current document is saved as a PostScript file. See example 2 below.

See also `app.` printerNames.

Example 1: Set the printer, and print.

```
var pp = this.getPrintParams();
pp.printerName = "hp officejet d series";
this.print(pp);
```

<a id="89060"></a>
Example 2: Save the current document as a PostScript file.

```
var pp = this.getPrintParams();
pp.fileName = "/c/temp/myDoc.ps";
pp.printerName = "";
this.print(pp);
```

<a id="86941"></a>
<a id="pslevel"></a>
<a id="id819"></a>
#### psLevel

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Level of PostScript that is emitted to PostScript printers. Level 0 indicates to use the PostScript level of the printer. Level 1 is not supported. In addition to 0, current legal values of `psLevel` are 2 and 3. If the printer only supports PostScript level 1, `printAsImage` is set to `true`. Illegal values are treated as 3. The default value for `psLevel` is 3.

<a id="25286"></a>
<a id="rasterflags"></a>
<a id="id820"></a>
#### rasterFlags

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | Integer | R/W |

A bit field of flags. These flags can be set or cleared using bitwise operations through the `constants` `rasterFlagValues` object. The default is set by user preferences.

**constants.rasterFlagValues Object**

The table that follows lists the properties of the rasterFlagValues object. None of these properties are available in Adobe Reader.

| Property | Description |
|----------|-------------|
| `textToOutline` | Text converted to outlines can become thicker (especially noticeable on small fonts). If text is mixed into artwork with transparency, it may be converted to outline during flattening, resulting in inconsistency with text that is not mixed into artwork. In this case, turning on this option ensures that all text looks consistent. |
| `strokesToOutline` | Strokes converted to outlines can become thicker (especially noticeable on thin strokes). If strokes are mixed into artwork with transparency, they may be converted to outlines during flattening, resulting in inconsistency with strokes that are not mixed into artwork. In this case, turning on this option ensures that all strokes look consistent. |
| `allowComplexClip` | This option ensures that the boundaries between vector artwork and rasterized artwork fall closely along object paths. Selecting this option reduces stitching artifacts that result when part of an object is flattened while another part of the object remains in vector form. However, selecting this option may result in paths that are too complex for the printer to handle. |
| `preserveOverprint` | Select this option if you are printing separations and the document contains overprinted objects. Selecting this option generally preserves overprint for objects that are not involved in transparency and therefore improves performance. This option has no effect when printing composite. Turning it off might result in more consistent output because all overprinting will be flattened, whether or not it is involved in transparency. |

Example 1: In the Advanced Printing Setup dialog box, check the “Convert All Text to Outlines” check box in the Transparency Flattening option.

```
pp = getPrintParams();
rf = pp.constants.rasterFlagValues;
pp.rasterFlags = rf.textToOutline;
this.print(pp);
```

<a id="62217"></a>
Example 2: In the Advanced Printing Setup dialog box, uncheck “Complex Clip Regions” (checked by default) in the Transparency Flattening option.

```
pp = getPrintParams();
rf = pp.constants.rasterFlagValues;
pp.rasterFlags = pp.rasterFlags & ~rf.allowComplexClip;
// or pp.rasterFlags &= ~rf.allowComplexClip;
this.print(pp);
```

<a id="54392"></a>
<a id="reversepages"></a>
<a id="id821"></a>
#### reversePages

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Set to `true` to print pages in reverse order (last to first). The default value is `false`.

<a id="27667"></a>
<a id="tilelabel"></a>
<a id="id822"></a>
#### tileLabel

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Label each page of tiled output. Labeled pages indicate row and column, file name, and print date. The default is `false`.

<a id="94282"></a>
<a id="tilemark"></a>
<a id="id823"></a>
#### tileMark

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | Integer | R/W |

Tile marks indicate where to cut the page and where overlap occurs. The value is set through the `constants` `tileMarks` object. If set to an illegal value, it is treated as `none`. The default is `none`.

**constants.tileMarks Object**

| Property | Description |
|----------|-------------|
| `none` | No tile marks |
| `west` | Western style tile marks |
| `east` | Eastern style tile marks |

<a id="73551"></a>
<a id="tileoverlap"></a>
<a id="id824"></a>
#### tileOverlap

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | Integer | R/W |

The number of points that tiled pages have in common. Value must be between 0 and 144. Illegal values are treated as 0. The default value is 0.

<a id="75324"></a>
<a id="tilescale"></a>
<a id="id825"></a>
#### tileScale

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | Number | R/W |

The amount that tiled pages are scaled. Pages that are not tiled are unaffected by this value. The default is unscaled (1.0). Larger values increase the size of the printout (for example, 2.0 is twice as large, a value of 0.5 is half as large). The value of `tileScale` must be between 0.01 and 99.99. Illegal values are treated as 1.0, which is the default value.

<a id="88218"></a>
<a id="transparencylevel"></a>
<a id="id826"></a>
#### transparencyLevel

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | Integer | R/W |

An integer value from 1 to 100 indicates how hard Acrobat tries to preserve high-level drawing operators. A value of 1 indicates complete rasterization of the image, which results in poor image quality but high speeds. A value of 100 indicates as much should be preserved as possible, but can result in slow print speeds. If set to an illegal value, 75 is used. When rasterizing, the `bitmapDPI` and `gradientDPI` values are used. The default value is 75.

<a id="15187"></a>
<a id="useprintercrd"></a>
<a id="id827"></a>
#### usePrinterCRD

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Takes one of three values. The value is set through the `constants` `usages` object. See also useT1Conversion; the two properties use the same values, but the interpretations are different.

**constants.usages Object**

| Property | Description |
|----------|-------------|
| `auto` | Let Acrobat decide whether the printer Color Rendering Dictionary (CRD) should be used. Acrobat maintains a list of a handful of printers that have incorrect CRDs.  Illegal values are treated as `auto`. The default is `auto`. |
| `use` | Use the printer’s CRD. |
| `noUse` | Do not use the printer’s CRD. |

<a id="62958"></a>
<a id="uset1conversion"></a>
<a id="id828"></a>
#### useT1Conversion

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Takes one of three values. The value of the `useT1Conversion` property is set through the `constants` `usages` object. See also usePrinterCRD; the two properties use the same values, but the interpretations are different.

> **Note**
>
> This property is supported on Windows platforms only.

This property uses the constants.usages Object values as follows.

| Property | Description |
|----------|-------------|
| `auto` | Let Acrobat decide whether to disable converting Type 1 fonts to more efficient printer representations (for example, TrueType). Acrobat maintains a list of a handful of printers that have problems with these fonts.  Illegal values are treated as `auto`. The default is `auto`. |
| `use` | Allow conversion of Type 1 fonts even if the printer is known to have problems with alternative font representations. |
| `noUse` | Never convert Type 1 fonts to more efficient representations. |

<a id="79704"></a>
<a id="rdn"></a>
<a id="id829"></a>
## RDN

This generic object represents a Relative Distinguished Name. It is used by `securityHandler.` newUser and the `certificate.` issuerDN and subjectCN properties.

It has the following properties.

| Property | Type | Access | Version (Key) | Description |
|----------|------|--------|---------------|-------------|
| `businessCategory` | String | R | 8.0 | Business category |
| `c` | String | R | 5.0 | Country or region. Must be a two-character upper case ISO 3166 standard string (for example, “US”). |
| `cn` | String | R | 5.0 | Common name (for example, “John Smith”) |
| `countryOfCitizenship` | String | R | 8.0 | Country of citizenship |
| `countryOfResidence` | String | R | 8.0 | Country of residence |
| `dateOfBirth` | String | R | 8.0 | Date of birth (not supported by `newUser`) |
| `dc` | String | R | 8.0 | Domain Component |
| `dnQualifier` | String | R | 8.0 | Distinguished Name Qualifier |
| `e` | String | R | 6.0 | Email address (for example, “[jsmith@example.com](mailto:jsmith@example.com)”) |
| `gender` | String | R | 8.0 | Gender |
| `generationQualifier` | String | R | 8.0 | Generation qualifier |
| `givenName` | String | R | 8.0 | Given name |
| `initials` | String | R | 8.0 | Initials |
| `l` | String | R | 8.0 | Locality or province |
| `name` | String | R | 8.0 | Name |
| `nameAtBirth` | String | R | 8.0 | Name at birth |
| `o` | String | R | 5.0 | Organization name (for example, “Adobe Systems Incorporated”) |
| `ou` | String | R | 5.0 | Organizational unit (for example, “Acrobat Engineering”) |
| `placeOfBirth` | String | R | 8.0 | Place of birth |
| `postalAddress` | String | R | 8.0 | Postal address (not supported by `newUser`) |
| `postalCode` | String | R | 8.0 | Postal code |
| `pseudonym` | String | R | 8.0 | Pseudonym |
| `serialNumber` | String | R | 8.0 | Serial number |
| `sn` | String | R | 8.0 | Surname |
| `st` | String | R | 8.0 | State |
| `street` | String | R | 8.0 | Street |
| `title` | String | R | 8.0 | Title |

<a id="32813"></a>
<a id="readstream"></a>
<a id="id830"></a>
## ReadStream

A ReadStream object is an object literal that represents a stream of data. It contains a method to allow reading the data stream.

| Method | Parameters | Returns | Description |
|--------|------------|---------|-------------|
| `read` | `nBytes` | String | The read method takes the number of bytes to read and returns a hex-encoded string with the data from the stream. The read method is a destructive operation on the stream and returns a zero length string to indicate the end of the stream. |

<a id="47886"></a>
<a id="rendition"></a>
<a id="id831"></a>
## Rendition

A Rendition contains information needed to play a media clip, including embedded media data (or a URL) and playback settings. It corresponds to a Rendition in the Acrobat authoring user interface.

A Rendition is a base type for either a MediaRendition or a MediaSelector. A function that accepts a Rendition can take either of these two types. The properties and methods described in this section are available for both MediaRendition and MediaSelector. Use the `type` property to distinguish between MediaRendition and MediaSelector.

<a id="rendition-properties"></a>
<a id="id832"></a>
### Rendition properties

<a id="57156"></a>
<a id="alttext"></a>
<a id="id833"></a>
#### altText

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

The alternate text string for the rendition (an empty string if no alternate text was specified). This property is available only if the `type` of the `rendition` is `app.media.renditionType.media` (a MediaRendition).

Example: Get the `altText` of a rendition.

```
this.media.getRendition("myClip").altText;
```

See the examples that follow `app.media.` getAltTextSettings.

<a id="26757"></a>
<a id="id834"></a>
<a id="id835"></a>
#### doc

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Doc | R |

A reference to the document that contains the Rendition.

<a id="94327"></a>
<a id="id836"></a>
<a id="id837"></a>
#### fileName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

If the media is embedded, this property returns an empty string. Otherwise it returns the file name or URL of the media. This property is available only if the `type` of the `rendition` is `app.media.renditionType.media`.

<a id="69594"></a>
<a id="id838"></a>
<a id="id839"></a>
#### type

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Number | R |

An `app.media.renditionType` value indicating the type of rendition.

Currently, there are two types: MediaRendition and RenditionList:

- When `Rendition.type` is equal to `app.media.renditionType.media`, the Rendition is a MediaRendition. A MediaRendition is an individual Rendition, as it appears in the Settings tab of the Multimedia Properties dialog box.
- When `Rendition.type` is equal to `app.media.renditionType.selector`, the Rendition is a RenditionList. A RenditionList is an array of MediaRendition. The list is the one that appears in the Settings tab of the Multimedia Properties dialog box.

Future versions of Acrobat may add more `renditionType` values, so JavaScript code should not assume that only the existing `app.media.renditionType` values may be encountered.

<a id="97659"></a>
<a id="id840"></a>
<a id="id841"></a>
#### uiName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

The name of the Rendition, as found in the N entry in its dictionary in the PDF file.

Example: The following is executed as a Rendition action.

```
console.println("Preparing to play ""
    + event.action.rendition.uiName + """);
```

See the event object for a description of `event.action.rendition`.

<a id="rendition-methods"></a>
<a id="id842"></a>
### Rendition methods

<a id="15194"></a>
<a id="getplaysettings"></a>
<a id="id843"></a>
#### getPlaySettings

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Creates and returns a `MediaSettings` object that can be used to create a MediaPlayer object.

This method is available only for a MediaRendition.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `bGetData` | (optional) A Boolean value. If `true`, the MediaSettings object returns the MediaData (See MediaSettings. data). |

**Returns**

A `MediaSettings` object

> **Note**
>
> `app.media.getAltTextSettings` calls `getPlaySettings(false)` to obtain the correct settings to display alternate text.

This `MediaSettings` object includes these properties:

- `autoPlay`
- `baseURL`     (if specified in `rendition`)
- `bgColor`
- `bgOpacity`
- `data`        (if `bGetData` is true)
- `duration`
- `endAt`
- `layout`
- `monitorType`
- `palindrome`
- `showUI`
- `rate`
- `repeat`
- `startAt`
- `visible`
- `volume`
- `windowType`

In the current version of Acrobat, all of these properties are present in the settings object (except as noted above). `null` is used when values such as `startAt` are unspecified. This may change in the future to return only those values that are actually specified, with defaults assumed for the rest.

Example:

```
// Get the MediaSettings for this Rendition
var settings = myRendition.getPlaySettings();
if( settings.startAt !== null ) // Do NOT use this strict comparison!
...
if( settings.startAt ) // This is OK
...
```

See `app.media.` getAltTextSettings and `app.media.` openPlayer for examples of usage.

<a id="80973"></a>
<a id="id844"></a>
<a id="id845"></a>
#### select

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Selects a media player to play a MediaRendition or a RenditionSelector. If the Rendition is a RenditionSelector, `select` examines every MediaRendition contained within and selects the most suitable one. (See type for a description of RenditionSelector and MediaRendition.)

The return value is a `MediaSelection` object that can be used to create a `MediaSettings` object. This object can then be used to create a `MediaPlayer` object.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `bWantRejects` | (optional) If `bWantRejects` is `true`, the `rejects` property of the resulting MediaSelection will contain information about media players that were rejected during the selection process. |
| `oContext` | (optional) `oContext` is a `MediaSelection.selectContext` value from a previous `Rendition.select` call.  This parameter allows you to write a loop that calls `Rendition.select` repeatedly until you find a media player that satisfies any selection criteria that you want to test in JavaScript code. |

**Returns**

A `MediaSelection` object

Example 1: Get a usable MediaSelection for this Rendition.

```
var selection = rendition.select();
```

<a id="50647"></a>
Example 2: Get the name of the selected rendition. This script is executed from a Rendition action event.

```
var selection = event.action.rendition.select();
console.println( "Preparing to play " + selection.rendition.uiName);
```

<a id="90781"></a>
<a id="testcriteria"></a>
<a id="id846"></a>
#### testCriteria

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Tests the Rendition against any criteria that are specified in the PDF file, such as minimum bandwidth, and returns a Boolean value indicating whether the Rendition satisfied all of those criteria.

**Returns**

Boolean

<a id="62908"></a>
<a id="report"></a>
<a id="id847"></a>
## Report

The Report object allows the user to programmatically generate PDF documents suitable for reporting with JavaScript. Use the `writeText` constructor to create a `Report` object; for example,

```
var rep = new Report();
```

The properties and methods can then be used to write and format a report.

<a id="report-properties"></a>
<a id="id848"></a>
### Report properties

<a id="47833"></a>
<a id="absindent"></a>
<a id="id849"></a>
#### absIndent

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | Not available in Reader | Number | R/W |

Controls the absolute indentation level. It is desirable to use the `indent` and `outdent` methods whenever possible, because they correctly handle indentation overflows.

If a report is indented past the middle of the page, the effective indent is set to the middle. Note that `divide` indicates that it has been indented too far.

<a id="95175"></a>
<a id="id850"></a>
<a id="id851"></a>
#### color

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | Not available in Reader | Color | R/W |

Controls the color of any text and any divisions written into the report.

Text is written to the report with `writeText` and divisions (horizontal rules) are written using `divide`.

Example:

```
var rep = new Report();
rep.size = 1.2;
rep.color = color.blue;
rep.writeText("Hello World!");
```

<a id="16633"></a>
<a id="id852"></a>
<a id="id853"></a>
#### size

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | Not available in Reader | Number | R/W |

Controls the size of any text created by `writeText` It is a multiplier. Text size is determined by multiplying the `size` property by the default size for the given style.

Example: Write a “Hello World!” document.

```
var rep = new Report();
rep.size = 1.2;
rep.writeText("Hello World!");
```

<a id="50854"></a>
<a id="id854"></a>
<a id="id855"></a>
#### style

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Not available in Reader | String | R/W |

This property controls the style of the text font for the text created by `writeText`. Values of `style` are:

```
DefaultNoteText
NoteTitle
```

Example: Start a new report, set font size, write short text and open report.

```
var rep = new Report();
rep.size = 1.2;
rep.style = "DefaultNoteText";
rep.writeText("Hello World!");
rep.open("My Report");
```

<a id="report-methods"></a>
<a id="id856"></a>
### Report methods

<a id="45222"></a>
<a id="breakpage"></a>
<a id="id857"></a>
#### breakPage

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | Not available in Reader |

Ends the current page and begins a new one.

<a id="79384"></a>
<a id="divide"></a>
<a id="id858"></a>
#### divide

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | Not available in Reader |

Writes a horizontal rule across the page at the current location with the given width. The rule goes from the current indent level to the rightmost edge of the bounding box. If the indent level is past the middle of the bounding box, the rule shows this.

**Parameters**

| Property | Description |
|----------|-------------|
| `nWidth` | (optional) The horizontal rule width to use. |

<a id="76312"></a>
<a id="indent"></a>
<a id="id859"></a>
#### indent

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | Not available in Reader |

Increments the current indentation mark by `nPoints` or the default amount. If a report is indented past the middle of the page, the effective indent is set to the middle. Note that `divide` makes a mark to indicate whether it has been indented too far.

See writeText for an example of usage.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nPoints` | (optional) The number of points to increment the indentation mark. |

<a id="52175"></a>
<a id="id860"></a>
<a id="id861"></a>
#### mail

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | Not available in Reader |

Ends report generation and mails the report.

See also mailGetAddrs, `app.` mailMsg, the Doc mailForm method, and the `FDF` object mail method.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `bUI` | (optional) Specifies whether to display a user interface. If `true` (the default), the rest of the parameters are used to seed the compose-new-message window that is displayed to the user. If `false`, the `cTo` parameter is required and all others are optional.   -  (Acrobat 7.0) When this method is executed in a non-privileged context, the `bUI` parameter is not honored and defaults to `true`. See priv. |
| `cTo` | (optional) A semicolon-separated list of recipients for the message. |
| `cCc` | (optional) A semicolon-separated list of CC recipients for the message. |
| `cBcc` | (optional) A semicolon-separated list of BCC recipients for the message. |
| `cSubject` | (optional) The subject of the message. The length limit is 64 KB. |
| `cMsg` | (optional) The content of the message. The length limit is 64 KB. |

<a id="10871"></a>
<a id="id862"></a>
<a id="id863"></a>
#### open

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | Not available in Reader |

Ends report generation, opens the report in Acrobat and returns a Doc that can be used to perform additional processing of the report.

**Parameters**

| Property | Description |
|----------|-------------|
| `cTitle` | The report title. |

**Returns**

A Doc.

Example: Open a report, get the Doc, and set some properties of the document.

```
var docRep = rep.open("myreport.pdf");
docRep.info.Title = "End of the month report: August 2000";
docRep.info.Subject = "Summary of comments at the August meeting";
```

See writeText for a more complete example.

<a id="12120"></a>
<a id="outdent"></a>
<a id="id864"></a>
#### outdent

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | Not available in Reader |

The opposite of indent; that is, decrements the current indentation mark by `nPoints` or the default amount.

See writeText for an example of usage.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nPoints` | (optional) The number of points to decrement the indentation mark. |

<a id="14001"></a>
<a id="id865"></a>
<a id="id866"></a>
#### Report

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | Not available in Reader |

A constructor. Creates a new `Report` object with the given media and bounding boxes (values are defined in points or 1/72 of an inch). Defaults to a 8.5 x 11 inch media box and a bounding box that is indented 0.5 inches on all sides from the media box.

**Parameters**

| Property | Description |
|----------|-------------|
| `aMedia` | (optional) The media type. |
| `aBBox` | (optional) The bounding box size. |

**Returns**

A `Report` object.

<a id="55306"></a>
<a id="id867"></a>
<a id="id868"></a>
#### save

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | Not available in Reader |

Ends report generation and saves the report to the specified path.

> **Note**
>
> This method can only be executed during a batch or console event. See priv. The event object contains a discussion of JavaScript events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cDIPath` | The device-independent path. |
| `cFS` | (optional) The file system. The only value for `cFS` is “CHTTP”. In this case, the `cDIPath` parameter should be an URL. This parameter is only relevant if the web server supports WebDAV. |

Example 1:

```
rep.save("/c/myReports/myreport.pdf");
```

Example 2:

```
rep.save({
    cDIPath: "http://www.example.com/reports/WebDAV/myreport.pdf",

     cFS:"CHTTP"}
);
```

<a id="30283"></a>
<a id="writetext"></a>
<a id="id869"></a>
#### writeText

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | Not available in Reader |

Writes out a block of text to the report. Every call begins on a new line at the current indentation mark. Correctly wraps Roman, CJK, and WGL4 text.

**Parameters**

| Property | Description |
|----------|-------------|
| `String` | The block of text to use. |

Example:

```
// Get the comments in this document, and sort by author
this.syncAnnotScan();
annots = this.getAnnots({nSortBy: ANSB_Author});

// Open a new report
var rep = new Report();

rep.size = 1.2;
rep.color = color.blue;

 if (annots) {
    rep.writeText("Summary of Comments: By Author");
    rep.color = color.black;
    rep.writeText(" ");
    rep.writeText("Number of Comments: " + annots.length);
    rep.writeText(" ");

    var msg = "200 page %s: "%s"";
    var theAuthor = annots[0].author;
    rep.writeText(theAuthor);
    rep.indent(20);
    for (var i=0; i < annots.length; i++) {
        if (theAuthor != annots[i].author) {
            theAuthor = annots[i].author;
            rep.writeText(" ");
            rep.outdent(20);
            rep.writeText(theAuthor);
            rep.indent(20);
        }
        rep.writeText(
            util.printf(msg, 1 + annots[i].page, annots[i].contents));
    }
} else {
    var msg = "No annotations found in this document, %s.";
    rep.writeText(util.printf(msg, this.documentFileName));
}
// Now open the report
var docRep = rep.open("myreport.pdf");
docRep.info.Title = "End of the month report: August 2006";
docRep.info.Subject = "Summary of comments at the August meeting";
```

<a id="66963"></a>
<a id="row"></a>
<a id="id870"></a>
## Row

This generic JavaScript object contains the data from every column in a row. It is returned by the `Statement` object method. It contains the following properties:

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `columnArray` | Array | R | An array of `Column` objects.  It is equivalent to what the Statement object method would return if called on the same `Statement` object at the same time that this `row` object was created. |
| column properties | any | R | There is a property corresponding to each column selected by the query, containing the data for that row in that column. |

<a id="43548"></a>
<a id="screenannot"></a>
<a id="id871"></a>
## ScreenAnnot

A ScreenAnnot object represents a screen annotation, which is a rectangular area within a PDF document viewed on the display screen. A ScreenAnnot may have Renditions and RenditionActions associated with it for multimedia playback.

> **Note**
>
> The ScreenAnnot object is part of the Acrobat 6.0 (and Later) Compatible Media JavaScript API. Multimedia assets that use this approach rely on the underlying operating system to locate and launch a multimedia player residing on the user’s system. Acrobat 9.0 (and Later) natively supports Flash video (FLV) and Flash applications (SWF) which can be embedded in, or streamed to, a PDF document. Native support for Flash enables reliable cross-platform playback. No additional media player or specific codec is necessary.

Acrobat 6.0 (and Later) Compatible Media is superseded by the multimedia of Acrobat 9.0 (and Later), which uses rich media annotations. Developers of PDFs with multimedia assets are, therefore, strongly encouraged to use the rich media annotations of Acrobat 9 (and Later). Refer to the AnnotRichMedia object for JavaScript support for rich media annotations.

<a id="screenannot-properties"></a>
<a id="id872"></a>
### ScreenAnnot properties

<a id="36955"></a>
<a id="id873"></a>
<a id="id874"></a>
#### altText

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R |

The alternate text string for the annotation (an empty string if no alternate text was specified).

Example: Get an annotation and write its `altText` to the debug console.

```
var annot = this.media.getAnnot({ nPage:0, cAnnotTitle: "myScreen" });
console.println( "annot.altText = " + annot.altText );
```

<a id="93566"></a>
<a id="alwaysshowfocus"></a>
<a id="id875"></a>
#### alwaysShowFocus

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Normally, a screen annotation shows and hides a focus rectangle to indicate whether it has the keyboard focus. If this property is `true`, the focus rectangle is displayed by the screen annotation even if it does not have the focus. This is used for docked media playback, so that the focus rectangle of the annotation can remain visible even though the media player actually has the keyboard focus.

This property is not saved in the PDF file. If you change it, the change affects the current session only.

<a id="63528"></a>
<a id="id876"></a>
<a id="id877"></a>
#### display

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Integer | R/W |

Same as the Field object `display` property.

This property is not saved in the PDF file. If you change it, the change affects the current session only.

Example: Hide the annotation.

```
var annot = this.media.getAnnot({ nPage:0, cAnnotTitle: "myScreen" });
annot.display = display.hidden;
```

<a id="64999"></a>
<a id="id878"></a>
<a id="id879"></a>
#### doc

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Doc | R |

A reference to the document that contains the screen annotation.

<a id="13656"></a>
<a id="id880"></a>
<a id="id881"></a>
#### events

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | `Events` object | R/W |

An `Events` object containing the EventListeners that are attached to a screen annotation.

This property is not saved in the PDF file. If you change it, the change affects the current session only.

Example: Create a simple focus EventListener.

```
var annot = this.media.getAnnot({ nPage:0, cAnnotTitle: "myScreen" });
var myFocusEvent = {
    onFocus: function () {
        console.println("Focusing...");
    }
};
annot.events.add( myFocusEvent );
```

This EventListener can be removed at a later time by executing the following code.

```
annot.events.remove( myFocusEvent );
```

<a id="94094"></a>
<a id="extfocusrect"></a>
<a id="id882"></a>
#### extFocusRect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array of 4 Numbers | R/W |

When a screen annotation draws a focus rectangle, the rectangle normally encloses only the screen annotation itself. If `extFocusRect` is specified, the screen annotation takes the union of its normal rectangle and `extFocusRect`, and it uses the resulting rectangle to draw the focus rectangle.

This property is not saved in the PDF file. If you change it, the change affects the current session only.

<a id="77921"></a>
<a id="innerdevicerect"></a>
<a id="id883"></a>
#### innerDeviceRect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array of 4 Numbers | R |

This property and `outerDeviceRect` define the interior and exterior rectangles of the screen annotation as it appears in the current page view.

Example: Get the `innerDeviceRect`.

```
annot = this.media.getAnnot({ nPage:0, cAnnotTitle: "myScreen" });
console.println("annot.innerDeviceRect = "
    + annot.innerDeviceRect.toSource() );
```

<a id="95673"></a>
<a id="notrigger"></a>
<a id="id884"></a>
#### noTrigger

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

If `true`, the screen annotation cannot be triggered through the Acrobat user interface. Typically, clicking on a screen annotation starts playback of a media player. This property suppresses this.

This property is not saved in the PDF file. If you change it, the change affects the current session only.

Example: Use form buttons to control the media clip, so turn off interaction with the annotation.

```
annot = this.media.getAnnot({ nPage:0, cAnnotTitle: "myScreen" });
annot.noTrigger = true;
```

<a id="96759"></a>
<a id="outerdevicerect"></a>
<a id="id885"></a>
#### outerDeviceRect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array of 4 Numbers | R8 |

This property and `innerDeviceRect` define the interior and exterior rectangles of the screen annotation as it appears in the current page view.

<a id="92482"></a>
<a id="id886"></a>
<a id="id887"></a>
#### page

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Number | R |

The page number of the PDF file in which the screen annotation is located.

<a id="16634"></a>
<a id="player"></a>
<a id="id888"></a>
#### player

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | ScreenAnnot | R/W |

A reference to the MediaPlayer associated with a screen annotation. This property exists only for a `ScreenAnnot` object that is connected to a MediaPlayer. The property is set by `MediaPlayer.open` or by methods that call `open` indirectly, such as `app.media.openPlayer`.

<a id="96047"></a>
<a id="id889"></a>
<a id="id890"></a>
#### rect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | D | No | All | Array of 4 Numbers | R/W |

The rectangle of the screen annotation in default user coordinates. Changing this property dirties the PDF file; the new setting is saved if the PDF file is saved. `innerDeviceRect` and `outerDeviceRect` are also updated to reflect the new rectangle.

Example: Adjust the position of the annotation slightly.

```
var annot = this.media.getAnnot({ nPage:0, cAnnotTitle: "myScreen" });
var aRect = annot.rect;
aRect[0] += 10;
aRect[2] += 10;
annot.rect = aRect;
```

<a id="screenannot-methods"></a>
<a id="id891"></a>
### ScreenAnnot methods

<a id="24895"></a>
<a id="hasfocus"></a>
<a id="id892"></a>
#### hasFocus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Tells whether the screen annotation currently has the keyboard focus.

**Returns**

Boolean

<a id="93849"></a>
<a id="id893"></a>
<a id="id894"></a>
#### setFocus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Sets the keyboard focus to the screen annotation. The focus is set synchronously (before `setFocus` returns) if it is safe to do so. If it is unsafe to set the focus synchronously (for example, when the property is changed within an on event method), `bAllowAsync` determines what happens:

- If `true`, the focus will be set asynchronously during idle time.
- If `false` or omitted, the focus remains unchanged.

The return value is `true` if the operation was performed synchronously, or `false` if it was deferred to be performed asynchronously.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `bAllowAsync` | (optional) A Boolean value that determines the behavior of `setFocus` when it is not safe to set the focus synchronously. If `true`, the focus will be set asynchronously during idle time. If `false` or omitted, the focus remains unchanged. The default is `false`. |

**Returns**

Boolean

<a id="68641"></a>
<a id="id895"></a>
<a id="id896"></a>
## search

The `search` object is a static object that accesses the functionality provided by the Acrobat Search plug-in. This plug-in must be installed to interface with the `search` object (see available).

See also the `Index` object, which is returned by some of the methods of the `search` object.

The results for `query` calls are displayed in the Find dialog box of Acrobat.

> **Note**
>
> Acrobat 7.0 indexes are incompatible with the search engines of Acrobat 5.0 and earlier versions. As well, in Acrobat 7.0, searching indexes created by versions of Acrobat 5.0 and earlier is not possible on the Mac OS platform.

<a id="search-properties"></a>
<a id="id897"></a>
### search properties

<a id="22722"></a>
<a id="attachments"></a>
<a id="id898"></a>
#### attachments

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Boolean | R/W |

Determines whether any PDF file attachments should be searched along with the base document. The default is `false`.

This property is ignored on the Mac OS platform when searching a document from within the Safari web browser. As a result, attachments are not searched inside Safari.

<a id="29386"></a>
<a id="id899"></a>
<a id="id900"></a>
#### available

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Boolean | R |

**Returns** `true` if the Search plug-in is loaded and query capabilities are possible. A script author should check this Boolean before performing a query or other `search` object manipulation.

Example: Make sure the `search` object exists and is available.

```
if (typeof search != "undefined" && search.available) {
    search.query("Cucumber");
}
```

<a id="80980"></a>
<a id="bookmarks"></a>
<a id="id901"></a>
#### bookmarks

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Specifies whether bookmarks are searched for the query. The default is `false`.

<a id="89341"></a>
<a id="docinfo"></a>
<a id="id902"></a>
#### docInfo

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Specifies whether the document information is searched for the query. The default is `false`.

<a id="81268"></a>
<a id="doctext"></a>
<a id="id903"></a>
#### docText

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Specifies whether the document text is searched for the query. The default is `true`.

<a id="95372"></a>
<a id="docxmp"></a>
<a id="id904"></a>
#### docXMP

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Specifies whether document-level XMP metadata is searched for the query. The default is `false`.

<a id="85878"></a>
<a id="ignoreaccents"></a>
<a id="id905"></a>
#### ignoreAccents

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Boolean | R/W |

Specifies whether accents and diacriticals are ignored while searching the query term. The default is `false`.

<a id="45257"></a>
<a id="ignoreasiancharacterwidth"></a>
<a id="id906"></a>
#### ignoreAsianCharacterWidth

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Specifies whether the Kana characters in the document exactly match the search query. The default is `false`.

<a id="96142"></a>
<a id="indexes"></a>
<a id="id907"></a>
#### indexes

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | Array | R |

An array of all of the `Index` objects currently accessible by the search engine.

> **Note**
>
> (Acrobat 7.0) This property can only be accessed during a batch or console event. See priv. The event object contains a discussion of JavaScript events.

Example: Enumerate all of the indexes and dump their names.

```
for (var i = 0; i < search.indexes.length; i++) {
    console.println("Index[" + i + "]=", search.indexes[i].name);
}
```

<a id="68401"></a>
<a id="jpegexif"></a>
<a id="id908"></a>
#### jpegExif

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Specifies whether EXIF data associated with JPEG images in the PDF document is searched. The default is `false`.

<a id="15077"></a>
<a id="legacysearch"></a>
<a id="id909"></a>
#### legacySearch

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R |

> **Note**
>
> Beginning with Acrobat 10.0, this property is deprecated. This property will always return false and access is restricted to read only.

Provides the capability to search indexes generated by Acrobat Catalog in Acrobat 5.0 and earlier versions. See the sections in Acrobat Help pertaining to searching such indexes.

<a id="72708"></a>
<a id="markup"></a>
<a id="id910"></a>
#### markup

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Specifies whether markup (annotations) are searched for the query. The default is `false`.

<a id="17139"></a>
<a id="matchcase"></a>
<a id="id911"></a>
#### matchCase

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Boolean | R/W |

Specifies whether the search query is case sensitive. The default is `false`.

<a id="29234"></a>
<a id="matchwholeword"></a>
<a id="id912"></a>
#### matchWholeWord

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Specifies whether search finds only occurrences of complete words that are specified in the query. For example, when this option is set to `true`, if you search for the word “stick”, the words “tick” and “sticky” will not be highlighted. The default is `false`.

<a id="21610"></a>
<a id="maxdocs"></a>
<a id="id913"></a>
#### maxDocs

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Integer | R/W |

The maximum number of documents that will be returned as part of the search query. The default is 100 documents.

<a id="87907"></a>
<a id="objectmetadata"></a>
<a id="id914"></a>
#### objectMetadata

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Boolean | R/W |

This property determines whether object-level metadata should be searched. This is the same data that is visible from Tools pane> Interactive objects > Select Object.

The default is `false`.

<a id="13660"></a>
<a id="proximity"></a>
<a id="id915"></a>
#### proximity

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Boolean | R/W |

Specifies whether the search query will reflect the proximity of words in the results ranking when performing the search that contains *AND* Boolean clauses. The default is `false`. See the sections in the Acrobat Help pertaining to Search capabilities for a more thorough discussion of proximity.

<a id="26700"></a>
<a id="proximityrange"></a>
<a id="id916"></a>
#### proximityRange

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Integer | R/W |

The range of proximity search in number of words. This property will be used only if the property `proximity` is set to `true`. See the sections in the Acrobat Help pertaining to Search capabilities for a more thorough discussion of proximity.

The default is 900 words. The value of this parameter can be any non-zero positive integer.

<a id="29056"></a>
<a id="refine"></a>
<a id="id917"></a>
#### refine

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Boolean | R/W |

Specifies whether the search query will take the results of the previous query and refine the results based on the next query. The default is `false`. See the sections in the Acrobat Help pertaining to Search capabilities for a more thorough discussion of refining queries.

<a id="34599"></a>
<a id="stem"></a>
<a id="id918"></a>
#### stem

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Boolean | R/W |

Specifies whether the search query will take the stemming of words (for example, run, runs, running) into account when performing the search. The default is `false`. See the sections in the Acrobat Help pertaining to Search capabilities for a more thorough discussion of stemming.

<a id="70958"></a>
<a id="wordmatching"></a>
<a id="id919"></a>
#### wordMatching

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | String | R/W |

How individual words in the query will be matched to words in the document. Values are:

```
MatchPhrase
MatchAllWords
MatchAnyWord
BooleanQuery (default)
```

This property is relevant only when a query has more than one word. The `BooleanQuery` option is ignored when searching the active document.

<a id="search-methods"></a>
<a id="id920"></a>
### search methods

<a id="10631"></a>
<a id="addindex"></a>
<a id="id921"></a>
#### addIndex

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | P | Yes | All |

Adds the specified index to the list of searchable indexes.

> **Note**
>
> As of Acrobat 8.1, this method will only index pdx files.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| cDIPath | A device-independent path to an index file on the user’s hard drive. |
| cDIPath | (optional) Whether the index should be selected for searching. |

**Returns**

An `Index` object.

Example: Adds the standard help index for Acrobat to the index list:

```
search.addIndex("/c/program files/adobe/Acrobat 5.0/help/exchhelp.pdx", true);
```

<a id="45356"></a>
<a id="getindexforpath"></a>
<a id="id922"></a>
#### getIndexForPath

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Searches the index list and returns the `Index` object whose path corresponds to the specified path.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| cDIPath | A device-independent path to an index file on the user’s hard drive. |

**Returns**

The `Index` object whose path corresponds to the specified path.

<a id="21823"></a>
<a id="query"></a>
<a id="id923"></a>
#### query

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | All |

Searches the specified document or index for the specified text. Properties associated with the `search` object (such as `matchCase`, `matchWholeWord`, `stem`) may affect the result.

> **Note**
>
> As of Acrobat 8.1, if the `cDIPath` parameter is specified, this method is only permitted to execute through the console or in a batch process.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cQuery` | The text for which to search. |
| `cWhere` | (optional) Specifies where the text should be searched. Values are:  *ActiveDoc Folder Index ActiveIndexes*  The default is `ActiveIndexes`. |
| `cDIPath` | (optional) A device-independent path to a folder or Catalog index on the user’s computer.  When `cWhere` is `Folder` or `Index`, this parameter is required. |

**Examples**

Search for the word “Acrobat”.

| cWhere | Query |
|--------|-------|
| `ActiveIndexes` | *search.query(“Acrobat”); // “ActiveIndexes” is the default. search.query(“Acrobat”, “ActiveIndexes”);* |
| `ActiveDoc` | `search.query("Acrobat", "ActiveDoc");` |
| `Folder` | *search.query(“Acrobat”,”Folder”,”/c/myDocuments”); search.query(“Acrobat”,”Folder”,app.getPath(“user”,”documents”)); search.query(“Acrobat”, “Folder”, “//myserver/myDocuments”);* |
| `Index` | `search.query("Acrobat", "Index", "/c/Myfiles/public/index.pdx");` |

<a id="25991"></a>
<a id="removeindex"></a>
<a id="id924"></a>
#### removeIndex

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | P | Yes | All |

Removes the specified `Index` object from the index list.

> **Note**
>
> As of Acrobat 8.1, this method is only permitted to execute through the console or in a batch process.

**Parameters**

| Property | Description |
|----------|-------------|
| `index` | The `Index` object to remove from the index list. |

<a id="56402"></a>
<a id="id977"></a>
<a id="id978"></a>
## SOAP

The SOAP object allows remote procedure calls to be made to, or sends an XML Message to, a remote server from JavaScript.

The SOAP 1.1 protocol (see [http://www.w3.org/TR/SOAP/](http://www.w3.org/TR/SOAP/)) is used to marshall JavaScript parameters to a remote procedure call (either synchronously or asynchronously) and to unmarshall the result as a JavaScript object. The SOAP object also has the ability to communicate with web services, described by the Web Services Description Language (WSDL—see [http://www.w3.org/TR/wsdl](http://www.w3.org/TR/wsdl)).

> **Note**
>
> The SOAP methods `connect`, `request` and `response` are available only for documents open in Acrobat Pro and Acrobat Standard.

<a id="soap-properties"></a>
<a id="id979"></a>
### SOAP properties

<a id="49077"></a>
<a id="wiredump"></a>
<a id="id980"></a>
#### wireDump

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

If `true`, synchronous SOAP requests will cause the XML request and response to be dumped to the JavaScript Console. This is useful for debugging SOAP problems.

> **Note**
>
> Beginning with Acrobat 8.0, this property is deprecated, new services should use `Net.SOAP.wireDump`.

<a id="soap-methods"></a>
<a id="id981"></a>
### SOAP methods

<a id="56159"></a>
<a id="id982"></a>
<a id="id983"></a>
#### connect

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | Requires forms right |

Converts the URL of a WSDL document (cURL) to a JavaScript object with callable methods corresponding to the web service.

The parameters to the method calls and the return values obey the rules specified for the `SOAP.request` method.

> **Note**
>
> Beginning with Acrobat 8.0, this method is deprecated, new services should use `Net.SOAP.connect`. Not supported in Acrobat Reader.

**Parameters**

| Property | Description |
|----------|-------------|
| `cURL` | The URL of a WSDL document. It must be an HTTP or HTTPS URL. |

**Returns**

A WSDL Service Proxy object with a JavaScript method corresponding to each operation in the WSDL document provided at the URL.

The parameters required for the method depend on the WSDL operation you are calling and how the operation encodes its parameters:

- If the WSDL operation is using the SOAP RPC encoding (as described in Section 7 of the SOAP 1.1 Specification), the arguments to the service method are the same as the parameter order in the WSDL document.
- If the WSDL service is using the SOAP document/literal encoding, the function will have a single argument indicating the request message. The argument may be a JavaScript object literal describing the message or it may be either a string or a `ReadStream` object with an XML fragment describing the message. The return value of the service method will correspond to the return value of the WSDL operation.

The JavaScript function objects corresponding to each web service method use the following properties if they are set. The default is for none of the properties to be set.

| Property | Description |
|----------|-------------|
| `asyncHandler` | Indicates that the web service method should be performed asynchronously. The property corresponds to the `oAsync` parameter of `SOAP.request`. |
| `requestHeader` | Indicates that the web service method should include a SOAP Header in the request. The property corresponds to the `oReqHeader` parameter of `SOAP.request`. |
| `responseHeader` | Indicates that the web service method should return a SOAP Header from the response. The property corresponds to the `oRespHeader` parameter of `SOAP.request`. |
| `authenticator` | Indicates how authentication should be handled for the web service method. The property corresponds to the `oAuthenticate` parameter of `SOAP.request`. |

**Exceptions**

SOAP Faults cause a `SOAPError` exception to be thrown. If there is a problem at the networking level, such as an unavailable endpoint, a `NetworkError` is thrown. See the request method for more information.

Example: Echo a string and an integer using an echo service WSDL document.

A service WSDL Document URL is needed. These can be obtained from the “Round 2 Interop Services - using SOAP 1.2” section at the following URL: [http://www.whitemesa.com/interop.htm](http://www.whitemesa.com/interop.htm).

```
   var cURL =
<get a URL for this service from
            http://www.whitemesa.com/interop.htm>;

   // Connect to the test service
   var service = SOAP.connect(cURL);

   // Print out the methods this service supports to the console
   for(var i in service) console.println(i);

   var cTestString = "This is my test string";

   // Call the echoString service -- it is an RPC Encoded method
   var result = service.echoString(cTestString);

   // This should be the same as cTestString
   console.println(result + " == " + cTestString);

   // Call the echoInteger service -- JavaScript doesn't support integers
   // so we make our own integer object.
   var oTestInt =
   {
       soapType: "xsd:int",
       soapValue: "10"
   };
   var result = service.echoInteger(oTestInt);

   // This should be the same as oTestInt.soapValue
   console.println(result + " == " + oTestInt.soapValue);
```

This produces the following output:

```
echoBase64
echoBoolean
echoDate
echoDecimal
echoFloat
echoFloatArray
echoHexBinary
echoInteger
echoIntegerArray
echoPolyMorph
echoPolyMorphArray
echoPolyMorphStruct
echoString
echoStringArray
echoStruct
echoStructArray
echoVoid
This is my test string == This is my test string
10 == 10
```

<a id="74868"></a>
<a id="queryservices"></a>
<a id="id984"></a>
#### queryServices

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | All |

Locates network services that have published themselves using DNS Service Discovery (DNS-SD). This method can locate services that have registered using Multicast DNS (mDNS) for location on a local networking link or through unicast DNS for location within an enterprise. The results of service location are always returned asynchronously and the query continues (with notification as services become available or unavailable) until it is stopped.

The result of querying for services is a set of service names that can be bound when needed by calling `resolveService`.

Services can either use a third-party mDNS responder to be located in the local network link or register themselves in a DNS server (either statically or dynamically) to be located within an enterprise networking environment.

> **Note**
>
> Beginning with Acrobat 8.0, this method is deprecated, new services should use `Net.Discovery.queryServices`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cType` | The DNS SRV Service Name to search for. Some possible examples are:  *“http”* : Locate web servers  *“ftp”* : Locate FTP servers  See the DNS SRV Service Name Registry for more examples |
| `oAsync` | A notification object that is notified when services are located on the network or when services that had previously been reported are removed. The notification methods are not called until the `queryServices` method returns and are called during idle processing. The `oAsync` parameter should implement the following methods: * *addServices*: This method is called when available services matching the query are located. The parameter is an array of `Service Description` objects for the services that have been added. * *removeServices*: This method is called when services that had previously been introduced by calling the `addServices` notification method are no longer available. The parameter is an array of `Service Description` objects for the services that have been removed.  -  In Acrobat 7.0, only services located through mDNS (that is, in the “local.” domain) are updated dynamically. |
| `aDomains` | (optional) An array of domains that the query should be made for. The only valid domains are: * *ServiceDiscovery.local*: Search for services in the local networking link using Multicast DNS (mDNS). This is useful for finding network services in an *ad hoc* networking environment, but network services will only be located within the scope of the current network router. * *ServiceDiscovery.DNS*: Search for services in the default DNS domain using unicast DNS. This is useful for locating network services in the context of a DNS server, but typically requires IS assistance to register a service and is less dynamic. |

**Returns**

A service query object that manages the duration of the query. The query will continue until one of the following conditions is met:

- The service query object returned from `queryServices` is garbage collected.
- The `stop` method of the service query object returned from `queryServices` is called.

| Method | Description |
|--------|-------------|
| `stop` | Causes the query to terminate. This method can be called from a notification callback but the operation will not stop until idle processing time. |

**Exceptions**

Standard Acrobat exceptions.

<a id="16405"></a>
**Service Description Object**

The service description object passed to `addServices` and `removeServices` have the following properties:

| Property | Description |
|----------|-------------|
| `name` | The Unicode display name of the service. |
| `domain` | The DNS domain in which the service was located. If the service was located in the local networking link, the domain name will be “local”. |
| `type` | The DNS SRV Service Name of the service that was located-this will be the same as the `cType` parameter passed to `queryServices`. This can be useful when the same notification callback is being used for multiple queries. |

Example: Locates network services that have published themselves using DNS Service Discovery.

This example code will produce different output depending on where it is run.

```
var oNotifications =
{
    addServices: function(services)
    {
        for(var i = 0; i < services.length; i++)
        console.println("ADD: "+ services[i].name + " in domain "
            + services[i].domain);
    },
    removeServices: function(services)
    {
        for(var i = 0; i < services.length; i++)
        console.println("DEL: " + services[i].name + " in domain "

             + services[i].domain);
    }
};
SOAP.queryServices({
    cType:"http",
    oAsync:oNotifications,
    aDomains:[ServiceDiscovery.local, ServiceDiscovery.DNS]
});
```

The output depends on the current network environment; if there are no services advertised by DNS Service Discovery, the example will produce no output. The following is a representative output:

```
ADD: My Web Server in domain local.
ADD: Joe's Web Server in domain local.
ADD: Example.org Web Server in domain example.org.
```

<a id="96557"></a>
<a id="resolveservice"></a>
<a id="id985"></a>
#### resolveService

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | All |

Allows a service name to be bound to a network address and port in order for a connection to be made. The connection information is returned asynchronously and should be treated as temporary since the network location of a service may change over time (for example, if a DHCP lease expires or if a service moves to a new server).

> **Note**
>
> Beginning with Acrobat 8.0, this method is deprecated, new services should use `Net.Discovery.resolveService`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cType` | The DNS SRV Service Name to resolve. |
| `cDomain` | The domain that the service was located in. |
| `cService` | The service name to resolve. |
| `oResult` | An object that will be called when the service is resolved.  See oResult. |

**Returns**

A service query object that manages the duration of the resolve. The resolve will continue until one of the following conditions is met:

- The service query object returned from `resolveService` is garbage collected.
- The `resolve` method of the `oResult` object is called indicating that the operation completed (either by resolving the service, error, or a timeout).
- The `stop` method of the service query object returned from `resolveService` is called.

| Method | Description |
|--------|-------------|
| `stop` | Causes the resolve to terminate. This method can be called from a notification callback but the operation will not stop until idle time. |

**Exceptions**

Standard Acrobat exceptions.

<a id="20694"></a>
<a id="oresult-parameter"></a>
<a id="oresult"></a>
#### oResult parameter

The `oResult` object is a notification object that will be called when the service is resolved. The notification methods will not be called until the `resolveService` method returns and are called during idle processing. The `oResult` parameter should implement the following method:

| Method | Description |
|--------|-------------|
| `resolve` | This method is called with two parameters (`nStatus` and `oInfo`) when the service is resolved or if it cannot be resolved.   The parameter `nStatus` is the state indicating if the service could be resolved (see below). If the service was successfully resolved, the `oInfo` object, an instance of the `ServiceInfo` object (see below), specifies the connection information. |

The `nStatus` parameter passed to the resolve method can have one of the following values:

| Value | Description |
|-------|-------------|
| `0` | The service was successfully resolved. |
| `1` | The service timed out before being resolved. The default timeout in Acrobat 7 or later is 60 seconds. |
| `-1` | There was an networking error trying to resolve the service. |

The `ServiceInfo` object passed to the resolve method has the following properties:

| Property | Description |
|----------|-------------|
| `target` | The IP address or DNS name of the machine supplying the service. |
| `port` | The port on the machine supplying the service. |
| `info` | An object with name - value pairs that the service has supplied. For example, in the case of an HTTP service, the path property will contain the path on the web service so that the service URL would be `http://<target>:<port>/<info["path"]>)`. |

Example: This example code will produce different output depending on where it is run. If there are no services advertised by DNS Service Discovery, this example will produce no output.

```
var oNotifications =
{
    resolve: function(status, info)
    {
        if(status == 0)
            console.println("RESOLVE: http://"
                + info.target + ":" + info.port + "/"
                + info.info.path);
        else console.println("ERROR: " + status);
    }
};
SOAP.resolveService({
    cType: "http",
    cDomain: "local.",
    cService: "Joe's Web Server",
    oResult: oNotifications
});
```

The output depends on the current network environment-the following is a representative output:

```
RESOLVE: http://172.16.0.0:80/index.html
```

<a id="74380"></a>
<a id="id986"></a>
<a id="id987"></a>
#### request

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | F |

Initiates a remote procedure call (RPC) or sends an XML message to a SOAP HTTP endpoint. The method either waits for the endpoint to reply (synchronous processing) or calls a method on the notification object (asynchronous processing).

> **Note**
>
> Beginning with Acrobat 8.0, this method is deprecated, new services should use `Net.SOAP.request`. Not supported in Acrobat Reader.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cURL` | The URL for a SOAP HTTP endpoint. The URL method must be one of: * *http* : Connect to a server at a URI on a port. For example, [http://serverName:portNumber/URI](http://serverName:portNumber/URI) * *https* : Connect to a secured (SSL) server at a URI on a port.  For example, [https://serverName:portNumber/URI](https://serverName:portNumber/URI) |
| `oRequest` | An object that specifies the remote procedure name and parameters or the XML message to send.  See Additional notes on the oRequest parameter. |
| `oAsync` | (optional) An object that specifies that the method invocation will occur asychronously. The default is for the request to be made synchronously. The object has been modified in Acrobat 7.0.  (Acrobat 6.0) The `oAsync` object literal must have a function called `response` that will be called with two parameters (`oResult` and `cURI)` when the response returns. `oResult` is the same result object that would have been returned from the request call if it was called synchronously. `cURI` is the URI of the endpoint that the request was made to.  (Acrobat 7.0) The `oAsync` object response callback has the following parameters: * *response*: The response object from the SOAP request. * *uri*: The URI that the SOAP request was made to. * *exception*: An exception object (see the exceptions below) if there was an error, `null` otherwise. * *header*: A response SOAP header (see the description of the `oRespHeader` parameter) or `null` if there are no response headers. |
| `cAction` | (optional) In SOAP 1.1, this parameter is passed as the SOAPAction header. In SOAP 1.2, this parameter is passed as the action parameter in the Content-Type header.  The default is for the action to be an empty string.  The SOAPAction is a URN written to an HTTP header used by firewalls and servers to filter SOAP requests. The WSDL file for the SOAP service or the SOAP service description will usually describe the SOAPAction header required (if any). |
| `bEncoded` | (optional) Encoded the request using the SOAP Encoding described in the SOAP Specification. Otherwise, the literal encoding is used.  The default is `true`. |
| `cNamespace` | (optional) A namespace for the message schema when the request does not use the SOAP Encoding.  The default is to omit the schema declaration. |
| `oReqHeader` | (optional, Acrobat 7.0) An object that specifies a SOAP header to be included with the request. The default is to send a request with only a SOAP Body.  The object is specified in the same way as the `oRequest` object except for two additional properties that can be specified in the request description: * *soapActor*: The recipient (or actor specified as a URI) that the SOAP header should be processed by. The default is the first recipient to process the request. * *soapMustUnderstand*: A Boolean value indicating that the request body cannot be interpreted if this header type is not understood by the recipient. The default is that understanding the header is optional. |
| `oRespHeader` | (optional, Acrobat 7.0) An object that will be populated with the SOAP headers returned when the method completes if the function is being called synchronously (the header will be passed to the `oAsync` callback method otherwise).  The default is for the headers not to be returned.  See the description of the `cResponseStyle` parameter for the object format. |
| `cVersion` | (optional, Acrobat 7.0) The version of the SOAP protocol to use when generating the XML Message-either 1.1 or 1.2.  The default is to use “SOAPVersion.version\_1\_1”. |
| `oAuthenticate` | (optional, Acrobat 7.0) An object that specifies how to handle HTTP authentication or credentials to use for Web Service Security. The default is to present a user interface to the user to handle HTTP authentication challenges for BASIC and DIGEST authentication modes. The `oAuthenticate` object can have the following properties: * *Username*: A string containing the user name to use for authentication. * *Password*: A string containing the credential to use. * *UsePlatformAuth*: A Boolean value indicating that platform authentication should be used. If `true`, `Username` and `Password` are ignored and the underlying platform networking code is used. This may cause an authentication UI to be shown to the user and/or the credentials of the currently logged in user to be used. The default is `false` and is only supported on the Windows platform. |
| `cResponseStyle` | (optional, Acrobat 7.0) An enumerated type indicating how the return value (in the case of the SOAP Body) and the `oRespHeader` object (in the case of a SOAP header) will be structured: * *SOAPMessageStyle.JS*: (Default) The response will be an object describing the SOAP Body (or SOAP Header) of the returned message (this is the result that Acrobat 6.0 produced). This is recommended when using the SOAP encoding for the request but is not ideal when using the literal encoding-using the XML or Message style is better. * *SOAPMessageStyle.XML*: The response will be a stream object containing the SOAP Body (or SOAP Header) as an XMLfragment. If there are any attachments associated with the response, the Stream object will have an object property `oAttachments`. The object keys are the unique names for the attachment parts and the value must be a Stream object containing the attachment contents. * *SOAPMessageStyle.Message*: The response will be an object describing the SOAP Body (or SOAP Header) corresponding to the XML Message.  This differs from the JavaScript response style in the following ways: * XML Elements are returned as an array of objects rather than an object to maintain order and allow elements with the same name. * XML Attributes are preserved using the `soapAttributes` property. * Namespaces are processed and returned in the `soapName` and `soapQName` properties. * The content of an element is in the `soapValue` property. |
| `cRequestStyle` | (optional, Acrobat 7.0.5) Allows the interpretation of `oRequest` to be altered. The following values are permitted: * *SOAPRequestStyle.SOAP*: (the default) The request is made using the SOAP messaging model. * *SOAPRequestStyle.RawPost*: The `oRequest` parameter is used as the request body for an HTTP Post. `oRequest` must be a `ReadStream` object. If this method is called within the context of a document, the document must be open in the browser. Additionally, the origination URL of the document (scheme, server, and port) must match the origination of the `cURL` parameter. The response is a `ReadStream` object with the response from the request. |
| `cContentType` | (optional, Acrobat 7.0.5) Allows the HTTP content-type header to be specified. The default is to use the SOAP messaging HTTP content-type. |

**Returns**

A response object if the method was called synchronously (that is, there is no `oAsync` parameter) or nothing if the method was called asynchronously. See the description of `cResponseStyle` above for the object description.

The SOAP types in the result are mapped to JavaScript types as follows:

| SOAP type | JavaScript type |
|-----------|-----------------|
| xsd:string | String |
| xsd:integer | Number |
| xsd:float | Number |
| xsd:dateTime | Date |
| xsd:boolean | Boolean |
| xsd:hexBinary | `ReadStream` object |
| xsd:base64Binary | `ReadStream` object |
| SOAP-ENC:base64 | `ReadStream` object |
| SOAP-ENC:Array | Array |
| No Type Information | String |

**Exceptions**

`SOAPError` is thrown when the SOAP endpoint returns a SOAPFault. The `SOAPError` Exception object has the following properties:

| Property | Description |
|----------|-------------|
| `faultCode` | A string indicating the SOAP Fault Code for this fault. |
| `faultActor` | A string indicating the SOAP Actor that generated the fault. |
| `faultDetail` | A string indicating detail associated with the fault. |

`NetworkError` is thrown when there is a failure from the underlying HTTPtransport layer or in obtaining a Network connection. The NetworkError Exception object has the property `statusCode`, which is an HTTP Status code or –1 if the network connection could not be made.

Standard Acrobat exceptions can also be thrown.

> **Note**
>
> If the method was called asynchronously, the exception object may be passed to the `response` callback method.

<a id="57773"></a>
**Additional notes on the oRequest parameter**

The `oRequest` parameter is an object literal that specifies the remote procedure name and the parameters to call. The object literal uses the fully qualified method name of the remote procedure as the key. The namespace should be separated from the method name by a colon.

For example, if the namespace for the method is `http://mydomain/methods` and the method name is `echoString`, the fully qualified name would be `http://mydomain/methods:echoString`. The value of this key is an object literal, each key is a parameter of the method, and the value of each key is the value of the corresponding parameter of the method. For example:

```
oRequest: {
    "http://soapinterop.org/:echoString":{inputString: "Echo!"}
}
```

When passing parameters to a remote procedure, JavaScript types are bound to SOAP types automatically as listed in the table:

| JavaScript type | SOAP type |
|-----------------|-----------|
| String | xsd:string |
| Number | xsd:float |
| Date | xsd:dateTime |
| Boolean | xsd:boolean |
| `ReadStream` object | SOAP-ENC:base64 |
| Array | SOAP-ENC:Array |
| Other | No type information |

> **Note**
>
> The `xsd` namespace refers to the XML Schema Datatypes namespace `http://www.w3.org/2001/XMLSchema`. The `SOAP-ENC` namespace refers to the SOAP Encoding namespace `http://schemas.xmlsoap.org/soap/encoding/`.

The `oRequest` object supports the following properties:

| Property | Description |
|----------|-------------|
| `soapType` | The SOAP type that will be used for the value when generating the SOAP message. It is useful when a datatype is needed other than the automatic datatype binding described above. The type should be namespace qualified using the `<namespace>:<type>` notation, for example  `http://mydomain/types:myType`  However, the `xsd` (XMLSchema Datatypes), `xsi` (XMLSchema Instance), and SOAP-ENC (SOAP Encoding) namespaces are implicitly defined in the SOAP message, so the `soapType` can use them, as in `xsd:int` for the XMLSchema Datatype Integer type. |
| `soapValue` | (Acrobat 6.0) The value that will be used when generating the SOAP message. It can be a string or a `ReadStream` object. `soapValue` is passed unescaped (that is, not XML Entity escaped). For example, `<` is not converted to `&lt;` in the XML Message. Consequently, `soapValue` can be a raw XML fragment that will be passed to the XML Message.  (Acrobat 7.0) `soapValue` can now also be an array of nodes that are an ordered set of children of the node in the request message. |
| `soapName` | The element name that will be used when generating the SOAP message instead of the key name in the object literal.  For example, integers are not supported in JavaScript, but an integer parameter to a SOAP method can be constructed as follows:  `var oIntParameter = { soapType: "xsd:int", soapValue: "1" };`  Later, the `oRequest` parameter for the `SOAP.request` method might be this:  `oRequest: { "http://soapinterop.org/:echoInteger": { inputInteger: oIntParameter } }`  Example 1 below shows this technique. |
| `soapAttributes` | (Acrobat 7.0) An object specifying XML attributes to be included when building the element corresponding to the request node. The object keys are the attribute names and the corresponding value is the attribute value. |
| `soapQName` | (Acrobat 7.0) An object specifying the namespace qualified name (QName) of the request node. For example, in the element `<ns:local xmlns:ns="urn:example.org">`, the element name is a QName consisting of a local name (`"local"`) and a namespace (`"urn:example.org"`).   This object has two properties: * *localName*: A string indicating the local name of the QName. * *nameSpace*: A string indicating the namespace of the QName. |
| `soapAttachment` | (Acrobat 7.0) A Boolean value indicating that the `soapValue` contents of the node should be encoded as an attachment according to the SwA specification. The `soapValue` *must* be a stream if the corresponding `soapAttachment` property is `true`, otherwise an exception will be thrown. |
| `soapParamOrder` | (Acrobat 7.0) An array indicating the order in which RPC parameters should be sent to the server. The array is a set of strings with the parameter names. This value is only applicable when `bEncoding` is `true`. |

<a id="44692"></a>
Example 1: Use `request` to initiate a remote procedure call for echo services.

A service WSDL Document URL is needed. It can be obtained from the “Round 2 Interop Services - using SOAP 1.2” section at the following URL: [http://www.whitemesa.com/interop.htm](http://www.whitemesa.com/interop.htm).

```
   var cURL =
<get a URL for this service from
            http://www.whitemesa.com/interop.htm>;

   var cTestString = "This is my test string";

   // Call the echoString SOAP method -- it is an RPC Encoded method
   var response = SOAP.request(
   {
       cURL: cURL,
       oRequest: {
           "http://soapinterop.org/:echoString": {
               inputString: cTestString
           }
       },
       cAction: "http://soapinterop.org/"
   });

   var result =

    response["http://soapinterop.org/:echoStringResponse"]["return"];

   // This should be the same as cTestString
   console.println(result + " == " + cTestString);

   // Call the echoInteger SOAP method -- JavaScript doesn't support
   // integers so we make our own integer object.
   var oTestInt =
   {
       soapType: "xsd:int",
       soapValue: "10"
   };

   var response = SOAP.request(
   {
       cURL: cURL,
       oRequest: {
           "http://soapinterop.org/:echoInteger": {
               inputInteger: oTestInt
           }
       },
       cAction: "http://soapinterop.org/"
   });

   var result =

    response["http://soapinterop.org/:echoIntegerResponse"]["return"];

   // This should be the same as oTestInt.soapValue
   console.println(result + " == " + oTestInt.soapValue);
```

This produces the following output:

```
This is my test string == This is my test string
10 == 10
```

Example 2: Set a SOAP Header and gets it back.

```
var cURL = <URL of a Service>;
var NS = "http://www.example.com/soap/:";
var oHeader = {};
oHeader[NS + "testSession"] =
{
    soapType: "xsd:string",
    soapValue: "Header Test String"
};
var oResultHeader = {};
var oRequest = {};
oRequest[NS + "echoHeader"] = {};
var response = SOAP.request(
{
    cURL: cURL,
    oRequest: oRequest,
    cAction: "http://soapinterop.org/",
    oReqHeader: oHeader,
    oRespHeader: oResultHeader
});
```

Example 3: A request for echo services with HTTP Authentication.

```
var oAuthenticator =
{
    Username: "myUserName",
    Password: "myPassword"
};
var response = SOAP.request(
{
    cURL: cURL,
    oRequest: {
        "http://soapinterop.org/:echoString":
        {
            inputString: cTestString
        }
    },
    cAction: "http://soapinterop.org/",
    oAuthenticate: oAuthenticator
});
```

<a id="71544"></a>
<a id="id988"></a>
<a id="id989"></a>
#### response

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | F |

Initiates a remote procedure call (RPC) or sends an XML message to a SOAP HTTP endpoint without waiting for a reply.

> **Note**
>
> Beginning with Acrobat 8.0, this method is deprecated, new services should use `Net.SOAP.response`. Not supported in Acrobat Reader.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cURL` | The URL for a SOAP HTTP endpoint. The URL method must be one of these: * *http*: Connect to a server at a URI on a port. For example, [http://serverName:portNumber/URI](http://serverName:portNumber/URI) * *https*: Connect to a secured (SSL) server at a URI on a port.  For example, [https://serverName:portNumber/URI](https://serverName:portNumber/URI)  See the `cURL` parameter of `SOAP.` request. |
| `oRequest` | An object that specifies the remote procedure name and parameters or the XML message to send.  See the `oRequest` parameter of `SOAP.` request. |
| `cAction` | (optional) The SOAP Action header for this request as specified by the SOAP Specification.  The default is for the SOAP Action to be empty.  See the `cAction` parameter of `SOAP.` request. |
| `bEncoded` | (optional) A Boolean value specifying whether the request was encoded using the SOAP Encoding described in the SOAP Specification. The default is `true`. |
| `cNamespace` | (optional) A namespace for the message schema when the request does not use the SOAP Encoding (the `bEncoded` flag is `false`).   The default is to have no namespace. |
| `oReqHeader` | (optional, Acrobat 7.0) An object that specifies a SOAP header to be included with the request.  The default is to send a request with only a SOAP Body.  See the `oReqHeader` parameter of der `SOAP.` request. |
| `cVersion` | (optional, Acrobat 7.0) The version of the SOAP protocol to use.  The default is to use “SOAPVersion.version\_1\_1”.  See the `cVersion` parameter of `SOAP.` request. |
| `oAuthenticate` | (optional, Acrobat 7.0) An object that specifies the type of authentication scheme to use and to provide credentials.  The default is for an interactive UI to be displayed if HTTP authentication is encountered.  See the `oAuthenticate` parameter of `SOAP.` request. |
| `cRequestStyle` | (optional, Acrobat 7.0.5) Same as `cRequestStyle` for `SOAP.` request, except that there is no response from the server. |
| `cContentType` | (optional, Acrobat 7.0.5) Same as `cContentType` for `SOAP.` request, except that there is no response from the server. |

**Returns**

Boolean

**Exceptions**

If there is a problem at the networking level, such as an unavailable endpoint, a `NetworkError` will be thrown.

<a id="52655"></a>
Example: See request.

<a id="75761"></a>
<a id="streamdecode"></a>
<a id="id990"></a>
#### streamDecode

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Allows the `oStream` object to be decoded with the specified encoding type, `cEncoder`. It returns a decoded `ReadStream` object. Typically, it is used to access data returned as part of a SOAP method that was encoded in Base64 or hex encoding.

> **Note**
>
> Beginning with Acrobat 8.0, this method is deprecated, new services should use `Net.streamDecode` (see Net methods).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oStream` | A stream object to be decoded with the specified encoding type. |
| `cEncoder` | Permissible values for this string are “hex” (hex-encoded) and “base64” (Base 64-encoded). |

**Returns**

`ReadStream` object

<a id="22036"></a>
<a id="streamdigest"></a>
<a id="id991"></a>
#### streamDigest

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Allows the `oStream` object to be digested with the specified encoding type, `cEncoder`. It returns a `ReadStream` object containing the computed digest of the `oStream`. Typically, this is used to compute a digest to validate the integrity of the original data stream or as part of an authentication scheme for a web service.

> **Note**
>
> Beginning with Acrobat 8.0, this method is deprecated, new services should use `Net.streamDigest` (see Net methods).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oStream` | A stream object to compute the digest of, using the specified message digest algorithm. |
| `cEncoder` | The digest algorithm to use. The `cEncoder` parameter must be one of the following values: * *StreamDigest.MD5*: Digest the content using the MD5 Digest Algorithm (see RFC 1321). * *StreamDigest.SHA1*: Digest the content using the SHA-1 Digest Algorithm (see RFC 3174). |

**Returns**

A `ReadStream` object with the binary digest of the stream. To be used as a string, the result must be converted to a text format such as Base64 or hex using `SOAP.streamEncode`.

Example: Digest a string by first converting it to a stream, then calling streamDigest.

```
var srcStm = SOAP.streamFromString("This is a string I want to digest");
var digest = SOAP.streamDigest(srcStm, StreamDigest.SHA1);
```

<a id="25086"></a>
<a id="streamencode"></a>
<a id="id992"></a>
#### streamEncode

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This function encodes a stream object. Typically, it is used to pass data as part of a SOAP method when it must be encoded in Base 64 or hex encoding.

> **Note**
>
> Beginning with Acrobat 8.0, this method is deprecated, new services should use `Net.streamEncode` (see Net methods).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oStream` | A stream object to be encoded with the specified encoding type. |
| `cEncoder` | A string specifying the encoding type. Permissible values are “hex” (for hex-encoded) and “base64” (base 64-encoded). |

**Returns**

A `ReadStream` object that has the appropriate encoding applied.

<a id="82501"></a>
<a id="streamfromstring"></a>
<a id="id993"></a>
#### streamFromString

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This function converts a string to a `ReadStream` object. Typically, this is used to pass data as part of a SOAP method.

**Parameters**

| Property | Description |
|----------|-------------|
| `cString` | The string to be converted. |

**Returns**

`ReadStream` object

<a id="73242"></a>
<a id="stringfromstream"></a>
<a id="id994"></a>
#### stringFromStream

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This function converts a `ReadStream` object to a string. Typically, this is used to examine the contents of a stream object returned as part of a response to a SOAP method.

**Parameters**

| Property | Description |
|----------|-------------|
| `oStream` | The `ReadStream` object to be converted. |

**Returns**

String

<a id="11412"></a>
<a id="sound"></a>
<a id="id995"></a>
## Sound

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This object represents a sound that is stored in the document. The array of all Sound objects can be obtained from the Doc sounds property. See also Doc methods getSound, importSound, and deleteSound.

<a id="sound-properties"></a>
<a id="id996"></a>
### Sound properties

<a id="79739"></a>
<a id="id997"></a>
<a id="id998"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| Deprecated | No | No | No | String | R/W |

The name associated with this Sound object.

Example: Write the names to the console of all embedded sounds in the current document.

```
console.println("Dumping all sound objects in this document.");
var s = this.sounds;
for (var i = 0; i < this.sounds.length; i++)
    console.println("Sound[" + i + "]=" + s[i].name);
```

<a id="sound-methods"></a>
<a id="id999"></a>
### Sound methods

<a id="17744"></a>
<a id="pause"></a>
<a id="id1000"></a>
#### pause

Pauses the currently playing sound. If the sound is already paused, the sound play is resumed.

<a id="33208"></a>
<a id="play"></a>
<a id="id1001"></a>
#### play

Plays the sound asynchronously.

<a id="92859"></a>
<a id="id1002"></a>
<a id="id1003"></a>
#### stop

Stops the currently playing sound.

<a id="63410"></a>
<a id="span"></a>
<a id="id1004"></a>
## Span

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

A generic object that represents a length of text and its associated properties in a rich text form field or annotation. A rich text value consists of an array of span objects representing the text and formatting.

> **Note**
>
> Span objects are a copy of the rich text value of the field or annotation. To modify and reset the rich text value to update the field, use the Field object `richValue` property, or the `Annotation` object property `richContents`, and the `event` object properties `richValue`, `richChange`, and `richChangeEx`.

<a id="span-properties"></a>
<a id="id1005"></a>
### Span properties

<a id="52413"></a>
<a id="id1006"></a>
<a id="id1007"></a>
#### alignment

| Type | Access |
|------|--------|
| String | R/W |

The horizontal alignment of the text. Alignment for a line of text is determined by the first span on the line. The values of `alignment` are

```
left
center
right
```

The default value is `left`.

Example: The example following superscript uses `alignment`.

<a id="21820"></a>
<a id="fontfamily"></a>
<a id="id1008"></a>
#### fontFamily

| Type | Access |
|------|--------|
| String | R/W |

The font family used to draw the text. It is an array of family names to be searched for in order. The first entry in the array is the font name of the font to use. The second entry is an optional generic family name to use if an exact match of the first font is not found. The generic family names are

```
symbol, serif, sans-serif, cursive, monospace, fantasy
```

The default generic family name is `sans-serif`.

Example: Set the `defaultStyle` font family for a rich text field.

```
f = this.getField("Text1");
style = f.defaultStyle;

// If Courier Std is not found on the user's system, use a monospace font
style.fontFamily = ["Courier Std", "monospace" ];
f.defaultStyle = style;
```

<a id="29520"></a>
<a id="fontstretch"></a>
<a id="id1009"></a>
#### fontStretch

| Type | Access |
|------|--------|
| String | R/W |

Specifies the normal, condensed or extended face from a font family to be used to draw the text. The values of `fontStretch` are

```
ultra-condensed, extra-condensed, condensed, semi-condensed, normal,

 semi-expanded, expanded, extra-expanded, ultra-expanded
```

The default value is `normal`.

<a id="58492"></a>
<a id="fontstyle"></a>
<a id="id1010"></a>
#### fontStyle

| Type | Access |
|------|--------|
| String | R/W |

Specifies the text is drawn with an italic or oblique font.

```
italic
normal
```

The default is `normal`.

<a id="72325"></a>
<a id="fontweight"></a>
<a id="id1011"></a>
#### fontWeight

| Type | Access |
|------|--------|
| Number | R/W |

The weight of the font used to draw the text. For the purposes of comparison, normal is anything under 700 and bold is greater than or equal to 700. The values of `fontWeight` are

```
100,200,300,400,500,600,700,800,900
```

The default value is 400.

<a id="62996"></a>
<a id="strikethrough"></a>
<a id="id1012"></a>
#### strikethrough

| Type | Access |
|------|--------|
| Boolean | R/W |

If `strikethrough` is `true`, the text is drawn with a strikethrough. The default is `false`.

<a id="43036"></a>
<a id="subscript"></a>
<a id="id1013"></a>
#### subscript

| Type | Access |
|------|--------|
| Boolean | R/W |

Specifies the text is subscript. If `true`, subscript text is drawn with a reduced point size and a lowered baseline. The default is `false`.

<a id="42303"></a>
<a id="superscript"></a>
<a id="id1014"></a>
#### superscript

| Type | Access |
|------|--------|
| Boolean | R/W |

Specifies the text is superscript. If `true`, superscript text is drawn with a reduced point size and a raised baseline. The default is `false`.

Example: Write rich text to a rich text field using various properties. See the Field object richValue property for more details and examples.

```
var f = this.getField("myRichField");

// Create an array to hold the Span objects
var spans = new Array();

// Each Span object is an object, so we must create one
spans[0] = new Object();
spans[0].alignment = "center";
spans[0].text = "The answer is x";

spans[1] = new Object();
spans[1].text = "2/3";
spans[1].superscript = true;

spans[2] = new Object();
spans[2].superscript = false;
spans[2].text = ".  ";

spans[3] = new Object();
spans[3].underline = true;
spans[3].text = "Did you get it right?";
spans[3].fontStyle = "italic";
spans[3].textColor = color.red;

// Now assign our array of Span objects to the field using

 // field.richValue
f.richValue = spans;
```

<a id="51541"></a>
<a id="id1015"></a>
<a id="id1016"></a>
#### text

The text within the span.

| Type | Access |
|------|--------|
| String | R/W |

Example: The example following superscript uses `text`.

<a id="21770"></a>
<a id="id1017"></a>
<a id="id1018"></a>
#### textColor

A color array representing the RGB color to be used to draw the text (see the color object). The default color is black.

| Type | Access |
|------|--------|
| Color Array | R/W |

Example: The example following superscript uses `textColor`.

<a id="92976"></a>
<a id="id1019"></a>
<a id="id1020"></a>
#### textSize

The point size of the text. The value of `textSize` can be any number between 0 and 32767, inclusive. A text size of zero means to use the largest point size that will allow all text data to fit in the field’s rectangle.

The default text size is 12.0.

| Type | Access |
|------|--------|
| Number | R/W |

Example: The example following the Field object richValue property uses `textSize`.

<a id="31477"></a>
<a id="underline"></a>
<a id="id1021"></a>
#### underline

If `underline` is `true`, the text is underlined. The default is `false`.

| Type | Access |
|------|--------|
| Boolean | R/W |

Example: The example following superscript uses `underline`.

<a id="11682"></a>
<a id="spell"></a>
<a id="id1022"></a>
## spell

This object allows users to check the spelling of Comments and Form Fields and other spelling domains. To be able to use the `spell` object, the user must have installed the Acrobat Spelling plug-in and the spelling dictionaries.

> **Note**
>
> The `spell` object is not available in versions of Adobe Reader prior to 7.0. In Adobe Reader 7.0, all properties and methods—with the exception of `customDictionaryCreate`, `customDictionaryDelete` and `customDictionaryExport` —are accessible.

<a id="spell-properties"></a>
<a id="id1023"></a>
### spell properties

<a id="83162"></a>
<a id="id1024"></a>
<a id="id1025"></a>
#### available

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0.  For Adobe Reader, 7.0 or later. | No | No | All | Boolean | R |

`true` if the `spell` object is available.

Example:

```
console.println("Spell checking available: " + spell.available);
```

<a id="13633"></a>
<a id="dictionarynames"></a>
<a id="id1026"></a>
#### dictionaryNames

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0. For Adobe Reader, 7.0 or later. | No | No | All | Array | R |

An array of available dictionary names. A subset of this array can be passed to `check`, `checkText`, and `checkWord`, and to `spellDictionaryOrder` to force the use of a specific dictionary or dictionaries and the order they should be searched.

A listing of valid dictionary names for the user’s installation can be obtained by executing `spell.dictionaryNames` from the console.

<a id="89351"></a>
<a id="dictionaryorder"></a>
<a id="id1027"></a>
#### dictionaryOrder

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0. For Adobe Reader, 7.0 or later. | No | No | All | Array | R |

The dictionary array search order specified by the user on the Spelling Preferences panel. The Spelling plug-in will search for words first in the Doc `spellDictionaryOrder` array if it has been set for the document, followed by this array of dictionaries.

<a id="64363"></a>
<a id="domainnames"></a>
<a id="id1028"></a>
#### domainNames

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0. For Adobe Reader, 7.0 or later. | No | No | All | Array | R |

The array of spelling domains that have been registered with the Spelling plug-in by other plug-ins. A subset of this array can be passed to `check` to limit the scope of the spell check.

Depending on the user’s installation, valid domains can include:

```
Everything
Form Field
All Form Fields
Comment
All Comments
```

<a id="62448"></a>
<a id="languages"></a>
<a id="id1029"></a>
#### languages

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0. For Adobe Reader, 7.0 or later. | No | No | All | Array | R |

This property returns the array of available ISO 639-2/3166-1 language/country codes. A subset of this array can be passed to the `check`, `checkText`, `checkWord`, and `customDictionaryCreate` methods, and to the Doc `spellLanguageOrder` property to force the use of a specific language or languages and the order they should be searched.

Depending on the user’s installation, valid language/country codes can include codes from the following list.

| Code | Description |
|------|-------------|
| `ca_ES` | Catalan |
| `cs_CZ` | Czech |
| `da_DK` | Danish |
| `nl_NL` | Dutch |
| `en_CA` | English-Canadian |
| `en_GB` | English-UK |
| `en_US` | English-US |
| `fi_FI` | Finnish |
| `fr_CA` | French-Canadian |
| `fr_FR` | French |
| `de_DE` | German |
| `de_CH` | German-Swiss |
| `el_GR` | Greek |
| `hu_HU` | Hungarian |
| `it_IT` | Italian |
| `nb_NO` | Norwegian-Bokmal |
| `nn_NO` | Norwegian-Nynorsk |
| `pl_PL` | Polish |
| `pt_BR` | Portuguese-Brazil |
| `pt_PT` | Portuguese |
| `ru_RU` | Russian |
| `es_ES` | Spanish |
| `sv_SE` | Swedish |
| `tr_TR` | Turkish |

> **Note**
>
> In Acrobat 7.0, the entries in this array are different from the entries returned in Acrobat 6.0. On input from JavaScript, the Acrobat 6.0 ISO codes are internally mapped onto the new ISO codes in order not to break any JavaScript code developed for Acrobat 6.0. Codes are not translated on output.

Example: List all available language codes.

```
console.println( spell.languages.toSource() );
```

<a id="64159"></a>
<a id="languageorder"></a>
<a id="id1030"></a>
#### languageOrder

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0. For Adobe Reader, 7.0 or later. | No | No | All | Array | R |

The dictionary search order as an array of ISO 639-2, 3166 language codes. It is the order specified by the user on the Spelling Preferences panel. The Spelling plug-in searches for words first in the Doc `spellLanguageOrder` array if it has been set for the document, followed by this array of languages.

Example: Get a listing of the dictionary search order.

```
console.println( spell.languageOrder.toSource() );
```

<a id="spell-methods"></a>
<a id="id1031"></a>
### spell methods

-

<a id="81814"></a>
<a id="adddictionary"></a>
<a id="id1032"></a>
#### addDictionary

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| deprecated | No | No | P, X |

> **Note**
>
> Beginning with Acrobat 6.0, this method is no longer supported and always returns `false`. Use the customDictionaryOpen method instead.

Adds a dictionary to the list of available dictionaries.

A dictionary actually consists of four files: `DDDxxxxx.hyp`, `DDDxxxxx.lex`, `DDDxxxxx.clx`, and `DDDxxxxx.env`. The `cFile` parameter must be the device-independent path of the `.hyp` file, for example, “`/c/temp/testdict/TST.hyp` “. The Spelling plug-in will look in the parent directory of the TST.hyp file for the other three files. All four file names must start with the same unique 3 characters to associate them with each other, and they must end with the dot three extensions listed above, even in Mac OS.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cFile` | The device-independent path to the dictionary files. |
| `cName` | The dictionary name used in the spelling dialog box. It can be used as the input parameter to the `check`, `checkText`, and `checkWord` methods. |
| `bShow` | (optional) If `true` (the default), then the `cName` value is combined with “User”. That name is shown in all lists and menus. For example, if `cName` is “Test”, “User: Test” is added to all lists and menus.  If `false`, this custom dictionary is not shown in any lists or menus. |

**Returns**

`false`

<a id="47325"></a>
<a id="addword"></a>
<a id="id1033"></a>
#### addWord

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0. For Adobe Reader, 7.0 or later. | P | Yes | All |

Adds a new word to a dictionary. See also the removeWord.

> **Note**
>
> Beginning with Acrobat 7.0, this method is allowed only during a console or batch event. See priv.

Internally, the `spell` object scans the user “Not-A-Word” dictionary and removes the word if it is listed there. Otherwise, the word is added to the user dictionary. The actual dictionary is not modified.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cWord` | The new word to add. |
| `cName` | (optional) The dictionary name or language code. An array of the currently installed dictionaries can be obtained using `dictionaryNames` or `languages`. |

**Returns**

`true` if successful, otherwise, `false`.

<a id="46770"></a>
<a id="check"></a>
<a id="id1034"></a>
#### check

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0.  For Adobe Reader, 7.0 or later. | No | No | All |

Presents the Spelling dialog box to allow the user to correct misspelled words in form fields, annotations, or other objects.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `aDomain` | (optional) An array of Doc that should be checked by the Spelling plug-in, for example, form fields or comments. When you do not supply an array of domains, the “EveryThing” domain will be used. An array of the domains that have been registered can be obtained using the `domainNames` property. |
| `aDictionary` | (optional) The array of dictionary names or language codes that the spell checker should use. The order of the dictionaries in the array is the order the spell checker will use to check for misspelled words. An array of the currently installed dictionaries can be obtained using `spell.dictionaryNames` or `spell.languages`. When this parameter is omitted, the `spellDictionaryOrder` list will be searched followed by the `dictionaryOrder` list. |

**Returns**

`true` if the user changed or ignored all the flagged words. When the user dismisses the dialog box before checking everything, the method returns `false`.

Example: Set the dictionaries, then spell check the comments and form fields of the current document. Reports back to the console.

```
var dictionaries = ["de", "French", "en-GB"];
var domains = ["All Form Fields", "All Annotations"];
if (spell.check(domains, dictionaries) )
    console.println("You get an A for spelling.");
else
    console.println("Please spell check this form before you submit.");
```

<a id="17744"></a>
<a id="checktext"></a>
<a id="id1035"></a>
#### checkText

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0. For Adobe Reader, 7.0 or later. | No | No | All |

Presents the spelling dialog box to allow the user to correct misspelled words in the specified string.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cText` | The string to check. |
| `aDictionary` | (optional) The array of dictionary names or language codes that the spell checker should use. The order of the dictionaries in the array is the order the spell checker will use to check for misspelled words. An array of installed dictionaries can be obtained using `spell.dictionaryNames` or `spell.languages`. When this parameter is omitted, the `spellDictionaryOrder` list will be searched followed by the `dictionaryOrder` list. |

**Returns**

The result from the spelling dialog box in a new string.

Example: Spell check a particular field, and update the spelling in the field.

```
var f = this.getField("Text Box")    // A form text box
f.value = spell.checkText(f.value);  // Let the user pick the dictionary
```

<a id="21151"></a>
<a id="checkword"></a>
<a id="id1036"></a>
#### checkWord

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0. For Adobe Reader, 7.0 or later. | No | No | All |

Checks the spelling of a specified word.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cWord` | The word to check. |
| `aDictionary` | (optional) The array of dictionary names or language codes that the spell checker should use, to check for misspelled words. The spell checker uses the dictionaries in the order they appear in the array. An array of installed dictionaries can be obtained using `spell.dictionaryNames` or `spell.languages`. If this parameter is omitted, the `spellDictionaryOrder` list is searched, followed by the `dictionaryOrder` list. |

**Returns**

A `null` object if the word is correct, otherwise an array of alternative spellings for the unknown word.

Example 1: Insert the array of suggested alternative spellings into a list box.

```
var word = "subpinna"; /* misspelling of "subpoena" */
var dictionaries = ["English"];
var f = this.getField("Alternatives") // Alternative spellings list box

 f.clearItems();
f.setItems(spell.checkWord(word, dictionaries));
```

<a id="86751"></a>
Example 2: The following script marks misspelled words in the document with a squiggle annotation whose contents are the suggested alternative spellings. The script can be executed from the console, as a mouse-up action within the document, a menu, or as a batch sequence.

```
var ckWord, numWords;
for (var i = 0; i < this.numPages; i++ )
{
    numWords = this.getPageNumWords(i);
    for (var j = 0; j < numWords; j++)
    {
        ckWord = spell.checkWord(this.getPageNthWord(i, j))
        if ( ckWord != null )
        {
            this.addAnnot({
                page: i,
                type: "Squiggly",
                quads: this.getPageNthWordQuads(i, j),
                author: "A. C. Acrobat",
                contents: ckWord.toString()
            });
        }
    }
}
```

<a id="10279"></a>
<a id="customdictionaryclose"></a>
<a id="id1037"></a>
#### customDictionaryClose

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0. For Adobe Reader, 7.0 or later. | No | No | All |

Closes a custom dictionary that was opened using `customDictionaryOpen` or `customDictionaryCreate`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | Dictionary name used when this dictionary was opened or created. |

**Returns**

`true` if successful, `false` on failure.

<a id="65594"></a>
<a id="customdictionarycreate"></a>
<a id="id1038"></a>
#### customDictionaryCreate

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Use this method to create a new custom dictionary file and add it to the list of available dictionaries.

> **Note**
>
> This method is allowed only during a console or batch event. See priv.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | Dictionary name used in the spelling dialog box. It can be used as the input parameter to `check`, `checkText`, and `checkWord` methods. |
| `cLanguage` | (optional) Use this parameter to associate this dictionary with a language. A list of available languages can be obtained from the spell.languages property. |
| `bShow` | (optional) If `true` (the default), the `cName` parameter is combined with “User: “ and shown that name in all lists and menus. For Example, if `cName` is “Test”, “User: Test” is added to all lists and menus. When `bShow` is `false`, this custom dictionary is not shown in any lists or menus. |

**Returns**

`true` if successful, `false` on failure. This method will fail if the user does not have read and write permission to this directory.

Example: Open a PDF document in Acrobat and execute the following script in the console. This script extracts the first word of each bookmark. If that word is already in a dictionary, it is discarded. An unknown word is added into a newly created dictionary, called JavaScript” in this case.

```
spell.customDictionaryCreate("JavaScript", "en", true);
function GetJSTerms(bm, nLevel)
{
    var newWord = bm.name.match(re);
    var ckWord = spell.checkWord( newWord[0] );
    if ( ckWord != null )
    {
        var cWord = spell.addWord( newWord[0], "JavaScript");
        if ( cWord )  console.println( newWord[0] );
    }
    if (bm.children != null)
    for (var i = 0; i < bm.children.length; i++)
    GetJSTerms(bm.children[i], nLevel + 1);
}
console.println("nAdding New words to the "JavaScript" "

     + "dictionary:");
var re = /^w+/;
GetJSTerms(this.bookmarkRoot, 0);
```

<a id="27386"></a>
<a id="customdictionarydelete"></a>
<a id="id1039"></a>
#### customDictionaryDelete

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Use this method to close and delete a custom dictionary file that was opened by `customDictionaryOpen` or `customDictionaryCreate`.

> **Note**
>
> This method is allowed only during a console or batch event. See priv.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The name of the dictionary to be deleted. This is the name used when this dictionary was opened or created. |

**Returns**

`true` if successful, `false` on failure. This method will fail if the user does not have sufficient file system permission.

Example: Delete a custom dictionary.

```
spell.customDictionaryDelete("JavaScript");
```

<a id="36485"></a>
<a id="customdictionaryexport"></a>
<a id="id1040"></a>
#### customDictionaryExport

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not allowed in Reader: Only available in Acrobat products |

Exports a custom dictionary to a new file that was opened using the spell methods `customDictionaryOpen` or `customDictionaryCreate`.

The user is prompted for an export directory, where the custom dictionary is saved as a `.clam` file using the dictionary name and language specified in `customDictionaryCreate`. For example, if the dictionary name is “JavaScript” and the “en” language as specified when it was created, the export file name will be `JavaScript-eng.clam`.

Exported custom dictionaries can be used in subsequent `customDictionaryOpen` calls.

> **Note**
>
> This method is allowed only during a console or batch event. See priv.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The dictionary name used when this dictionary was opened or created. |

**Returns**

`true` if successful, `false` on failure. This method will fail if the user does not have sufficient file system permission.

Example: Export a custom dictionary, which can then be sent to other users. (See the example that follows customDictionaryCreate.)

```
spell.customDictionaryExport("JavaScript");
```

<a id="30271"></a>
<a id="customdictionaryopen"></a>
<a id="id1041"></a>
#### customDictionaryOpen

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0. For Adobe Reader, 7.0 or later. | No | No | All |

Adds a custom export dictionary to the list of available dictionaries. See customDictionaryExport.

> **Note**
>
> A custom dictionary file can be created using the `customDictionaryCreate` and `customDictionaryExport` methods.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cDIPath` | The device-independent path to the custom dictionary file. |
| `cName` | Dictionary name used in the spelling dialog box. It can be used as the input parameter to `check`, `checkText`, and `checkWord` methods. |
| `bShow` | (optional) If `true`, the default, the `cName` parameter is combined with “User: “ and that name is shown in all lists and menus. For example, if `cName` is “Test”, add “User: Test” is added to all lists and menus. When `bShow` is `false`, this custom dictionary is not shown in any lists or menus. |

**Returns**

`true` if successful, `false` on failure. This method fails if the user does not have read permission for the file.

Example: This example continues the ones following customDictionaryCreate and customDictionaryExport. It adds a custom export dictionary to the list of available dictionaries.

The user places the custom export dictionary in any folder for which there is read/write permission. A particular choice is the user `dictionaries` folder, whose location of can be obtained from the `app.getPath` method.

```
app.getPath("user", "dictionaries");
```

After the export dictionary has been placed, listing it can be made automatic by adding some folder-level JavaScript. The path to the user JavaScripts folder can be obtained by executing

```
app.getPath("user", "javascript");
```

Finally, create a `.js` file in this folder and add the line

```
var myDictionaries = app.getPath("user", "dictionaries");
spell.customDictionaryOpen( myDictionaries, "JavaScripts", true);
```

The next time Acrobat is started, the “JavaScript” dictionary will be open and available.

<a id="68941"></a>
<a id="ignoreall"></a>
<a id="id1042"></a>
#### ignoreAll

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0. For Adobe Reader, 7.0 or later. | No | No | All |

Adds or removes a word from the Spelling ignored-words list of the current document.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cWord` | The word to be added or removed from the ignored list. |
| `bIgnore` | (optional) If `true` (the default), the word is added to the document ignored word list; if `false`, the word is removed from the ignored list. |

**Returns**

`true` if successful. This method throws an exception if no document is open.

Example:

```
var bIgnored = spell.ignoreAll("foo");
if (bIgnored) console.println(""foo" will be ignored);
```

<a id="17528"></a>
<a id="removedictionary"></a>
<a id="id1043"></a>
#### removeDictionary

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| deprecated | No | No | P, X |

> **Note**
>
> Beginning with Acrobat 6.0, this method is no longer supported. The return value of this method is always `false`. Use the customDictionaryClose method.

Removes a user dictionary that was added with `addDictionary`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The name of the dictionary to remove. Must be the same name as was used with `addDictionary`. |

**Returns**

`false`

<a id="37786"></a>
<a id="removeword"></a>
<a id="id1044"></a>
#### removeWord

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0. For Adobe Reader, 7.0 or later. | P | Yes | All |

Removes a word from a dictionary. Words cannot be removed from user dictionaries that were created using either `customDictionaryCreate` or `customDictionaryExport`.

See also addWord.

> **Note**
>
> Internally, the `spell` object scans the user dictionary and removes the previously added word if it is there. Otherwise, the word is added to the user’s “Not-A-Word” dictionary. The actual dictionary is not modified.

As of Acrobat 8.1, this method is only permitted to execute through the console or in a batch process.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cWord` | The word to remove. |
| `cName` | (optional) The dictionary name or language code. An array of installed dictionaries can be obtained using `dictionaryNames` or `languages`. |

**Returns**

`true` if successful, `false` otherwise

<a id="51706"></a>
<a id="userwords"></a>
<a id="id1045"></a>
#### userWords

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0. For Adobe Reader, 7.0 or later. | No | No | All |

Gets the array of words a user has added to, or removed from, a dictionary. See also addWord and checkWord.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | (optional) The dictionary name or language code. An array of installed dictionaries can be obtained using `dictionaryNames` or `languages`. If `cName` is not specified, the default dictionary is used. The default dictionary is the first dictionary specified in the Spelling preferences dialog box. |
| `bAdded` | (optional) If `true`, return the user’s array of added words. If `false`, return the user’s array of removed words. The default is `true`. |

**Returns**

The user’s array of added or removed words.

Example: List the words added to the “JavaScript” dictionary. (See the example that follows the description of customDictionaryCreate.)

```
var aUserWords = spell.userWords({cName: "JavaScript"});
aUserWords.toSource();
```

<a id="32392"></a>
<a id="tableinfo"></a>
<a id="id1046"></a>
## TableInfo

This generic JavaScript object contains basic information about a table. It is returned by `connection.getTableList` and contains the following properties.

| Property | Type | Access | Description |
|----------|------|--------|-------------|
| `name` | String | R | The identifying name of a table. This string can be used in SQL statements to identify the table that the TableInfo object is associated with. |
| `description` | String | R | A string that contains database-dependent information about the table. |

<a id="79743"></a>
<a id="template"></a>
<a id="id1047"></a>
## Template

Template objects are named pages within the document. These pages may be hidden or visible and can be copied or spawned. They are typically used to dynamically create content (for example, to add pages to an invoice on overflow).

See also the Doc templates property, and createTemplate, getTemplate, and removeTemplate methods.

<a id="template-properties"></a>
<a id="id1048"></a>
### Template properties

<a id="78212"></a>
<a id="id1049"></a>
<a id="id1050"></a>
#### hidden

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | D | No | Not allowed in Reader: Only available in Acrobat products | Boolean | R/W |

Determines whether the template is hidden. Hidden templates cannot be seen by the user until they are spawned or are made visible. When an invisible template is made visible, it is appended to the document.

This property behaves as follows in Adobe Reader:

- Setting this property in versions of Adobe Reader earlier than 5.1 generates an exception.
- For Adobe Reader 5.1 and 6.0, setting this property depends on Advanced Forms Feature document rights.
- For Adobe Reader 7.0, this property cannot be set under any circumstances.

<a id="16107"></a>
<a id="id1051"></a>
<a id="id1052"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

The name of the template that was supplied when the template was created.

<a id="template-methods"></a>
<a id="id1053"></a>
### Template methods

<a id="97092"></a>
<a id="spawn"></a>
<a id="id1054"></a>
#### spawn

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | D | No | F |

Creates a new page in the document based on the template.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nPage` | (optional) The 0-based index of the page number after which or on which the new page will be created, depending on the value of `bOverlay`. The default is 0. |
| `bRename` | (optional) Specifies whether form fields on the page should be renamed. The default is `true`. |
| `bOverlay` | (optional) If `true` (the default), the template is overlaid on the specified page. If `false`, it is inserted as a new page before the specified page.   To append a page to the document, set `bOverlay` to `false` and set `nPage` to the number of pages in the document.  -  For certified documents or documents with Advanced Form Features rights, the `bOverlay` parameter is disabled. A template cannot be overlaid for these types of documents. |
| `oXObject` | (optional, Acrobat 6.0) The value of this parameter is the return value of an earlier call to `spawn`. |

**Returns**

Prior to Acrobat 6.0, this method returned nothing. Now, `spawn` returns an object representing the page contents of the page spawned. This return object can then be used as the value of the optional parameter `oXObject` for subsequent calls to `spawn`.

> **Note**
>
> Repeatedly spawning the same page can cause a large increase in the file size. To avoid this problem, `spawn` now returns an object that represents the page contents of the spawned page. This return value can be used as the value of the `oXObject` parameter in subsequent calls to the `spawn` method to spawn the same page.

Example 1: Spawn all templates and appends them one by one to the end of the document.

```
var a = this.templates;
for (i = 0; i < a.length; i++)
    a[i].spawn(this.numPages, false, false);
```

**Example 2 (Acrobat 6.0)**

Spawn the same template 31 times using the `oXObject` parameter and return value. Using this technique avoids overly inflating the file size.

```
var t = this.templates;
var T = t[0];
var XO = T.spawn(this.numPages, false, false);
for (var i=0; i<30; i++) T.spawn(this.numPages, false, false, XO);
```

<a id="87483"></a>
<a id="id1055"></a>
<a id="id1056"></a>
## Thermometer

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This object is a combined status window and progress bar that indicates to the user that a lengthy operation is in progress. To acquire a Thermometer object, use `app.thermometer`.

Example: This example shows how to use all properties and methods of the Thermometer object.

```
var t = app.thermometer;         // Acquire a thermometer object
t.duration = this.numPages;
t.begin();
for ( var i = 0; i < this.numPages; i++)
{
    t.value = i;
    t.text = "Processing page " + (i + 1);
    if (t.cancelled) break;       // Break if the operation is cancelled
    .
.. process the page ...
}
t.end();
```

<a id="thermometer-properties"></a>
<a id="id1057"></a>
### Thermometer properties

<a id="74557"></a>
<a id="cancelled"></a>
<a id="id1058"></a>
#### cancelled

Specifies whether the user wants to cancel the current operation. The user can indicate the desire to terminate the operation by pressing the Esc key on the Windows and UNIX platforms and Command-period on the Mac OS platform.

| Type | Access |
|------|--------|
| Boolean | R |

<a id="35975"></a>
<a id="duration"></a>
<a id="id1059"></a>
#### duration

Sets the value that corresponds to a full thermometer display. The thermometer is subsequently filled in by setting its `value`. The default duration is 100.

| Type | Access |
|------|--------|
| Number | R/W |

<a id="17228"></a>
<a id="id1060"></a>
<a id="id1061"></a>
#### text

Sets the text string that is displayed by the thermometer.

| Type | Access |
|------|--------|
| String | R/W |

<a id="68275"></a>
<a id="id1062"></a>
<a id="id1063"></a>
#### value

Sets the current value of the thermometer and updates the display. The value can range from 0 (empty) to the value set in `duration`. For example, if the thermometer’s duration is 10, the current value must be between 0 and 10, inclusive. If the value is less than zero, it is set to zero. If the value is greater than `duration`, it is set to `duration`.

| Type | Access |
|------|--------|
| Number | R/W |

<a id="thermometer-methods"></a>
<a id="id1064"></a>
### Thermometer methods

<a id="37386"></a>
<a id="begin"></a>
<a id="id1065"></a>
#### begin

Initializes the thermometer and displays it with the current value as a percentage of the duration.

Example: Count the words on each page of the current document, report the running total, and use the thermometer to track progress.

```
var t = app.thermometer; // acquire a thermometer object
t.duration = this.numPages;
t.begin();
var cnt=0;
for ( var i = 0; i < this.numPages; i++)
{
    t.value = i;
    t.text = "Processing page " + (i + 1);
    cnt += getPageNumWords(i);
    console.println("There are " + cnt + "words in this doc.");
    if (t.cancelled) break;
}
t.end();
```

<a id="93535"></a>
<a id="id1066"></a>
<a id="id1067"></a>
#### end

Draws the thermometer with its current value set to the thermometer’s duration (a full thermometer), then removes the thermometer from the display.

<a id="92096"></a>
<a id="this"></a>
<a id="id1068"></a>
## this

In JavaScript, the special keyword `this` refers to the current object. In Acrobat, the current object is defined as follows:

- In an object method, it is the object to which the method belongs.
- In a constructor function, it is the object being constructed.
- In a document-level script or field-level script, it is the Doc and therefore can be used to set or get document properties and functions.
- In a function defined in one of the folder-level JavaScripts files, it is undefined. Calling functions should pass the Doc to any function at this level that needs it.

For example, assume that the following function was defined at the plug-in folder level:

```
function PrintPageNum(doc)
{ /* Print the current page number to the console. */
    console.println("Page = " + doc.pageNum);
}
```

The following script outputs the current page number to the console twice and then prints the page:

```
/* Must pass the Doc. */
PrintPageNum(this);
/* Same as the previous call. */
console.println("Page = " + this.pageNum);
/* Prints the current page. */

 this.print(false, this.pageNum, this.pageNum);
```

Variables and functions that are defined in scripts are parented off of the `this` object. For example:

```
var f = this.getField("Hello");
```

is equivalent to

```
this.f = this.getField("Hello");
```

with the exception that the variable `f` can be garbage collected at any time after the script is run.

**Variable and function name conflicts**

JavaScript programmers should avoid using property and method names from the Doc as variable names. Using method names after the reserved word `var` will throw an exception, as the following line shows:

```
var getField = 1; // TypeError: redeclaration of function getField
```

Use of property names will not throw an exception, but the value of the property may not be altered if the property refers to an object:

```
// "title" will return "1", but the document will now be named "1".
var title = 1;

// Property not altered, info still an object
var info = 1; // "info" will return [object Info]
```

The following is an example of avoiding variable name clash.

```
var f = this.getField("mySignature"); // uses the ppklite sig handler

// Use "Info" rather than "info" to avoid a clash
var Info = f.signatureInfo();

// Some standard signatureInfo properties
console.println("name = " + Info.name);
```

<a id="24782"></a>
<a id="tts"></a>
<a id="id1069"></a>
## TTS

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.05 | No | No | All |

The JavaScript `TTS` object allows users to transform text into speech. To be able to use the `TTS` object, the user’s computer must have a Text-To-Speech engine installed on it. The Text-To-Speech engine will render text as digital audio and then speak it. It has been implemented mostly with accessibility in mind but can potentially have many other applications. The `TTS` object is present on both the Windows and Mac OS platforms (since it is a JavaScript object).

> **Note**
>
> Acrobat 5.0 has taken a very different approach to providing accessibility for disabled users by integrating directly with popular screen readers. Therefore, some of the screen reading features defined in 4.05 using the TTS object have been removed in 5.0 because they conflict with the screen reader. The TTS object remains, however, because it still has useful functionality in its own right that might be popular for multimedia documents.

<a id="tts-properties"></a>
<a id="id1070"></a>
### TTS properties

<a id="17738"></a>
<a id="id1071"></a>
<a id="id1072"></a>
#### available

`true` if the TTS object is available and the Text-To-Speech engine can be used.

| Type | Access |
|------|--------|
| Boolean | R |

Example:

```
console.println("Text to speech available: " + tts.available);
```

<a id="65337"></a>
<a id="numspeakers"></a>
<a id="id1073"></a>
#### numSpeakers

The number of speakers available to the Text-To-Speech engine. See also the speaker property and the getNthSpeakerName method.

| Type | Access |
|------|--------|
| Integer | R |

<a id="40775"></a>
<a id="pitch"></a>
<a id="id1074"></a>
#### pitch

Sets the baseline pitch for the voice of a speaker. The valid range for pitch is from 0 to 10, with 5 being the default for the mode.

| Type | Access |
|------|--------|
| Integer | R/W |

<a id="37694"></a>
<a id="soundcues"></a>
<a id="id1075"></a>
#### soundCues

- - Version (Key)
  - Save-Prefs
  - Security
  - Product
  - Type
  - Access
- - deprecated
  - No
  - No
  - All
  - Boolean
  - R/W

Deprecated. Returns `false`.

<a id="16595"></a>
<a id="speaker"></a>
<a id="id1076"></a>
#### speaker

Allows users to specify different speakers with different tone qualities when performing text-to-speech. See also the numSpeakers property and the getNthSpeakerName method.

| Type | Access |
|------|--------|
| String | R/W |

<a id="96528"></a>
<a id="speechcues"></a>
<a id="id1077"></a>
#### speechCues

- - Version (Key)
  - Save-Prefs
  - Security
  - Product
  - Type
  - Access
- - deprecated
  - No
  - No
  - All
  - Boolean
  - R/W

Deprecated. Returns `false`.

<a id="91461"></a>
<a id="speechrate"></a>
<a id="id1078"></a>
#### speechRate

| Type | Access |
|------|--------|
| Integer | R/W |

Sets the speed at which text will be spoken by the Text-To-Speech engine. The value for `speechRate` is expressed in number of words per minute.

<a id="13865"></a>
<a id="volume"></a>
<a id="id1079"></a>
#### volume

| Type | Access |
|------|--------|
| Integer | R/W |

Sets the volume for the speech. Valid values are 0 (mute) to 10 (loudest).

<a id="tts-methods"></a>
<a id="id1080"></a>
### TTS methods

<a id="71154"></a>
<a id="getnthspeakername"></a>
<a id="id1081"></a>
#### getNthSpeakerName

Gets the *n* th speaker name in the Text-To-Speech engine (see also the numSpeakers and speaker properties).

**Parameters**

| Property | Description |
|----------|-------------|
| `nIndex` | The index of the desired speaker name. |

**Returns**

The name of the specified speaker.

Example: Enumerate through all of the speakers available.

```
for (var i = 0; i < tts.numSpeakers; i++) {
    var cSpeaker = tts.getNthSpeakerName(i);
    console.println("Speaker[" + i + "] = " + cSpeaker);
    tts.speaker = cSpeaker;
    tts.qText ("Hello");
    tts.talk();
}
```

<a id="42857"></a>
<a id="id1082"></a>
<a id="id1083"></a>
#### pause

Immediately pauses text-to-speech output on a TTS object. Playback of the remaining queued text can be resumed by calling `resume`.

<a id="21233"></a>
<a id="qsilence"></a>
<a id="id1084"></a>
#### qSilence

Queues a period of silence into the text.

**Parameters**

| Property | Description |
|----------|-------------|
| `nDuration` | The amount of silence in milliseconds. |

<a id="82021"></a>
<a id="qsound"></a>
<a id="id1085"></a>
#### qSound

Puts the specified sound into the queue to be performed by `talk`. It accepts one parameter, `cSound`, from a list of possible sound cue names. These names map directly to sound files stored in the SoundCues folder, if it exists.

```
tts.qSound("DocPrint");         // Plays DocPrint.wav
```

The SoundCues folder should exist at the program level for the viewer, for example, `C:Program FilesAdobeAcrobat 9.0SoundCues`.

> **Note**
>
> Windows only—`qSound` can handle only 22 KHz,16-bit PCM.wav files. These should be at least 1 second long to avoid a queue delay problem in MS SAPI. If the sound lasts less than 1 second, it should be edited and have a silence added to the end of it.

**Parameters**

| Property | Description |
|----------|-------------|
| `cSound` | The sound cue name to use. |

<a id="23481"></a>
<a id="qtext"></a>
<a id="id1086"></a>
#### qText

Puts text into the queue to be performed by `talk`.

**Parameters**

| Property | Description |
|----------|-------------|
| `cText` | The text to convert to speech. |

Example:

```
tts.qText("Hello, how are you?");
```

<a id="90260"></a>
<a id="reset"></a>
<a id="id1087"></a>
#### reset

Stops playback of queued text and flushes the queue. It also resets all the properties of the TTS object to their default values. Text playback cannot be resumed with `resume`.

<a id="91678"></a>
<a id="resume"></a>
<a id="id1088"></a>
#### resume

Resumes playback of text on a paused TTS object.

<a id="68290"></a>
<a id="id1089"></a>
<a id="id1090"></a>
#### stop

Stops playback of queued text and flushes the queue. Playback of text cannot be resumed with `resume`.

<a id="22624"></a>
<a id="talk"></a>
<a id="id1091"></a>
#### talk

Sends whatever is in the queue to be spoken by the Text-To-Speech engine. If text output had been paused, `talk` resumes playback of the queued text.

Example:

```
tts.qText("Hello there!");
tts.talk();
```

<a id="70434"></a>
<a id="util"></a>
<a id="id1092"></a>
## util

A static JavaScript object that defines a number of utility methods and convenience functions for string and date formatting and parsing.

<a id="util-methods"></a>
<a id="id1093"></a>
### util methods

<a id="98835"></a>
<a id="crackurl"></a>
<a id="id1094"></a>
#### crackURL

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.05 | No | No | All |

Breaks a URL into its component parts.

Beginning with version 9.0, `util.crackURL` can break a URL that uses Internet Protocol version 6 (IPv6) addressing. The return object for `util.crackURL` includes an additional property, `nURLType`, to help determine the IP type of the URL being passed to the argument of `util.crackURL`.

No effort is made to determine the IP type if a direct URL is not used and the corresponding DNS name is used.

**Parameters**

| Property | Description |
|----------|-------------|
| `cURL` | A string specifying the URL. |

**Returns**

An object containing the following properties:

| Property | Description |
|----------|-------------|
| `cScheme` | The scheme of the URL. It may be `file`, `http` or `https`. |
| `cUser` | (Optional) The user name specified in the URL. |
| `cPassword` | (Optional) The password specified in the URL. |
| `cHost` | The hostname of the URL. |
| `nPort` | The port number of the URL. |
| `cPath` | (Optional) The path portion of the URL. |
| `cQuery` | (Optional) The parameter string portion of the URL. |
| `cFragment` | (Optional) The fragments of the URL. |
| `nURLType` | (Version 9.0) An integer valued property that takes a value of 0 if `cURL` uses IPv4 and a value of 1 if `cURL` uses IPv6. (IPv4 and IPv6 refer to the Internet Protocol versions 4 and 6, respectively.) |

This method throws a parameter error if the parameter is missing, the URL is not well-formed, or the URL scheme is not `file`, `http`, or `https`.

Example 1: The following code

```
util.crackURL("http://example.org/myPath?name0=value0&name1=value1#frag");
```

would return

```
   {
       cScheme: "http",
       cHost: "example.org",
       nPort: 80,
       cPath: "/myPath",
       cQuery
: "name0=value0&name1=value1",
       cFragment: "frag"
   }
```

**Example 2 (Version 9.0)**

Version 9.0 can break a URL into its components when the URL uses version 6 Internet Protocol.

```
var a = util.crackURL("http://[2001:1890:110b:15ce:250:56ff:febb:6111]/Ex");
if ( a.nURLType == 1 )
   console.println("host = [" + a.cHost + "]");
else
   console.println("host = " + a.cHost);
```

<a id="71009"></a>
<a id="iconstreamfromicon"></a>
<a id="id1095"></a>
#### iconStreamFromIcon

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Converts an XObject-based `Icon` object into an `Icon Stream` object.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oIcon` | An `Icon` object to be converted into an `Icon Stream` object. |

**Returns**

`Icon Stream` object

This method allows an icon obtained from the Doc `importIcon` or `getIcon` methods to be used in a method such as `app.addToolButton`, which would otherwise accept only an `Icon Stream` object as an input parameter.

Example: Import an icon into the document-level named icons tree and add a toolbutton to the application.

```
this.importIcon("myIcon", "/C/temp/myIcon.jpg", 0);
var oIcon = util.iconStreamFromIcon(this.getIcon("myIcon"));
app.addToolButton({
    cName: "myButton",
    oIcon: oIcon,
    cExec: "console.println('My Button!');",

     cTooltext: "My button!",
    nPos: 0
});
```

<a id="84295"></a>
<a id="printd"></a>
<a id="id1096"></a>
#### printd

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

**Returns** a date using a specified format.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cFormat` | The date and time format. It can be one of the following types:  -  A string that is a pattern of supported substrings that are place-holders for date and time data. Recognized date and time strings are shown in the table below. -  Beginning with Acrobat 5.0, a number specifying the format. Supported values (along with examples of each format) are: * *0*: PDF date format. Example: D:20000801145605+07’00’ * *1*: Universal. Example: D:20000801145605+07’00’ * *2*: Localized string. Example: 2000/08/01 14:56:05  -  Beginning with Acrobat 7.0, if `bXFAPicture` is `true`, this parameter is interpreted using the XFA Picture Clause format. |
| `oDate` | A Date object to format. Date objects can be obtained from the `Date` constructor of core JavaScript or from the `util.scand` method. |
| `bXFAPicture` | (optional, Acrobat 7.0) A Boolean value specifying whether the value of `cFormat` is interpreted using the XFA Picture Clause format, which gives extensive support for localized times and dates. See the sections on date and time pictures in [XFA Specification](https://www.pdfa.org/norm-refs/XFA-3_3.pdf). The default is `false`. |

**Returns**

The formatted date string.

<a id="42262"></a>
**cFormat String Patterns**

| String | Effect | Example |
|--------|--------|---------|
| mmmm | Long month | September |
| mmm | Abbreviated month | Sep |
| mm | Numeric month with leading zero | 09 |
| m | Numeric month without leading zero | 9 |
| dddd | Long day | Wednesday |
| ddd | Abbreviated day | Wed |
| dd | Numeric date with leading zero | 03 |
| d | Numeric date without leading zero | 3 |
| yyyy | Long year | 1997 |
| yy | Abbreviated Year | 97 |
| HH | 24 hour time with leading zero | 09 |
| H | 24 hour time without leading zero | 9 |
| hh | 12 hour time with leading zero | 09 |
| h | 12 hour time without leading zero | 9 |
| MM | minutes with leading zero | 08 |
| M | minutes without leading zero | 8 |
| ss | seconds with leading zero | 05 |
| s | seconds without leading zero | 5 |
| tt | am/pm indication | am |
| t | single digit am/pm indication | a |
| j | Japanese Emperor Year (abbreviated)  -  Introduced in Acrobat 6.0. In Acrobat 7.0, this format string has been deprecated in favor of the XFA Picture Clause format. |  |
| jj | Japanese Emperor Year  -  Introduced in Acrobat 6.0. In Acrobat 7.0, this format string has been deprecated in favor of the XFA Picture Clause format. |  |
|  | se as an escape character |  |

Example 1: Format the current date in long format:

```
var d = new Date();
console.println("Today is " + util.printd("mmmm dd, yyyy", d));
```

**Example 2 (Acrobat 5.0)**

Display the date in a local format

```
console.println(util.printd(2, new Date() ));
```

**Example 3 (Acrobat 7.0)**

Use the XFA-Picture Clause to write the current date to the console.

```
// Execute in console
console.println(
    util.printd("EEE, 'the' D 'of' MMMM, YYYY", new Date(), true));
// The output on this day is
Tue, the 13 of July, 2004
```

Locale-Sensitive Picture Clauses. Normally processing of picture clauses occurs in the ambient locale. It is possible, however, to indicate that picture processing be done in a specific locale. This is of use when formatting or parsing data that is locale-specific and different from the ambient locale. The syntax for this extension to compound picture clauses is:

```
category-name(locale-name){picture-symbols}
```

The code executed in the console,

```
util.printd("date(fr){DD MMMM, YYYY}", new Date(), true)
```

yields the output on this day,

```
13 juillet, 2004
```

The XFA-Picture Clause gives extensive support for Chinese, Chinese (Taiwan), Japanese, and Korean (CCJK) times and dates. The example below, a custom format script of a text field, gives the current date formatted for a Japanese locale.

```
event.value = util.printd("date(ja){ggYY/M/D}", new Date(), true)
```

<a id="95657"></a>
<a id="printf"></a>
<a id="id1097"></a>
#### printf

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Formats one or more arguments as a string according to a format string. It is similar to the C function of the same name. This method converts and formats incoming arguments into a result string according to a format string (`cFormat`).

The format string consists of two types of objects:

- Ordinary characters, which are copied to the result string.
- Conversion specifications, each of which causes conversion and formatting of the next successive argument to `printf`.

Each conversion specification is constructed as follows:

```
%[,nDecSep][cFlags][nWidth][.nPrecision]cConvChar
```

The following table describes the components of a conversion specification.

| `nDecSep` | A comma character (`,`) followed by a digit that indicates the decimal/separator format: * *0*: Comma separated, period decimal point * *1*: No separator, period decimal point * *2*: Period separated, comma decimal point * *3*: No separator, comma decimal point |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cFlags` | Only valid for numeric conversions and consists of a number of characters (in any order), which will modify the specification: * *+*: Specifies that the number will always be formatted with a sign. * *space*: If the first character is not a sign, a space will be prefixed. * *0*: Specifies padding to the field with leading zeros. * *#*: Specifies an alternate output form. For `f`, the output will always have a decimal point. |
| `nWidth` | A number specifying a minimum field width. The converted argument is formatted to be at least this many characters wide, including the sign and decimal point, and may be wider if necessary. If the converted argument has fewer characters than the field width, it is padded on the left to make up the field width. The padding character is normally a space, but is 0 if the zero padding flag is present (`cFlags` contains `0`). |
| `nPrecision` | A period character (`.`) followed by a number that specifies the number of digits after the decimal point for float conversions. |
| `cConvChar` | Indicates how the argument should be interpreted: * *d*: Integer (truncating if necessary) * *f*: Floating-point number * *s*: String * *x*: Integer (truncating if necessary) and formatted in unsigned hexadecimal notation |

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cFormat` | The format string to use. |
| `arguments` | The optional arguments(s) that contain the data to be inserted in place of the `%` tags specified in the first parameter, the format string. The number of optional arguments must be the same as the number of `%` tags. |

> **Note**
>
> The `util.printf` function does not accept an object literal with properties that contain the arguments. Arguments are entered in the usual comma-delimited list.

**Returns**

A result string formatted as specified.

Example: Take an irrational number and display it using various formats of `util.printf`.

```
var n = Math.PI * 100;
console.clear();
console.show();
console.println(util.printf("Decimal format: %d", n));
console.println(util.printf("Hex format: %x", n));
console.println(util.printf("Float format: %.2f", n));
console.println(util.printf("String format: %s", n));
```

The output of the above script is as follows:

```
Decimal format: 314
Hex format: 13A
Float format: 314.16
String format: 314.159265358979
```

<a id="86394"></a>
<a id="printx"></a>
<a id="id1098"></a>
#### printx

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Formats a source string, `cSource`, according to a formatting string, `cFormat`. A valid format for `cFormat` is any string that may contain special masking characters:

| Value | Effect |
|-------|--------|
| ? | Copy next character. |
| X | Copy next alphanumeric character, skipping any others. |
| A | Copy next alpha character, skipping any others. |
| 9 | Copy next numeric character, skipping any others. |
| ‘’\*’’ | Copy the rest of the source string from this point on. |
| ‘’'’ | Escape character. |
| `>` | Upper case translation until further notice. |
| `<` | Lower case translation until further notice. |
| = | Preserve case until further notice (default). |

**Parameters**

| Property | Description |
|----------|-------------|
| `cFormat` | The formatting string to use. |
| `cSource` | The source string to use. |

**Returns**

The formatted string.

Example: Format a string as a U.S. telephone number.

```
var v = "aaa14159697489zzz";
v = util.printx("9 (999) 999-9999", v);
console.println(v);
```

<a id="readfileintostream"></a>
<a id="id1099"></a>
#### readFileIntoStream

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 10.0 | No | No | All |

Loads an external file into a JavaScript stream, optionally base64 encodes it, and returns the content as a base64 encoded stream.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cDIPath` | (optional) A device-independent path to an arbitrary file on the user’s hard drive. This path may be absolute or relative to the current document.  If not specified, the user is presented with the File Open dialog to locate the file.  If the `cDIPath` parameter is specified, this method can only be executed in privileged context, during a batch or console event (or when the document is certified with a certificate trusted to execute “embedded high privileged JavaScript”). |
| `bEncodeBase64` | (optional) If true, base64-encode the file content. |

**Returns**

The File content as a ReadStream object that is optionally base 64-encoded.

Example: Assume there is a text field myField in this document. This example reads the contents of a file c:/data/myData.txt in a ReadStream object, converts it to a string, and displays it in the multiline text field.

```
var rStream = util.readFileIntoStream("/c/data/myData.txt");
var cFile = util.stringFromStream(rStream);
this.getField("myTextField").value = cFile;
```

<a id="30061"></a>
<a id="scand"></a>
<a id="id1100"></a>
#### scand

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | No | No | All |

Converts a date into a JavaScript Date object according to the rules of a format string. This routine is much more flexible than using the date constructor directly.

> **Note**
>
> Given a two-digit year for input, `scand` uses the *date horizon* heuristic to resolve the ambiguity. If the year is less than 50, it is assumed to be in the 21st century (that is, add 2000). If it is greater than or equal to 50, it is in the 20th century (add 1900).

The supplied date `cDate` should be in the same format as described by `cFormat`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cFormat` | The rules to use for formatting the date. `cFormat` uses the same syntax as found in `printd`. |
| `cDate` | The date to convert. |

**Returns**

The converted Date object, or `null` if the conversion fails.

Example 1:

```
/* Turn the current date into a string. */
var cDate = util.printd("mm/dd/yyyy", new Date());
console.println("Today's date: " + cDate);
/* Parse it back into a date. */
var d = util.scand("mm/dd/yyyy", cDate);
/* Output it in reverse order. */
console.println("Yet again: " + util.printd("yyyy mmm dd", d));
```

Example 2: Retrieve a text field value, see if it is a date of the acceptable format, then report results in an alert box or the console window.

The method returns `null` if the conversions fails, which can occur if the user inputs a data different than what is expected. In this case, test the return value for `null`.

```
var d= util.scand("mm/dd/yyyy", this.getField("myDate").value);
    if ( d== null )
        app.alert("Please enter a valid date of the form" +

             " "mm/dd/yyyy".")
    else {
        console.println("You entered the date: "
            + util.printd("mmmm dd, yyyy",d));
}
```

<a id="18255"></a>
<a id="spanstoxml"></a>
<a id="id1101"></a>
#### spansToXML

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Converts an array of `Span` objects into an XML(XFA) String as described in the [PDF Reference](https://adobe.com/go/pdfreference).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| An array of `Span` objects | An array of Span objects to be converted into an XML string. |

**Returns**

String

Example: Get the value of a rich text field, turns all of the text blue, converts it to an XML string and then prints it to the console.

```
var f = getField("Text1");
var spans = f.richValue;
for(var index = 0; index < spans.length; index++)
    spans[index].textColor = color.blue;
console.println(util.spansToXML(spans));
```

<a id="10740"></a>
<a id="id1102"></a>
<a id="id1103"></a>
#### streamFromString

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Converts a string to a `ReadStream` object.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cString` | The string to be converted into a `ReadStream` object. |
| `cCharSet` | (optional) The encoding for the string in `cString`. The options are utf-8, utf-16, Shift-JIS, BigFive, GBK, UHC. The default is utf-8. |

**Returns**

`ReadStream` object

Example: Take the response given in a text field of this document and append it to an attached document.

```
var v = this.getField("myTextField").value;
var oFile = this.getDataObjectContents("MyNotes.txt");
var cFile = util.stringFromStream(oFile, "utf-8");
cFile += "rn" + cFile;
oFile = util.streamFromString( cFile, "utf-8");
this.setDataObjectContents("MyNotes.txt", oFile);
```

This example uses the Doc methods `getDataObjectContents` and `setDataObjectContents` and `util.stringFromStream`.

<a id="25458"></a>
<a id="id1104"></a>
<a id="id1105"></a>
#### stringFromStream

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Converts a `ReadStream` object to a string.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oStream` | `ReadStream` object to be converted into a string. |
| `cCharSet` | (optional) The encoding for the string in `oStream`. The options are utf-8, utf-16, Shift-JIS, BigFive, GBK, UHC. The default is utf-8. |

**Returns**

String

Example: Assume there is a text file embedded in this document. This example reads the contents of the attachment and displays it in the multiline text field.

```
var oFile = this.getDataObjectContents("MyNotes.txt");
var cFile = util.stringFromStream(oFile, "utf-8");
this.getField("myTextField").value = cFile;
```

This example uses `getDataObjectContents` to get the file stream of the attached document.

<a id="70013"></a>
<a id="xmltospans"></a>
<a id="id1106"></a>
#### xmlToSpans

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Converts an XML (XFA) string, as described in the [PDF Reference](https://adobe.com/go/pdfreference), to an array of Span objects suitable for specifying as the `richValue` or `richContents` of a field or annotation.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| a string | An XML (XFA) string to be converted to an array of `Span` objects. |

**Returns**

An Array of `Span` objects

Example: Get the rich text string from “Text1”, convert it to XML, then convert it back to an array of Span objects and repopulate the text field.

```
var f = getField("Text1");
var spans = f.richValue;
var str = util.spansToXML(spans);
var spans = util.xmlToSpans(str);
f.richValue = spans;
```

<a id="22317"></a>
<a id="xfa"></a>
<a id="id1108"></a>
## XFA

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.02 | No | No | All |

The XFA object provides access to the XFA `appModel` container. More detailed information is available in the [JavaScript Developer Guide](../jsdevguide/index.md).

An XFA object is returned by the `XMLData.parse` and `XMLData.applyXPath` methods.

Example: The following code detects whether the PDF document has Acrobat forms or was created by LiveCycle Designer and has XML forms. The script can be run in the console, or as a batch sequence; in the latter case, the script can be used to classify all selected document as an XML form (dynamic or static) or as an Acrobat form.

```
// This script assumes you are using Acrobat 8.0.
console.println("Document name: " + this.documentFileName);
// The xfa object is undefined in an Acrobat form.
if ( typeof xfa == "object" ) {
    if ( this.dynamicXFAForm )
        console.println("  This is a dynamic XML form.");
    else
        console.println("  This is a static XML form.");
    if ( this.XFAForeground )
        console.println("  This document has imported artwork");
}
else console.println("  This is an Acrobat form.");
```

<a id="43545"></a>
<a id="xmldata"></a>
<a id="id1109"></a>
## XMLData

`XMLData` is a static object that allows the creation of a JavaScript object representing an XML document tree and permits the manipulation of arbitrary XML documents through the XFA Data DOM. (In XFA, there are several other DOMs parallel to the Data DOM, but for the purpose of the `XMLData` object, only the Data DOM is used.)

PDF documents that return `true` to the Doc `dynamicXFAForm` property can use the `XMLData` object but cannot have its form fields manipulated by that object, because the two data DOMs are isolated from each other.

<a id="xmldata-methods"></a>
<a id="id1110"></a>
### XMLData methods

<a id="36467"></a>
<a id="applyxpath"></a>
<a id="id1111"></a>
#### applyXPath

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Enables you to manipulate and query an XML document by using XPath expressions. The XPath language is described in the W3C document *XML Path Language (XPath)*, which is available at [http://www.w3.org/TR/xpath](http://www.w3.org/TR/xpath).

XPath expressions evaluate to one of the known four types: Boolean, Number, String, Node-set. In JavaScript, they are returned, respectively, as the following types: Boolean, Number, String, and Object.

If an object is returned, it is of type `XFA` object, which represents either a tree started by a single node or a tree started by a list of nodes (a tree list). The type of this object is the same as the one returned by the `XMLData.parse`.

> **Note**
>
> XFA provides a query mechanism, SOM expressions, which is similar to that of XPath. Because XPath is widely used in the XML community, the `applyXPath` method allows users to use XPath expressions if they choose.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oXml` | An XFAObject object representing an XML document tree.  -  An exception is thrown if the value of this parameter is a nodeList XFA object instead of the root of an XML tree. |
| `cXPath` | A string parameter with the XPATH query to be performed on the document tree. |

**Returns**

Boolean, Number, String, or XFAObject.

<a id="47440"></a>
Example: This example shows each of the return types of `XMLData.applyXPath` (Boolean, number, string, or XFAObject). It extracts information from an XML data string, in this case, the family tree of the “Robat” family).

```
var cXMLDoc = "<family name = 'Robat'>
    <grandad id = 'm1' name = 'A.C.' gender='M'>
        <child> m2 </child>
        <personal>
            <income>100000</income>
        </personal>
    </grandad>
    <dad id = 'm2' name = 'Bob' gender='M'>
        <parent> m1 </parent>
        <spouse> m3 </spouse>
        <child> m4 </child>
        <child> m5 </child>
        <child> m6 </child>
        <personal>
            <income>75000</income>
        </personal>
    </dad>
    <mom id = 'm3' name = 'Mary' gender='F'>
        <spouse> m2 </spouse>
        <personal>
            <income>25000</income>
        </personal>
    </mom>
    <daughter id = 'm4' name = 'Sue' gender='F'>
        <parent> m2 </parent>
        <personal>
            <income>40000</income>
        </personal>
    </daughter>
    <son id = 'm5' name = 'Jim' gender='M'>
        <parent> m2 </parent>
        <personal>
            <income>35000</income>
        </personal>
    </son>
    <daughter id = 'm6' name = 'Megan' gender='F'>
        <parent> m2 </parent>
        <personal>
            <income>30000</income>
        </personal>
    </daughter>
</family>";
var myXML= XMLData.parse( cXMLDoc, false);
```

The following line returns an XFAObject.

Get mom’s data.

```
var a = XMLData.applyXPath(myXML, "//family/mom")
a.saveXML('pretty');
<?xml version="1.0" encoding="UTF-8"?>
<mom id="m3" name="Mary" gender="F">
    <spouse> m2 </spouse>
    <personal>
        <income>25000</income>
    </personal>
</mom>
// get the income element value
a.personal.income.value = "20000"; // change the income
```

Get dad’s name, an attribute.

```
var b = XMLData.applyXPath(myXML, "//family/dad/@name");
b.saveXML('pretty');
<?xml version="1.0" encoding="UTF-8"?>
name="Bob"
// assign to a variable
var dadsName = b.value; // dadsName = "Bob"
```

Get all attributes of dad node.

```
var b = XMLData.applyXPath( myXML, "//family/dad/attribute::*" );
for(var i=0; i < b.length; i++)
    console.println(b.item(i).saveXML('pretty'))
```

The loop above outputs the following to the console.

```
<?xml version="1.0" encoding="UTF-8"?>
id="m2"
<?xml version="1.0" encoding="UTF-8"?>
name="Bob"
<?xml version="1.0" encoding="UTF-8"?>
gender="M"
```

Extract particular information from this

```
console.println("For attribute 2, we have " + b.item(2).name + " = '"
    + b.item(2).value + "'.");
```

which yields an output of

```
For attribute 2, we have gender = 'M'.
```

Get dad’s second child.

```
var c = XMLData.applyXPath(myXML, "//family/dad/child[position()=2]");
c.saveXML('pretty')
<?xml version="1.0" encoding="UTF-8"?>
<child> m5 </child>
```

This is the `id` of dad’s second child. The examples below get the family data on this child.

The following returns a string.

```
// Calculate the value of dadsName using XPath methods.
var dadsName = XMLData.applyXPath(myXML, "string(//family/dad/@name)")
// dadsName is assigned a value of "Bob" with this one line.
```

Get the family information on dad’s second child. The following line assigns `c = "m5"`. The return value of the call to `applyXPath` is a string, and the function `normalize-space` converts its argument to a string and removes any surrounding spaces.

```
var c = XMLData.applyXPath(myXML,
    "normalize-space(//family/dad/child[2])");
var d = "//*[@id = '" + c + "']";     // Note: d= "//*[@id = 'm5']"
XMLData.applyXPath(myXML, d ).saveXML('pretty'); // show what we have
<son id="m5" name="Jim" gender="M">
    <parent> m2 </parent>
    <personal>
        <income>35000</income>
    </personal>
</son>
```

Now display information about the sixth child node of the family root. The XPath functions `name` and `concat` are used.

```
var e = XMLData.applyXPath(myXML,
    "concat(name(//family/child::*[position()=6]), '=',
    //family/child::*[position()=6]/@name)" );
console.println(e); // the output is "daughter=Megan"
```

Get the names of all members of the “Robat” family.

```
e = XMLData.applyXPath(myXML,"//family/child::*" );
for ( var i = 1; i <= e.length; i++ )  {
    var str = "string(//family/child::*["+i+"]/@name)";
    console.println(XMLData.applyXPath(myXML,str));
}
```

The output is

```
A.C.
Bob
Mary
Sue
Jim
Megan
```

The following code shows a Boolean return value.

```
var f = XMLData.applyXPath( myXML, "//family/dad/@id = 'm2'" );
if ( f == true ) console.println("dad's id is 'm2'");
else console.println("dad's id is not 'm2'");
```

The following code shows a numeric return value.

```
// Get dad's income
g = XMLData.applyXPath( myXML, "number(//family/dad/personal/income)" );
// Double dad's salary, implied conversion to a number type
console.println("Dad's double salary is " +
    XMLData.applyXPath( myXML, "//family/dad/personal/income * 2" ) );
```

Now compute the total income of the family “Robat”.

```
console.println("Total income of A.C. Robat's family is "
    + XMLData.applyXPath( myXML, "sum(//income)" ) + ".");
```

The above line writes the following to the console.

```
Total income of A.C. Robat's family is 305000.
```

List the individual incomes.

```
var g = XMLData.applyXPath( myXML, "//income")
for ( var i =0; i< g.length; i++) console.println(g.item(i).value);
```

<a id="63609"></a>
<a id="parse"></a>
<a id="id1112"></a>
#### parse

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Creates an object representing an XML document tree. Its parameters are the same as those of the `loadXML` method in the XFA Data DOM.

This method returns an object of type `XFA` object that represents either a tree headed by a single node or a tree started by a list of nodes (a tree list).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `param1` | A string containing the XML document. |
| `param2` | (optional) A Boolean value specifying whether the root node of the XML document should be ignored. The default value is `true`. If `false`, the root node should not be ignored. |

**Returns**

XFAObject

Example 1: Consider the XML document as first introduced in the example following the `XMLData.` applyXPath method.

```
var x = XMLData.parse( cXMLDoc, false );
var y = x.family.name;                       // An XFAObject
console.println(y.value);                   // Output to console is "Robat"
```

Get information about dad.

```
y = x.family.dad.id;                         // An XFAObject
console.println(y.value);                    // Output to console is "m2"

y = x.family.dad.name.value;                 // y = "Bob"
x.family.dad.name.value = "Robert";          // Change name to "Robert"
y = x.family.dad.name.value;                 // y = "Robert"

y = x.family.dad.personal.income.value;      // y = "75000"
x.family.dad.personal.income.value = "80000";// Give dad a raise
```

Example 2: Create a simple XML document and manipulate it.

```
x = XMLData.parse("<a> <c>A.</c><d>C.</d> </a>, false);
x.saveXML("pretty");
```

The output of the previous line is

```
<?xml version="1.0" encoding="UTF-8"?>
<xfa:data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
    <a>
        <c>A.</c>
        <d>C.</d>
    </a>
</xfa:data>
```

Now create another simple document.

```
y = XMLData.parse("<b>Robat</b>", false);
y.saveXML("pretty");
```

The output of this line

```
<?xml version="1.0" encoding="UTF-8"?>
<xfa:data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
    <b>Robat</b>
</xfa:data>
```

Append `y` on to `x`.

```
x.nodes.append(y.clone(true).nodes.item(0));
x.saveXML("pretty");
```

The result:

```
<?xml version="1.0" encoding="UTF-8"?>
<xfa:data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
    <a>
        <c>A.</c>
        <d>C.</d>
    </a>
    <b>Robat</b>
</xfa:data>
```

Now execute

```
x.nodes.insert(y.clone(true).nodes.item(0), x.nodes.item(0));
x.saveXML("pretty")
```

to obtain

```
<?xml version="1.0" encoding="UTF-8"?>
<xfa:data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
    <b>Robat</b>
    <a>
        <c>A.</c>
        <d>C.</d>
    </a>
    <b>Robat</b>
</xfa:data>
```

Now remove these two nodes.

```
x.nodes.remove( x.nodes.namedItem("b") );
x.nodes.remove( x.nodes.namedItem("b") );
```

Now, we are back to the original XML document.

```
<?xml version="1.0" encoding="UTF-8"?>
<xfa:data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
    <a>
        <c>A.</c>
        <d>C.</d>
    </a>
</xfa:data>
```

Executing the following line

```
x.a.nodes.insert( y.clone(true).nodes.item(0), x.a.nodes.item(0));
x.saveXML("pretty");
```

yields the following output:

```
<?xml version="1.0" encoding="UTF-8"?>
<xfa:data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
    <a>
        <b>Robat</b>
        <c>A.</c>
        <d>C.</d>
    </a>
</xfa:data>
```

Now remove that node just inserted.

```
x.a.nodes.remove( x.a.nodes.namedItem("b"));
```

Now insert `y` (actually a clone of `y`) between the first and second children of the element `a`.

```
x.a.nodes.insert( y.clone(true).nodes.item(0), x.a.nodes.item(1));
```

This produces the following

```
<?xml version="1.0" encoding="UTF-8"?>
<xfa:data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
<a>
    <c>A.</c>
    <b>Robat</b>
    <d>C.</d>
</a>
</xfa:data>
```

Remove that node just inserted:

```
x.a.nodes.remove( x.a.nodes.namedItem("b"));
```

Finally, append `y` onto `a`.

```
x.a.nodes.append( y.clone(true).nodes.item(0));
```

yielding

```
<?xml version="1.0" encoding="UTF-8"?>
<xfa:data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
    <a>
        <c>A.</c>
        <d>C.</d>
        <b>Robat</b>
    </a>
</xfa:data>
```
