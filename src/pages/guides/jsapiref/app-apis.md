# App APIs

<a id="81243"></a>
<a id="app"></a>
<a id="id128"></a>
## app

A static JavaScript object that represents the Acrobat application. It defines a number of Acrobat-specific functions plus a variety of utility routines and convenience functions.

<a id="app-properties"></a>
<a id="id129"></a>
### app properties

<a id="82645"></a>
<a id="activedocs"></a>
<a id="id130"></a>
#### activeDocs

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | Yes | All | array | R |

An array containing the Doc object for each active document. If no documents are active, `activeDocs` returns nothing; that is, it has the same behavior as `d` `=` `new Array(0)` in core JavaScript.

In versions of Acrobat earlier than 7.0, executing the script `d = app.activeDocs` in the console returned `[object Global]` to the console. Beginning with Acrobat 7.0, no `toString()` value is output to the console.

> **Note**
>
> You should be aware of the following version-related information:

- In Acrobat 5.0, this property returns an array containing the Doc object for each active document.
- In Acrobat 5.0.5, this property was changed to return an array of Doc objects of only those open documents that have the Doc object `disclosed` property set to `true`.
- Beginning with the Acrobat 5.0.5 Accessibility and Forms Patch and continuing with Acrobat 6.0 and later, the behavior is as follows: During a batch, console or menu event, `activeDocs` ignores the `disclosed` property and returns an array of Doc objects of the active documents. During any other event, `activeDocs` returns an array of Doc objects of only those active documents that have `disclosed` set to `true`.
- Beginning with Acrobat 7.0, execution of JavaScript through a menu event is no longer privileged. See priv.

The array returned by `app.activeDocs` includes any documents opened by `app.openDoc` with the `bHidden` parameter set to `true`, subject to the security restrictions described above.

Example: This example searches among the open documents for the document with a title of `myDoc`, then inserts a button in that document using the Doc object `addField` method. Whether the documents must be `disclosed` depends on the version of Acrobat executing this code and on the placement of the code (for example, console versus mouse-up action).

```
var d = app.activeDocs;
for (var i=0; i < d.length; i++)
if (d[i].info.Title == "myDoc") {
    var f = d[i].addField("myButton", "button", 0, [20, 100, 100, 20]);
    f.setAction("MouseUp","app.beep(0)");
    f.fillColor=color.gray;99849106
}
```

<a id="69217"></a>
<a id="calculate"></a>
<a id="id131"></a>
#### calculate

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

If `true` (the default value), calculations can be performed. If `false`, calculations are not permitted.

The use of this property is discouraged; the Doc object property `calculate` is preferred.

<a id="99849"></a>
<a id="constants"></a>
<a id="id132"></a>
#### constants

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 7.0 | No | No | All | Object | R |

A wrapper object for holding various constant values. Currently, this property returns an object with a single property, `align`.

`app.constants.align` is an object that has the possible properties `left`, `center`, `right`, `top`, and `bottom`, indicating the type of alignment. These values can be used to specify alignment, such as when adding a watermark.

Example: See the Doc object methods addWatermarkFromFile and addWatermarkFromText for examples.

<a id="46620"></a>
<a id="focusrect"></a>
<a id="id133"></a>
#### focusRect

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.05 | P | No | All | Boolean | R/W |

Turns the focus rectangle on and off. The focus rectangle is the faint dotted line around buttons, check boxes, radio buttons, and signatures to indicate that the form field has the keyboard focus. A value of true `turns` on the focus rectangle.

Example: Turn off the focus rectangle.

```
app.focusRect = false;
```

<a id="35940"></a>
<a id="formsversion"></a>
<a id="id134"></a>
#### formsVersion

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | No | No | All | Number | R |

The version number of the viewer forms software. Check this property to determine whether objects, properties, or methods in newer versions of the software are available if you want to maintain backward compatibility in your scripts.

Example: Toggle fullscreen mode.

```
if (typeof app.formsVersion != "undefined" && app.formsVersion >= 5.0) {
        app.fs.defaultTransition = "";
        app.fs.isFullScreen = !app.fs.isFullScreen;
}
else app.fullscreen = !app.fullscreen;
```

<a id="72896"></a>
<a id="frompdfconverters"></a>
<a id="id135"></a>
#### fromPDFConverters

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array | R |

An array of file type conversion ID strings. A conversion ID string can be passed to the Doc object `saveAs` method.

Example: List all currently supported conversion ID strings.

```
for ( var i = 0; i < app.fromPDFConverters.length; i++)
    console.println(app.fromPDFConverters[i]);
```

<a id="70082"></a>
<a id="fs"></a>
<a id="id136"></a>
#### fs

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Object | R |

A `FullScreen` object, which can be used to access the fullscreen properties.

Example:

```
// This code puts the viewer into fullscreen (presentation) mode.
app.fs.isFullScreen = true;
```

See also `fullScreenObject.` isFullScreen.

<a id="42010"></a>
<a id="fullscreen"></a>
<a id="id137"></a>
#### fullscreen

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

The use of this property is discouraged; it has been superseded by the `FullScreen` object property `isFullScreen`. The `fs` method returns a `FullScreen` object that can be used to access the fullscreen properties.

Controls whether the viewer is in full screen mode or regular viewing mode.

> **Note**
>
> A PDF document being viewed from within a web browser cannot be put into full screen mode. Full screen mode can be initiated from within the browser, but applies only to a document open in the Acrobat viewer application, if any, not to the browser itself.

<a id="82355"></a>
<a id="language"></a>
<a id="id138"></a>
#### language

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | String | R |

The language of the running Acrobat viewer. It can be one of the following strings.

| String | Language |
|--------|----------|
| `CHS` | Chinese Simplified |
| `CHT` | Chinese Traditional |
| `DAN` | Danish |
| `DEU` | German |
| `ENU` | English |
| `ESP` | Spanish |
| `FRA` | French |
| `ITA` | Italian |
| `KOR` | Korean |
| `JPN` | Japanese |
| `NLD` | Dutch |
| `NOR` | Norwegian |
| `PTB` | Brazilian Portuguese |
| `SUO` | Finnish |
| `SVE` | Swedish |

<a id="49059"></a>
<a id="media"></a>
<a id="id139"></a>
#### media

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object | R |

Defines an extensive number of properties and methods useful for setting up and controlling a multimedia player.

