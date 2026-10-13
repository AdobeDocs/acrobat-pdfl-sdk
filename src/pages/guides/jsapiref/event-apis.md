# Event APIs

<a id="38077"></a>
<a id="event"></a>
<a id="id436"></a>
## event

All JavaScript scripts are executed as the result of a particular event. For each of these events, JavaScript creates an `event` object. During the occurrence of each event, you can access this object to get and possibly manipulate information about the current state of the event.

Each event has a `type` and a `name` property that uniquely identify the event. This section describes all the events, listed as type/name pairs, and indicates which additional properties, if any, they define.

The `rc` property of an event is its return code. The description for each event describes whether it listens to (is affected by) the return code.

It is important for JavaScript writers to know when these events occur and in what order they are processed. Some methods or properties can only be accessed during certain events.

<a id="96982"></a>
<a id="event-type-name-combinations"></a>
<a id="id437"></a>
### Event type/name combinations

| [App/Init](./event-apis.md#40668) | [Field/Calculate](./event-apis.md#18804) | [Page/Close](./event-apis.md#17115) |
|--------------------------------------|---------------------------------------------|----------------------------------------|
| [Batch/Exec](./event-apis.md#22318) | [Field/Focus](./event-apis.md#81424) | [Screen/Blur](./event-apis.md#58772) |
| [Bookmark/Mouse Up](./event-apis.md#69923) | [Field/Format](./event-apis.md#41224) | [Screen/Close](./event-apis.md#46576) |
| [Console/Exec](./event-apis.md#49873) | [Field/Keystroke](./event-apis.md#53758) | [Screen/Focus](./event-apis.md#26372) |
| [Doc/DidPrint](./event-apis.md#95882) | [Field/Mouse Down](./event-apis.md#70126) | [Screen/InView](./event-apis.md#95360) |
| [Doc/DidSave](./event-apis.md#54367) | [Field/Mouse Enter](./event-apis.md#48038) | [Screen/Mouse Down](./event-apis.md#70918) |
| [Doc/Open](./event-apis.md#94455) | [Field/Mouse Exit](./event-apis.md#92326) | [Screen/Mouse Enter](./event-apis.md#53256) |
| [Doc/WillClose](./event-apis.md#47806) | [Field/Mouse Up](./event-apis.md#75790) | [Screen/Mouse Exit](./event-apis.md#20493) |
| [Doc/WillPrint](./event-apis.md#69309) | [Field/Validate](./event-apis.md#33923) | [Screen/Mouse Up](./event-apis.md#99716) |
| [Doc/WillSave](./event-apis.md#94560) | [Link/Mouse Up](./event-apis.md#23496) | [Screen/Open](./event-apis.md#55831) |
| [External/Exec](./event-apis.md#79170) | [Menu/Exec](./event-apis.md#79394) | [Screen/OutView](./event-apis.md#91599) |
| [Field/Blur](./event-apis.md#41111) | [Page/Open](./event-apis.md#77991) |  |

<a id="40668"></a>
<a id="app-init"></a>
<a id="id438"></a>
#### App/Init

This event (the *application initialization event*) occurs when the viewer is started. Script files, called *folder-level JavaScripts*, are read in from the application and user JavaScript folders. They load in the following order: config.js, glob.js, all other files, then any user files.

This event does not listen to the `rc` return code.

<a id="22318"></a>
<a id="batch-exec"></a>
<a id="id439"></a>
#### Batch/Exec

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event occurs during the processing of each document of a batch sequence. Scripts authored as part of a batch sequence can access the `event` object upon execution.

The `target` for this event is the Doc.

This event listens to the `rc` return code. If `rc` is set to `false`, the batch sequence is stopped.

<a id="69923"></a>
<a id="bookmark-mouse-up"></a>
<a id="id440"></a>
#### Bookmark/Mouse Up

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event occurs whenever a user clicks a bookmark that executes a JavaScript.

The `target` for this event is the bookmark object that was clicked.

This event does not listen to the `rc` return code.

<a id="49873"></a>
<a id="console-exec"></a>
<a id="id441"></a>
#### Console/Exec

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event occurs whenever a user evaluates a JavaScript in the console.

This event does not listen to the `rc` return code.

<a id="95882"></a>
<a id="doc-didprint"></a>
<a id="id442"></a>
#### Doc/DidPrint

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event is triggered after a document has printed.

The `target` for this event is the Doc.

This event does not listen to the `rc` return code.

<a id="54367"></a>
<a id="doc-didsave"></a>
<a id="id443"></a>
#### Doc/DidSave

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event is triggered after a document has been saved.

The `target` for this event is the Doc.

This event does not listen to the `rc` return code.

<a id="94455"></a>
<a id="doc-open"></a>
<a id="id444"></a>
#### Doc/Open

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.0 | No | No | All |

This event is triggered whenever a document is opened. When a document is opened, the document-level script functions are scanned and any exposed scripts are executed.

The `target` for this event is the Doc. This event also defines the `targetName` property.

This event does not listen to the `rc` return code.

<a id="47806"></a>
<a id="doc-willclose"></a>
<a id="id445"></a>
#### Doc/WillClose

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event is triggered before a document is closed.

The `target` for this event is the Doc.

This event does not listen to the `rc` return code.

<a id="69309"></a>
<a id="doc-willprint"></a>
<a id="id446"></a>
#### Doc/WillPrint

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event is triggered before a document is printed.

The `target` for this event is the Doc.

This event does not listen to the `rc` return code.

<a id="94560"></a>
<a id="doc-willsave"></a>
<a id="id447"></a>
#### Doc/WillSave

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event is triggered before a document is saved.

The `target` for this event is the Doc.

This event does not listen to the `rc` return code.

<a id="79170"></a>
<a id="external-exec"></a>
<a id="id448"></a>
#### External/Exec

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event is the result of an external access, for example, through OLE, AppleScript, or loading an FDF.

This event does not listen to the `rc` return code.

<a id="41111"></a>
<a id="field-blur"></a>
<a id="id449"></a>
#### Field/Blur

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.05 | No | No | All |

This event occurs after all other events just as a field loses focus. This event is generated regardless of whether a mouse click is used to deactivate the field (for example, a tab key could be used instead).

Additional properties defined:

- `target`: The field whose validation script is being executed.
- `modifier`, `shift`, `targetName`, and `value`.

This event does not listen to the `rc` return code.

<a id="18804"></a>
<a id="field-calculate"></a>
<a id="id450"></a>
#### Field/Calculate

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

This event is defined when a change in a form requires that all fields that have a calculation script attached to them be executed. All fields that depend on the value of the changed field will now be recalculated. These fields may in turn generate additional `Field/Validate`, `Field/Blur`, and `Field/Focus` events.

Calculated fields may have dependencies on other calculated fields whose values must be determined beforehand. The *calculation order array* contains an ordered list of all the fields in a document that have a calculation script attached. When a full calculation is needed, each of the fields in the array is calculated in turn starting with the zeroth index of the array and continuing in sequence to the end of the array.

To change the calculation order of fields, use the Forms > Edit Fields > Set Field Calculation Order menu item while in Edit Form mode.

The `target` for this event is the field whose calculation script is being executed. This event also defines the `source` and `targetName` properties.

This event listens to the `rc` return code. If the return code is set to `false`, the field’s value is not changed. If true, the field takes on the value found in the `value` property.

<a id="81424"></a>
<a id="field-focus"></a>
<a id="id451"></a>
#### Field/Focus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.05 | No | No | All |

This event occurs after the mouse-down event but before the mouse-up event after the field gains the focus. It occurs regardless of whether a mouse click is used to activate the field (or, for example, the tab key) and is the best place to perform processing that must be done before the user can interact with the field.

The `target` for this event is the field whose validation script is being executed. This event also defines the `modifier`, `shift`, and `targetName` properties.

This event does not listen to the `rc` return code.

<a id="41224"></a>
<a id="field-format"></a>
<a id="id452"></a>
#### Field/Format

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

This event is triggered once all dependent calculations have been performed. It allows the attached JavaScript to change the way that the data value appears to a user (also known as its presentation or appearance). For example, if a data value is a number and the context in which it should be displayed is currency, the formatting script can add a dollar sign ($) to the front of the value and limit it to two decimal places past the decimal point.

The `target` for this event is the field whose format script is being executed. This event also defines the `commitKey`, `targetName`, and `willCommit` properties.

This event does not listen to the `rc` return code. However, the resulting `value` is used as the field’s formatted appearance.

<a id="53758"></a>
<a id="field-keystroke"></a>
<a id="id453"></a>
#### Field/Keystroke

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

This event occurs whenever a user types a keystroke into a text box or combo box (including cut and paste operations) or selects an item in a combo box list or list box field. A keystroke script may limit the type of keys allowed. For example, a numeric field might only allow numeric characters.

The Acrobat user interface allows the author to specify a `Selection Change` script for list boxes. The script is triggered every time an item is selected. This is implemented as the keystroke event where the keystroke value is equivalent to the user selection. This behavior is also implemented for the combo box—the “keystroke” could be thought to be a paste into the text field of the value selected from the drop-down list.

There is a final call to the keystroke script before the validate event is triggered. This call sets the `willCommit` to `true` for the event. With keystroke processing, it is sometimes useful to make a final check on the field value (pre-commit) before it is committed. This allows the script writer to gracefully handle particularly complex formats that can only be partially checked on a keystroke-by-keystroke basis.

The `keystroke` event of text fields is called in situations other than when the user is entering text with the keyboard or committing the field value. It is also called to validate the default value of a field when set through the UI or by JavaScript and to validate entries provided by autofill. In these situations not all properties of the event are defined. Specifically `event.target` will be `undefined` when validating default values and `event.richChange` and `event.richValue` will be `undefined` when validating autofill entries.

The `target` for this event is the field whose keystroke script is being executed. This event also defines the `commitKey`, `change`, `changeEx`, `keyDown`, `modifier`, `selEnd`, `selStart`, `shift`, `targetName`, `value`, and `willCommit` properties.

This event listens to the `rc` return code. If set to `false`, the keystroke is ignored. The resulting `change` is used as the keystroke if the script wants to replace the keystroke code. The resultant `selEnd` and `selStart` properties can change the current text selection in the field.

<a id="70126"></a>
<a id="field-mouse-down"></a>
<a id="id454"></a>
#### Field/Mouse Down

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

This event is triggered when a user starts to click a form field and the mouse button is still down. A mouse-down event does not occur unless a `mouse enter` event has already occurred. It is advised that you perform very little processing during this event (for example, play a short sound).

The `target` for this event is the field whose validation script is being executed. This event also defines the `modifier`, `shift`, and `targetName` properties.

This event does not listen to the `rc` return code.

<a id="48038"></a>
<a id="field-mouse-enter"></a>
<a id="id455"></a>
#### Field/Mouse Enter

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

This event is triggered when a user moves the pointer inside the rectangle of a field. This is the typical place to open a text field to display help text, for example.

The `target` for this event is the field whose validation script is being executed. This event also defines the `modifier`, `shift`, and `targetName` properties.

This event does not listen to the `rc` return code.

<a id="92326"></a>
<a id="field-mouse-exit"></a>
<a id="id456"></a>
#### Field/Mouse Exit

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

This event occurs when a user moves the mouse pointer outside of the rectangle of a field. A `mouse exit` event will not occur unless a `mouse enter` event has already occurred.

The `target` for this event is the field whose validation script is being executed. This event also defines the `modifier`, `shift`, and `targetName` properties.

This event does not listen to the `rc` return code.

<a id="75790"></a>
<a id="field-mouse-up"></a>
<a id="id457"></a>
#### Field/Mouse Up

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

This event is triggered when the user clicks a form field and releases the mouse button. This is the typical place to attach routines such as the submit action of a form. A mouse-up event will not occur unless a mouse-down event has already occurred.

The `target` for this event is the field whose validation script is being executed. This event also defines the `modifier`, `shift`, and `targetName` properties.

This event does not listen to the `rc` return code.

<a id="33923"></a>
<a id="field-validate"></a>
<a id="id458"></a>
#### Field/Validate

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 3.01 | No | No | All |

Regardless of the field type, user interaction with a field may produce a new value for that field. After the user has either clicked outside a field, tabbed to another field, or pressed the enter key, the user is said to have *committed* the new data value.

This event is the first event generated for a field after the value has been committed so that a JavaScript can verify that the value entered was correct. If the validate event is successful, the next event triggered is the `calculate` event.

The `target` for this event is the field whose validation script is being executed. This event also defines the `change`, `changeEx`, `keyDown`, `modifier`, `shift`, `targetName`, and `value` properties.

This event does not listen to the `rc` return code. If the return code is set to `false`, the field value is considered to be invalid and the value of the field is unchanged.

<a id="23496"></a>
<a id="link-mouse-up"></a>
<a id="id459"></a>
#### Link/Mouse Up

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event is triggered when a link containing a JavaScript action is activated by the user.

The `target` for this event is the Doc.

This event does not listen to the rc return code.

<a id="79394"></a>
<a id="menu-exec"></a>
<a id="id460"></a>
#### Menu/Exec

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 5.0 | No | No | All |

This event occurs whenever JavaScript that has been attached to a menu item is executed. The user can add a menu item and associate JavaScript actions with it. For example,

```
app.addMenuItem({ cName: "Hello", cParent: "File",
    cExec: "app.alert('Hello',3);", nPos: 0});
```

The script `app.alert('Hello',3)` will execute during a menu event. There are two ways for this to occur:

- The user can select the menu item in the user interface.
- Programmatically, when `app.execMenuItem("Hello")` is executed (perhaps, during a mouse-up event of a button field).

The `target` for this event is the currently active document, if one is open. This event also defines the `targetName` property.

This event listens to the `rc` return code in the case of the enable and marked proc for menu items. (See the `cEnabled` and `cMarked` parameters of `app.` addMenuItem.) A return code of `false` will disable or unmark a menu item. A return code of `true` will enable or mark a menu item.

<a id="77991"></a>
<a id="page-open"></a>
<a id="id461"></a>
#### Page/Open

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.05 | No | No | All |

This event occurs whenever a new page is viewed by the user and after page drawing for the page has occurred.

The `target` for this event is the Doc.

This event does not listen to the `rc` return code.

<a id="17115"></a>
<a id="page-close"></a>
<a id="id462"></a>
#### Page/Close

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 4.05 | No | No | All |

This event occurs whenever the page being viewed is no longer the current page; that is, the user switched to a new page or closed the document.

The `target` for this event is the Doc.

This event does not listen to the `rc` return code.

<a id="58772"></a>
<a id="screen-blur"></a>
<a id="id463"></a>
#### Screen/Blur

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event occurs after all other events, just as the screen annotation loses focus. This event is generated regardless of whether a mouse click is used to deactivate the screen annotation (for example, the tab key might be used).

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="46576"></a>
<a id="screen-close"></a>
<a id="id464"></a>
#### Screen/Close

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event occurs whenever the page being viewed is no longer the current page; that is, the user switched to a new page or closed the document.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier`, `shift`, and `target` properties.

This event does not listen to the `rc` return code.

<a id="26372"></a>
<a id="screen-focus"></a>
<a id="id465"></a>
#### Screen/Focus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event occurs after the mouse-down event but before the mouse-up after the field gains the focus. This routine is called regardless of whether a mouse click is used to activate the screen annotation (for example, the tab key might be used). It is the best place to perform processing that must be done before the user can interact with the field.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="95360"></a>
<a id="screen-inview"></a>
<a id="id466"></a>
#### Screen/InView

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event occurs whenever a new page first comes into view by the user. When the page layout is set to Continuous or Continuous - Facing, this event occurs before the Screen/Open event.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="70918"></a>
<a id="screen-mouse-down"></a>
<a id="id467"></a>
#### Screen/Mouse Down

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event is triggered when a user starts to click a screen annotation and the mouse button is still down. It is advised that you perform very little processing (that is, play a short sound) during this event. A mouse-down event will not occur unless a `mouse enter` event has already occurred.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="53256"></a>
<a id="screen-mouse-enter"></a>
<a id="id468"></a>
#### Screen/Mouse Enter

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event is triggered when a user moves the mouse pointer inside the rectangle of an screen annotation.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="20493"></a>
<a id="screen-mouse-exit"></a>
<a id="id469"></a>
#### Screen/Mouse Exit

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event is the opposite of the `Mouse Enter` event and occurs when a user moves the mouse pointer outside of the rectangle of a screen annotation. A `Mouse Exit` event will not occur unless a `Mouse Enter` event has already occurred.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="99716"></a>
<a id="screen-mouse-up"></a>
<a id="id470"></a>
#### Screen/Mouse Up

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event is triggered when the user clicks a screen annotation and releases the mouse button. This is the typical place to attach routines such as starting a multimedia clip. A mouse-up event will not occur unless a mouse-down event has already occurred.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="55831"></a>
<a id="screen-open"></a>
<a id="id471"></a>
#### Screen/Open

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event occurs whenever a new page is viewed by the user and after page drawing for the page has occurred.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="91599"></a>
<a id="screen-outview"></a>
<a id="id472"></a>
#### Screen/OutView

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

This event occurs whenever a page first goes out of view from the user. When the page layout is set to Continuous or Continuous - Facing, this event occurs after the `Screen/Close` event.

The `target` for this event is the `ScreenAnnot` object that initiated this event. `targetName` is the title of the screen annotation. This event also defines the `modifier` and `shift` properties.

This event does not listen to the `rc` return code.

<a id="73503"></a>
<a id="document-event-processing"></a>
<a id="id473"></a>
### Document Event Processing

When a document is opened, the `Doc/Open` event occurs. Functions are scanned and any exposed (top-level) scripts are executed. Next, if the NeedAppearances entry in the PDF file is set to `true` in the AcroForm dictionary, the formatting scripts of all form fields in the document are executed. (See the [PDF Reference](https://adobe.com/go/pdfreference).) Finally, the `Page/Close` event occurs.

> **Note**
>
> For users who create PDF files containing form fields with the NeedAppearances entry set to true, be sure to do a Save As before posting such files on the web. Performing a Save As on a file generates the form appearances, which are saved with the file. This increases the performance of Adobe Reader when it loads the file within a web browser.

<a id="93066"></a>
<a id="form-event-processing"></a>
<a id="id474"></a>
### Form event processing

The order in which the form events occur is shown in the state diagram below. Certain dependencies are worth noting. For example, the mouse-up event cannot occur if the Focus event did not occur.

[formsevent.png]

<a id="multimedia-event-processing"></a>
<a id="id475"></a>
### Multimedia event processing

Whenever an event is triggered and dispatched to an EventListener, a multimedia `event` object is passed as a parameter to the EventListener. This object is similar to the event object used elsewhere in Acrobat and it has the properties listed below.

Multimedia `event` objects triggered by rendition actions (for example, in custom JavaScript entered from the Actions tab in the Multimedia Properties panel) also include these properties:

|  |  |
|---|---|
| `action.annot` | The `ScreenAnnot` object for this event. |
| `action.rendition` | The `Rendition` object for this event. |

Multimedia event objects that have been dispatched by the standard multimedia event dispatcher also include these properties. These are not present if you provide your own `events.dispatch` method.

|  |  |
|---|---|
| `media.doc` | The document, same as `target.doc`. |
| `media.events` | The events object, same as `target.events`. |
| `media.id` | A copy of `event.name` with spaces removed. |

Individual events may have additional properties. See the description of each `EventListener` object method for details.

An event method called by the standard event dispatcher may set either of these properties to stop further event dispatching:

```
stopDispatch
stopAllDispatch
```

To stop the current event from being dispatched to any remaining EventListeners, an event method can set `event.stopDispatch` to `true`. If this is done in an `on` event method, no more `on` methods will be called for the event, but `after` methods will still be called. If you set `event.stopAllDispatch`, no more event methods of either type will be called. See the `EventListener` object for a description of the `on` and `after` EventListeners.

<a id="event-properties"></a>
<a id="id476"></a>
### event properties

<a id="26427"></a>
<a id="change"></a>
<a id="id477"></a>
#### change

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | String | R/W |

A string specifying the change in value that the user has just typed. A JavaScript may replace part or all of this string with different characters. The change may take the form of an individual keystroke or a string of characters (for example, if a paste into the field is performed).

<a id="79488"></a>
**Example**: Change all keystrokes to upper case.

```
// Custom Keystroke for text field
event.change = event.change.toUpperCase();
```

<a id="64007"></a>
<a id="changeex"></a>
<a id="id478"></a>
#### changeEx

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Various | R |

Contains the export value of the change and is available only during a `Field/Keystroke` event for list boxes and combo boxes.

For the list box, the keystroke script, if any, is entered under the Selection Change tab in the properties dialog box.

For the combo box, `changeEx` is only available if the pop-up list is used—that is, a selection (with the mouse or the keyboard) is being made from the list. If the combo is editable and the user types in an entry, the `Field/Keystroke` event behaves as for a text field (that is, there are no `changeEx` or `keyDown` event properties).

Beginning with Acrobat 6.0, `event.changeEx` is defined for text fields. When `event.fieldFull` is `true`, `changeEx` is set to the entire text string the user attempted to enter and `event.change` is the text string cropped to what fits within the field. Use `event.richChangeEx` (and `event.richChange`) to handle rich text fields.

Example 1: This example implements a simple HTML online help file system.

Here is a combo box, which is described programmatically.

```
var c = this.addField({
    cName: "myHelp",
    cFieldType: "combobox",
    nPageNum: 0,
    oCoords: [72,12+3*72, 3*72, 0+3*72]
})
```

Now set the items in the combo box.

```
c.setItems([
    ["Online Help", "http://www.example.com/myhelp.html"],
    ["How to Print", "http://www.example.com/myhelp.html#print"],
    ["How to eMail", "http://www.example.com/myhelp.html#email"]
]);
```

Set the action.

```
c.setAction("Keystroke", "getHelp()");
```

This function is defined at the document level.

```
function getHelp() {
    if ( !event.willCommit && (event.changeEx != "") )
        app.launchURL(event.changeEx);
}
```

Example 2: For an example of the use of `changeEx` with text fields, see the example following fieldFull.

<a id="88273"></a>
<a id="commitkey"></a>
<a id="id479"></a>
#### commitKey

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.0 | No | No | All | Number | R |

Determines how a form field will lose focus. Values are:

- *0*: Value was not committed (for example, escape key was pressed).
- *1*: Value was committed because of a click outside the field using the mouse.
- *2*: Value was committed because of pressing the Enter key.
- *3*: Value was committed by tabbing to a new field.

Example: To automatically display an alert dialog box after a field has been committed, add the following to the field’s format script:

```
if (event.commitKey != 0)
    app.alert("Thank you for your new field value.");
```

<a id="98939"></a>
<a id="fieldfull"></a>
<a id="id480"></a>
#### fieldFull

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Boolean | R |

Set to `true` when the user attempts to enter text that does not fit in the field due to either a space limitation (the Field object property `doNotScroll` is set to `true`) or the maximum character limit (the Field object property `charLimit` is set to a positive value). When `fieldFull` is `true`, `event.changeEx` is set to the entire text string the user attempted to enter and `event.change` is the text string cropped to what fits within the field.

Only available in keystroke events for text fields.

**Events**

Keystroke

Example 1: This is a custom keystroke script for a text field that has a character limit. When the field gets filled, or if the user commits the data entered, the focus moves to another field.

```
if ( event.fieldFull | event.willCommit )
    this.getField("NextTabField").setFocus();
```

Example 2: Test whether the user has overfilled the text field. A custom keystroke script for a text field. Initially, the field is set so that text does not scroll.

```
if ( event.fieldFull )
{
    app.alert("You've filled the given space with text,"
    + " and as a result, you've lost some text. I'll set the field to"
    + " scroll horizontally, and paste in the rest of your"
    + " missing text.");
    this.resetForm([event.target.name]);     // Reset field to lose focus
    event.target.doNotScroll = false;        // Make changes
    event.change = event.changeEx;
}
```

Field properties generally cannot be changed during a keystroke event, so it is necessary for the field to lose focus as a way to commit the data. The user then has to reset the focus and continue entering data.

<a id="72020"></a>
<a id="keydown"></a>
<a id="id481"></a>
#### keyDown

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Boolean | R |

Available only during a keystroke event for list box and combo box. For a list box or the pop-up part of a combo box, the value is `true` if the arrow keys were used to make a selection, `false` otherwise.

For the combo box, `keyDown` is only available if the pop-up part of it is used, that is, a selection (with the mouse or the keyboard) is being made from the pop-up. If the combo is editable and the user types in an entry, the `Field/Keystroke` event behaves as for a text field (that is, there are no `changeEx` or `keyDown` event properties).

<a id="41458"></a>
<a id="modifier"></a>
<a id="id482"></a>
#### modifier

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Boolean | R/W |

Specifies whether the modifier key is down during a particular event. The modifier key on the Microsoft Windows platform is Control and on the Mac OS platform is Option or Command. This property is not supported on UNIX.

<a id="54531"></a>
<a id="id483"></a>
<a id="id484"></a>
#### name

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 4.05 | No | No | All | String | R/W |

The name of the current event as a text string. The `type` and name together uniquely identify the event. Valid names are:

```
Keystroke        Mouse Exit
Validate         WillPrint
Focus            DidPrint
Blur             WillSave
Format           DidSave
Calculate        Init
Mouse Up         Exec
Mouse Down       Open
Mouse Enter      Close
```

**Events**

All

<a id="98376"></a>
<a id="rc"></a>
<a id="id485"></a>
#### rc

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Boolean | R/W |

Used for validation. Indicates whether a particular event in the event chain should succeed. Set to `false` to prevent a change from occurring or a value from committing. The default is `true`.

**Events**

Keystroke, Validate, Menu

<a id="85239"></a>
<a id="richchange"></a>
<a id="id486"></a>
#### richChange

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | No | Array of `Span` objects | R/W |

Specifies the change in value that the user has just typed. The `richChange` property is only defined for rich text fields and mirrors the behavior of the `event.change` property. The value of `richChange` is an array of `Span` objects that specify both the text entered into the field and the formatting. Keystrokes are represented as single member arrays, while rich text pasted into a field is represented as an array of arbitrary length.

When `event.fieldFull` is `true`, `richChangeEx` is set to the entire rich formatted text string the user attempted to enter and `event.richChange` is the rich formatted text string cropped to what fits within the field. Use `event.changeEx` (and `event.change`) to handle (plain) text fields.

Related objects and properties are `event.` richValue, the Span object, the Field object defaultStyle, richText, and richValue properties, and the `Annotation` object richContents property.

**Events**

Keystroke

Example: This example changes the keystroke to upper case, alternately colors the text blue and red, and switches underlining off and on.

```
// Custom Keystroke event for a rich text field.
var span = event.richChange;
for ( var i=0; i<span.length; i++)
{
    span[i].text = span[i].text.toUpperCase();
    span[i].underline = !span[i].underline;
    span[i].textColor = (span[i].underline) ? color.blue : color.red;
}
event.richChange = span;
```

<a id="86693"></a>
<a id="richchangeex"></a>
<a id="id487"></a>
#### richChangeEx

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array of `Span` objects | R/W |

This property is only defined for rich text fields. It mirrors the behavior of the `event.changeEx` property for text fields. Its value is an array of `Span` objects that specify both the text entered into the field and the formatting. Keystrokes are represented as single member arrays, while rich text pasted into a field is represented as an array of arbitrary length.

If `event.fieldFull` is `true`, `richChangeEx` is set to the entire rich formatted text string the user attempted to enter and `event.richChange` is the rich formatted text string cropped to what fits within the field. Use `event.changeEx` (and `event.change`) to handle (plain) text fields.

Related objects and properties include `event.` richChange, `event.` richValue, the Span object, the Field object defaultStyle, richText, and richValue properties, and the Annotation object richContents property.

**Events**

Keystroke

Example: If the text field is filled up by the user, allow additional text by setting the field to scroll.

```
if ( event.fieldFull )
{
    app.alert("You've filled the given space with text,"
    + " and as a result, you've lost some text. I'll set the field to"
    + " scroll horizontally, and paste in the rest of your"
    + " missing text.");
    this.resetForm([event.target.name]);    // Reset field to lose focus
    event.target.doNotScroll = false;       // Make changes
    if ( event.target.richText )
        event.richChange = event.richChangeEx
    else
        event.change = event.changeEx;
}
```

See also `event`. fieldFull.

<a id="73797"></a>
<a id="richvalue"></a>
<a id="id488"></a>
#### richValue

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 6.0 | No | No | All | Array of `Span` objects | R/W |

This property mirrors the `richValue` property of the Field object and the `event.value` property for each event.

Related objects and properties include the Span object, the Field object properties defaultStyle, richText, richValue, `event.` richChange, `event.` richChangeEx, and the Annotation object richContents property.

**Events**

Keystroke

Example: Turn all bold text into red underlined text.

```
// Custom format event for a rich text field.
var spans = event.richValue;
for ( var i = 0; i < spans.length; i++ )
{
    if( spans[i].fontWeight >= 700 )
    {
        spans[i].textColor = color.red;
        spans[i].fontWeight = 400;     // change to default weight
        spans[i].underline = true;
    }
}
event.richValue = spans;
```

<a id="70481"></a>
<a id="selend"></a>
<a id="id489"></a>
#### selEnd

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Integer | R/W |

The ending position of the current text selection during a keystroke event.

Example: Merge the last change (of a text field) with the uncommitted change. The function uses both `selEnd` and `selStart`.

```
function AFMergeChange(event)
{
    var prefix, postfix;
    var value = event.value;

    if(event.willCommit) return event.value;
    if(event.selStart >= 0)
        prefix = value.substring(0, event.selStart);
    else prefix = "";
    if(event.selEnd >= 0 && event.selEnd <= value.length)
        postfix = value.substring(event.selEnd, value.length);
    else postfix = "";
    return prefix + event.change + postfix;
}
```

<a id="57955"></a>
<a id="selstart"></a>
<a id="id490"></a>
#### selStart

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Integer | R/W |

The starting position of the current text selection during a keystroke event.
Example: See the example following selEnd.

<a id="22573"></a>
<a id="shift"></a>
<a id="id491"></a>
#### shift

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Boolean | R |

`true` if the shift key is down during a particular event, `false` otherwise.

Example: The following is a mouse-up button action:

```
if (event.shift)
    this.gotoNamedDest("dest2");
else
    this.gotoNamedDest("dest1");
```

<a id="92374"></a>
<a id="source"></a>
<a id="id492"></a>
#### source

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | Object | R |

The Field object that triggered the calculation event. This object is usually different from the `target` of the event, which is the field that is being calculated. For dynamic stamp calculation, `event.source` corresponds to the `Doc` object that triggered the event.

<a id="17801"></a>
<a id="target"></a>
<a id="id493"></a>
#### target

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Object | R |

The target object that triggered the event. In all mouse, focus, blur, calculate, validate, and format events, it is the Field object that triggered the event. In other events, such as page open and close, it is the Doc or `this` object.
<a id="40616"></a>

<a id="targetname"></a>
<a id="id494"></a>
#### targetName

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

Tries to return the name of the JavaScript being executed. Can be used for debugging purposes to help identify the code causing exceptions to be thrown. Common values of `targetName` include:

- The folder-level script file name for `App/Init` events
- The document-level script name for `Doc/Open` events
- The PDF file name being processed for `Batch/Exec` events
- The field name for `Field` events
- The menu item name for `Menu/Exec` events
- The screen annotation name for `Screen` events (multimedia events)

When an exception is thrown, `targetName` is reported if there is an identifiable name.

Example: The first line of the folder-level JavaScript file conserve `.js` has an error in it. When the viewer starts, an exception is thrown and the message reveals the source of the problem.

```
MissingArgError: Missing required argument.
App.alert:1:Folder-Level:App:conserve.js
 ===> Parameter cMsg.
```

<a id="12523"></a>
<a id="id495"></a>
<a id="id496"></a>
#### type

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 5.0 | No | No | All | String | R |

The type of the current event. The type and `name` together uniquely identify the event. Valid types are:

```
Batch            External
Console          Bookmark
App              Link
Doc              Field
Page             Menu
```

<a id="98853"></a>
<a id="id497"></a>
<a id="id498"></a>
#### value

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Various | R/W |

This property has different meanings for different `field` events:

- For the `Field/Validate` event, it is the value that the field contains when it is committed. For a combo box, it is the face value, not the export value (see changeEx).

For example, the following JavaScript verifies that the field value is between zero and 100:

```
if (event.value < 0 | event.value > 100) {
    app.beep(0);
    app.alert("Invalid value for field " + event.target.name);
    event.rc = false;
}
```

- For a `Field/Calculate` event, JavaScript should set this property. It is the value that the field should take upon completion of the event.

For example, the following JavaScript sets the calculated value of the field to the value of the SubTotal field plus tax.

```
var f = this.getField("SubTotal");
event.value = f.value * 1.0725;
```

- For a `Field/Format` event, JavaScript should set this property. It is the value used when generating the appearance for the field. By default, it contains the value that the user has committed. For a combo box, this is the face value, not the export value (see changeEx for the export value).

For example, the following JavaScript formats the field as a currency type of field.

```
event.value = util.printf("$%.2f", event.value);
```

- For a `Field/Keystroke` event, it is the current value of the field. If modifying a text field, for example, this is the text in the text field before the keystroke is applied.
- For `Field/Blur` and `Field/Focus` events, it is the current value of the field. During these two events, `event.value` is read only. That is, the field value cannot be changed by setting `event.value`.

Beginning with Acrobat 5.0, for a list box that allows multiple selections (see `field.` multipleSelection), the following behavior occurs. If the field value is an array (that is, multiple items are selected), `event.value` returns an empty string when getting, and does not accept setting.

<a id="47823"></a>
<a id="willcommit"></a>
<a id="id499"></a>
#### willCommit

| Version (Key) | Save-Prefs | Security | Product | Type | Access |
|---------------|------------|----------|---------|------|--------|
| 3.01 | No | No | All | Boolean | R |

Verifies the current keystroke event before the data is committed. It can be used to check target form field values to verify, for example, whether character data was entered instead of numeric data. JavaScript sets this property to `true` after the last `keystroke` event and before the field is validated.
Example: This example shows the structure of a keystroke event.

```
var value = event.value
if (event.willCommit)
    // Final value checking.
else
    // Keystroke-level checking.
```

<a id="12169"></a>
<a id="eventlistener"></a>
<a id="id500"></a>
## EventListener

This object is a collection of multimedia event methods with optional local data. Event method names begin with `on` or `after`, followed by the event name, for example, `onPause` or `afterPause`. When an event is dispatched, matching `on` event methods are called immediately and matching `after` event methods are called a short while later, at the next idle time.

`on` event methods have certain restrictions:

- An `on` event method for a `MediaPlayer` object cannot call any of that MediaPlayer’s methods, nor can it call any other Acrobat methods that may indirectly cause a method of the MediaPlayer to be called. For example, an `on` method must not close the document, save it, change the active page, change the focus, or anything else that may eventually call a method of the MediaPlayer.
- `on` event methods cannot be reentered.

`after` event methods do not have these restrictions and therefore are more versatile for most purposes. Use an `on` event method only when the event must be processed synchronously, such as an `onGetRect` method.

Inside an event method, `this` is the EventListener object. The document is available in `event.media.doc` and the event target (MediaPlayer or ScreenAnnot) is in `event.target`.

`Events.add` installs EventListener objects for dispatching, `Events.dispatch` dispatches an event to the matching event methods, and `Events.remove` removes EventListener objects from the dispatch table.

Example: Install `onPlay` and `afterPlay` event listeners using two techniques. These listeners report back to the console when there are executed.

```
// Create a simple MediaEvents object
var events = new app.media.Events
({
    // Called immediately during a Play event:
    onPlay: function() { console.println( "onPlay" ); },

    // Called during idle time after the Play event:
    afterPlay: function() { console.println( "afterPlay" ); },
});
var player = app.media.createPlayer({events: events});
player.events.add({
    afterPlay: function( e ) {
        app.alert("Playback started, doc.URL = " + e.media.doc.URL );
    }
});
player.open();
```

<a id="eventlistener-methods"></a>
<a id="id501"></a>
### EventListener methods

The events listed here are specific to multimedia.

In addition to these events, a screen annotation may receive the standard events used elsewhere in Acrobat (Destroy, Mouse Up, Mouse Down, Mouse Enter, Mouse Exit, Page Open, Page Close, Page Visible, Page Invisible, Focus, and Blur). See the event object for details on those events.

<a id="30006"></a>
<a id="afterblur"></a>
<a id="id502"></a>
#### afterBlur

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Blur event is triggered when a MediaPlayer or screen annotation loses the keyboard focus after having it. See also onBlur (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

Example: The following script is executed as a Rendition action. The user clicks the screen annotation to open but not play the movie clip. Clicking outside the screen annotation (a Blur event) plays the movie. Clicking the screen annotation (a Focus event) while the movie is playing pauses the movie. To continue, the user clicks outside the screen annotation again.

```
var playerEvents = new app.media.Events
({
    afterBlur: function () { player.play(); },
    afterFocus: function () { player.pause(); }
});
var settings = { autoPlay: false };
var args = { settings: settings, events: playerEvents};
var player = app.media.openPlayer(args);
```

See also afterFocus.

<a id="83809"></a>
<a id="afterclose"></a>
<a id="id503"></a>
#### afterClose

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Close event is triggered when a media player is closed for any reason. See also onClose (the difference between `on` and `after` event methods are explained in EventListener).

To start another media player from the Close event, be sure to test `doc.media.canPlay` first to make sure playback is allowed. For example, playback may not be allowed because the document is closing.

The `event` object for a Close event includes these properties in addition to the standard event properties:

| Parameter | Description |
|-----------|-------------|
| `media.closeReason` | Why the player was closed, from `app.media.closeReason`. |
| `media.hadFocus` | Did the player have the focus when it was closed? |

When a player closes while it has the focus, it first receives a Blur event and then the Close event. In the Close event, `media.hadFocus` indicates whether the player had the focus before closing.

When the `afterClose` event method is called, the MediaPlayer has already been deleted and its JavaScript object is dead.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

Example: See onClose for a representative example.

<a id="59810"></a>
<a id="afterdestroy"></a>
<a id="id504"></a>
#### afterDestroy

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Destroy event is triggered when a screen annotation is destroyed.

When the `afterDestroy` event method is called, the screen annotation has already been deleted from the document and its JavaScript object is dead.

See also onDestroy (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="44303"></a>
<a id="afterdone"></a>
<a id="id505"></a>
#### afterDone

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Done event is triggered when media playback reaches the end of media.

See also onDone (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="92605"></a>
<a id="aftererror"></a>
<a id="id506"></a>
#### afterError

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Error event is triggered when an error occurs in a MediaPlayer. See also onError (the difference between `on` and `after` event methods are explained in EventListener).

The `event` object for an Error event includes these properties in addition to the standard `event` properties:

|  |  |
|---|---|
| `media.code` | Status code value. |
| `media.serious` | True for serious errors, false for warnings. |
| `media.text` | Error message text. |

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="87938"></a>
<a id="afterescape"></a>
<a id="id507"></a>
#### afterEscape

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Escape event is triggered when the user presses the Escape key while a MediaPlayer is open and has the keyboard focus. A MediaPlayer may receive an Escape event before it receives the Ready event.

See also onEscape (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="66809"></a>
<a id="aftereveryevent"></a>
<a id="id508"></a>
#### afterEveryEvent

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

If an `Events` object contains an `onEveryEvent` or `afterEveryEvent` property, its EventListener methods are called for every event, not just a specific one. (The difference between `on` and `after` event methods are explained in EventListener).

The EventListener functions in an `onEveryEvent` or `afterEveryEvent` property are called before any listener functions that name the specific event.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

Example: Have `onEveryEvent`, `afterEveryEvent`, `onPlay` and `afterPlay` report back to the console.

```
var events = new app.media.Events(
{
    // This is called immediately at the start of every event:
    onEveryEvent: function( e )
    { console.println( 'onEveryEvent, event = ' + e.name ); },

    // This is called during a Play event, after onEveryEvent is

     // called:
    onPlay: function() { console.println( "onPlay" ); },

    // This is called for every event, but later during idle time:
    afterEveryEvent: function( e )
    { console.println( "afterEveryEvent, event = " + e.name ); },

    // This is called during idle time after a Play event,
    // and after afterEveryEvent is called:
    afterPlay: function() { console.println( "afterPlay" ); },
});
```

<a id="64720"></a>
<a id="afterfocus"></a>
<a id="id509"></a>
#### afterFocus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Focus event is triggered when a MediaPlayer or screen annotation gets the keyboard focus. See also onFocus (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

Example: See afterBlur for an example of usage.

<a id="39032"></a>
<a id="afterpause"></a>
<a id="id510"></a>
#### afterPause

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Pause event is triggered when media playback pauses, either because of user interaction or when the `pause` method is called. See also onPause (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="72989"></a>
<a id="afterplay"></a>
<a id="id511"></a>
#### afterPlay

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Play event is triggered when media playback starts or resumes, either because of user interaction or when the `play` method is called. See also onPlay (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="75362"></a>
<a id="afterready"></a>
<a id="id512"></a>
#### afterReady

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Ready event is triggered when a newly-created MediaPlayer is ready for use. See also onReady (the difference between `on` and `after` event methods are explained in EventListener).

Most methods of a `MediaPlayer` object cannot be called until the Ready event is triggered.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

See afterScript, below, `Markers.` get and the MediaOffset object.

Example: This (document-level) script plays multiple media clips. For each screen annotation, a media (OpenPlayer) player is opened. When it is ready, the `afterReady` script signals this fact to Multiplayer.

```
// Parameters: doc, page, rendition/annot name, mulitPlayer instance
function OnePlayer( doc, page, name, multiPlayer )
{
    var player = app.media.openPlayer({
        annot: doc.media.getAnnot(
            { nPage: page, cAnnotTitle: name }),
        rendition: doc.media.getRendition( name ),
        settings: { autoPlay: false },
        events: {
            afterReady: function( e ) {
            multiPlayer.afterReady( player );
            },
        }
    });
    return player;
}
// Parameters: doc, page, list of rendition/annot names
function MultiPlayer( doc, page )
{
    var nPlayersCueing = 0;  // number of players cueing up
    var players = [];       // the SinglePlayers

    this.afterReady = function( player ) {
        if( ! player.didAfterReady ) {
            player.didAfterReady = true;
            nPlayersCueing--;
            if( nPlayersCueing == 0 ) this.play();
        }
    }
    this.play = function() {
        for( var i = 0;  i < players.length;  i++ ) players[i].play();
    }
    for( var i = 2;  i < arguments.length;  i++ ) {
        players[i-2] = new OnePlayer(doc,page,arguments[i],this );
        nPlayersCueing++;
    }
}
```

Playing multiple media clips is accomplished by executing the following code from, for example, a mouse-up action of a form button.

```
var myMultiPlayer = new MultiPlayer( this, 0, "Clip1", "Clip2" );
```

See afterScript for another example of `afterReady`.

<a id="96936"></a>
<a id="afterscript"></a>
<a id="id513"></a>
#### afterScript

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Script event is triggered when a script trigger is encountered in the media during playback. See also onScript (the difference between `on` and `after` event methods are explained in EventListener).

The `event` object for a Script event includes these properties in addition to the standard `event` properties:

|  |  |
|---|---|
| `media.command` | Command name |
| `media.param` | Command parameter string |

These two strings can contain any values that the media clip provides. They do not necessarily contain executable JavaScript code and it is up to the `onScript` or `afterScript` EventListener to interpret them.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

Example: The following is part of a complete example presented after `MediaPlayer.seek`. The media is an audio clip (`.wma`) of famous quotations, which supports markers and scripts. The `afterReady` listener counts the number of markers, one at the beginning of each quotation. At the end of each quotation, there is also an embedded command script. The `afterScript` listener watches for these commands and if it is a `pause` command, it pauses the player.

```
var nMarkers=0;
var events = new app.media.Events;
events.add({
    // Count the number of quotes in this audio clip, save as nMarkers
    afterReady: function() {
        var g = player.markers;
        while ( (index =  g.get( { index: nMarkers } ) ) != null )

             nMarkers++;
    },
    // Each quote should be followed by a script, if the command is to

     // pause, then pause the player.
    afterScript: function( e ) {
        if ( e.media.command == "pause" ) player.pause();
    }
});
var player = app.media.openPlayer({
    rendition: this.media.getRendition( "myQuotes" ),
    settings: { autoPlay: false },
    events: events
});
```

<a id="67314"></a>
<a id="afterseek"></a>
<a id="id514"></a>
#### afterSeek

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Seek event is triggered when a MediaPlayer is finished seeking to a playback offset as a result of a `seek` call. See also onSeek (the difference between `on` and `after` event methods are explained in EventListener).

Not all media players trigger Seek events.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="20336"></a>
<a id="afterstatus"></a>
<a id="id515"></a>
#### afterStatus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Status event is triggered on various changes of status that a MediaPlayer reports. See also onStatus (the difference between `on` and `after` event methods are explained in EventListener).

The `event` object for a Status event includes these properties in addition to the standard `event` properties:

|  |  |
|---|---|
| `media.code` | Status code value, defined in `app.media.status`. |
| `media.text` | Status message text. |

The following values are used only by some media players and only when
`media.code == app.media.status.buffering`. They are zero otherwise.

|  |  |
|---|---|
| `media.progress` | Progress value from 0 to media.total. |
| `media.total` | Maximum progress value. |

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

Example: Monitor the status of the player, as executed from a Rendition event associated with a screen annotation.

```
var events = new app.media.Events
events.add({
    afterStatus: function ( e ) {
        console.println( "Status code " + e.media.code +
            ", description: " + e.media.text);
    }
});
app.media.openPlayer({ events: events });
```

<a id="72199"></a>
<a id="afterstop"></a>
<a id="id516"></a>
#### afterStop

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Stop event is triggered when media playback stops, either because of user interaction or when the `stop` method is called. See also onStop (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="50864"></a>
<a id="onblur"></a>
<a id="id517"></a>
#### onBlur

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Blur event is triggered when a MediaPlayer or screen annotation loses the keyboard focus after having it. See also afterBlur (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="45762"></a>
<a id="onclose"></a>
<a id="id518"></a>
#### onClose

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Close event is triggered when a MediaPlayer is closed for any reason. See also afterClose (the difference between `on` and `after` event methods are explained in EventListener).

To start another media player from the Close event, be sure to test `doc.media.canPlay` first to make sure playback is allowed. For example, playback may not be allowed because the document is closing.

The `event` object for a Close event includes these properties in addition to the standard `event` properties:

| `media.closeReason` | Why the player was closed, from `app.media.closeReason` |
|---------------------|---------------------------------------------------------|
| `media.hadFocus` | Did the player have the focus when it was closed? |

When a player closes while it has the focus, it first receives a Blur event and then the Close event. In the Close event, `media.hadFocus` indicates whether the player had the focus before closing.

When the afterClose event method is called, the MediaPlayer has already been deleted and its JavaScript object is dead.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

Example: This script gets information about why the media clip closed, executed from a Rendition action. See `app.media.` closeReason.

```
var playerEvents = new app.media.Events({
    onClose: function (e) {
        var eReason, r = app.media.closeReason;
        switch ( e.media.closeReason )
        {
            case r.general: eReason = "general"; break;
            case r.error: eReason = "error"; break;
            case r.done: eReason = "done"; break;
            case r.stop: eReason = "stop"; break;
            case r.play: eReason = "play"; break;
            case r.uiGeneral: eReason = "uiGeneral"; break;
            case r.uiScreen: eReason = "uiScreen"; break;
            case r.uiEdit: eReason = "uiEdit"; break;
            case r.docClose: eReason = "Close"; break;
            case r.docSave: eReason = "docSave"; break;
            case r.docChange: eReason = "docChange"; break;
        }
        console.println("Closing...The reason is  " + eReason );
    }
});
app.media.openPlayer({ events: playerEvents });
```

<a id="56842"></a>
<a id="ondestroy"></a>
<a id="id519"></a>
#### onDestroy

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Destroy event is triggered when a screen annotation is destroyed. See also afterDestroy (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="34158"></a>
<a id="ondone"></a>
<a id="id520"></a>
#### onDone

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Done event is triggered when media playback reaches the end of media. See also afterDone (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="95692"></a>
<a id="onerror"></a>
<a id="id521"></a>
#### onError

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Error event is triggered when an error occurs in a MediaPlayer. See also afterError (the difference between `on` and `after` event methods are explained in EventListener).

The `event` object for an Error event includes these properties in addition to the standard `event` properties:

|  |  |
|---|---|
| `media.code` | Status code value |
| `media.serious` | `true` for serious errors, `false` for warnings |
| `media.text` | Error message text |

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="38753"></a>
onEscape

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Escape event is triggered when the user presses the Escape key while a MediaPlayer is open and has the keyboard focus. A MediaPlayer may receive an Escape event before it receives the Ready event.

See also afterEscape (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="48650"></a>
<a id="oneveryevent"></a>
<a id="id522"></a>
#### onEveryEvent

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

If an `Events` object contains an `onEveryEvent` or `afterEveryEvent` property, its EventListener methods are called for every event, not just a specific one.

The EventListener methods in an `onEveryEvent` or `afterEveryEvent` property are called before any listener functions that name the specific event. (The difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="14108"></a>
onFocus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Focus event is triggered when a MediaPlayer or screen annotation gets the keyboard focus. See also afterFocus (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="61508"></a>
<a id="ongetrect"></a>
<a id="id523"></a>
#### onGetRect

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The GetRect event is triggered whenever the multimedia plug-in needs to get the display rectangle for a docked MediaPlayer.

The `event` object for a GetRect event includes this property in addition to the standard `event` properties:

| Parameter | Description |
|-----------|-------------|
| `media.rect` | Player rectangle, an array of four numbers in device space |

The `onGetRect` method must set this property in the `oMediaEvent` before returning.

> **Note**
>
> Although you can write an `afterGetRect` listener, there is no useful purpose for it. If it returns a `rect` property, it will be ignored. The `onGetRect` listener is where the `rect` property must be set.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

Example: Page 0 has a series of (thumbnail-size) ScreenAnnots and page 1 is a blank page. Put the viewer into continuous facing mode so that both pages are seen side-by-side. Below is a typical Rendition action or mouse-up button JavaScript action.

```
var rendition = this.media.getRendition("Clip1");
var settings = rendition.getPlaySettings();
var annot = this.media.getAnnot({ nPage:0,cAnnotTitle:"ScreenClip1" });
var player = app.media.openPlayer({
    rendition: rendition,
    annot: annot,
    settings: { windowType: app.media.windowType.docked },
    events:
    {
        onGetRect: function (e) {
            var width = e.media.rect[2] - e.media.rect[0];
            var height = e.media.rect[3] - e.media.rect[1];
            width *= 3; // Triple width and height
            height *= 3;
            e.media.rect[0] = 36; // Move left,upper to
            e.media.rect[1] = 36; // upper left-hand corner
            e.media.rect[2] = e.media.rect[0]+width;
            e.media.rect[3] = e.media.rect[1]+height;
            return e.media.rect; // Return this
        }
    }
});
player.page = 1; // show on page 1, this triggers an onGetRect event.
```

See `MediaPlayer.` page and `MediaPlayer.` triggerGetRect for a variation on this same example.

<a id="78625"></a>
<a id="onpause"></a>
<a id="id524"></a>
#### onPause

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Pause event is triggered when media playback pauses, either because of user interaction or when the `play` method is called. See also afterPause (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="42101"></a>
<a id="onplay"></a>
<a id="id525"></a>
#### onPlay

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Play event is triggered when media playback starts or resumes, either because of user interaction or when the `pause` method is called. See also afterPlay (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="82350"></a>
<a id="onready"></a>
<a id="id526"></a>
#### onReady

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Ready event is triggered when a newly-created MediaPlayer is ready for use. Most methods of a `MediaPlayer` object cannot be called until the Ready event is triggered. See also afterReady (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="85317"></a>
<a id="onscript"></a>
<a id="id527"></a>
#### onScript

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Script event is triggered when a script trigger is encountered in the media during playback. See also afterScript (the difference between `on` and `after` event methods are explained in EventListener).

The `event` object for a Script event includes these properties in addition to the standard `event` properties:

|  |  |
|---|---|
| `media.command` | Command name |
| `media.param` | Command parameter string |

These two strings can contain any values that the media clip provides. They do not necessarily contain executable JavaScript code and it is up to the `onScript` or `afterScript` EventListener to interpret them.

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="11271"></a>
<a id="onseek"></a>
<a id="id528"></a>
#### onSeek

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Seek event is triggered when a MediaPlayer is finished seeking to a playback offset as a result of a `seek` call. Not all media players trigger Seek events.

See also afterSeek (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="12658"></a>
<a id="onstatus"></a>
<a id="id529"></a>
#### onStatus

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Status event is triggered on various changes of status that a MediaPlayer reports. See also afterStatus (the difference between `on` and `after` event methods are explained in EventListener).

The `event` object for a Status event includes these properties in addition to the standard `event` properties:

|  |  |
|---|---|
| `media.code` | Status code value, defined in `app.media.status` |
| `media.text` | Status message text |

The following values are used only by some media players, and only when
`media.code == app.media.status.buffering`. They are zero otherwise.

|  |  |
|---|---|
| `media.progress` | Progress value from 0 to media.total |
| `media.total` | Maximum progress value |

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="67418"></a>
<a id="onstop"></a>
<a id="id530"></a>
#### onStop

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The Stop event is triggered when media playback stops, either because of user interaction or when the `stop` method is called.

See also afterStop (the difference between `on` and `after` event methods are explained in EventListener).

**Parameters**

| Parameter | Description |
|-----------|-------------|
| `oMediaEvent` | An `event` object that is automatically passed to this EventListener. |

<a id="36164"></a>
<a id="events"></a>
<a id="id531"></a>
## Events

A multimedia Events object is a collection of `EventListener` objects. The `events` property of a `MediaPlayer` object or a `ScreenAnnot` object is an Events object.

The constructor for an Events object is `app.media.Events`.

Example: This following is executed as a rendition action.

```
console.println("Ready to play "" + event.action.rendition.uiName
    +"" from screen annot "" + event.targetName + "".");
// Create a simple app.media.Events object
var events = new app.media.Events({
    // The Event object is passed as a parameter to all event

     // listeners, this is a the parameter "e" below/
    // Called immediately during a Play event:
    onPlay: function( e ) { console.println( "onPlay: media.id = "
        + e.media.id  ); },
    // Called during idle time after the Play event:
    afterPlay: function() { console.println( "afterPlay" ); },
});
var player = app.media.openPlayer({ events: events });
```

<a id="events-methods"></a>
<a id="id532"></a>
### Events methods

<a id="48718"></a>
<a id="add"></a>
<a id="id533"></a>
#### add

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

Adds any number of `EventListener` objects to the dispatch table for this `Events` object. Any previous listeners are preserved and when an event is triggered, all matching listener methods are called.

The standard event dispatcher first calls any `onEveryEvent` methods in the order they were added, then calls any `on` events for the specific event being dispatched, also in the order they were added. Finally, it sets a very short timer (one millisecond) to call any `after` events. When that timer is triggered, the `after` events are called in the same order described for on events.

See the description of `on` and `after` events in the introductory paragraphs to EventListener object.

> **Note**
>
> If you try to add the same EventListener twice, the second attempt is ignored. If you add an EventListener from inside an event method, the new listener’s methods will be called as part of the dispatching for the current event.

**Parameters**

Any number of parameters, each one an `EventListener` object.

Example: Add an EventListener for the onPlay event. The player is a MediaPlayer object.

```
player.events.add
({
    onPlay: function() { console.println( "onPlay" ); }
});
```

See also remove.

<a id="27002"></a>
<a id="id534"></a>
<a id="id535"></a>
#### dispatch

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

When a MediaPlayer triggers an event, the Multimedia plug-in creates an `event` object and calls `MediaPlayer.events.dispatch(event)`. Similarly, a ScreenAnnot calls `ScreenAnnot.events.dispatch(event)`.

The dispatch method is the only part of the event dispatching system that the Acrobat Multimedia plug-in calls directly. You can substitute your own, entirely different event dispatching system by providing your own `MediaPlayer.events` object with its own `dispatch` method.

The `dispatch` method is responsible for calling each of the EventListeners associated with the event, as identified by `oMediaEvent.name.` In most cases, a PDF file will not provide its own `dispatch` method but will use the standard event dispatching system.

**Parameters**

| Property | Description |
|----------|-------------|
| `oMediaEvent` | An `event` object. |

If you write your own `dispatch` method, note that `oMediaEvent.name` may contain spaces. The standard `dispatch` method makes a copy of `oMediaEvent.name` in `oMediaEvent.media.id` with the spaces removed, to allow the name to be used directly as part of a JavaScript event method name.

Also, if you write your own `dispatch` method, it will be called synchronously when each event occurs, and any processing you do will be subject to the same limitations as described for `on` event methods (see EventListener object). In particular, the method cannot make any calls to a `MediaPlayer` object nor do anything that can indirectly cause a MediaPlayer method to be called.

The `dispatch` method is not usually called directly from JavaScript code, although it can be.

Example: Create a new media player with a custom event dispatcher. This is an advanced technique that would rarely be used in a typical PDF JavaScript.

```
var player = doc.media.newPlayer(
{
    events:
    {
        dispatch: function( e )
        {
            console.println( 'events.dispatch' + e.toSource() );
        }
    }
});
// Synthesize and dispatch a Script event, as if one had been

 // encountered while the media was playing. With the standard event

 // dispatcher, this will call any and all event listeners that have been
// added for this event. With the custom dispatcher above, it will log a
// message to the console.
var event = new Event;
event.name = "Script";
event.media = { command: "test", param: "value" };
player.events.dispatch( event );
```

<a id="18138"></a>
<a id="id536"></a>
<a id="id537"></a>
#### remove

| Version (Key) | Save-Prefs | Security | Product |
|---------------|------------|----------|---------|
| 6.0 | No | No | All |

The method removes one or more EventListeners that were previously added with `Events.add`. If you use an object literal directly in `Events.add`, you will not be able to remove that listener using `Media.remove` because there is no way to pass a reference to the same object. To be able to remove an EventListener, you must pass it to the `add` method in a variable instead of as an object literal, so that you can pass the same variable to `remove`, as in the example below.

The `remove` method can be called from inside an event method to remove any EventListener, even the listener that the current event method is part of. The current event method continues executing, but no other event methods in the same EventListener object will be called.

**Parameters**

Any number of `EventListener` objects.

Example: Assume `player` is a MediaPlayer object.

```
var listener = { afterStop: function() { app.alert("Stopped!"); } }
player.events.add( listener );      // Add listener
.....
player.events.remove( listener );   // Later, remove it
```