See the [app.media](./app-apis.md#19976) object for a listing of the properties and methods of this object, as well as numerous examples of use.

<a id="72376"></a>
<a id="monitors"></a>
<a id="id140"></a>
#### monitors

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | `Monitors` object | R |

A `Monitors` object, which is an array containing one or more `Monitor` objects representing each of the display monitors connected to the user’s system. Each access to `app.monitors` returns a new, up-to-date copy of this array.

A `Monitors` object also has several methods that can be used to select a display monitor. Alternatively, JavaScript code can look through the array explicitly.

Example: Count the number of display monitors connected to the user’s system.

```
var monitors = app.monitors;
console.println("There are " + monitors.length
    + " monitor(s) connected to this system.");
```

<a id="19633"></a>
<a id="numplugins"></a>
<a id="id141"></a>
#### numPlugIns

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| deprecated | No | No | All | Number | R |

> **Note**
>
> This method has been superseded by the `plugIns` property.

Indicates the number of plug-ins that have been loaded by Acrobat.

<a id="17183"></a>
<a id="openinplace"></a>
<a id="id142"></a>
#### openInPlace

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | P | No | All | Boolean | R/W |

Specifies whether cross-document links are opened in the same window or opened in a new window.

Example: Open cross-document links in the same window.

```
app.openInPlace = true;
```

<a id="50421"></a>
<a id="platform"></a>
<a id="id143"></a>
#### platform

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | No | No | All | String | R |

The platform that the script is currently executing on. There are three valid values:

```
WIN
MAC
UNIX
```

<a id="56835"></a>
<a id="plugins"></a>
<a id="id144"></a>
#### plugIns

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Array | R |

An array of `PlugIn` objects representing the plug-ins that are currently installed in the viewer.

Example:

```
// Get array of PlugIn objects
var aPlugins = app.plugIns;
// Get number of plug-ins
var nPlugins = aPlugins.length;
// Enumerate names of all plug-ins
for ( var i = 0; i < nPlugins; i++)
    console.println("Plugin #"+i+" is " + aPlugins[i].name);
```

<a id="52944"></a>
<a id="printcolorprofiles"></a>
<a id="id145"></a>
#### printColorProfiles

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Acrobat only | Array of Strings | R |

A list of available printer color spaces. Each of these values is suitable to use as the value of the `colorProfile` property of a `PrintParams` object.

Example: Print out a listing of available printer color spaces:

```
var l = app.printColorProfiles.length
for ( var i = 0; i < l; i++)
    console.println("(" + (i+1) + ") " + app.printColorProfiles[i]);
```

<a id="16579"></a>
<a id="printernames"></a>
<a id="id146"></a>
#### printerNames

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array of Strings | R |

A list of available printers. Each of these values is suitable to use in the `printerName` property of the `PrintParams` object. If no printers are installed on the system, an empty array is returned.

Example: Print out a listing of available printers:

```
var l = app.printerNames.length
for ( var i = 0; i < l; i++)
    console.println("(" + (i+1) + ") " + app.printerNames[i]);
```

<a id="70509"></a>
<a id="runtimehighlight"></a>
<a id="id147"></a>
#### runtimeHighlight

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Acrobat Pro only | Boolean | R/W |

If `true`, the background color and hover color for form fields are shown.

Example: If run-time highlighting is off (`false`), do nothing, otherwise change the preferences.

```
if (!app.runtimeHighlight)
{
    app.runtimeHighlight = true;
    app.runtimeHighlightColor = color.red;
}
```

<a id="80977"></a>
<a id="runtimehighlightcolor"></a>
<a id="id148"></a>
#### runtimeHighlightColor

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | Acrobat Pro only | Color array | R/W |

Sets the color for runtime highlighting of form fields.

The value of this property is a color array. (See Color arrays for details.)

Example: See the runtimeHighlight property.

<a id="18969"></a>
<a id="thermometer"></a>
<a id="id149"></a>
#### thermometer

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object | R |

A `Thermometer` object, which is a combined status window/progress bar that indicates to the user that a lengthy operation is in progress.

Example: See the Thermometer object.

<a id="92576"></a>
<a id="toolbar"></a>
<a id="id150"></a>
#### toolbar

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | Acrobat Pro only | Boolean | R/W |

Allows a script to show or hide both the horizontal and vertical Acrobat toolbars of Acrobat 9 or earlier. In Acrobat X, allows a script to show or hide the Plugin Addon Tools panel on the right side of the display area. It does not hide the toolbar (Acrobat 9 or earlier) or the tools panel (Acrobat X), in external windows (that is, in an Acrobat window within a web browser).

Example: Hide the toolbar.

```
app.toolbar = false;
```

<a id="25841"></a>
<a id="toolbarhorizontal"></a>
<a id="id151"></a>
#### toolbarHorizontal

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| deprecated | No | No | P | boolean | R/W |

> **Note**
>
> This property has been deprecated in Acrobat 5.0 and later. If accessed, it acts like `toolbar`.

Allows a script to show or hide the Acrobat horizontal toolbar. It does not hide the toolbar in external windows (that is, in an Acrobat window within a web browser).

<a id="42746"></a>
<a id="toolbarvertical"></a>
<a id="id152"></a>
#### toolbarVertical

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| deprecated | No | No | P | boolean | R/W |

> **Note**
>
> This property has been deprecated in Acrobat 5.0 and later. If accessed, it acts like `toolbar`.

Allows a script to show or hide the Acrobat vertical toolbar. It does not hide the toolbar in external windows (that is, in an Acrobat window within a web browser).

<a id="39047"></a>
<a id="viewertype"></a>
<a id="id153"></a>
#### viewerType

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | String | R |

A string that indicates which viewer application is running. It can be one of these values.

| Value | Description |
|-------|-------------|
| `Reader` | Acrobat Reader version 5.0 or earlier / Adobe Reader version 5.1 or later |
| `Exchange` | Adobe Acrobat earlier than version 6.0 / Acrobat Standard version 6.0 or later |
| `Exchange-Pro` | Acrobat Pro version 6.0 or later |

<a id="29204"></a>
<a id="viewervariation"></a>
<a id="id154"></a>
#### viewerVariation

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

Indicates the packaging of the running viewer application. It can be one of these values:

```
Reader
Fill-In
Business Tools
Full
```

<a id="16762"></a>
<a id="viewerversion"></a>
<a id="id155"></a>
#### viewerVersion

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | No | No | All | Number | R |

Indicates the version number of the current viewer application.

<a id="app-methods"></a>
<a id="id156"></a>
### app methods

<a id="52015"></a>
<a id="addmenuitem"></a>
<a id="id157"></a>
#### addMenuItem

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | All |

Adds a menu item to a menu.

> **Note**
>
> Starting Acrobat X, the number of top-level menu items has been reduced. The menu items available from Acrobat X onwards are: File, Edit, View, Window, and Help. If any of your previous scripts referred to a top-level menu item that no longer exists, the reference will not work.

> **Note**
>
> This method can only be executed during application initialization or console events. See the event object for a discussion of JavaScript events.

See also the addSubMenu, execMenuItem, hideMenuItem, and listMenuItems methods.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The language-independent name of the menu item. This name can be used by other methods (for example, `hideMenuItem`) to access the menu item. |
| `cUser` | (optional) The user string (language-dependent name) to display as the menu item name. If `cUser` is not specified, `cName` is used. |
| `cParent` | The name of the parent menu item. Its submenu will have the new menu item added to it. If `cParent` has no submenu, an exception is thrown.  Menu item names can be obtained with the `listMenuItems` method. |
| `nPos` | (optional) The position within the submenu to locate the new menu item. The default behavior is to append to the end of the submenu. Specifying `nPos` as `0` adds the menu to the top of the submenu. Beginning with Acrobat 6.0, the value of `nPos` can also be the language-independent name of a menu item.  (Acrobat 6.0) If the value `nPos` is a string, this string is interpreted as a named item in the menu (a language-independent name of a menu item). The named item determines the position at which the new menu item is to be inserted. See `bPrepend` for additional details.  The `nPos` parameter is ignored in certain menus that are alphabetized. The alphabetized menus are  -  The first section of View > Navigation Panels. -  The first section of View > Toolbars. -  When `nPos` is a number, `nPos` is not obeyed in the Tools menu. A menu item introduced into the Tools menu comes in at the top of the menu. `nPos` is obeyed when it is a string referencing another user-defined menu item. |
| `cExec` | An expression string to evaluate when the menu item is selected by the user.  -  Beginning with Acrobat 7.0, execution of JavaScript through a menu event is no longer privileged. See priv. |
| `cEnable` | (optional) An expression string that is evaluated to determine whether to enable the menu item. The default is that the menu item is always enabled. This expression should set `event.rc` to `false` to disable the menu item. |
| `cMarked` | (optional) An expression string that determines whether the menu item has a check mark next to it. The expression should set `event.rc` to `false` to uncheck the menu item and `true` to check it. The default is that the menu item is not marked. |
| `bPrepend` | (optional, Acrobat 6.0) Determines the position of the new menu item relative to the position specified by `nPos`. The default value is `false`. If `bPrepend` is `true`, the rules for insertion are as follows:   -  If `nPos` is a string, the new item is placed before the named item. -  If `nPos` is a number, the new item is placed before the numbered item. -  If the named item cannot be found or `nPos` is not between zero and the number of items in the list, inclusive, the new item is inserted as the first item in the menu (rather than at the end of the menu).  `bPrepend` is useful when the named item is the first item in a group. |

Example 1: At the top of the File menu, add a menu item that opens an alert dialog box displaying the active document title. This menu is only enabled if a document is opened.

```
app.addMenuItem({ cName: "Hello", cParent: "File",
    cExec: "app.alert(event.target.info.title, 3);",
    cEnable: "event.rc = (event.target != null);",
    nPos: 0
});
```

**Example 2 (Acrobat 6.0)**

Place two menu items in the File menu, one before the Close item and the other after the Close item.

```
// Insert after the "Close" item (the default behavior)
app.addMenuItem( { cName: "myItem1", cUser: "My Item 1", cParent:
    "File", cExec: "_myProc1()", nPos: "Close"});
// Insert before the "Close" item, set bPrepend to true.
app.addMenuItem( { cName: "myItem2", cUser: "My Item 2", cParent:
    "File", cExec: "_myProc2()", nPos: "Close", bPrepend: true });
```

<a id="61494"></a>
<a id="addsubmenu"></a>
<a id="id158"></a>
#### addSubMenu

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | All |

Adds a menu item with a submenu to the application.

See also the addMenuItem, execMenuItem, hideMenuItem, and listMenuItems methods.

> **Note**
>
> Starting Acrobat X, the number of top-level menu items has been reduced. The menu items available from Acrobat X onwards are: File, Edit, View, Window, and Help. If any of your previous scripts referred to a top-level menu item that no longer exists, the reference will not work.

> **Note**
>
> This method can only be executed during application initialization or console events. See the event object for a discussion of JavaScript events.

See also the addSubMenu, execMenuItem, hideMenuItem, and listMenuItems methods.

| Parameter | Description |
|-----------|-------------|
| `cName` | The language-independent name of the menu item. This language-independent name is used to access the menu item (for example, for `hideMenuItem`). |
| `cUser` | (optional) The user string (language-dependent name) to display as the menu item name. If `cUser` is not specified, `cName` is used. |
| `cParent` | The name of the parent menu item to receive the new submenu.  Menu item names can be discovered with `listMenuItems`. |
| `nPos` | (optional) The position within the parent’s submenu to locate the new submenu. The default is to append to the end of the parent’s submenu. Specifying `nPos` as `0` adds the submenu to the top of the parent’s submenu.  The `nPos` parameter is ignored in certain menus that are alphabetized. The alphabetized menus are  -  The first section of View > Navigational Panels. -  The first section of View > Toolbars. -  When `nPos` is a number, `nPos` is not obeyed in the Tools menu. A menu item introduced into the Tools menu comes in at the top of the menu. `nPos` is obeyed when `nPos` is a string referencing another user-defined menu item. |

Example: See the newDoc method.

<a id="99640"></a>
<a id="addtoolbutton"></a>
<a id="id159"></a>
#### addToolButton

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Adds a button to the “Add-on” toolbar of Acrobat 9 or earlier. In Acrobat X, adds a button to the Plugin Addon Tools panel on the right side of the display area.

If there is an active document (for example, `docA.pdf)` open in Acrobat when this method is called to add a button, Acrobat will remove the button when `docA.pdf` is either no longer active or is closed. In the former case, the button will be automatically added to the toolbar if `docA.pdf` becomes the active document again.

The icon size is restricted to 20 by 20 pixels. If an icon of larger dimensions is used, an exception is thrown.

> **Note**
>
> (Acrobat 7.0) A number of changes have been made with regard to the secure use of this method. Execution of `addToolButton` in the console and application initialization is considered privileged execution and is trusted.

If this method is called from nonprivileged script, the warning “JavaScript Window” appears on the “Add-on” toolbar, which will not be dockable. (See priv.)

See also removeToolButton.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | A unique language-independent identifier for the button. The language-independent name is used to access the button for other methods (for example, `removeToolButton`).   -  The value of `cName` must be unique. To avoid a name conflict, check `listToolbarButtons`, which lists all toolbar button names currently installed. |
| `oIcon` | An `Icon Stream` object.  Beginning with Acrobat 7.0, this parameter is optional if a `cLabel` is provided. |
| `cExec` | The expression string to evaluate when the button is selected. |
| `cEnable` | (optional) An expression string that determines whether to enable the toolbutton. The default is that the button is always enabled. This expression should set `event.rc` to `false` to disable the button. |
| `cMarked` | (optional) An expression string that determines whether the toolbutton is marked. The default is that the button is not marked. This expression should set `event.rc` to `true` to mark the button. |
| `cTooltext` | (optional) The text to display in the button help text when the mouse is over the toolbutton. The default is not to have a tool tip.  -  Avoid the use of extended characters in the `cTooltext` string as the string may be truncated. |
| `nPos` | (optional) The button number to place the added button before in the toolbar. If `nPos` is `-1` (the default), the button is appended to the toolbar. |
| `cLabel` | (optional, Acrobat 7.0) A text label to be displayed on the button to the right of the icon. The default is not to have a label. |

**Returns**

`undefined`

Example: Create a button from an icon graphic on the user’s hard drive. This script is executed from the console.

```
// Create a document
var myDoc = app.newDoc();

// import icon (20x20 pixels) from the file specified
myDoc.importIcon("myIcon", "/C/myIcon.jpg", 0);

// convert the icon to a stream.
oIcon = util.iconStreamFromIcon(myDoc.getIcon("myIcon"));

// close the doc now that we have grabbed the icon stream
myDoc.closeDoc(true);

// add a toolbutton
app.addToolButton({
    cName: "myToolButton",
    oIcon: oIcon,
    cExec: "app.alert('Someone pressed me!')",
    cTooltext: "Push Me!",
    cEnable: true,
    nPos: 0
});

app.removeToolButton("myToolButton")
```

See also the example following `util.` iconStreamFromIcon.

<a id="20224"></a>
<a id="alert"></a>
<a id="id160"></a>
#### alert

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Displays an alert dialog box.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cMsg` | A string containing the message to be displayed. |
| `nIcon` | (optional) An icon type. Possible values are these: * *0*: Error (default) * *1*: Warning * *2*: Question * *3*: Status  -  In Mac OS, there is no distinction between warnings and questions. |
| `nType` | (optional) A button group type. Possible values are these: * *0*: OK (default) * *1*: OK, Cancel * *2*: Yes, No * *3*: Yes, No, Cancel |
| `cTitle` | (optional, Acrobat 6.0) The dialog box title. If not specified, the title “Adobe Acrobat” is used. |
| `oDoc` | (optional, Acrobat 6.0) The Doc object that the alert should be associated with. |
| `oCheckbox` | (optional, Acrobat 6.0) If specified, a check box is created in the lower left region of the alert box. `oCheckbox` is a generic JavaScript object that has three properties. The first two property values are passed to the `alert` method; the third property returns a Boolean value. * *cMsg*: (optional) A string to display with the check box. If not specified, the default string is “Do not show this message again”. * *bInitialValue*: (optional) If `true`, the initial state of the check box is checked. The default is `false`. * *bAfterValue*: When the alert method exits, contains the state of the check box when the dialog box is closed. If `true`, the check box was checked when the alert box is closed. |

**Returns**

`nButton`, the type of the button that was pressed by the user:

- *1*: OK
- *2*: Cancel
- *3*: No
- *4*: Yes

Example 1: Display a simple alert box:

```
app.alert({
    cMsg: "Error! Try again!",
    cTitle: "Acme Testing Service"
});
```

Example 2: Close the document with the user’s permission:

```
// A MouseUp action
var nButton = app.alert({
    cMsg: "Do you want to close this document?",
    cTitle: "A message from A. C. Robat",
    nIcon: 2, nType: 2
});
if ( nButton == 4 ) this.closeDoc();
```

**Example 3 (Acrobat 6.0)**

One document creates an alert box in another document. There are two documents, DocA and DocB, one open in a browser and the other in the viewer.

```
// The following is a declaration at the document level in DocA
var myAlertBoxes = new Object;
myAlertBoxes.oMyCheckbox = {
    cMsg: "Care to see this message again?",
    bAfterValue: false
}
```

The following is a mouse-up action in DocA. The variable `theOtherDoc` is the Doc object of DocB. The alert box asks if the user wants to see this alert box again. If the user clicks the check box, the alert does not appear again.

```
if ( !myAlertBoxes.oMyCheckbox.bAfterValue )
{
    app.alert({
        cMsg: "This is a message from the DocA?",
        cTitle: "A message from A. C. Robat",
        oDoc:theOtherDoc,
        oCheckbox: myAlertBoxes.oMyCheckbox
    });
}
```

<a id="40142"></a>
<a id="beep"></a>
<a id="id161"></a>
#### beep

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Causes the system to play a sound.

> **Note**
>
> On Mac OS and UNIX systems the beep type is ignored.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nType` | (optional) The sound type. Values are associated with sounds as follows: * *0*: Error * *1*: Warning * *2*: Question * *3*: Status * *4*: Default (default value) |

<a id="93097"></a>
<a id="beginpriv"></a>
<a id="id162"></a>
#### beginPriv

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | All |

Raises the execution privilege of the current stack frame such that methods marked secure can execute without security exceptions. For the method to succeed, there must be a frame on the stack representing the execution of a trusted function, and all frames (including the frame making the call) between the currently executing frame and that frame must represent the execution of trust propagator functions.

Use `app.endPriv` to revoke privilege. The `app.trustedFunction` method can create a trusted function, and `app.trustPropagatorFunction` can create a trust propagator function. The term stack frame is discussed following the description of `app.trustedFunction`.

**Returns**

`undefined` on success, exception on failure

Example: For examples of usage, see trustedFunction and trustPropagatorFunction.

<a id="38492"></a>
<a id="browsefordoc"></a>
<a id="id163"></a>
#### browseForDoc

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | All |

Presents a file system browser and returns an object containing information concerning the user’s response.

> **Note**
>
> This method can only be executed during a batch or console event. See the event object for a discussion of JavaScript events. See priv.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `bSave` | (optional) A Boolean value that, if `true`, specifies that the file system browser should be presented as it would be for a save operation. The default is `false`. |
| `cFilenameInit` | (optional) A string that specifies the default file name for the file system browser to be populated with. |
| `cFSInit` | (optional) A string that specifies the file system that the file system browser operates on initially. Two values are supported: “” (the empty string) representing the default file system and “CHTTP”. The default is the default file system. This parameter is only relevant if the web server supports WebDAV. |

**Returns**

On success, returns an object that has three properties.

| Property | Description |
|----------|-------------|
| `cFS` | A string containing the resulting file system name for the chosen file. |
| `cPath` | A string containing the resulting path for the chosen file. |
| `cURL` | A string containing the resulting URL for the chosen file. |

If the user cancels, the return value is `undefined`. On error, throws an exception.

Example 1: Browse for a document and report the results to the console.

```
var oRetn = app.browseForDoc({
    cFilenameInit: "myComDoc.pdf",
    cFSInit: "CHTTP",
});
if ( typeof oRetn != "undefined" )
    for ( var o in oRetn )
        console.println( "oRetn." + o + "=" + oRetn[o]);
else console.println("User cancelled!");
```

If the user selects a file on a WebDAV server, a possible output of this code is given below:

```
oRetn.cFS=CHTTP
oRetn.cPath=http://www.example.com/WebDAV/myComDoc.pdf
oRetn.cURL=http://www.example.com/WebDAV/myComDoc.pdf
```

Should the user select a file in the default file system, a typical output of this code is given below:

```
oRetn.cFS=DOS
oRetn.cPath=/C/temp/myComDoc.pdf
oRetn.cURL=file:///C|/temp/myComDoc.pdf
```

The script can go on to open the selected file using `app.openDoc`.

```
var myURL = (oRetn.cFS=="CHTTP") ? encodeURI(oRetn.cPath) : oRetn.cPath;
var oDoc = app.openDoc({cPath: myURL, cFS: oRetn.cFS});
```

> **Note**
>
> `app.openDoc` requires `cPath` to be an escaped string when retrieving a file from a WebDAV server. See `app.` openDoc for a brief description and example.

Example 2: Browse and save a document.

```
var oRetn = app.browseForDoc({
    bSave: true,
    cFilenameInit: "myComDoc.pdf",
    cFSInit: "CHTTP",
});
if ( typeof oRetn != "undefined" ) this.saveAs({
    cFS: oRetn.cFS, cPath: oRetn.cPath, bPromptToOverwrite: false});
```

<a id="17506"></a>
<a id="clearinterval"></a>
<a id="id164"></a>
#### clearInterval

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Cancels a previously registered interval initially set by the `setInterval` method.

See also setTimeOut and clearTimeOut.

**Parameters**

| Property | Description |
|----------|-------------|
| `oInterval` | The registered interval to cancel. |

Example: See setTimeOut.

<a id="16685"></a>
<a id="cleartimeout"></a>
<a id="id165"></a>
#### clearTimeOut

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Cancels a previously registered time-out interval. Such an interval is initially set by `setTimeOut`.

See also setInterval and clearInterval.

**Parameters**

| Property | Description |
|----------|-------------|
| `oTime` | The previously registered time-out interval to cancel. |

Example: See setTimeOut.

<a id="77464"></a>
<a id="endpriv"></a>
<a id="id166"></a>
#### endPriv

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | All |

Revokes any privilege bestowed upon the current stack frame by `app.beginPriv`. Does not revoke privilege bestowed by the current event.

**Related methods** are `app.` trustedFunction, `app.` trustPropagatorFunction and `app.` beginPriv.

**Returns**

`undefined` on success, exception on failure

Example: For examples of usage, see trustedFunction and trustPropagatorFunction.

<a id="27233"></a>
<a id="execdialog"></a>
<a id="id167"></a>
#### execDialog

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Presents a modal dialog box to the user. Modal dialog boxes must be closed by the user before the host application can be directly used again.

The `monitor` parameter specifies a *dialog descriptor*, which is a generic object literal that consists of a set of handler functions for various events and a set of properties that describe the contents of the dialog box.

Dialog box items are identified by an *ItemID*, which is a unique 4-character string. An *ItemID* is necessary only if the element must be referred to elsewhere in the dialog box description (for example, to set or get a value for the element, to add a handler for the element, or to set a tab order including the element).

> **Note**
>
> To distinguish Acrobat dialog boxes from those created by JavaScript, dialog boxes that are added at the document level have a title of “JavaScript Dialog” and display the text “Warning: JavaScript Dialog” at the bottom.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `monitor` | An object literal. It consists of several handlers (see Dialog box handlers) and a `description` property that describes the dialog box elements (see description property). |
| `inheritDialog` | (optional) A `Dialog` object that should be reused when displaying this dialog box. It is useful when displaying a series of dialog boxes (such as a wizard) to prevent one from disappearing before the new one is displayed. The default is not to reuse a dialog box. |
| `parentDoc` | (optional) A Doc object to use as the parent for this dialog box. The default parent is the Acrobat application. |

**Returns**

A string, which is the *ItemID* of the element that caused the dialog box to be dismissed. The return value is “ok” or “cancel” if the dismissing element is the `ok` or `cancel` button.

> **Note**
>
> Debugging is disabled while a modal dialog box created by `app.execDialog` is active.

<a id="26717"></a>
**Dialog box handlers**

The dialog box handlers are called when specific dialog box events occur. Each handler is optional and is passed a `Dialog` object that can be used to query or set values in the dialog box. The supported handlers are listed in the table that follows.

| Dialog box handler | Description |
|--------------------|-------------|
| `initialize` | Called when the dialog box is being initialized. |
| `validate` | Called when a field is modified to determine if the value is acceptable (by returning `true`) or unacceptable (by returning `false`). |
| `commit` | Called when the OK button of the dialog box is clicked. |
| `destroy` | Called when the dialog box is being destroyed. |
| `ItemID` | Called when the dialog box element *ItemID* is modified. For a text box, it is when the text box loses focus. For other controls, it is when the selection changes.  If *ItemID* is not a JavaScript identifier, the name must be enclosed in double quotes when the method is defined, as in the example below. |

```
"bt:1": function () { .. }
  //If *ItemID* is a JavaScript identifier, the double quotes are optional. For example, the following are both correct.  ``"butn": function () { .. }
  butn: function () { .. }
```

<a id="36916"></a>
**description property**

The `description` property is an object literal that contains properties describing the dialog. Its `elements` property specifies the elements of the dialog box, and each of the elements in turn can have an `elements` property describing subelements.

The dialog properties at the root level of the `description` property are listed in the table that follows.

| Property | Type | Description |
|----------|------|-------------|
| `name` | String | The title bar of the dialog box, which should be localized. |
| `first_tab` | String | An *ItemID* for the dialog box item that should be first in the tab order. This dialog box item will also be active when the dialog box is created. This property is required for setting up a tabbing order. See the `next_tab` property defined below. |
| `width` | Numeric | The width of the dialog box in pixels. If no width is specified, the combined width of the contents is used. |
| `height` | Numeric | The height of the dialog box in pixels. If no height is specified, the combined height of the contents is used. |
| `char_width` | Numeric | The width of the dialog box in characters. If no width is specified, the combined width of the contents is used. |
| `char_height` | Numeric | The height of the dialog box in characters. If no height is specified, the combined height of the contents is used. |
| `align_children` | String | The alignment for all descendants. Must be one of the following values: * “align\_left”: Left aligned * “align\_center”: Center aligned * “align\_right”: Right aligned * “align\_top”: Top aligned * “align\_fill”: Align to fill the parent’s width; may widen objects. * “align\_distribute”: Distribute the contents over the parent’s width. * “align\_row”: Distribute the contents over the parent’s width with a consistent baseline. * “align\_offscreen”: Align items one on top of another. |
| `elements` | Array | An array of *object literals* that describe the dialog box elements contained within this dialog (see elements property). |

<a id="26936"></a>
**elements property**

A dialog box `elements` property specifies an object literal with the following set of properties.

| Property | Type | Description |
|----------|------|-------------|
| `name` | String | The displayed name of the dialog box element, which should be localized. This property is ignored for the “edit\_text” type. |
| `item_id` | String | An *ItemID* for this dialog box, which is a unique 4-character string. |
| `type` | String | The type of this dialog box element. It must be one of the following strings: * button” - A push button. * check\_box” - A check box. * radio” - A radio button. * list\_box” - A list box. * hier\_list\_box” - A hierarchical list box. * static\_text” - A static text box. * edit\_text” - An editable text box. * popup” - A pop-up control. * ok” - An OK button. * ok\_cancel” - An OK and Cancel Button. * ok\_cancel\_other” - An OK, Cancel, and Other button. * view” - A container for a set controls. * cluster” - A frame for a set of controls. * gap” - A place holder. |
| `next_tab` | String | An *ItemID* for the next dialog box item in the tab order. Tabbing does not stop at any dialog box item that is not the target of the `next_tab` (or `first_tab`) property. Tabbing should form a circular linked list. |
| `width` | Numeric | Specifies the width of the element in pixels. If no width is specified, the combined width of the contents is used. |
| `height` | Numeric | Specifies the height of the element in pixels. If no height is specified, the combined height of the contents is used. |
| `char_width` | Numeric | Specifies the width of the element in characters. If no width is specified, the combined width of the contents is used. |
| `char_height` | Numeric | Specifies the height of the element in characters. If no height is specified, the combined height of the contents is used. |
| `font` | String | The font to use for this element. Must be one of the following strings: * default” - Default font * dialog” - Dialog box font * palette” - Palette (small) Font |
| `bold` | Boolean | Specify if the font is bold. |
| `italic` | Boolean | Specify if the font is italic. |
| `alignment` | String | Sets the alignment for this element. Must be one of the following values: * align\_left”: Left aligned * align\_center”: Center aligned * align\_right”: Right aligned * align\_top”: Top aligned * align\_fill”: Align to fill the parent’s width; may widen objects. * align\_distribute”: Distribute the contents over the parent’s width. * align\_row”: Distribute the contents over the parent’s width with a consistent baseline. * align\_offscreen”: Align items one on top of another. |
| `align_children` | String | Sets the alignment for all descendants. Possible values are the same as for `alignment`. |
| `elements` | Array | An array of object literals that describe the subelements of this dialog box element. Its properties are the same as those described in this table. |

| Element type | Property | Type | Description |
|--------------|----------|------|-------------|
| static\_text | `multiline` | Boolean | If `true`, this static text element is multiline.  For Mac OS, the height property must be at least 49 to display the up/down buttons, which allow users to read the whole box content. |
| edit\_text | `multiline` | Boolean | If `true`, this edit text element is multiline. |
| edit\_text | `readonly` | Boolean | If `true`, this text element is read only. This property is ignored when `password` is set to `true`. |
| edit\_text | `password` | Boolean | If `true`, this text element is a password field. |
| edit\_text | `PopupEdit` | Boolean | If `true`, it is a pop-up edit text element. |
| edit\_text | `SpinEdit` | Boolean | If `true`, it is a spin edit text element. |
| radio | `group_id` | String | The group name to which this radio button belongs. |
| ok, ok\_cancel,\| ok\_cancel\_other | `ok_name` | String | The name for the OK button. |
| ok, ok\_cancel,\| ok\_cancel\_other | `cancel_name` | String | The name for the cancel button. |
| ok, ok\_cancel,\| ok\_cancel\_other | `other_name` | String | The name for the other button. |

Example 1: The following dialog box descriptor can be a document-level or folder-level JavaScript. The dialog box created contains text fields for your first and last name. When the OK button is clicked, the names entered are reported to the console.

```
var dialog1 = {

    initialize: function (dialog) {
        // Create a static text containing the current date.
        var todayDate = dialog.store()["date"];
        todayDate = "Date: " + util.printd("mmmm dd, yyyy", new Date());
        dialog.load({ "date": todayDate });
    },
    commit:function (dialog) { // called when OK pressed
        var results = dialog.store();
        // Now do something with the data collected, for example,
        console.println("Your name is " + results["fnam"]
            + " " + results["lnam"] );
    },
    description:
    {
        name: "Personal Data",    // Dialog box title
        align_children: "align_left",
        width: 350,
        height: 200,
        elements:
        [
            {
                type: "cluster",
                name: "Your Name",
                align_children: "align_left",
                elements:
                [
                    {
                        type: "view",
                        align_children: "align_row",
                        elements:
                        [
                            {
                                type: "static_text",
                                name: "First Name: "
                            },
                            {
                                item_id: "fnam",
                                type: "edit_text",
                                alignment: "align_fill",
                                width: 300,
                                height: 20
                            }
                        ]
                    },
                    {
                        type: "view",
                        align_children: "align_row",
                        elements:
                        [
                            {
                                type: "static_text",
                                name: "Last Name: "
                            },
                            {
                                item_id: "lnam",
                                type: "edit_text",
                                alignment: "align_fill",
                                width: 300,
                                height: 20
                            }
                        ]
                    },
                    {
                        type: "static_text",
                        name: "Date: ",
                        char_width: 25,
                        item_id: "date"
                    },
                ]
            },
            {
                alignment: "align_right",
                type: "ok_cancel",
                ok_name: "Ok",
                cancel_name: "Cancel"
            }
        ]
    }
};
```

Now, the following line can be executed from actions such as the mouse-up action of a button or a menu action.

```
app.execDialog(dialog1);
```

Example 2: The following example uses a check box and a radio button field. This code might be a document-level JavaScript.

```
var dialog2 =
{
    initialize: function(dialog) {
        // Set a default value for radio button field
        dialog.load({"rd01": true });
        this.hasPet = false;
        // Disable radio button field
        dialog.enable({
            "rd01" : this.hasPet,
            "rd02" : this.hasPet,
            "rd03" : this.hasPet
        });
    },
    commit: function(dialog) {
        // When the user presses "Ok", this handler will execute first
        console.println("commit");
        var results = dialog.store();
        // Do something with the data, for example,
        var hasPet = (this.hasPet) ? "have" : "don't have";
        console.println("You " + hasPet + " a pet.");
        if (this.hasPet)
            console.println("You have " + this.getNumPets(results)
                + " pet(s).");
    },
    getNumPets: function (results) {
        for ( var i=1; i<=3; i++) {
            if ( results["rd0"+i] ) {
                switch (i) {
                    case 1:
                        var nPets = "one";
                        break;
                    case 2:
                        var nPets = "two";
                        break;
                    case 3:
                        var nPets = "three or more";
                }
            }
        };
        return nPets;
    },
    ok: function(dialog) {
        // The handler for the Ok button will be handed after commit
        console.println("Ok!");
    },
    ckbx: function (dialog) {
        // Process the checkbox, if the user has a pet, turn on radios
        this.hasPet = !this.hasPet;
        dialog.enable({
            "rd01" : this.hasPet,
            "rd02" : this.hasPet,
            "rd03" : this.hasPet
        });
    },
    cancel: function(dialog) { // Handle the cancel button
        console.println("Cancel!");
    },
    other: function(dialog){ // Handle the other button
        app.alert("Thanks for pressing me!");
        dialog.end("other"); // End the dialog box, return "other"!
    },
    // The dialog box description
    description:
    {
        name: "More Personal Information",
        elements:
        [
            {
                type: "view",
                align_children: "align_left",
                elements:
                [
                    {
                        type: "static_text",
                        name: "Personal Information",
                        bold: true,
                        font: "dialog",
                        char_width: 30,
                        height: 20
                    },
                    {
                        type: "check_box",
                        item_id: "ckbx",
                        name: "Pet Owner"
                    },
                    {
                        type: "view",
                        align_children: "align_row",
                        elements:
                        [
                            {
                                type: "static_text",
                                name: "Number of pets: "
                            },
                            {
                                type: "radio",
                                item_id: "rd01",
                                group_id: "rado",
                                name: "One"

                            },
                            {
                                type: "radio",
                                item_id: "rd02",
                                group_id: "rado",
                                name: "Two",
                            },
                            {
                                type: "radio",
                                item_id: "rd03",
                                group_id: "rado",
                                name: "Three or more",
                            }
                        ]
                    }
                ]
            },
            {
                type: "gap",    //Add a small vertical gap between
                height: 10      //..radio fields and buttons
            },
            {
                type: "ok_cancel_other",
                ok_name: "Ok",
                cancel_name: "Cancel",
                other_name: "Press Me"
            }
        ]
    }
};
```

The following line can be executed in situations such as the mouse-up action of a button or a menu action.

```
var retn = app.execDialog(dialog2);
```

The value of `retn` is “ok” if the Ok button was clicked, “cancel” if the Cancel button was clicked, and “other” if the button labeled “Press Me” was clicked.

Example 3: This example uses a list box.

```
var dialog3 = {
    // This dialog box is called when the dialog box is created
    initialize: function(dialog) {
        this.loadDefaults(dialog);
    },
    // This dialog box is called when the OK button is clicked.
    commit: function(dialog) {
            // See the Dialog object for a description of how dialog.load
            // and dialog.store work.
            var elements = dialog.store()["subl"];
            // do something with the data.
    },
    // Callback for when the button "butn" is clicked.
    butn: function(dialog) {
        var elements = dialog.store()["subl"]
        for(var i in elements) {
            if ( elements[i] > 0 ) {
                app.alert("You chose "" + i
                    + "", which has a value of " + elements[i] );
            }
        }
    },
    loadDefaults: function (dialog) {
        dialog.load({
            subl:
            {
                "Acrobat Professional": +1,
                "Acrobat Standard": -2,
                "Adobe Reader": -3
            }
        })
    },
    // The dialog box description
    description:
    {
        name: "Adobe Acrobat Products", // Title of the dialog box
        elements: // Child element array
        [
            {
                type: "view",
                align_children: "align_left",
                elements: // Child element array
                [
                    {
                        type: "cluster",
                        name: "Select",
                        elements: // Child Element Array
                        [
                            {
                                type: "static_text",
                                name: "Select Acrobat you use",
                                font: "default"
                            },
                            {
                                type: "list_box",
                                item_id: "subl",
                                width: 200,
                                height: 60
                            },
                            {
                                type: "button",
                                item_id: "butn",
                                name: "Press Me"
                            }
                        ]
                    },
                    {
                        type: "ok_cancel"
                    }
                ]
            }
        ]
    }
}
```

Then execute

```
app.execDialog(dialog3);
```

In the example above, if the line `type: "list_box"` is replaced by `type: "popup"` and the `height` specification is removed, the example will run with a pop-up control rather than a list box.

Example 4: This example shows a hierarchical list box. After the dialog box is opened, a hierarchical list is presented. After a selection is made and the user clicks the Select button, the document jumps to the destination chosen by the user. The Doc object is passed to the dialog box by making it a property of the dialog box.

```
var dialog4 = {
    initialize: function(dialog) {
        dialog.load({
            subl:
                {
                    "Chapter 1":
                    {
                        "Section 1":
                        {
                            "SubSection 1": -1,
                            "SubSection 2": -2,
                        },
                        "Section 2":
                        {
                            "SubSection 1": -3,
                            "SubSection 2": -4,
                        }
                    },
                    "Chapter 3": -5,
                    "Chapter 4": -6
                }
        })
    },
    subl: function(dialog) {
        console.println("Selection Box Hit");
    },
    getHierChoice: function (e)
    {
        if (typeof e == "object") {
            for ( var i in e ) {
                if ( typeof e[i] == "object" ) {
                    var retn = this.getHierChoice(e[i]);
                    if ( retn ) {
                        retn.label = i + ", " + retn.label;
                        return retn;
                    }
                // if e[i] > 0, we've found the selected item
                } else  if ( e[i] > 0 ) return { label:i, value: e[i] };
            }
        } else {
            if ( e[i] > 0 ) return e[i];
        }
    },
    butn: function (dialog)
    {
        var element = dialog.store()["subl"]
        var retn = this.getHierChoice(element);
        if ( retn ) {
            // Write to the console the full name of the item selected
            console.println("The selection you've chosen is ""
                    + retn.label + "", its value is " + retn.value );
            dialog.end("ok");
            // this.doc is the doc object of this document
            this.doc.gotoNamedDest("dest"+retn.value);
        }
        else app.alert("Please make a selection, or cancel");
    },
    cncl: function (dialog) { dialog.end("cancel") },
    // Dialog box description
    description:
    {
        name: "My Novel",
        elements:
        [
            {
                type: "view",
                align_children: "align_left",
                elements:
                [
                    {
                        type: "cluster",
                        name: "Book Headings",
                        elements:
                        [
                            {
                                type: "static_text",
                                name: "Make a selection",
                            },
                            {
                                type: "hier_list_box",
                                item_id: "subl",
                                char_width: 20,
                                height: 200
                            }
                        ]
                    },
                    {
                        type: "view",
                        align_children: "align_row",
                        elements:
                        [
                            {
                                type: "button",
                                item_id: "cncl",
                                name: "Cancel"
                            },
                            {
                                item_id: "butn",
                                type: "button",
                                name: "Select"
                            }
                        ]
                    }
                ]
            }
        ]
    }
};
```

This function attaches the Doc object to the dialog box, then passes the dialog box to the `app.execDialog` method. The `dialog4` object and this function can be at the document level.

```
function dotheDialog(dialog,doc)
{
    dialog.doc = doc;
    var retn = app.execDialog( dialog )
}
```

Finally, the following script can be executed from a mouse-up action, for example.

```
dotheDialog( dialog4, this );
```

<a id="37556"></a>
Example 5: See trustPropagatorFunction which shows how to execute privileged code from a non-privileged context.

<a id="25717"></a>
<a id="execmenuitem"></a>
<a id="id168"></a>
#### execMenuItem

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | No | Yes | All |

Executes the specified menu item.

Beginning with Acrobat 5.0, `app.execMenuItem("SaveAs")` can be called, subject to the restrictions described below. Executing the Save As menu item saves the current file to the user’s hard drive after presenting a dialog box asking the user to select a folder and file name. The file is saved as a linearized file if “Save As Optimizes for Fast Web View” is checked in the Documents preferences.

> **Note**
>
> (Acrobat 7.0) In previous versions of Acrobat, the following code could only be executed during a batch, console or menu event.

```
app.execMenuItem("SaveAs");
```

Acrobat 7.0 removes this restriction, so that `app.execMenuItem("SaveAs")` can be executed during a mouse-up event, for example.

If the user preferences are set to “Save As Optimizes for Fast Web View”, a form object will not survive a Save As operation. Field objects are no longer valid, and an exception may be thrown when trying to access a Field object immediately after saving. See the examples that follow.

For security reasons, scripts are not allowed to execute the Quit menu item. Beginning with Acrobat 6.0, scripts are not allowed to execute the Paste menu item.

(Acrobat 8.0) The execution of menu items through `execMenuItem` method is restricted to a short list of safe menus. The `execMenuItem` method will *silently fail* if a named menu item is executed that is not on the safe menu list. Menu items *may be removed* in future releases, or their *behavior may change*.

To see the list of safe menus, create a form button, and in the Button Properties dialog box, select the Actions tab. From the Select Action list, select “Execute a menu item”. Finally, click the Add button to see the Menu Item dialog box with the list of safe menus.

The `app.execMenuItem` method may be executed, without restriction, in a privileged context, such as in the console or in a batch sequence. For folder JavaScript, `app.execMenuItem` can be executed, again, without restriction, through a trusted function with raised privilege. See Example 4, below.

Another approach to executing `app.execMenuItem` without restriction is through Sign & Certify. When the document author signs and certifies the document, privileged methods can be executed from a non-privileged context provided the document consumer lists the author’s certificate in the list of trusted identities and the consumer trusts the author for execution of embedded high privilege JavaScript.

To ensure a secure environment, the menu items that can be executed are limited to the following:

| AcroSendMail:SendMail | HandMenuItem | ShowHideToolbarBasicTools |
|-----------------------|--------------|---------------------------|
| ActualSize | HelpReader | ShowHideToolbarCommenting |
| AddFileAttachment | InsertPages | ShowHideToolbarData |
| Annots:Tool:InkMenuItem | LastPage | ShowHideToolbarEdit |
| BookmarkShowLocation | NextPage | ShowHideToolbarEditing |
| Close | OneColumn | ShowHideToolbarFile |
| CropPages | OpenOrganizer | ShowHideToolbarFind |
| DeletePages | PageSetup | ShowHideToolbarForms |
| DocHelpUserGuide | PrevPage | ShowHideToolbarMeasuring |
| ExtractPages | Print | ShowHideToolbarNavigation |
| Find | PropertyToolbar | ShowHideToolbarPageDisplay |
| FindCurrentBookmark | Quit | ShowHideToolbarPrintProduction |
| FindSearch | ReplacePages | ShowHideToolbarRedaction |
| FirstPage | RotatePages | ShowHideToolbarTasks |
| FitHeight | SaveAs | ShowHideToolbarTypewriter |
| FitPage | Scan | SinglePage |
| FitVisible | ShowHideAnnotManager | Spelling |
| FitWidth | ShowHideArticles | Spelling:Check |
| FullScreen | ShowHideBookmarks | TwoColumns |
| GeneralInfo (Properties) | ShowHideFields | TwoPages |
| GeneralPrefs | ShowHideFileAttachment | Web2PDF:OpenURL |
| GoBack | ShowHideModelTree | ZoomDragMenuItem |
| GoBackDoc | ShowHideOptCont | ZoomTo |
| GoForward | ShowHideSignatures | ZoomViewIn |
| GoForwardDoc | ShowHideThumbnails | ZoomViewOut |
| GoToPage |  |  |

This list applies only to document-level access to menu items. It does not apply to application-level JavaScript or JavaScript from a privileged context.

The list is written to the Acrobat registry and can be edited if you determine that the list must be expanded. If you need to modify the list, you can edit the related registry entries:

- The key for the default list is HKEY\_LOCAL\_MACHINESOFTWAREPoliciesAdobeAdobe Acrobat9.0FeatureLockDowncDefaultExecMenuItems.
- The key for the list used by Tuner is HKEY\_LOCAL\_MACHINESOFTWAREPoliciesAdobeAdobe Acrobat9.0FeatureLockDowncAdminExecMenuItems.

For both keys, the value name is `tWhiteList` and the type is `REG_SZ`. The value data contains all menu item names and each menu item name is separated with the “|” delimiter.

See also addMenuItem, addSubMenu, and hideMenuItem. Use listMenuItems to have the console list the names of all menu items.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cMenuItem` | The menu item to execute.  A list of menu item names can be obtained with `listMenuItems`. |
| `oDoc` | (optional, Acrobat 7.0) `oDoc` is the Doc object of a document that is not hidden (see the Doc object hidden property). If this parameter is present, `execMenuItem` executes the menu item in the document’s context. |

Example 1: This example executes the File > Open menu item. It displays a dialog box asking for the file to be opened.

```
app.execMenuItem("Open");
```

Example 2 (Acrobat 5.0)

This example illustrates how a form object does not survive the execution of `app.execMenuItem("SaveAs")`, as noted above.

```
var f = this.getField("myField");
// Assume preferences set to save linearized
app.execMenuItem("SaveAs");
// Exception thrown, field not updated
f.value = 3;
```

Example 3 (Acrobat 5.0)

After executing `app.execMenuItem("SaveAs")`, Field objects must be acquired again.

```
var f = this.getField("myField");
// Assume preferences set to save linearized
app.execMenuItem("SaveAs");
// Get the field again after the linear save
var f = getField("myField");
// Field updated to a value of 3
f.value = 3;
```

**Example 4 (Acrobat 8.0 and later)**

Execute `app.execMenuItem` in folder JavaScript using a trusted function.

```
myTrustedMenu = app.trustedFunction( function( name )
{
    app.beginPriv();
    app.execMenuItem(name);
    app.endPriv();
});
```

Once Acrobat or Adobe Reader is restarted, the script, for example,

```
myTrustedMenu("PropertyToolbar");
```

may be executed from a non-privileged context, such as a mouse-up button action, without silent failure. The script above shows/hides the Properties toolbar.

<a id="28851"></a>
<a id="getnthpluginname"></a>
<a id="id169"></a>
#### getNthPlugInName

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| deprecated | No | No | All |

> **Note**
>
> This method has been superseded by the `plugIns` property.

Obtains the name of the *n* th plug-in that has been loaded by the viewer.

**Parameters**

| Property | Description |
|----------|-------------|
| `nIndex` | The *n* th plug-in loaded by the viewer. |

**Returns**

`cName`, the plug-in name that corresponds to `nIndex`.

<a id="92839"></a>
<a id="getpath"></a>
<a id="id170"></a>
#### getPath

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | All |

**Returns** the path to folders created during installation. A distinction is made between application folders and user folders. The method throws a `GeneralError` exception (see Error object) if the path does not exist.

> **Note**
>
> (Acrobat 7.0) This method can only be executed during a batch or console event (see the event object). See also priv.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cCategory` | (optional) The category of folder sought. Valid values are `app` (the default) and `user`. |
| `cFolder` | (optional) A platform-independent string that indicates the folder. Valid values are  *root, eBooks, preferences, sequences, documents, javascript, stamps, dictionaries, plugIns spPlugIns,help, temp, messages, resource, update*  The default is `root`. |

**Returns**

The path to the folder determined by the parameters. An exception is thrown if the folder does not exist.

Example 1: Find the path to the user’s Sequences folder.

```
try {
    var userBatch = app.getPath("user","sequences");
} catch(e) {
    var userBatch = "User has not defined any custom batch sequences";
}
console.println(userBatch);
```

<a id="28719"></a>
Example 2: On a Windows platform, create and save a document to the My Documents folder.

```
var myDoc = app.newDoc();
var myPath = app.getPath("user", "documents") + "/myDoc.pdf"
myDoc.saveAs(myPath);
myDoc.closeDoc();
```

<a id="20707"></a>
<a id="goback"></a>
<a id="id171"></a>
#### goBack

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Goes to the previous view on the view stack, which is equivalent to clicking the Previous View button on the Acrobat toolbar.

Example: Create a go-back button. This code could be part of a batch sequence, for example, to place navigation buttons on the selected PDF documents.

```
var aRect = this.getPageBox();
var width = aRect[2] - aRect[0];
// The rectangle is 12 points high and 18 points wide, centered at bottom
rect = [width/2-8, 10, width/2+8, 22];
f = this.addField("goBack", "button", 0, rect);
f.textFont="Wingdings";
f.textSize=0;
f.buttonSetCaption("u00E7");              // Left pointing arrow
f.setAction("MouseUp", "app.goBack()");    // Add an action
```

<a id="76600"></a>
<a id="goforward"></a>
<a id="id172"></a>
#### goForward

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Goes to the next view on the view stack, which is equivalent to clicking the go Next View button on the Acrobat toolbar.

Example: See the example following `app.` goBack.

<a id="35938"></a>
<a id="hidemenuitem"></a>
<a id="id173"></a>
#### hideMenuItem

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | No | Yes | All |

Removes a specified menu item.

See also addMenuItem, addSubMenu, execMenuItem, and listMenuItems.

> **Note**
>
> This method can only be executed during a console or application initialization event. See the event object for a discussion of JavaScript events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The menu item name to remove.  Menu item names can be discovered with `listMenuItems`. |

<a id="18455"></a>
<a id="hidetoolbarbutton"></a>
<a id="id174"></a>
#### hideToolbarButton

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | No | Yes | All |

Removes the specified toolbar button from the “Add-on” toolbar of Acrobat 9 or earlier. In Acrobat X, hides the specified button from the Plugin Addon Tools panel on the right side of the display area.

> **Note**
>
> This method can only be executed during console or application initialization event. See the event object for a discussion of JavaScript events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The name of the toolbar button to remove.  Toolbar item names can be discovered with `listToolbarButtons`. |

Example: A file named, `myConfig.js`, containing the following script is placed in one of the folder-level JavaScript folders.

```
app.hideToolbarButton("Hand");
```

When the viewer is started, the “Hand” icon does not appear.

<a id="88818"></a>
<a id="launchurl"></a>
<a id="id175"></a>
#### launchURL

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | All |

Launches a URL in a browser window.

> **Note**
>
> Beginning with Acrobat 8.1, File and JavaScript URLs can be executed only when operating in a privileged context, such as during a batch or console event. File and JavaScript URLs begin with the scheme names `javascript` or `file`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cURL` | A string that specifies the URL to launch. |
| `bNewFrame` | (optional) If `true`, this method launches the URL in a new window of the browser application. The default is `false`. |

**Returns**

The value `undefined` is returned on success. An exception is thrown on failure.

Example 1:

```
app.launchURL("http://www.example.com/", true);
```

<a id="94035"></a>
Example 2: Add an online help item to the menu system. This code should be placed in a folder-level JavaScript file, or executed from the JavaScript Debugger console.

```
app.addMenuItem({
    cName: "myHelp", cUser: "Online myHelp",
    cParent: "Help",
    cExec: "app.launchURL('www.example.com/myhelp.html');",
    nPos: 0
});
```

**Related methods** are openDoc and the Doc object getURL method.

<a id="86089"></a>
<a id="listmenuitems"></a>
<a id="id176"></a>
#### listMenuItems

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Beginning with Acrobat 6.0, returns an array of `TreeItem` objects, which describes a menu hierarchy.

Prior to Acrobat 6.0, this method returned a list of menu item names to the console.

See also addMenuItem, addSubMenu, execMenuItem, and hideMenuItem.

**Returns**

Array of `TreeItem` objects.

<a id="63097"></a>
**TreeItem Object**

A generic JavaScript object that represents a menu or toolbar item hierarchy. An array of these objects is returned by `app.listMenuItems` and `app.listToolbarButtons` (starting in Acrobat 6.0). It contains the following properties.

| `cName` | The name of a menu item or toolbar button. |
|---------|--------------------------------------------|
| `oChildren` | (optional) An array of `treeItem` objects containing the submenus or flyout buttons. |

Example 1: List all menu item names to the console.

```
var menuItems = app.listMenuItems()
for( var i in menuItems)
    console.println(menuItems[i] + "n")
```

Example 2: List all menu items to the console using a fancy format.

```
function FancyMenuList(m, nLevel)
{
    var s = "";
    for (var i = 0; i < nLevel; i++) s += " ";
    console.println(s + "+-" + m.cName);
    if ( m.oChildren != null )
        for ( var i = 0; i < m.oChildren.length; i++ )
            FancyMenuList(m.oChildren[i], nLevel + 1);
}
var m = app.listMenuItems();
for ( var i=0; i < m.length; i++ ) FancyMenuList(m[i], 0);
```

<a id="35171"></a>
<a id="listtoolbarbuttons"></a>
<a id="id177"></a>
#### listToolbarButtons

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Beginning with Acrobat 6.0, returns an array of `treeItem` objects that describes a toolbar hierarchy (with flyout toolbars).

Prior to Acrobat 6.0, this method displayed a list of toolbar button names in the console.

(Acrobat 8.0) In the Documents category of the Preferences dialog box, when “Show each document in its own window (requires restart)” item is checked, the document window must be empty in order for `listToolbarButtons` to return the array of `TreeItem` objects.

**Returns**

Array of `TreeItem` objects

Example: List all toolbar names in the console.

```
var toolbarItems = app.listToolbarButtons()
for( var i in toolbarItems)
    console.println(toolbarItems[i] + "n")
```

See also the hideToolbarButton method.

<a id="76382"></a>
<a id="loadpolicyfile"></a>
<a id="id178"></a>
#### loadPolicyFile

- - Version (Key)
  - Save-Prefs
  - Security
  - Product
- - 9.0
  - No
  - No
  - All

Specifies a cross-domain policy file from a location specified by the url parameter. Acrobat uses policy files as a permission mechanism to permit PDFs to load data from servers other than their own. With the addition of `app.loadPolicyFile()`, Acrobat can load policy files from arbitrary locations, as shown in the following example:

```
app.loadPolicyFile("http://www.example.com/sub/dir/pf.xml");
```

This causes Acrobat to retrieve a policy file from the specified URL when a crossdomain policy check is required. Any permissions granted by the policy file at that location will apply to all content at the same level or lower in the virtual directory hierarchy of the server. The following code continues the previous example:

```
this.getURL("http://www.example.com/sub/dir/vars.txt", true) // allowed
this.getURL("http://www.example.com/sub/dir/deep/vars2.txt", true) // allowed
this.getURL("http://www.example.com/mydir/vars3.txt", true) // not allowed
```

Any number of policy files can be loaded using `loadPolicyFile()`. When considering a request that requires a policy file, Acrobat always waits for the completion of any policy file downloads before denying a request. As a final fallback, if no policy file specified with `loadPolicyFile()` authorizes a request, Acrobat consults the original default location, `/crossdomain.xml`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `url` | The url of the location of a cross-domain policy file.  The length of url is limited to 1024 bytes. If a larger string is passed an exception is thrown.  -  This method does not take single object argument with properties that contain the arguments as many JavaScript for Acrobat methods do. The argument of this method is a string. |

**Returns**

Nothing

<a id="75294"></a>
<a id="mailgetaddrs"></a>
<a id="id179"></a>
#### mailGetAddrs

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

> **Note**
>
> This method is a Windows-only feature.

Displays an address book dialog box to let the user choose e-mail recipients. The dialog box is optionally prepopulated with semicolon-separated lists of addressees in the `cTo`, `cCc`, and `cBcc` strings. The `bCc` and `bBcc` Boolean values control whether the user should be allowed to choose CC and BCC recipients.

See also mailMsg, the Doc object methods mailDoc and mailForm, the `FDF` object mail method and the `Report` object mail method.

> **Note**
>
> (Acrobat 7.0) This method can only be executed during a batch or console event. See also priv. See the event object for a discussion of JavaScript events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cTo` | (optional) A semicolon-separated list of “To” addressees to use. |
| `cCc` | (optional) A semicolon-separated list of CC addressees to use. |
| `cBcc` | (optional) A semicolon-separated list of BCC addressees to use. |
| `cCaption` | (optional) A string to appear on the caption bar of the address dialog box. |
| `bCc` | (optional) A Boolean value to indicate whether the user can choose CC recipients. |
| `bBcc` | (optional) A Boolean value to indicate whether the user can choose BCC recipients. This Boolean should only be used when `bCc` is `true` ; otherwise, the method fails (and returns `undefined`). |

**Returns**

On failure (the user cancelled), returns undefined. On success, returns an array of three strings for To, CC, and BCC.

Example: Give the user two chances to provide mail addresses.

```
var attempts = 2;
while (attempts > 0)
{
    var recipients = app.mailGetAddrs
    ({
        cCaption: "Select Recipients, Please",
        bBcc: false
    })
    if (typeof recipients == "undefined" ) {
        if (--attempts == 1)
            app.alert("You did not choose any recipients, try again");
    } else break;
}
if (attempts == 0)
    app.alert("Cancelling the mail message");
else {
    // JavaScript statements to send mail
}
```

<a id="29487"></a>
<a id="mailmsg"></a>
<a id="id180"></a>
#### mailMsg

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | No | Yes | All |

Sends out an e-mail message with or without user interaction.

See also the Doc object mailDoc and mailForm methods, the `FDF` object mail method and the `Report` object mail method.

> **Note**
>
> On Windows: The client machine must have its default mail program configured to be MAPI enabled to use this method.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `bUI` | Indicates whether user interaction is required. If `true`, the remaining parameters are used to seed the compose-new-message window that is displayed to the user. If `false`, the `cTo` parameter is required and others are optional.   -  (Acrobat 7.0) When this method is executed in a non-privileged context, the `bUI` parameter is not honored and defaults to `true`. See priv. |
| `cTo` | A semicolon-separated list of addressees. |
| `cCc` | (optional) A semicolon-separated list of CC addressees. |
| `cBcc` | (optional) A semicolon-separated list of BCC addressees. |
| `cSubject` | (optional) Subject line text. The length limit is 64 KB. |
| `cMsg` | (optional) Mail message text. The length limit is 64 KB. |

Example: Open the compose new message window.

```
app.mailMsg(true);
```

Send the message to `fun1@example.com` and `fun2@example.com`.

```
app.mailMsg(false, "fun1@example.com; fun2@example.com", "", "",
"This is the subject", "This is the body of the mail.");
```

It is possible to compose a message containing form data.

```
var cMyMsg = "Below are the current budget figures:nn";
cMyMsg += "Date Compiled: " + this.getField("date").value + "n";
cMyMsg += "Current Estimate: " + this.getField("budget").value + "n";
app.mailMsg({
    bUI: true,
    cTo: "myBoss@example.com",
    cSubject: "The latest budget figures",
    cMsg: cMyMsg
} );
```

<a id="24970"></a>
<a id="newdoc"></a>
<a id="id181"></a>
#### newDoc

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | Yes | Not available in Reader |

Creates a new document and returns its Doc object. The optional parameters specify the media box dimensions of the document in points.

> **Note**
>
> This method can only be executed during a batch or console event. See priv. See the event object for a discussion of JavaScript events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `nWidth` | (optional) The width (in points) for the new document. The default value is 612. |
| `nHeight` | (optional) The height (in points) for the new document. The default value is 792. |

**Returns**

The object of the newly created document.

Example: Add a New item to the Acrobat File menu. Within New, there are three menu items: Letter, A4, and Custom. This script should go in a folder-level JavaScripts `.js` file.

```
app.addSubMenu({ cName: "New", cParent: "File", nPos: 0 })
app.addMenuItem({ cName: "Letter", cParent: "New", cExec:
    "app.newDoc();"});
app.addMenuItem({ cName: "A4", cParent: "New", cExec:
    "app.newDoc(420,595)"});
app.addMenuItem({ cName: "Custom...", cParent: "New", cExec:
    "var nWidth = app.response({ cQuestion:'Enter Width in Points',
        cTitle:     'Custom Page Size'});"
    +"if (nWidth == null) nWidth = 612;"
    +"var nHeight = app.response({ cQuestion:'Enter Height in Points',
        cTitle: 'Custom Page Size'});"
    +"if (nHeight == null) nHeight = 792;"
    +"app.newDoc({ nWidth: nWidth, nHeight: nHeight })"});
```

The script above works for versions of Acrobat prior to 7.0. For Acrobat 7.0, it works correctly if the user JavaScript preference Enable Menu Items JavaScript Execution Privileges is enabled.

If this item is not checked, the `app.newDoc` method must be executed through a `trustedFunction` because execution of JavaScript through a menu event is no longer privileged beginning with Acrobat 7.0. See priv.

The same example can be worked as follows:

```
trustedNewDoc = app.trustedFunction( function (nWidth, nHeight)
{
    app.beginPriv();
        switch( arguments.length ) {
            case 2:
                app.newDoc( nWidth, nHeight );
                break;
            case 1:
                app.newDoc( nWidth );
                break;
            default:
                app.newDoc();
        }
    app.endPriv();
})
app.addSubMenu({ cName: "New", cParent: "File", nPos: 0 })
app.addMenuItem({ cName: "Letter", cParent: "New", cExec:
    "trustedNewDoc();"});
app.addMenuItem({ cName: "A4", cParent: "New", cExec:
    "trustedNewDoc(420,595)"});
app.addMenuItem({ cName: "Custom...", cParent: "New", cExec:
    "var nWidth = app.response({ cQuestion:'Enter Width in Points',
        cTitle: 'Custom Page Size'});"
    +"if (nWidth == null) nWidth = 612;"
    +"var nHeight = app.response({ cQuestion:'Enter Height in Points',
        cTitle: 'Custom Page Size'});"
    +"if (nHeight == null) nHeight = 792;"
    +"trustedNewDoc(nWidth, nHeight) "});
```

The code is incomplete. In the case of the Custom menu item, additional lines can be inserted to prevent the user from entering the empty string, or a value too small or too large. See the [PDF Reference](https://adobe.com/go/pdfreference) for the current limitations.

Example: Create a blank document and acquire the Doc object, then insert a watermark.

```
var myNewDoc = app.newDoc();
myNewDoc.addWatermarkFromText("Confidential",0,font.Helv,24,color.red);
```

This example uses the Doc object addWatermarkFromText method.

<a id="10067"></a>
<a id="newcollection"></a>
<a id="id183"></a>
#### newCollection

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 9.0 | No | No | All |

Creates a new collection-based PDF, a PDF portfolio, with no content.

To work with an existent PDF portfolio, begin with Doc. collection.

**Returns**

A Doc object of the newly created PDF.

Example: Create a new PDF portfolio and get the Doc object of the newly created PDF.

```
var doc = app.newCollection();
```

<a id="93566"></a>
<a id="newfdf"></a>
<a id="id184"></a>
#### newFDF

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Creates a new `FDF` object that contains no data.

> **Note**
>
> This method is available only during batch, console and application initialization. Not available in Adobe Reader. See priv.

**Returns**

A new `FDF` object.

Example: Create an FDF with an embedded PDF file.

```
var fdf = app.newFDF();
fdf.addEmbeddedFile( "/c/myPDFs/myFile.pdf", 1);
fdf.save( "/c/myFDFs/myFile.fdf" );
```

This example continues following the description of `app.` openFDF.

<a id="61826"></a>
<a id="opendoc"></a>
<a id="id185"></a>
#### openDoc

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Opens a specified PDF document and returns its Doc object. This object can be used by the script to call methods, or to get or set properties in the newly opened document.

> **Note**
>
> When a batch sequence is running, a modal dialog box is open, which prevents user interference while processing. Consequently, this method cannot be executed through a batch sequence.

> **Note**
>
> The `app.openDoc` API cannot be called from a doc open script. A script which is executed on the doc open action is known as doc open script. In such cases, Viewer raises a `NotAllowedError` exception, which `escript` passes to the user. However, it can be called successfully from other triggers, such as a page open action.

An exception is thrown and an invalid Doc object is returned when an HTML document is opened using this method. To catch the exception, enclose `app.openDoc` in a `try/catch` construct. See example 2 below.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cPath` | A device-independent path to the document to be opened. If `oDoc` is specified, the path can be relative to it. The target document must be accessible in the default file system.  -  When `cFS` is set to “CHTTP”, the `cPath` string should be escaped, perhaps using the core JavaScript global function `encodeURI`. See [Example 5 (Acrobat 7.0)](./app-apis.md#30714) below. |
| `oDoc` | (optional) A Doc object to use as a base to resolve a relative `cPath`. Must be accessible in the default file system. |
| `cFS` | (optional, Acrobat 7.0) A string that specifies the source file system name. Two values are supported: “” (the empty string, which is the default), representing the default file system, and “CHTTP”. This parameter is relevant only if the web server supports WebDAV. |
| `bHidden` | (optional, Acrobat 7.0) A Boolean value that if `true`, opens the PDF file with its window hidden. The default is `false`. |
| `bUseConv` | (optional, Acrobat 7.0) A Boolean value that is used when `cPath` references a non-PDF file. If `true`, the method tries to convert the non-PDF file to a PDF document. The default is `false`.   -  (Acrobat 7.0) `bUseConv` can only be set to `true` during a console or batch event. See also priv. |
| `cDest` | (optional, Acrobat 8.0) The name of the destination within a document. This parameter forces opening at named destination within the PDF document. For details on named destinations and how to create them, see the [PDF Reference](https://adobe.com/go/pdfreference). |

**Returns**

A Doc object or `null` :

- In Acrobat 5.0, this method returns a Doc object.
- In Acrobat 5.0.5, the method returns the Doc object unless the `disclosed` property of the target document is not `true`, in which case it returns `null`.
- Beginning with the Acrobat 5.0.5 Accessibility and Forms Patch and continuing with Acrobat 6.0 and later, `openDoc` behaves as follows:
  - During a batch, console or menu event, `openDoc` ignores the `disclosed` property and returns the Doc object of the file specified by `cPath`.
  - During any other event, `openDoc` returns the Doc, if `disclosed` is `true`, and `null`, otherwise.

Example 1: This example opens another document, inserts a prompting message into a text field, sets the focus in the field, and then closes the current document.

```
var otherDoc = app.openDoc("/c/temp/myDoc.pdf");
otherDoc.getField("name").value="Enter your name here: "
otherDoc.getField("name").setFocus();
this.closeDoc();
```

Same example as above, but a relative path is used.

```
var otherDoc = app.openDoc("myDoc.pdf", this);
otherDoc.getField("name").value="Enter your name here: "
otherDoc.getField("name").setFocus();
this.closeDoc();
```

This example uses the Doc closeDoc method and the Field object setFocus method.

<a id="25282"></a>
Example 2: Open an HTML document on the user’s hard drive and convert it to PDF.

```
try {
    app.openDoc("/c/myWeb/myHomePage.html");
} catch (e) {};
```

**Example 3 (Acrobat 7.0)**

Open a hidden PDF document, extract information from it, and close it.

```
oDoc = app.openDoc({
    cPath:"/C/myDocs/myInfo.pdf",
    bHidden: true
});
var v = oDoc.getField("myTextField").value;
this.getField("yourTextField").value = v;
oDoc.closeDoc();
```

**Example 4 (Acrobat 7.0)**

Open a non-PDF file by converting it to a PDF document. The following script can be executed successfully from the console.

```
app.openDoc({
    cPath: "/c/temp/myPic.jpg",
    bUseConv: true
})
```

<a id="30714"></a>
**Example 5 (Acrobat 7.0)**

Open a file from a WebDAV server. The `app.openDoc` method requires the path to the file to be escaped.

```
var myURL = encodeURI("http://www.example.com/My Folder/ComDoc.pdf");
app.openDoc({cPath: myURL, cFS: "CHTTP" });
```

See also `app.` browseForDoc.

<a id="78489"></a>
**Example 6 (Acrobat 8.0)**

Open a document and jump to a named destination.

```
app.openDoc({ cPath: "/c/temp/myDoc.pdf", cDest: "myDest" });
```

In versions previous to 8.0, this jump is not possible unless the document is `disclosed`. See the example following gotoNamedDest.

<a id="28383"></a>
<a id="openfdf"></a>
<a id="id186"></a>
#### openFDF

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | Yes | Not available in Reader |

Creates a new `FDF` object by opening the specified file. The `FDF` object has methods and properties that can be used on the data that this file contains.

> **Note**
>
> This method is available only during batch, console and application initialization events. See also priv.

**Parameters**

| Property | Description |
|----------|-------------|
| `cDIPath` | The device-independent path to the file to be opened. |

**Returns**

The `FDF` object for the FDF file that is opened.

Example: Create an FDF file with an embedded PDF file.

```
var fdf = app.newFDF();
fdf.addEmbeddedFile( "/c/myPDFs/myFile.pdf", 1);
fdf.save( "/c/myFDFs/myFile.fdf" ); // save and close this FDF

// Now open the FDF file and embed another PDF doc.
var fdf = app.openFDF( "/c/myFDFs/myFile.fdf" );
fdf.addEmbeddedFile( "/c/myPDFs/myOtherFile.pdf", 1);
fdf.save( "/c/myFDFs/myFile.fdf" ); // save and close this FDF
```

See the `FDF` object signatureSign method for another example of usage.

<a id="24690"></a>
<a id="popupmenu"></a>
<a id="id187"></a>
#### popUpMenu

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

> **Note**
>
> `popUpMenuEx` is preferred over this method.

Creates a pop-up menu at the current mouse position, containing the specified items.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cItem` | (optional) If the argument is a string, it is listed in the menu as a menu item. The menu item name “-” is reserved to draw a separator line in the menu. |
| `Array` | (optional) If the argument is an array, it appears as a submenu where the first element in the array is the parent menu item. This array can contain further submenus. |

**Returns**

The name of the menu item that was selected, or `null` if no item was selected.

Example: Create a pop-up menu consisting of chapter of a document.

```
var cChoice = app.popUpMenu("Introduction", "-", "Chapter 1",
    [ "Chapter 2", "Chapter 2 Start", "Chapter 2 Middle",
    ["Chapter 2 End", "The End"]]);
app.alert("You chose the "" + cChoice + "" menu item");
```

<a id="40999"></a>
<a id="popupmenuex"></a>
<a id="id188"></a>
#### popUpMenuEx

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Creates a pop-up menu at the current mouse position. Each of the parameters is a `MenuItem` object that describes a menu item to be included in the pop-up menu.

This method is preferred over the use of `popUpMenu`.

**Parameters**

One or more `MenuItem` objects (see below).

**Returns**

The `cReturn` value of the menu item that was selected, or its `cName` if `cReturn` was not specified for that item. The method returns `null` if no selection was made.

<a id="52312"></a>
**MenuItem Object**

This generic JavaScript object represents a menu item. It has the following properties.

| Property | Description |
|----------|-------------|
| `cName` | The menu item name, which is the string to appear on the menu item. The value of “-” is reserved to draw a separator line in the menu. |
| `bMarked` | (optional) A Boolean value specifying whether the item is to be marked with a check. The default is `false` (not marked). |
| `bEnabled` | (optional) A Boolean value specifying whether the item is to appear enabled or grayed out. The default is `true` (enabled). |
| `cReturn` | (optional) A string to be returned when the menu item is selected. The default is the value of `cName`. |
| `oSubMenu` | (optional) A `MenuItem` object representing a submenu item or an array of submenu items, each represented by a `MenuItem` object. |

Example 1: Show all the features of the `popUpMenuEx` method.

```
var cChoice = app.popUpMenuEx
   (
       {cName: "Item 1", bMarked:true, bEnabled:false},
       {cName: "-"},
       {cName: "Item 2", oSubMenu:
           [ {cName: "Item 2, Submenu 1"},
               {
                   cName: "Item 2, Submenu 2",
                   oSubMenu: {cName:"Item 2, Submenu 2, Subsubmenu 1", cReturn: "0"}
               }
           ]
       },
       {cName: "Item 3"},
       {cName: "Item 4", bMarked:true, cReturn: "1"}
   )
   app.alert("You chose the "" + cChoice + "" menu item");
```

<a id="87385"></a>
Example 2: Because the `popupMenuEx` method takes a list of `MenuItem` objects, its parameters cannot be passed to it as a JavaScript variable. As a workaround, you can create an array of menu items and use the Function object method `apply` from core JavaScript. This method allows arguments to be passed as an array.

```
// Declare pop-up menu properties as an array.
var aParams = [
    {cName: "Example Web Page", cReturn: "www.example.com"},
    {cName: "-"},
    {cName: "The Example Product Line",
     cReturn: "www.example.com/products/main.html"},
    {cName: "Example Reader",
     cReturn: "www.example.com/products/reader/main.html"}
];
// Apply the function app.popUpMenuEx to the app object, with an array
// of parameters aParams
var cChoice = app.popUpMenuEx.apply( app, aParams );
if ( cChoice != null ) app.launchURL(cChoice);
```

<a id="29847"></a>
<a id="removetoolbutton"></a>
<a id="id189"></a>
#### removeToolButton

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Removes a previously added button from the toolbar.

> **Note**
>
> (Acrobat 7.0) To remove a toolbutton added by the `addToolButton` method, `removeToolButton` must be executed within the same context as when `addToolButton` was executed.

If no document was open in Acrobat when the button was added, there must be no document open in Acrobat when the button is removed. See example 2 below.

Similarly, if a certain document was the active document when a toolbutton was added, that same document must be active for the button to be removed using `removeToolButton`.

In the case of a document that is active when the toolbutton is added, the button is automatically removed when this document is closed. See also the notes following the description of addToolButton.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cName` | The language-independent identifier provided when `addToolButton` was called. |

Example 1: See the example following addToolButton.

<a id="26425"></a>
Example 2: This example shows the removal of a toolbutton with the same context as `addToolButton`. Initially, there is no document open in the Acrobat. Execute the following code from the console:

```
app.addToolButton({cName: "button1", cExec:"app.alert('pressed');",

     cTooltext:"Button1"});
```

Open a PDF document in Acrobat and execute the next line from the console:

```
app.removeToolButton({cName:"button1"});
```

An exception is thrown and the removal of the button fails.

If you close the PDF document and execute the `removeToolButton` script again, the button is removed.

<a id="87724"></a>
<a id="response"></a>
<a id="id190"></a>
#### response

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Displays a dialog box containing a question and an entry field for the user to reply to the question.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cQuestion` | The question to be posed to the user. |
| `cTitle` | (optional) The title of the dialog box. |
| `cDefault` | (optional) A default value for the answer to the question. If not specified, no default value is presented. |
| `bPassword` | (optional) If `true`, indicates that the user’s response should show as asterisks (\*) or bullets (•) to mask the response, which might be sensitive information. The default is `false`. |
| `cLabel` | (optional, Acrobat 6.0) A short string to appear in front of and on the same line as the edit text field. |

**Returns**

A string containing the user’s response. If the user clicks the Cancel button, the response is the `null` object.

Example: Asks for a response from the user and report back the response.

```
var cResponse = app.response({
    cQuestion: "How are you today?",
        cTitle: "Your Health Status",
        cDefault: "Fine",
        cLabel: "Response:"
});
if (cResponse == null)
    app.alert("Thanks for trying anyway.");
else
    app.alert("You responded, ""+cResponse+"", to the health "
        + "question.",3);
```

<a id="89991"></a>
<a id="setinterval"></a>
<a id="id191"></a>
#### setInterval

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Specifies a JavaScript script and a time period. The script is executed every time the period elapses.

The return value of this method must be held in a JavaScript variable. Otherwise, the interval object is subject to garbage-collection, which would cause the clock to stop.

To terminate the periodic execution, pass the returned interval object to `clearInterval`.

> **Note**
>
> Beginning with Acrobat 7.05, an interval is automatically terminated when the document whose script called `setInterval` is closed (assuming it was not previously terminated).

Opening and closing the document JavaScripts dialog box causes the JavaScript interpreter to re-read the document JavaScripts and consequently to re-initialize any document-level variables. Resetting document-level variables in this way after JavaScript expressions have been registered to be evaluated by `setInterval` or `setTimeOut` may cause JavaScript errors if those scripts use document-level variables.

See also clearInterval, setTimeOut and clearTimeOut.

**Parameters**

| Property | Description |
|----------|-------------|
| `cExpr` | The JavaScript script to be executed. |
| `nMilliseconds` | The time period in milliseconds. |

**Returns**

An `interval` object

Example: Create a simple color animation on a field called “Color” that changes every second.

```
function DoIt() {
    var f = this.getField("Color");
    var nColor = (timeout.count++ % 10 / 10);
    // Various shades of red.
    var aColor = new Array("RGB", nColor, 0, 0);
    f.fillColor = aColor;
}
// save return value as a variable
timeout = app.setInterval("DoIt()", 1000);
// Add a property to our timeout object so that DoIt() can keep
// a count going.
timeout.count = 0;
```

See setTimeOut for an additional example.

<a id="17472"></a>
<a id="settimeout"></a>
<a id="id192"></a>
#### setTimeOut

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

Specifies a JavaScript script and a time period. The script is executed one time only, after the period elapses.

The return value of this method must be held in a JavaScript variable. Otherwise, the timeout object is subject to garbage-collection, which would cause the clock to stop.

To cancel the timeout event, pass the returned timeout object to `clearTimeOut`.

> **Note**
>
> Beginning with Acrobat 7.05, an interval is automatically terminated when the document whose script called `setInterval` is closed (assuming it was not previously terminated).

Opening and closing the document JavaScripts dialog box causes the JavaScript interpreter to re-read the document JavaScripts and consequently to re-initialize any document-level variables. Resetting document-level variables in this way after JavaScript expressions have been registered to be evaluated by setInterval or `setTimeOut` may cause JavaScript errors if those scripts use document-level variables.

See also clearTimeOut, setInterval, and clearInterval.

**Parameters**

| Property | Description |
|----------|-------------|
| `cExpr` | The JavaScript script to be executed. |
| `nMilliseconds` | The time period in milliseconds. |

**Returns**

A `timeout` object

Example: Create a simple running marquee. Assume there is a text field named “marquee”. The default value of this field is “Adobe Acrobat version 8.0 will soon be here!”.

```
// Document-level JavaScript function
function runMarquee() {
    var f = this.getField("marquee");
    var cStr = f.value;
    // get field value
    var aStr = cStr.split("");        // Convert to an array
    aStr.push(aStr.shift());          // Move first char to last
    cStr = aStr.join("");             // Back to string again
    f.value = cStr;                   // Put new value in field
}

// Insert a mouse-up action into a "Go" button
run = app.setInterval("runMarquee()", 100);
// stop after a minute
stoprun=app.setTimeOut("app.clearInterval(run)",6000);

// Insert a mouse-up action into a "Stop" button
try {
    app.clearInterval(run);
    app.clearTimeOut(stoprun);
} catch (e){}
```

The Stop button code is protected with a try/catch construct. If the user clicks the Stop button without having first clicked Go, `run` and `stoprun` will be undefined and the Stop code will throw an exception. When the exception is thrown, the `catch` code is executed. In this example, the code does nothing if the user clicks Stop first.

<a id="32666"></a>
<a id="trustedfunction"></a>
<a id="id193"></a>
#### trustedFunction

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | No | All |

Marks a function as trusted. Trusted functions can explicitly increase the current *privilege level* for their stack frame. Typically, the stack frame (which corresponds to the body of the function) contains security-restricted methods that require a privileged context in which to run. By increasing the privilege level, these restricted methods can be executed in non-privileged contexts. See priv.

Within the body of the function definition, calls to the `app.beginPriv` and `app.endPriv` methods must enclose any code that normally executes in a privileged context, as the examples below show.

> **Note**
>
> This method is available only during batch, console and application initialization events

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oFunc` | A function object that specifies the function to mark as trusted. |

**Returns**

On success, returns the same function object that was passed in. After successful execution, the function object will be trusted. On error, throws `NotAllowedError`.

**Syntax**

This method can be called in two ways.

```
myTrustedFunction = app.trustedFunction(
    function()
    {
        <function body>
    }
);
```

or

```
function myOtherTrustedFunction()
{
    <function body>
};
app.trustedFunction(myOtherTrustedFunction);
```

The following examples, along with the examples following the `app.trustPropagatorFunction` method, contain many comments that clarify the notion of trusted function and highlight some of the nuances of the topic.

Example 1: `app.newDoc` is a security-restricted method that needs a privileged context in which to run. For example, it cannot normally be executed from a mouse-up event. This example shows how this method can be executed from a mouse-up event by creating a trusted function.

Place the following script in a `.js` file in the User (or App) JavaScript folder.

```
trustedNewDoc = app.trustedFunction( function (nWidth, nHeight)
{
    // Additional code may appear above
    app.beginPriv();    // Explicitly raise privilege
    app.newDoc( nWidth, nHeight );
    app.endPriv();
    // Additional code may appear below.
})
```

After Acrobat is restarted, the `trustedNewDoc` function can be executed from anywhere. The following script for a mouse-up action of a button creates a new document that is 200 points by 200 points.

```
trustedNewDoc( 200, 200 );
```

Because of security restrictions, `app.newDoc(200,200)` cannot normally be executed from a mouse-up event. The trusted function permits the creation of a new document.

> **Note**
>
> This example is simplified. The trusted function could be modified so that it also has the two optional arguments of the `app.newDoc` method.

The `trustedNewDoc` function can also be executed as a menu item.

```
app.addMenuItem( {
    cName: "myTrustedNewDoc",
    cUser: "New Doc", cParent: "Tools",
    cExec: "trustedNewDoc(200,200)", nPos: 0
} );
```

Again, `trustedNewDoc` could be enhanced by having the user input the dimensions for the new document, either through a series of `app.response` dialog boxes, or a full dialog box, created by `app.execDialog`.

> **Note**
>
> If `app.newDoc` is not enclosed in the `app.beginPriv/app.endPriv` pair, executing `trustedNewDoc` from a non-privileged context will fail and an exception will be thrown. You must explicitly raise the privilege level in the way shown.

Example 2: The `app.activeDocs` property behaves differently depending on the setting:

- During a console or batch event, it returns an array of all active documents.
- In a non-privileged context, it returns an array of only those active documents that have their `disclosed` property set to `true`.

To overcome this limitation in non-privileged context, you can define a trusted function that raises the privilege level and calls `activeDocs`. This function would be defined in a `.js` file in the User (or App) JavaScript folder.

```
trustedActiveDocs = app.trustedFunction (
    function()
    {
        app.beginPriv(); // Explicitly raise the privilege
        var d = app.activeDocs;
        app.endPriv();
        return d;
    }
)
```

The following code can be executed from a mouse-up action of a form button.

```
var d = trustedActiveDocs();
console.println("There are d = " + d.length
    + " files open in the viewer.")
for ( var i=0; i< d.length; i++)
    console.println((i+1) + ". " + d[i].documentFileName )
```

The console reports the number and file name of all documents—disclosed or not—open in the viewer.

<a id="70390"></a>
Example 3: A trusted function is capable of explicitly increasing the current privilege level only for its own stack frame. This example shows some related issues.

The following code attempts to make a trusted function more modular:

```
function mySaveAs(doc, path)
{
    doc.saveAs(doc, path);
}
myFunc = app.trustedFunction( function (doc, path)
{
    // privileged and/or non-privileged code here
    app.beginPriv();
    mySaveAs(doc, path);
    app.endPriv();
    // privileged and/or non-privileged code here
}
```

A problem occurs because when the privileged code `doc.saveAs(doc, path)` is executed, it is not within the stack frame (function body) of the calling trusted function `myFunc` but rather within the stack frame of `mySaveAs`, which is not a trusted function. Therefore, when `myFunc` is executed in a non-privileged context, it throws an exception.

A possible solution is to make `mySaveAs` into a trusted function so that `myFunc` succeeds. However, this exposes the privileged `doc.saveAs` function to non-privileged execution by anyone that knows this function is on your system.

You cannot simply enclose `doc.saveAs(doc,path)` in a `beginPriv/endPriv` pair. When `myFunc` is run from a non-privileged context, an exception will be thrown by the `app.beginPriv` within the body of the `mySaveAs` function. This is because `mySaveAs` is not trusted and therefore is not authorized to request an increased privilege level.

To summarize the observations above, there is a need for a kind of function that has the following characteristics:

- It can be called by a trusted function.
- It is not trusted itself and therefore cannot be directly called from a non-privileged context.

A *trust propagator* function satisfies these criteria (see trustPropagatorFunction below).

<a id="79731"></a>
<a id="trustpropagatorfunction"></a>
<a id="id194"></a>
#### trustPropagatorFunction

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 7.0 | No | Yes | All |

Marks a function as a *trust propagator*. Such a function is not itself trusted but can inherit trust if called from a trusted function.

A trust propagator function propagates trust, not privilege. Therefore, as with the method `app.trustedFunction`, an `app.beginPriv/app.endPriv` pair must enclose any code within the function body that normally executes in a privileged context.

Trust propagator functions can play the role of utility functions. They can be called by a trusted function and by another trust propagator function, but they cannot successfully be called by a function that is not trusted in a non-privileged context.

> **Note**
>
> Functions defined in `.js` files in the App JavaScript folder are implicitly trust propagator functions. Functions defined in `.js` files in the User JavaScript folder are not.

This method is available only during batch, console, and application initialization.

**Syntax**

This method can be called in two ways.

```
myPropagatorFunction = app.trustPropagatorFunction(
    function()
    {
        <function body>
    }
);
```

or

```
function myOtherPropagatorFunction()
{
    <function body>
};
app.trustPropagatorFunction(myOtherPropagatorFunction);
```

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oFunc` | A function object that specifies the function to mark as a trust propagator. |

**Returns**

On success, returns the same function object that was passed in. After successful execution, the function object will be a trust propagator. On error, throws `NotAllowedError`.

Example 1: For background, see example 3 following trustedFunction.

This example defines a trust propagator function, `mySaveAs`, to save a file to a folder, and a trusted function, `myTrustedSpecialTaskFunc`, to perform various tasks involving privileged and non-privileged code. The `mySaveAs` function cannot be called directly in a non-privileged context.

```
mySaveAs = app.trustPropagatorFunction(function(doc,path)
{
    app.beginPriv();
        doc.saveAs(path);
    app.endPriv();
})
myTrustedSpecialTaskFunc = app.trustedFunction(function(doc,path)
{
    // Privileged and/or non-privileged code above
    app.beginPriv();
        mySaveAs(doc,path);
    app.endPriv();
    // Privileged and/or non-privileged code below
});
```

Executing the code from a mouse-up button, for example, saves the current document to the specified path.

```
myTrustedSpecialTaskFunc(this, "/c/temp/mySavedDoc.pdf");
```

<a id="71246"></a>
Example 2: This example develops a simple dialog box using the `app.execDialog` method and executes privileged code.

The dialog box asks for your name and asks you to browse for a document from your local hard drive (or a network drive). When you click the OK button, the selected file is loaded into the viewer and your name is placed in the author field of the document properties. (The insertion of the name only occurs if the author field is empty.) The dialog box also displays the value of `identity.email`, which is privileged information.

Any privileged code is enclosed by a `beginPriv/endPriv` pair.

Note the use of the `ANTrustPropagateAll` function, which is useful for creating dialog boxes that use privileged code. It takes a single object as its argument, turns every function in the object into a trust propagator function, then returns that object.

```
myDialog = app.trustedFunction(function()
{
    app.beginPriv();
    var dialog = ANTrustPropagateAll({
        initialize:function(dialog) {
            this.data = {};   // An object to hold dialog data
            app.beginPriv();
            dialog.load({ "emai": "Email: " + identity.email });
            app.endPriv();
        },
        commit:function (dialog) { // Called when OK pressed
            var results = dialog.store();
            console.println("Your name is " + results["name"] );
            this.data.name = results["name"];
        },
        brws: function (dialog) {
            app.beginPriv();
            var oRetn = app.browseForDoc();
            if ( typeof oRetn != "undefined")
                this.data.oRetn = oRetn;
            app.endPriv();
        },
        doDialog:function() {
            app.beginPriv();
            var retn = app.execDialog(this);
            app.endPriv();
            return retn;
        },
        description: {
            name: "Open File & Populate Info Field",
            align_children: "align_left",
            elements:
            [
                {
                    type: "view",
                    align_children: "align_left",
                    elements:
                    [
                        {
                            type: "view",
                            align_children: "align_row",
                            elements:
                            [
                                {
                                    type: "static_text",
                                    name: "Name: "
                                },
                                {
                                    item_id: "name",
                                    type: "edit_text",
                                    alignment: "align_fill",
                                    width: 300,
                                    height: 20
                                },
                            ]
                        },
                        {
                            type: "static_text",
                            item_id: "emai",
                            name: "Email: ",
                            char_width: 25
                        },
                        {
                            type: "gap",
                            height: 10
                        },
                        {
                            type: "view",
                            align_children: "align_row",
                            elements:
                            [
                                {
                                    type: "button",
                                    name: "Browse",
                                    item_id: "brws"
                                },
                                {
                                    type: "ok_cancel",
                                    ok_name: "Ok",
                                    cancel_name: "Cancel"
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    });
    app.endPriv();
    try { // Protect against user pressing the Esc key
        // After everything is set up, run the dialog box using the doDialog
        // function, defined in the object dialog.
        var retn = dialog.doDialog();
        app.beginPriv();
        // If the user clicked the Ok button and there is oRetn data we load
        // the requested file using app.openDoc(), a restricted method.
        if ( (retn == "ok") && dialog.data.oRetn ) {
            var oDoc = app.openDoc({
                cPath: dialog.data.oRetn.cPath,
                cFS: dialog.data.oRetn.cFS
            });
            if ( !oDoc.info.Author  )
                oDoc.info.Author = dialog.data.name;
        }
        app.endPriv();
    } catch(e) {}
})
```

This dialog box can be activated from a button or, more appropriately, from a menu item or a toolbar button. For example, place the following code in a User JavaScript file to add a menu item to the Tools menu.

```
app.addMenuItem( { cName: "myDialog", cUser: "My Cool Dialog",
    cParent: "Tools", cExec: "myDialog()", nPos: 0 } );
```

<a id="19976"></a>
<a id="app-media"></a>
<a id="id195"></a>
## app.media

This object defines properties and functions useful in multimedia JavaScript code.

Several `app.media` properties are enumeration objects that list the values allowed in various properties. Future versions of Acrobat may add more such values, and JavaScript code should be prepared to encounter values other than the ones listed here. Similarly, JavaScript code may be run on an older version of Acrobat than it was designed for, in which case it must fall back to using the values available in that version.

> **Note**
>
> The `app.media` is part of the Acrobat 6.0 (and Later) Compatible Media JavaScript API. Multimedia assets that use this approach rely on the underlying operating system to locate and launch a multimedia player residing on the user’s system. Acrobat 9.0 natively supports Flash video (FLV) and Flash applications (SWF) which can be embedded in, or streamed to, a PDF document. Native support for Flash enables reliable cross-platform playback. No additional media player or specific codec is necessary.

Acrobat 6.0 (and Later) Compatible Media is superseded by the multimedia of Acrobat 9.0, which uses rich media annotations. Developers of PDFs with multimedia assets are, therefore, strongly encouraged to use the rich media annotations of Acrobat 9. Refer to the AnnotRichMedia object for JavaScript support for rich media annotations.

<a id="app-media-properties"></a>
<a id="id196"></a>
### app.media properties

<a id="81246"></a>
<a id="align"></a>
<a id="id197"></a>
#### align

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values that may be found in the `MediaSettings.floating.align` property. The alignment is relative to the window specified by the `MediaSettings.floating.over` property. (See the values for `app.media.` over.)

Valid values are listed in the table below.

| Value | Position of floating window |
|-------|-----------------------------|
| `app.media.align.topLeft` | At the top left corner |
| `app.media.align.topCenter` | At the top center |
| `app.media.align.topRight` | At the top right corner |
| `app.media.align.centerLeft` | At the center left |
| `app.media.align.center` | At the center |
| `app.media.align.centerRight` | At the center right |
| `app.media.align.bottomLeft` | At the bottom left corner |
| `app.media.align.bottomCenter` | At the bottom center |
| `app.media.align.bottomRight` | At the bottom right corner |

<a id="97250"></a>
<a id="canresize"></a>
<a id="id198"></a>
#### canResize

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values that may be found in the `MediaSettings.floating.canResize` property, which specifies whether a floating window may be resized by the user.

These values are listed in the table below.

| Value | Description |
|-------|-------------|
| `app.media.canResize.no` | May not be resized |
| `app.media.canResize.keepRatio` | May be resized only if the aspect ratio is preserved |
| `app.media.canResize.yes` | May be resized without preserving the aspect ratio |

<a id="42939"></a>
<a id="closereason"></a>
<a id="id199"></a>
#### closeReason

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values that may be found in the `event.reason` property for a Close event. These values are:

- app.media.closeReason.general
- app.media.closeReason.error
- app.media.closeReason.done
- app.media.closeReason.stop
- app.media.closeReason.play
- app.media.closeReason.uiGeneral
- app.media.closeReason.uiScreen
- app.media.closeReason.uiEdit
- app.media.closeReason.docClose
- app.media.closeReason.docSave
- app.media.closeReason.docChange

See the afterClose and onClose methods of the `EventListener` object.

<a id="55562"></a>
<a id="defaultvisible"></a>
<a id="id200"></a>
#### defaultVisible

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R |

This property is defined as `true`, which is the default value for `MediaSettings.visible`.

<a id="99487"></a>
<a id="ifoffscreen"></a>
<a id="id201"></a>
#### ifOffScreen

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values allowed in a `MediaSettings.floating.ifOffScreen` property, which specifies what action should be taken if the floating window is positioned totally or partially offscreen.

These values and their descriptions are given in the table below.

| Value | Description |
|-------|-------------|
| `app.media.ifOffScreen.allow` | Take no action |
| `app.media.ifOffScreen.forceOnScreen` | Move and/or resize the window so that it is on-screen |
| `app.media.ifOffScreen.cancel` | Cancel playing the media clip |

<a id="95552"></a>
<a id="layout"></a>
<a id="id202"></a>
#### layout

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values allowed in a `MediaSettings.layout` property.

The table below contains the values and their descriptions.

| Value | Description |
|-------|-------------|
| `app.media.layout.meet` | Scale to fit all content, preserve aspect, no clipping, background fill |
| `app.media.layout.slice` | Scale to fill the window, preserve aspect, and clip X or Y as needed |
| `app.media.layout.fill` | Scale X and Y separately to fill the window |
| `app.media.layout.scroll` | Natural size with scrolling |
| `app.media.layout.hidden` | Natural size with clipping |
| `app.media.layout.standard` | Use the player’s default settings |

<a id="91536"></a>
<a id="monitortype"></a>
<a id="id203"></a>
#### monitorType

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values allowed in a `MediaSettings.monitorType` property.

The table below contains the values and their descriptions:

| Value | Description |
|-------|-------------|
| `app.media.monitorType.document` | The monitor containing the largest section of the document window |
| `app.media.monitorType.nonDocument` | The monitor containing the smallest section of the document window |
| `app.media.monitorType.primary` | Primary monitor |
| `app.media.monitorType.bestColor` | Monitor with the greatest color depth |
| `app.media.monitorType.largest` | Monitor with the greatest area (in pixels squared) |
| `app.media.monitorType.tallest` | Monitor with the greatest height (in pixels) |
| `app.media.monitorType.widest` | Monitor with the greatest width (in pixels) |

<a id="16905"></a>
<a id="opencode"></a>
<a id="id204"></a>
#### openCode

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values that may be found in the code property of the return value from `MediaPlayer.open`. The values are:

- app.media.openCode.success
- app.media.openCode.failGeneral
- app.media.openCode.failSecurityWindow
- app.media.openCode.failPlayerMixed
- app.media.openCode.failPlayerSecurityPrompt
- app.media.openCode.failPlayerNotFound
- app.media.openCode.failPlayerMimeType
- app.media.openCode.failPlayerSecurity
- app.media.openCode.failPlayerData

<a id="77583"></a>
<a id="over"></a>
<a id="id205"></a>
#### over

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values allowed in a `MediaSettings.floating.over` property, the value of which is used to align a floating window. See `app.media.align`.

| Value | Description |
|-------|-------------|
| `app.media.over.pageWindow` | Align the floating window relative to the document (page) window |
| `app.media.over.appWindow` | Align the floating window relative to the application window |
| `app.media.over.desktop` | Align the floating window relative to the full virtual desktop |
| `app.media.over.monitor` | Align the floating window relative to the (selected) monitor display screen |

<a id="24937"></a>
<a id="pageeventnames"></a>
<a id="id206"></a>
#### pageEventNames

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values that may be found in the `event.name` property for a page-level action. Event names that represent direct user actions are not included here. This enumeration is used to distinguish page-level actions from user actions. The values are:

- app.media.pageEventNames.Open
- app.media.pageEventNames.Close
- app.media.pageEventNames.InView
- app.media.pageEventNames.OutView

Example: `app.media.pageEventNames` can be used to distinguish between a page-level action and a direct user action. The script below is folder-level or document-level JavaScript that can be called from anywhere in a document.

```
function myMMfunction () {
    if ( app.media.pageEventNames[event.name] ) {
        console.println("Page Event: " + event.name);
        ...
    } else {
        console.println("User Generated Event: " + event.name);
        ...
    }
}
```

<a id="30071"></a>
<a id="raisecode"></a>
<a id="id207"></a>
#### raiseCode

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates values that may be found in the `error.raiseCode` property when an exception is thrown. This property exists only when `error.name` is “RaiseError”. Other values may be encountered in addition to these.

```
app.media.raiseCode.fileNotFound
app.media.raiseCode.fileOpenFailed
```

<a id="51270"></a>
<a id="raisesystem"></a>
<a id="id208"></a>
#### raiseSystem

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates values that may be found in the `error.raiseSystem` property when an exception is thrown. This property exists only when `error.name` is “RaiseError”.

```
app.media.raiseSystem.fileError
```

Other values may be added to the above property.

<a id="45162"></a>
<a id="renditiontype"></a>
<a id="id209"></a>
#### renditionType

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values that may be found in `Rendition.type`. The values and their descriptions are given below.

| Value | Description |
|-------|-------------|
| `app.media.renditionType.unknown` | A type not known by this version of Acrobat |
| `app.media.renditionType.media` | A media rendition |
| `app.media.renditionType.selector` | A rendition selector |

<a id="19461"></a>
<a id="status"></a>
<a id="id210"></a>
#### status

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values that may be found in the `event.media.code` property for a Status event (see onStatus  and afterStatus). Most of these values have additional information that is found in the `event.text` property. The values are:

| Value | Description |
|-------|-------------|
| `app.media.status.clear` | Empty string—this status event clears any message |
| `app.media.status.message` | General message |
| `app.media.status.contacting` | Hostname being contacted |
| `app.media.status.buffering` | Progress message or nothing |
| `app.media.status.init` | Name of the engine being initialized |
| `app.media.status.seeking` | Empty string |

Along with the `event.media.status` code, there is also the `event.media.text`, a string that reflects the current status, as described above.

<a id="64005"></a>
<a id="trace"></a>
<a id="id211"></a>
#### trace

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R/W |

Set this property to `true` to print trace messages to the JavaScript console during player creation and event dispatching.

> **Note**
>
> `app.media.trace` is for test purposes only. Do not use this property in a PDF file that you publish. It will change in future versions of Acrobat.

<a id="81793"></a>
<a id="version"></a>
<a id="id212"></a>
#### version

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Number | R |

The version number of the multimedia API, currently 7.0.

<a id="31862"></a>
<a id="windowtype"></a>
<a id="id213"></a>
#### windowType

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Object (enumeration) | R |

Enumerates the values allowed in a `MediaSettings.windowType` property. These values are given in the table below.

| Value | Description |
|-------|-------------|
| `app.media.windowType.docked` | Docked to a PDF page |
| `app.media.windowType.floating` | Floating (pop-up) window |
| `app.media.windowType.fullScreen` | Full screen mode |

<a id="app-media-methods"></a>
<a id="id214"></a>
### app.media methods

<a id="53287"></a>
<a id="addstockevents"></a>
<a id="id215"></a>
#### addStockEvents

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Adds stock EventListeners to a `MediaPlayer` object and sets `player.stockEvents` as a reference to these listeners for later removal.

If the optional `annot` parameter is provided, a reference to the annotation is saved in `MediaPlayer.annot`. Later, when the player is opened with `MediaPlayer.open`, stock `EventListeners` will also be added to this annotation and `annot.player` will be set as a reference to the player.

**Parameters**

| Property | Description |
|----------|-------------|
| `player` | A required `MediaPlayer` object |
| `annot` | (optional) A `ScreenAnnot` object |

The stock EventListeners provide standard Acrobat behavior such as focus handling.

If `app.media.trace` is `true`, debug trace listeners are also included with the stock EventListeners.

Use the `removeStockEvents` method to remove EventListeners that were added with `addStockEvents`.

The `app.media.createPlayer` and `app.media.openPlayer` methods call `addStockEvents` internally, so in most cases it is not necessary to call this method yourself.

<a id="98736"></a>
<a id="alertfilenotfound"></a>
<a id="id216"></a>
#### alertFileNotFound

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Displays the standard file not found alert, with an optional Don’t Show Again check box.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oDoc` | `oDoc` is the Doc the alert is associated with |
| `cFilename` | `cFilename` is the name of the missing file |
| `bCanSkipAlert` | (optional) If `bCanSkipAlert` is `true` and the user checks the check box, returns `true`, otherwise returns `false`. The default is `false`. |

**Returns**

If `bCanSkipAlert` is `true`, returns `true` if the check box is checked, otherwise returns `false`.

Example:

```
if ( !doNotNotify )
{
    var bRetn = app.media.alertFileNotFound(this, cFileClip, true );
    var doNotNotify = bRetn;
}
```

<a id="81716"></a>
<a id="alertselectfailed"></a>
<a id="id217"></a>
#### alertSelectFailed

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Displays the standard alert for a `rendition.select` failure.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oDoc` | The Doc the alert is associated with |
| `oRejects` | (optional) If provided, an array of `MediaReject` objects as returned by `PlayerInfoList.select`. |
| `bCanSkipAlert` | (optional) If `true` and the user checks the check box, the method returns `true` ; otherwise, the method returns `false`. The default is `false`. |
| `bFromUser` | (optional) A Boolean value that affects the wording of the alert message. It should be `true` if a direct user action triggered this code, or `false` if some other action, such as selecting a bookmark, triggered it. The default is `false`. |

**Returns**

If `bCanSkipAlert` is `true`, returns `true` if the check box is checked, otherwise returns `false`.

> **Note**
>
> When `rendition.select` fails to find a usable player, and the `select` parameter `bWantRejects` is set to `true`, the returned `MediaSelection` object will contain an array of `MediaReject` objects, which can be passed to this method as the `oRejects` parameter. The `alertSelectFailed` method will, in turn, ask the user to go to the web to download an appropriate player.

Example: Displays Cannot Play Media Clip, with check box.

```
var bRetn = app.media.alertSelectFailed({
    oDoc: this,
    bCanSkipAlert: true
});
```

<a id="89486"></a>
<a id="argsdwim"></a>
<a id="id218"></a>
#### argsDWIM

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This method is a “do what I mean” function that is used by `app.media.createPlayer`, `app.media.openPlayer`, and `app.media.startPlayer`. It fills in default values for properties that are not provided in the `PlayerArgs` object, picking them out of the `event` object, so that these functions may be used as rendition action event handlers with no arguments or in custom JavaScript with explicit arguments.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `args` | A `PlayerArgs` object (see `app.media`. createPlayer). |

**Returns**

`PlayerArgs` object

Example: See createPlayer for an example of usage.

<a id="45001"></a>
<a id="canplayoralert"></a>
<a id="id219"></a>
#### canPlayOrAlert

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Determines whether any media playback is allowed and returns `true` if it is. If playback is not allowed, it alerts the user and returns `false`.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `args` | A `PlayerArgs` object (see `app.media.` createPlayer). |

**Returns**

`true` if media playback is allowed, otherwise `false`.

> **Note**
>
> The `createPlayer` method calls this function before attempting to create a player. If you write your own code to substitute for `createPlayer`, you can call `canPlayOrAlert` to alert the user in situations where playback is not allowed, such as in multimedia authoring mode.

The only property in the `args` object that is used is `doc`, so you can use the following code.

```
// There is a Doc in myDoc
if( app.media.canPlayOrAlert({ doc: myDoc })
/* OK to create player here */ ;
```

The above code displays “Cannot play media while in authoring mode”, or other alerts, as appropriate.

<a id="29947"></a>
<a id="computefloatwinrect"></a>
<a id="id220"></a>
#### computeFloatWinRect

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Calculates and returns the rectangle in screen coordinates needed as specified by its parameters.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `doc` | The Doc object for the document. |
| `floating` | The floating parameters from the object returned by `MediaSettings.floating`. |
| `monitorType` | A number indicating which monitor to use. See the `app.media.` monitorType property. |
| `uiSize` | (optional) The user interface size given as an array of four numbers \[w, x, y, z\] representing the size, as returned by `MediaPlayer.uiSize`. |

**Returns**

The rectangle in screen coordinates.

Example: Get the calculated rectangle for a floating window.

```
var floating =
{
    over: app.media.over.monitor,
    align: app.media.align.center,
    canResize: app.media.canResize.no,
    hasClose: false,
    hasTitle: true,
    width: 400,
    height: 400
}
var rect = app.media.computeFloatWinRect
    (this, floating, app.media.monitorType.primary);
```

<a id="75243"></a>
<a id="constrainrecttoscreen"></a>
<a id="id221"></a>
#### constrainRectToScreen

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a rectangle of screen coordinates, moved and resized if needed to place it entirely on some display monitor. If `anchorPt` is provided and `rect` must be shrunk to fit, it shrinks proportionally toward `anchorPt` (which is an array of two numbers representing a point as \[x, y\]).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `rect` | An array of four numbers representing the screen coordinates of the d rectangle. |
| `anchorPt` | (optional) An array of two points \[x, y\] that is to be an anchor point. |

**Returns**

A rectangle in screen coordinates.

<a id="97532"></a>
<a id="createplayer"></a>
<a id="id222"></a>
#### createPlayer

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Creates a `MediaPlayer` object without opening the player.

> **Note**
>
> To open the player, call `MediaPlayer.open`. You can combine these two steps into one by calling `app.media.openPlayer` instead of `createPlayer`.

If `createPlayer` is called inside a rendition action (for example, in custom JavaScript entered from the Actions tab in the Multimedia Properties panel), default values are taken from the action’s `event` object. The `args` parameter is not required in this case unless you want to override the rendition action’s values. `createPlayer` calls `argsDWIM` to process the `event` object and `args` (see PlayerArgs object object) parameter.

Unless `noStockEvents` of the `PlayerArgs` object is set to `true`, the `MediaPlayer` object is equipped with stock EventListeners that provide the standard behavior required to interact properly with Acrobat. Additional EventListeners can be provided in the PlayerArgs object or may be added afterward with `MediaPlayer.events.add`.

If `args.annot.player` is an open `MediaPlayer`, `createPlayer` closes that player, which triggers events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `args` | A PlayerArgs object, whose required and optional properties are described below.  If `createPlayer` is executed within a Rendition action with an associated rendition, this parameter is optional and its properties are populated by the defaults and by options selected in the UI. Otherwise, this parameter is required. |

<a id="42847"></a>
**PlayerArgs object**

| Property | Type | Description |
|----------|------|-------------|
| `doc` | Object | The Doc object of the document. Required if both `annot` and `rendition` are omitted, for example, for URL playback. |
| `annot` | Object | A `ScreenAnnot` object. Required for docked playback unless it is found in the `event` object or `MediaSettings.page` is provided. The new player is associated with the annotation. If a player was already associated with the annotation, it is stopped and closed. |
| `rendition` | Object | (optional) A `Rendition` object (either a MediaRendition or a RenditionList). Required unless `rendition` is found in the `event` object or `URL` is present. |
| `URL` | String | Either `URL` or `rendition` is required, with `URL` taking precedence. |
| `mimeType` | String | (optional) Ignored unless `URL` is present. If `URL` is present, either `mimeType` or `settings.players`, as returned by `app.media.getPlayers`, is required. |
| `settings` | Object | (optional) A `MediaSettings` object. Overrides the `rendition` settings. |
| `events` | Object | (optional) An `EventListener` object. Optional if stock events are used, added after stock events. |
| `noStockEvents` | Boolean | (optional) If `true`, do not use stock events. The default is `false`. |
| `fromUser` | Boolean | (optional) It should be `true` if a direct user action will trigger this code, or `false`, otherwise. The default depends on the `event` object. |
| `showAltText` | Boolean | (optional) If `true`, show alternate text (see `Rendition.` altText) if the media cannot be played. The default is `true`. |
| `showEmptyAltText` | Boolean | (optional) If `true` and alternate text (see `Rendition.` altText) is empty, show the alternate text as an empty box; if `false`, respond with an alert.  The default value is `true` if `fromUser` is `false`, and `false` if `fromUser` is `true`. |

**Returns**

`MediaPlayer` object

<a id="68527"></a>
Example 1: The following code is the definition of `openPlayer`, which uses `createPlayer` in its definition.

```
app.media.openPlayer = function( args )
{
    var player = null;
    try
    {
        args = app.media.argsDWIM( args );

        player = app.media.createPlayer( args );
        if( player )
        {
            var result = player.open();
            if( result.code != app.media.openCode.success )
            {
                player = null;
                app.media.alert
                    ( "Open", args, { code: result.code } );
            }
            else if( player.visible )
            player.setFocus();  // triggers Focus event
        }
    }
    catch( e )
    {
        player = null;
        app.media.alert( 'Exception', args, { error: e } );
    }

    return player;
}
```

Example 2: See the examples at the end of the description of openPlayer for examples of PlayerArgs usage.

<a id="42321"></a>
<a id="getalttextdata"></a>
<a id="id223"></a>
#### getAltTextData

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a MediaData object (see `MediaSettings.` data) that represents alternate text data for the given text. This object can be used to create a player to display the alternate text.

**Parameters**

| Property | Description |
|----------|-------------|
| `cAltText` | A string that is to be used as alternate text data. |

**Returns**

- `MediaData` object (see `MediaSettings.` data).

Example: See the embedded example following the `getAltTextSettings` method.

<a id="12647"></a>
<a id="getalttextsettings"></a>
<a id="id224"></a>
#### getAltTextSettings

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Takes a `PlayerArgs` object containing at least `settings`, `showAltText`, and `showEmptyAltText` properties, along with a selection object as returned by `rendition.select`, and finds the first available alternate text rendition if there is one. It then creates and returns a new `MediaSettings` object suitable for playback of the alternate text. Otherwise it returns `null`.

**Parameters**

| Property | Description |
|----------|-------------|
| `args` | A `PlayerArgs` object |
| `selection` | A `MediaSelection` object |

**Returns**

`MediaSettings` object or `null`

Example: This example plays back the alternate text of the rendition. The code plays back the alternate text in a screen annotation, but can be modified for playback in a floating window.

```
var rendition = this.media.getRendition("myClip");
var settings = rendition.getPlaySettings();
var args = {
    settings: settings,
    showAltText: true,
    showEmptyAltText: true
};
var selection = rendition.select();
settings = app.media.getAltTextSettings( args, selection );

// You can also play custom alternate text by uncommenting the next line
// settings.data = app.media.getAltTextData("A. C. Robat");

// Uncomment the code below to obtain a floating window to play back
// the alternate text
/*
settings.windowType = app.media.windowType.floating
settings.floating = {
    canResize: app.media.canResize.keepRatio,
    hasClose: true,
    width: 400,
    height: 100
} */

// Now define an args parameter for use with openPlayer, which will

 // play the alternate text.
args = {
    rendition: rendition,
    annot: this.media.getAnnot({nPage: 0, cAnnotTitle:"myScreen"}),
    settings: settings
};
app.media.openPlayer(args);
```

<a id="20177"></a>
<a id="getannotstockevents"></a>
<a id="id225"></a>
#### getAnnotStockEvents

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** an `event` object containing the stock EventListeners required in a screen annotation for normal playback in Acrobat. The stock EventListeners provide standard Acrobat behavior such as focus handling.

If `app.media.trace` is `true`, debug trace listeners are also included with the stock EventListeners.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `settings` | A number corresponding to the window type (see `app.media.windowType`). |

**Returns**

`event` object

<a id="53877"></a>
<a id="getannottraceevents"></a>
<a id="id226"></a>
#### getAnnotTraceEvents

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** an `Events` object containing EventListeners that provide a debugging trace as events are dispatched.

**Returns**

`Events` object

<a id="25402"></a>
<a id="getplayers"></a>
<a id="id227"></a>
#### getPlayers

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a `PlayerInfoList` object, which is an array of `PlayerInfo` objects representing the available media players.

The PlayerInfoList may be filtered using its `select` method, and it may be used in the `settings.players` property when creating a media player with `createPlayer`.

See PlayerInfoList object and PlayerInfo object for more details.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `cMimeType` | (optional) An optional MIME type such as “audio/wav”. If `cMimeType` is omitted, the list includes all available players. If `cMimeType` is specified, the list includes only players that can handle that MIME type. |

**Returns**

`PlayerInfoList` object

Example 1: List MP3 players to the debug console.

```
var mp = app.media.getPlayers("audio/mp3")
for ( var i = 0; i < mp.length; i++) {
    console.println("nmp[" + i + "] Properties");
    for ( var p in mp[i] ) console.println(p + ": " + mp[i][p]);
}
```

Example 2: Choose any player that can play Flash media by matching the MIME type. The code assumes the code below is executed as a Rendition action with associated rendition (so no arguments for `createPlayer` are required).

```
var player = app.media.createPlayer();
player.settings.players
    = app.media.getPlayers( "application/x-shockwave-flash" );
player.open();
```

<a id="16134"></a>
<a id="getplayerstockevents"></a>
<a id="id228"></a>
#### getPlayerStockEvents

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** an `Events` object containing the stock EventListeners required in a media player for normal playback in Acrobat. The stock EventListeners provide standard Acrobat behavior such as focus handling.

Use `MediaPlayer.events.add` to add these stock events to a media player.

The `app.media.createPlayer` and `app.media.openPlayer` methods automatically call `getPlayerStockEvents` internally, so it is not necessary to call this method yourself unless you are writing code that sets up all EventListeners explicitly.

If `app.media.trace` is `true`, debug trace listeners are also included with the stock EventListeners.

**Parameters**

| Property | Description |
|----------|-------------|
| `settings` | A `MediaSettings` object. |

**Returns**

`Events` object

<a id="63413"></a>
<a id="getplayertraceevents"></a>
<a id="id229"></a>
#### getPlayerTraceEvents

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** an `Events` object containing EventListeners that provide a debugging trace as events are dispatched.

**Returns**

An `Events` object

<a id="95330"></a>
<a id="getrenditionsettings"></a>
<a id="id230"></a>
#### getRenditionSettings

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Calls `Rendition.select` to get a `MediaSelection` object, then `MediaSelection.rendition.getPlaySettings` to get a `MediaSettings` object for playback. If either of these fails, it calls the `getAltTextSettings` method to get a `MediaSettings` object for alternate text playback. Finally, it returns the resulting `MediaSettings` object, or `null` if `getAltTextSettings` returned `null` (that is, alternate text was not specified or not allowed).

**Parameters**

| Property | Description |
|----------|-------------|
| `args` | A `PlayerArgs` object. |

**Returns**

`MediaSettings` object or `null`

Example: See example 3 following openPlayer.

<a id="27456"></a>
<a id="geturldata"></a>
<a id="id231"></a>
#### getURLData

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** a MediaData object (see `MediaSettings.` data) that represents data to be retrieved for a URL and optional MIME type. This MediaData object can be used to create a player that accesses data from that URL.

**Parameters**

| Property | Description |
|----------|-------------|
| `cURL` | The URL from which media data is to be retrieved. |
| `cMimeType` | (optional) The MIME type of the data. |

**Returns**

`MediaData` object

Example: Retrieve a media clip from the Internet and plays it in a floating window.

```
var myURLClip = "http://www.example.com/myClip.mpg";
var args = {
    URL: myURLClip,
    mimeType: "video/x-mpg",
    doc: this,
    settings: {
        players: app.media.getPlayers("video/x-mpg"),
        windowType: app.media.windowType.floating,
        data: app.media.getURLData(myURLClip,"video/x-mpg"),
        floating: { height: 400, width: 600 }
    }
}
app.media.openPlayer(args);
```

<a id="30722"></a>
<a id="geturlsettings"></a>
<a id="id232"></a>
#### getURLSettings

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Takes a `PlayerArgs` object that contains a `settings` property and returns a `MediaSettings` object suitable for playback of a URL. The settings property must contain a `URL` property and may contain a `mimeType` property. It may also contain additional settings that are copied into the resulting settings object.

**Parameters**

| Property | Description |
|----------|-------------|
| `args` | A `PlayerArgs` object. |

**Returns**

`MediaSettings` object

Example 1: Same example as above. `getURLSettings` calls `getURLData` and inserts the return `MediaData` object into the `data` property into the `setting`, which it then returns.

```
var myURLClip = "http://www.example.com/myClip.mpg";
args = {
    URL: myURLClip,
    mimeType: "video/x-mpg",
    doc: this,
    settings:
    {
        players: app.media.getPlayers("video/x-mpg"),
        windowType: app.media.windowType.floating,
        floating: { height: 400, width: 600 }
    }
};
settings = app.media.getURLSettings(args)
args.settings = settings;
app.media.openPlayer(args);
```

Example 2: The example below is a custom keystroke action of a combo box. The combo box is a simple playlist of streamed audio and video websites. The export value of each element in the list has the form “URL,mimeType”, for example

```
http://www.example.com/streaming/radio.asx,video/x-ms-asx
```

The script below splits the export value into a 2-element array, where the first element is the URL and the second is the mimeType. Any video is shown in the screen annotation “myScreen”. Otherwise, only audio is heard.

```
if (!event.willCommit)
{
    var aURLMime = event.changeEx.split(",")
    console.println("aURLMime[0] = " + aURLMime[0]);
    console.println("aURLMime[1] = " + aURLMime[1]);
    var args = {
        annot:this.media.getAnnot({ nPage:0,cAnnotTitle: "myScreen" }),
        URL: aURLMime[0],
        mimeType: aURLMime[1],
        doc: this,
        settings: {
            players: app.media.getPlayers(aURLMime[1]),
            windowType: app.media.windowType.docked
        }
    };
    settings = app.media.getURLSettings(args);
    args.settings = settings;
    var player = app.media.openPlayer(args);
}
```

<a id="17972"></a>
<a id="getwindowbordersize"></a>
<a id="id233"></a>
#### getWindowBorderSize

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

**Returns** an array of four numbers representing the size in pixels of the left, top, right, and bottom borders that would be used for a floating window with the properties specified in the parameters.

The `hasTitle` and `hasClose` parameters are Boolean values, and `canResize` may be any of the values in `app.media.canResize`.

These parameters have the same names as properties of a `MediaSettings.floating` object, so you can simply pass in a floating object as a single parameter:

```
var size = doc.media.getWindowBorderSize( settings.floating );
```

**Parameters**

| Property | Description |
|----------|-------------|
| `hasTitle` | (optional) The default is `true`. |
| `hasClose` | (optional) The default is `true`. |
| `canResize` | (optional) The default is `app.media.canResize.no`. |

**Returns**

An array of 4 numbers.

<a id="84417"></a>
<a id="openplayer"></a>
<a id="id234"></a>
#### openPlayer

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Calls `app.media.createPlayer` to create a `MediaPlayer` object and then calls `MediaPlayer.open` to open the player.

This method triggers several events, which may include `Ready` (see onReady and afterReady), `Play` (see onPlay and afterPlay), and `Focus` (see onFocus and afterFocus). See the `EventListener` object for a general description of these events.

The method alerts the user and returns `null` on failure. It does not throw exceptions.

**Parameters**

| Property | Description |
|----------|-------------|
| `args` | (optional) A `PlayerArgs` object. |

**Returns**

A `MediaPlayer` object, or `null` on failure

Example 1: This minimal example is a custom JavaScript from the Actions tab in the Multimedia Properties panel of a screen annotation. To override the parameters specified by the UI of the screen annotation, the `args` parameter is passed.

```
app.media.openPlayer();
```

Override `settings.repeat` : if repeat is set to 1, change it to 2. Otherwise, set it to 1.

```
var nRepeat =
    ( event.action.rendition.getPlaySettings().repeat == 1 ) ? 2 : 1;
var args = { settings: { repeat: nRepeat } };
app.media.openPlayer(args);
```

See the event object for an explanation of `event.action.rendition`. The above example also uses `Rendition.getPlaySettings` to access the settings associated with the rendition to be played (the one associated with the screen annotation).

<a id="87538"></a>
Example 2: The following script is executed from a mouse-up action of a form button. It plays a docked media clip in a screen annotation.

```
app.media.openPlayer({
    rendition: this.media.getRendition( "myClip" ),
    annot: this.media.getAnnot( {nPage:0,cAnnotTitle:"myScreen"} ),
    settings: { windowType: app.media.windowType.docked }
});
```

<a id="57275"></a>
Example 3: This example is a custom JavaScript from the Actions tab in the Multimedia Properties of a screen annotation. The user clicks the annotation and a randomly chosen movie clip is played.

```
   // These are placed at the top level of the document JavaScript
   var myRenditions = new Array();
   myRenditions[0] = "myClip1";
   myRenditions[1] = "myClip2";
   myRenditions[2] = "myClip3";

   // This code is a custom JavaScript of a ScreenAnnot. All renditions

    // are docked and are played in the ScreenAnnot.
   var l = myRenditions.length;
   randomIndex = Math.floor( Math.random() * l ) % l;

   var rendition = this.media.getRendition(myRenditions[randomIndex]);
   var settings = app.media.getRenditionSettings({ rendition: rendition });

   var args = { rendition: rendition, settings: settings }
app.media.openPlayer(args);
```

<a id="57992"></a>
<a id="removestockevents"></a>
<a id="id235"></a>
#### removeStockEvents

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Removes any stock EventListeners from a `MediaPlayer` object and from any associated `ScreenAnnot` object and deletes the `player.stockEvents`, `player.annot`, `annot.stockEvents`, and `annot.player` properties. This undoes the effect of a previous `addStockEvents` call.

**Parameters**

| Property | Description |
|----------|-------------|
| `player` | A `MediaPlayer` object |

<a id="99051"></a>
<a id="startplayer"></a>
<a id="id236"></a>
#### startPlayer

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Checks whether an annotation is provided in the `PlayerArgs` object and the annotation already has a player open. If so, it calls `player.play` on that player to start or resume playback. If not, it calls `app.media.openPlayer` to create and open a new `MediaPlayer` object. See openPlayer for more details.

> **Note**
>
> `app.media.startPlayer` is the default mouse-up action when you use the Acrobat user interface to create a multimedia annotation and rendition and you do not specify any custom JavaScript.

**Parameters**

| Property | Description |
|----------|-------------|
| `args` | (optional) A `PlayerArgs` object |

**Returns**

A `MediaPlayer` object or `null` on failure

Example: Start a screen annotation from a form button.

```
var args = {
    rendition: this.media.getRendition( "myClip" ),
    annot: this.media.getAnnot({ nPage: 0, cAnnotTitle: "myScreen" }),
};
app.media.startPlayer(args);
```
