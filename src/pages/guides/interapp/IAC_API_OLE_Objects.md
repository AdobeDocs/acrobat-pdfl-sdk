# OLE Automation

This chapter describes the objects, data types, and methods in the OLE automation interface.

The names `AcroExch.App` and `AxAcroPDFLib.AxAcroPDF` are the external strings OLE clients use to create objects of certain types. The Acrobat developer type libraries call them `CAcro.App` and `AcroPDFLib`, respectively.

Acrobat supports dual interfaces, so the methods all have a return type of `HResult`.

The following table summarizes the available objects and data types.

| Object | Description |
| --- | --- |
| [testlink AcroExch.App](IAC_API_OLE_Objects.md#50532405_31190) | The application itself. |
| [AcroExch.AVDoc](IAC_API_OLE_Objects.md#50532405_36696) | A document as seen in the user interface. |
| [AcroExch.PDDoc](IAC_API_OLE_Objects.md#50532405_34812) | The underlying PDF representation of a document. |
| [AcroExch.HiliteList](IAC_API_OLE_Objects.md#50532405_39171) | An entry in a highlight list. |
| [AcroExch.AVPageView](IAC_API_OLE_Objects.md#50532405_13484) | The area of the window that displays the contents of a page. |
| [AcroExch.PDPage](IAC_API_OLE_Objects.md#50532405_28781) | A single page in the PDF representation of a document. |
| [AcroExch.PDAnnot](IAC_API_OLE_Objects.md#50532405_42349) | An annotation on a page in the PDF file. |
| [AcroExch.PDBookmark](IAC_API_OLE_Objects.md#50532405_29095) | A bookmark in a PDF file. |
| [AcroExch.PDTextSelect](IAC_API_OLE_Objects.md#50532405_33981) | A selection of text on a single page. |
| [AxAcroPDFLib.AxAcroPDF](IAC_API_OLE_Objects.md#50532405_76583) | An object containing PDF browser controls. |
| [AcroExch.Point](IAC_API_OLE_Objects.md#50532405_76536) | A point, specified by its x–coordinate and y–coordinate. |
| [AcroExch.Rect](IAC_API_OLE_Objects.md#50532405_39836) | A rectangle, specified by the top-left and bottom-right points. |
| [AcroExch.Time](IAC_API_OLE_Objects.md#50532405_86731) | A specified time, accurate to the millisecond. |

<a id="50532405_31190"></a>
## AcroExch.App

The Acrobat application itself. This is a creatable interface. From the application layer, you can control the appearance of Acrobat, whether Acrobat appears, and the size of the application window. This object provides access to the menu bar and the toolbar, as well as the visual representation of a PDF file on the screen (through an `AVDoc` object).

### Methods

The `App` object has the following methods.

| Method | Description |
| --- | --- |
| [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231) | Closes all open documents. |
| [Exit](IAC_API_OLE_Objects.md#50532405_24553) | Exits Acrobat. |
| [GetActiveDoc](IAC_API_OLE_Objects.md#50532405_36544) | Gets the frontmost document. |
| [GetActiveTool](IAC_API_OLE_Objects.md#50532405_26079) | Gets the name of the currently active tool. |
| [GetAVDoc](IAC_API_OLE_Objects.md#50532405_26359) | Gets an `AcroExch.AVDoc` object via its index within the list of open `AVDoc` objects. |
| [GetFrame](IAC_API_OLE_Objects.md#50532405_24866) | Gets the window’s frame. |
| [GetInterface](IAC_API_OLE_Objects.md#50532405_91171) | Gets an `IDispatch` interface for a named object, typically a third-party plug-in. |
| [GetLanguage](IAC_API_OLE_Objects.md#50532405_84453) | Gets a code that specifies which language the Acrobat application’s user interface is using. |
| [GetNumAVDocs](IAC_API_OLE_Objects.md#50532405_17689) | Gets the number of open `AcroExch.AVDoc` objects. |
| [GetPreference](IAC_API_OLE_Objects.md#50532405_36273) | Gets a value from the preferences file. |
| [GetPreferenceEx](IAC_API_OLE_Objects.md#50532405_13271) | Gets the specified application preference, using the VARIANT type to pass values. |
| [Hide](IAC_API_OLE_Objects.md#50532405_35477) | Hides the Acrobat application. |
| [Lock](IAC_API_OLE_Objects.md#50532405_19732) | Locks the Acrobat application. |
| [Minimize](IAC_API_OLE_Objects.md#50532405_95716) | Minimizes the Acrobat application. |
| [Maximize](IAC_API_OLE_Objects.md#50532405_28128) | Maximizes the Acrobat application. |
| [MenuItemExecute](IAC_API_OLE_Objects.md#50532405_17615) | Executes the menu item whose language-independent menu item name is specified. |
| [MenuItemIsEnabled](IAC_API_OLE_Objects.md#50532405_38263) | Determines whether the specified menu item is enabled. |
| [MenuItemIsMarked](IAC_API_OLE_Objects.md#50532405_31861) | Determines whether the specified menu item is marked. |
| [MenuItemRemove](IAC_API_OLE_Objects.md#50532405_28065) | Removes the menu item whose language-independent menu item is specified. |
| [Restore](IAC_API_OLE_Objects.md#50532405_61057) | Restores the main window of the Acrobat application. |
| [SetActiveTool](IAC_API_OLE_Objects.md#50532405_34602) | Sets the active tool according to the specified name, and determines whether the tool is to be used only once or should remain active after being used (persistent). |
| [SetFrame](IAC_API_OLE_Objects.md#50532405_14415) | Sets the window’s frame to the specified rectangle. |
| [SetPreference](IAC_API_OLE_Objects.md#50532405_33867) | Sets a value in the preferences file. |
| [SetPreferenceEx](IAC_API_OLE_Objects.md#50532405_91929) | Sets the application preference specified by `nType` to the value stored at `pVal`. |
| [Show](IAC_API_OLE_Objects.md#50532405_20395) | Shows the Acrobat application. |
| [ToolButtonIsEnabled](IAC_API_OLE_Objects.md#50532405_10079) | Determines whether the specified toolbar button is enabled. |
| [ToolButtonRemove](IAC_API_OLE_Objects.md#50532405_31485) | Removes the specified button from the toolbar. |
| [Unlock](IAC_API_OLE_Objects.md#50532405_37485) | Unlocks the Acrobat application if it was previously locked. |
| [UnlockEx](IAC_API_OLE_Objects.md#50532405_30535) | Unlocks the Acrobat application if it was previously locked. |

<a id="50532405_33231"></a>
### CloseAllDocs

Closes all open documents. You can close each individual `AVDoc` object by calling `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907).

You must explicitly close all documents or call `App.CloseAllDocs`. Otherwise, the process never exits.

**Syntax**

```
VARIANT_BOOL CloseAllDocs();
```

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575)
- `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014)
- `PDDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `PDDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_24553"></a>
### Exit

Exits Acrobat. Applications should call `App.Exit` before exiting.

> **Note**
>
> Use `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231) to close all the documents before calling this method.

**Syntax**

```
VARIANT_BOOL Exit();
```

**Returns**

Returns `-1` if the entire shutdown process succeeded. This includes closing any open documents, releasing OLE references, and finally exiting the application. If any step fails, the function returns `0`, and the application continues running. This method does not work if the application is visible (if the user is in control of the application). In such cases, if the `Show` method had previously been called, you can call `Hide` and then `Exit`.

**Related methods**

- `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231)

<a id="50532405_36544"></a>
### GetActiveDoc

Gets the frontmost document.

**Syntax**

```
LPDISPATCH GetActiveDoc();
```

**Returns**

The `LPDISPATCH` for the frontmost `AcroExch.AVDoc` object. If there are no documents open, it returns `NULL`.

**Related methods**

- `App.` [GetAVDoc](IAC_API_OLE_Objects.md#50532405_35267)

<a id="50532405_26079"></a>
### GetActiveTool

Gets the name of the currently active tool.

**Syntax**

```
BSTR GetActiveTool();
```

**Returns**

Returns `NULL` if there is no active tool . Returns the name of the currently active tool otherwise. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of tool names.

**Related methods**

- `App.` [SetActiveTool](IAC_API_OLE_Objects.md#50532405_34602)

<a id="50532405_26359"></a>
### GetAVDoc

Gets an `AcroExch.AVDoc` object from its index within the list of open `AVDoc` objects. Use `App.` [GetNumAVDocs](IAC_API_OLE_Objects.md#50532405_17689) to determine the number of `AcroExch.AVDoc` objects.

**Syntax**

```
LPDISPATCH GetAVDoc(long nIndex);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nIndex | The index of the document to get. |

**Returns**

The `LPDISPATCH` for the specified `AcroExch.AVDoc` document, or `NULL` if `nIndex` is greater than the number of open documents.

**Related methods**

- `App.` [GetActiveTool](IAC_API_OLE_Objects.md#50532405_26079)

<a id="50532405_24866"></a>
### GetFrame

Gets the window’s frame.

GetFrame is not useful when the PDF file was opened with `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575). GetFrame returns the application window’s frame (not the document window’s frame). However, the application’s window is hidden when a document is opened using [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575) , and does not change in size as document windows are moved and resized.

This method is also not useful if the Acrobat application is in single document interface (SDI) mode.

**Syntax**

```
LPDISPATCH GetFrame();
```

**Returns**

The `LPDISPATCH` for the window’s frame, specified as an `AcroExch.Rect`.

If the Acrobat application is in SDI mode, a \[0,0,0,0\] `Rect` is returned.

**Related methods**

- `App.` [Maximize](IAC_API_OLE_Objects.md#50532405_28128)
- `App.` [SetFrame](IAC_API_OLE_Objects.md#50532405_14434)

<a id="50532405_91171"></a>
### GetInterface

Gets an `IDispatch` interface for a named object, typically a third-party plug-in. This is an entry point to functionality that is undefined and which must be provided by the plug-in author. If you are accessing third-party functionality through `GetInterface`, ask the author for additional information.

**Syntax**

```
LPDISPATCH GetInterface (BSTR szName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szName | Name of the object. |

**Returns**

The `LPDISPATCH` for the objects’s interface or `NULL` if the object was not found.

<a id="50532405_84453"></a>
### GetLanguage

Gets a code that specifies which language the Acrobat application’s user interface is using.

**Syntax**

```
BSTR GetLanguage();
```

**Returns**

String containing a three-letter language code. Must be one of the following:

- DEU-German
- ENU-English
- ESP-Spanish
- FRA-French
- ITA-Italian
- NLD-Dutch
- SVE-Swedish

**Related methods**

- `App.` [GetPreference](IAC_API_OLE_Objects.md#50532405_36273)
- `App.` [SetPreference](IAC_API_OLE_Objects.md#50532405_33867)

<a id="50532405_17689"></a>
### GetNumAVDocs

Gets the number of open `AcroExch.AVDoc` objects. The maximum number of documents the Acrobat application can open at a time is specified by the `avpMaxOpenDocuments` preference, which can be obtained with `App.` [GetPreferenceEx](IAC_API_OLE_Objects.md#50532405_13271) and set by `App.` [SetPreferenceEx](IAC_API_OLE_Objects.md#50532405_91929).

**Syntax**

```
long GetNumAVDocs();
```

**Returns**

The number of open `AcroExch.AVDoc` objects.

**Related methods**

- `App.` [GetActiveDoc](IAC_API_OLE_Objects.md#50532405_36544)
- `App.` [GetAVDoc](IAC_API_OLE_Objects.md#50532405_26359)

<a id="50532405_36273"></a>
GetPreference

> **Note**
>
> This method is deprecated; use [GetPreferenceEx](IAC_API_OLE_Objects.md#50532405_13271) instead. `GetPreference` is unable to accept important data types such as strings, but [GetPreferenceEx](IAC_API_OLE_Objects.md#50532405_13271) can convert many data types into acceptable formats.

Gets a value from the preferences file. Zoom values (used in `avpDefaultZoomScale` and `avpMaxPageCacheZoom`) are returned as percentages (for example, 1.00 is returned as 100). Colors (used in `avpNoteColor` – `PDcolorValue`) are automatically converted to RGB values from the representation used in the preferences file.

**Syntax**

```
long GetPreference(short nType);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nType | The preferences item whose value is set. For more information, see the [PDF Library documentation](https://www.adobe.com/go/pdflibrary). |

**Returns**

The value of the specified preference item.

**Related methods**

- `App.` [GetLanguage](IAC_API_OLE_Objects.md#50532405_84453)
- `App.` [SetPreference](IAC_API_OLE_Objects.md#50532405_33867)

<a id="50532405_13271"></a>
### GetPreferenceEx

Gets the specified application preference, using the VARIANT type to pass values.

**Syntax**

```
VARIANT GetPreferenceEx(short nType);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nType | The name of the preferences item whose value is obtained. |

**Returns**

The value of the specified preference item.

**Related methods**

- `App.` [GetLanguage](IAC_API_OLE_Objects.md#50532405_84453)
- `App.` [SetPreferenceEx](IAC_API_OLE_Objects.md#50532405_91929)

<a id="50532405_35477"></a>
### Hide

Hides the Acrobat application. When the viewer is hidden, the user has no control over it, and the Acrobat application exits when the last automation object is closed.

**Syntax**

```
VARIANT_BOOL Hide();
```

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `App.` [Show](IAC_API_OLE_Objects.md#50532405_20395)

<a id="50532405_19732"></a>
### Lock

Locks the Acrobat application. Typically, this method is called when using `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014) to draw into another application’s window. If you call `App.Lock`, you should call `App.` [UnlockEx](IAC_API_OLE_Objects.md#50532405_30535) when you are done using OLE automation.

There are some advantages and disadvantages of locking the viewer when using `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014). You must consider these before deciding whether to lock the viewer:

- Locking prevents problems that can sometimes occur if two processes are trying to open a file at the same time.
- Locking prevents a user from using Acrobat’s user interface (such as adding annotations) in your application’s window.
- Locking can prevent any other application, including the Acrobat application, from opening PDF files. This problem can be minimized by calling `App.` [UnlockEx](IAC_API_OLE_Objects.md#50532405_30535) as soon as the file has been opened.

**Syntax**

```
VARIANT_BOOL Lock(BSTR szLockedBy);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szLockedBy | A string that is used as the name of the application that has locked the Acrobat application. |

**Returns**

`-1` if the Acrobat application was locked successfully, `0` otherwise. Locking fails if the Acrobat application is visible.

**Related methods**

- `App.` [UnlockEx](IAC_API_OLE_Objects.md#50532405_30535)

<a id="50532405_95716"></a>
### Minimize

Minimizes the Acrobat application.

**Syntax**

```
VARIANT_BOOL Minimize(long BMinimize);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| BMinimize | If a positive number, the Acrobat application is minimized. If `0`, the Acrobat application is returned to its normal state. |

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `App.` [GetFrame](IAC_API_OLE_Objects.md#50532405_24866)
- `App.` [SetFrame](IAC_API_OLE_Objects.md#50532405_14434)

<a id="50532405_28128"></a>
### Maximize

Maximizes the Acrobat application.

**Syntax**

```
VARIANT_BOOL Maximize(long bMaximize);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bMaximize | If a positive number, the Acrobat application is maximized. If `0`, the Acrobat application is returned to its normal state. |

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `App.` [GetFrame](IAC_API_OLE_Objects.md#50532405_24866)
- `App.` [SetFrame](IAC_API_OLE_Objects.md#50532405_14434)

<a id="50532405_17615"></a>
### MenuItemExecute

Executes the menu item whose language-independent menu item name is specified.

**Syntax**

```
VARIANT_BOOL MenuItemExecute(BSTR szMenuItemName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szMenuItemName | The language-independent name of the menu item to execute. See the *PDF Library documentation* for a list of menu item names. |

**Returns**

Returns `-1` if the menu item executes successfully, or `0` if the menu item is missing or is not enabled.

**Related methods**

- `App.` [MenuItemIsEnabled](IAC_API_OLE_Objects.md#50532405_38263)
- `App.` [MenuItemIsMarked](IAC_API_OLE_Objects.md#50532405_31861)
- `App.` [MenuItemRemove](IAC_API_OLE_Objects.md#50532405_28065)

<a id="50532405_38263"></a>
### MenuItemIsEnabled

Determines whether the specified menu item is enabled.

**Syntax**

```
VARIANT_BOOL MenuItemIsEnabled(BSTR szMenuItemName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szMenuItemName | The language-independent name of the menu item whose enabled state is obtained. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of menu item names. |

**Returns**

`-1` if the menu item is enabled, `0` if it is disabled or does not exist.

**Related methods**

- `App.` [MenuItemExecute](IAC_API_OLE_Objects.md#50532405_17615)
- `App.` [MenuItemIsMarked](IAC_API_OLE_Objects.md#50532405_31861)
- `App.` [MenuItemRemove](IAC_API_OLE_Objects.md#50532405_28065)

<a id="50532405_31861"></a>
### MenuItemIsMarked

Determines whether the specified menu item is marked.

**Syntax**

```
VARIANT_BOOL MenuItemIsMarked(BSTR szMenuItemName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szMenuItemName | The language-independent name of the menu item whose marked state is obtained. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of menu item names. |

**Returns**

`-1` if the menu item is marked, `0` if it is not marked or does not exist.

**Related methods**

- `App.` [MenuItemExecute](IAC_API_OLE_Objects.md#50532405_17615)
- `App.` [MenuItemIsEnabled](IAC_API_OLE_Objects.md#50532405_38263)
- `App.` [MenuItemRemove](IAC_API_OLE_Objects.md#50532405_28065)

<a id="50532405_28065"></a>
### MenuItemRemove

Removes the menu item whose language-independent menu item is specified.

**Syntax**

```
VARIANT_BOOL MenuItemRemove(BSTR szMenuItemName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szMenuItemName | The language-independent name of the menu item to remove. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of menu item names. |

**Returns**

`-1` if the menu item was removed, `0` if the menu item does not exist.

**Related methods**

- `App.` [MenuItemExecute](IAC_API_OLE_Objects.md#50532405_17615)
- `App.` [MenuItemIsEnabled](IAC_API_OLE_Objects.md#50532405_38263)
- `App.` [MenuItemIsMarked](IAC_API_OLE_Objects.md#50532405_31861)

<a id="50532405_61057"></a>
### Restore

Restores the main window of the Acrobat application. Calling this with `bRestore` set to a positive number causes the main window to be restored to its original size and position and to become active.

**Syntax**

```
VARIANT_BOOL Restore(long bRestore);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bRestore | If a positive number, the Acrobat application is restored, `0` otherwise. |

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `App.` [GetFrame](IAC_API_OLE_Objects.md#50532405_24866)
- `App.` [SetFrame](IAC_API_OLE_Objects.md#50532405_14434)

<a id="50532405_34602"></a>
### SetActiveTool

Sets the active tool according to the specified name, and determines whether the tool is to be used only once or should remain active after being used (persistent).

**Syntax**

```
VARIANT_BOOL SetActiveTool(BSTR szButtonName,
                          long bPersistent);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szButtonName | The name of the tool to set as the active tool. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of tool names. |
| bPersistent | A request indicating whether the tool should be persistent. A positive number indicates a request to the Acrobat application for the tool to remain active after it has been used. If `0` is specified, the Acrobat application reverts to the previously active tool after this tool is used once. |

**Returns**

`-1` if the tool was set, `0` otherwise.

**Related methods**

- `App.` [GetActiveTool](IAC_API_OLE_Objects.md#50532405_26079)
- `App.` [ToolButtonIsEnabled](IAC_API_OLE_Objects.md#50532405_10079)
- `App.` [ToolButtonRemove](IAC_API_OLE_Objects.md#50532405_31485)

<a id="50532405_14415"></a>
### SetFrame

Sets the window’s frame to the specified rectangle. This method has no effect if the Acrobat application is in single document interface (SDI) mode.

**Syntax**

```
VARIANT_BOOL SetFrame(LPDISPATCH iAcroRect);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroRect | The `LPDISPATCH` for an `AcroExch.Rect` specifying the window frame. `iAcroRect` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

`-1` if the frame was set, `0` if `iAcroRect` is not of type `AcroExch.Rect`.

**Related methods**

- `App.` [GetFrame](IAC_API_OLE_Objects.md#50532405_24866)
- `App.` [Maximize](IAC_API_OLE_Objects.md#50532405_28128)

<a id="50532405_33867"></a>
### SetPreference

> **Note**
>
> This method is deprecated; use [SetPreferenceEx](IAC_API_OLE_Objects.md#50532405_91929) instead. `SetPreference` is unable to accept important data types such as strings, but [SetPreferenceEx](IAC_API_OLE_Objects.md#50532405_91929) can convert many data types into acceptable formats.

Sets a value in the preferences file. Zoom values (used in `avpDefaultZoomScale` and `avpMaxPageCacheZoom`) must be passed as percentages and are automatically converted to fixed point numbers (for example, 100 is automatically converted to 1.0). Colors (used in `avpHighlightColor` or `avpNoteColor`) are automatically converted from RGB values to the representation used in the preferences file.

**Syntax**

```
VARIANT_BOOL SetPreference(short nType, long nValue);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nType | The preferences item whose value is set. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of preference items. |
| nValue | The value to set. |

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `App.` [GetLanguage](IAC_API_OLE_Objects.md#50532405_84453)
- `App.` [GetPreferenceEx](IAC_API_OLE_Objects.md#50532405_13271)

<a id="50532405_91929"></a>
### SetPreferenceEx

Sets the application preference specified by `nType` to the value stored at `pVal`. If `pVal` has a non-conforming `VARTYPE`, `SetPreferenceEx` performs type conversion. For example, a string representation of an integer is converted to an actual integer.

**Syntax**

```
VARIANT_BOOL SetPreferenceEx(short nType, VARIANT* pVal);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nType | The preferences item whose value is set. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of preference items. |
| pVal | The value to set. |

**Returns**

Returns `-1` if `nType` is a supported type or the type conversion is successful, `0` otherwise.

**Related methods**

- `App.` [GetLanguage](IAC_API_OLE_Objects.md#50532405_84453)
- `App.` [GetPreferenceEx](IAC_API_OLE_Objects.md#50532405_13271)

<a id="50532405_20395"></a>
### Show

Shows the Acrobat application. When the viewer is shown, the user is in control, and the Acrobat application does not automatically exit when the last automation object is destroyed. However, it will exit if no documents are being displayed.

**Syntax**

```
VARIANT_BOOL Show();
```

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `App.` [Hide](IAC_API_OLE_Objects.md#50532405_35477)

<a id="50532405_10079"></a>
### ToolButtonIsEnabled

Determines whether the specified toolbar button is enabled.

**Syntax**

```
VARIANT_BOOL ToolButtonIsEnabled(BSTR szButtonName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szButtonName | The name of the button whose enabled state is checked. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of toolbar button names. |

**Returns**

`-1` if the button is enabled, `0` if it is not enabled or does not exist.

**Related methods**

- `App.` [GetActiveTool](IAC_API_OLE_Objects.md#50532405_26079)
- `App.` [SetActiveTool](IAC_API_OLE_Objects.md#50532405_34602)
- `App.` [ToolButtonRemove](IAC_API_OLE_Objects.md#50532405_31485)

<a id="50532405_31485"></a>
### ToolButtonRemove

Removes the specified button from the toolbar.

**Syntax**

```
VARIANT_BOOL ToolButtonRemove(BSTR szButtonName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szButtonName | The name of the button to remove. See the [PDF Library documentation](https://www.adobe.com/go/pdflibrary) for a list of toolbar button names. |

**Returns**

`-1` if the button was removed, `0` otherwise.

**Related methods**

- `App.` [GetActiveTool](IAC_API_OLE_Objects.md#50532405_26079)
- `App.` [SetActiveTool](IAC_API_OLE_Objects.md#50532405_34602)
- `App.` [ToolButtonIsEnabled](IAC_API_OLE_Objects.md#50532405_10079)

<a id="50532405_37485"></a>
### Unlock

> **Note**
>
> In version 4.0 or later, use `App.` [UnlockEx](IAC_API_OLE_Objects.md#50532405_30535) instead.

Unlocks the Acrobat application if it was previously locked. This method clears a flag that indicates the viewer is locked. If you called `App.` [Lock](IAC_API_OLE_Objects.md#50532405_19732) , you should call `App.Unlock` when you are done using OLE automation.

Use `App.` [Lock](IAC_API_OLE_Objects.md#50532405_19732) and App `.` [UnlockEx](IAC_API_OLE_Objects.md#50532405_30535) if you call [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575).

Typically, you call `App.` [Lock](IAC_API_OLE_Objects.md#50532405_19732) when your application initializes and `App.Unlock` in your application’s destructor method.

**Syntax**

```
VARIANT_BOOL Unlock();
```

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `App.` [Lock](IAC_API_OLE_Objects.md#50532405_19732)
- `App.` [UnlockEx](IAC_API_OLE_Objects.md#50532405_30535)

<a id="50532405_30535"></a>
### UnlockEx

Unlocks the Acrobat application if it was previously locked.

**Syntax**

```
VARIANT_BOOL UnlockEx (BSTR szLockedBy);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szLockedBy | A string indicating the name of the application to be unlocked. |

**Returns**

`-1` if successful, `0` if not.

**Related methods**

- `App.` [Lock](IAC_API_OLE_Objects.md#50532405_19732)

<a id="50532405_36696"></a>
## AcroExch.AVDoc

A view of a PDF document in a window. This is a creatable interface. There is one `AVDoc` object per displayed document. Unlike a `PDDoc` object, an `AVDoc` object has a window associated with it.

### Methods

The AVDoc object has the following methods.

| Method | Description |
| --- | --- |
| [BringToFront](IAC_API_OLE_Objects.md#50532405_25352) | Brings the window to the front. |
| [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710) | Clears the current selection. |
| [Close](IAC_API_OLE_Objects.md#50532405_10907) | Closes a document. |
| [FindText](IAC_API_OLE_Objects.md#50532405_28644) | Finds the specified text, scrolls so that it is visible, and highlights it. |
| [GetAVPageView](IAC_API_OLE_Objects.md#50532405_35375) | Gets the `AcroExch.AVPageView` associated with an `AcroExch.AVDoc`. |
| [GetFrame](IAC_API_OLE_Objects.md#50532405_28538) | Gets the rectangle specifying the window’s size and location. |
| [GetPDDoc](IAC_API_OLE_Objects.md#50532405_25013) | Gets the `AcroExch.PDDoc` associated with an `AcroExch.AVDoc`. |
| [GetTitle](IAC_API_OLE_Objects.md#50532405_12179) | Gets the window’s title. |
| [GetViewMode](IAC_API_OLE_Objects.md#50532405_29291) | Gets the current document view mode (pages only, pages and thumbnails, or pages and bookmarks). |
| [IsValid](IAC_API_OLE_Objects.md#50532405_42634) | Determines whether the `AcroExch.AVDoc` is still valid. |
| [Maximize](IAC_API_OLE_Objects.md#50532405_13863) | Maximizes the window if `bMaxSize` is a positive number. |
| [Open](IAC_API_OLE_Objects.md#50532405_23963) | Opens a file. |
| [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575) | Opens a PDF file and displays it in a user-specified window. |
| [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014) | Opens a PDF file and displays it in a user-specified window. |
| [PrintPages](IAC_API_OLE_Objects.md#50532405_30920) | Prints a specified range of pages displaying a print dialog box. |
| [PrintPagesEx](IAC_API_OLE_Objects.md#50532405_37344) | Prints a specified range of pages, displaying a print dialog box. |
| [PrintPagesSilent](IAC_API_OLE_Objects.md#50532405_16535) | Prints a specified range of pages without displaying any dialog box. |
| [PrintPagesSilentEx](IAC_API_OLE_Objects.md#50532405_38114) | Prints a specified range of pages without displaying any dialog box. |
| [SetFrame](IAC_API_OLE_Objects.md#50532405_14434) | Sets the window’s size and location. |
| [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749) | Sets the document’s selection to the specified text selection. |
| [SetTitle](IAC_API_OLE_Objects.md#50532405_28000) | Sets the window’s title. |
| [SetViewMode](IAC_API_OLE_Objects.md#50532405_37022) | Sets the mode in which the document will be viewed (pages only, pages and thumbnails, or pages and bookmarks) |
| [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147) | Changes the view so that the current text selection is visible. |

<a id="50532405_25352"></a>
### BringToFront

Brings the window to the front.

**Syntax**

```
VARIANT_BOOL BringToFront();
```

**Returns**

Returns `0` if no document is open, `-1` otherwise.

<a id="50532405_16710"></a>
### ClearSelection

Clears the current selection.

**Syntax**

```
VARIANT_BOOL ClearSelection();
```

**Returns**

Returns `-1` if the selection was cleared, `0` if no document is open or the selection could not be cleared.

**Related methods**

- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_26583)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_10907"></a>
### Close

Closes a document. You can close all open `AVDoc` objects by calling `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231).

To reuse an `AVDoc` object, close it with `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907) , then use the `AVDoc` object’s `LPDISPATCH` for `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575).

**Syntax**

```
VARIANT_BOOL Close(long bNoSave);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bNoSave | If a positive number, the document is closed without saving it. If `0` and the document has been modified, the user is asked whether or not the file should be saved. |

**Returns**

Always returns `-1`, even if no document is open.

**Related methods**

- `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231)
- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575)
- `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014)
- `PDDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `PDDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_28644"></a>
### FindText

Finds the specified text, scrolls so that it is visible, and highlights it.

**Syntax**

```
VARIANT_BOOL FindText(BSTR szText, long bCaseSensitive, long bWholeWordsOnly, long bReset);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szText | The text to be found. |
| bCaseSensitive | If a positive number, the search is case-sensitive. If `0`, it is case-insensitive. |
| bWholeWordsOnly | If a positive number, the search matches only whole words. If `0`, it matches partial words. |
| bReset | If a positive number, the search begins on the first page of the document. If `0`, it begins on the current page. |

**Returns**

`-1` if the text was found, `0` otherwise.

<a id="50532405_35375"></a>
### GetAVPageView

Gets the `AcroExch.AVPageView` associated with an `AcroExch.AVDoc`.

**Syntax**

```
LPDISPATCH GetAVPageView();
```

**Returns**

The `LPDISPATCH` for the `AcroExch.AVPageView` or `NULL` if no document is open.

**Related methods**

- `AVDoc.` [GetPDDoc](IAC_API_OLE_Objects.md#50532405_25013)
- `AVDoc.` [SetViewMode](IAC_API_OLE_Objects.md#50532405_37022)
- `AVPageView.` [GetAVDoc](IAC_API_OLE_Objects.md#50532405_35267)
- `AVPageView.` [GetDoc](IAC_API_OLE_Objects.md#50532405_11484)

<a id="50532405_28538"></a>
### GetFrame

Gets the rectangle specifying the window’s size and location.

**Syntax**

```
LPDISPATCH GetFrame();
```

**Returns**

The `LPDISPATCH` for an `AcroExch.Rect` containing the frame, or `NULL` if no document is open.

**Related methods**

- `AVDoc.` [SetFrame](IAC_API_OLE_Objects.md#50532405_14434)

<a id="50532405_25013"></a>
### GetPDDoc

Gets the `AcroExch.PDDoc` associated with an `AcroExch.AVDoc`.

**Syntax**

```
LPDISPATCH GetPDDoc();
```

**Returns**

The `LPDISPATCH` for the `AcroExch.PDDoc` or `NULL` if no document is open.

**Related methods**

- `AVDoc.` [GetAVPageView](IAC_API_OLE_Objects.md#50532405_35375)
- `AVPageView.` [GetAVDoc](IAC_API_OLE_Objects.md#50532405_26359)
- `AVPageView.` [GetDoc](IAC_API_OLE_Objects.md#50532405_11484)

<a id="50532405_12179"></a>
### GetTitle

Gets the window’s title.

**Syntax**

```
BSTR GetTitle();
```

**Returns**

The window’s title or `NULL` if no document is open.

**Related methods**

- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `AVDoc.` [SetTitle](IAC_API_OLE_Objects.md#50532405_37671)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_29291"></a>
### GetViewMode

Gets the current document view mode (pages only, pages and thumbnails, or pages and bookmarks).

**Syntax**

```
long GetViewMode();
```

**Returns**

The current document view mode or `0` if no document is open. The return value is one of the following:

- `PDDontCare`: `0`: leave the view mode as it is
- `PDUseNone`: `1`: display without bookmarks or thumbnails
- `PDUseThumbs`: `2`: display using thumbnails
- `PDUseBookmarks`: `3`: display using bookmarks
- `PDFullScreen`: `4`: display in full screen mode

**Related methods**

- `AVDoc.` [GetAVPageView](IAC_API_OLE_Objects.md#50532405_35375)
- `AVDoc.` [SetViewMode](IAC_API_OLE_Objects.md#50532405_37022)

<a id="50532405_42634"></a>
### IsValid

Determines whether the `AcroExch.AVDoc` is still valid. This method only checks if the document has been closed or deleted; it does not check the internal structure of the document.

**Syntax**

```
VARIANT_BOOL IsValid();
```

**Returns**

`-1` if the document can still be used, `0` otherwise.

**Related methods**

- `App.` [GetAVDoc](IAC_API_OLE_Objects.md#50532405_26359)
- `AVPageView.` [GetAVDoc](IAC_API_OLE_Objects.md#50532405_35267)

<a id="50532405_13863"></a>
### Maximize

Maximizes the window if `bMaxSize` is a positive number.

**Syntax**

```
VARIANT_BOOL Maximize(long bMaxSize);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bMaxSize | Indicates whether the window should be maximized. |

**Returns**

`-1` if a document is open, `0` otherwise.

**Related methods**

- `AVDoc.` [GetFrame](IAC_API_OLE_Objects.md#50532405_28538)
- `AVDoc.` [SetFrame](IAC_API_OLE_Objects.md#50532405_14434)

<a id="50532405_23963"></a>
### Open

Opens a file. A new instance of `AcroExch.AVDoc` must be created for each displayed PDF file.

> **Note**
>
> An application must explicitly close any `AVDoc` that it opens by calling `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907) (the destructor for the `AcroExch.AVDoc` class does not call `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)).

**Syntax**

```
VARIANT_BOOL Open(BSTR szFullPath, BSTR szTempTitle);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szFullPath | The full path of the file to open. |
| szTempTitle | An optional title for the window in which the file is opened. If `szTempTitle` is `NULL` or the empty string, it is ignored. Otherwise, `szTempTitle` is used as the window title. |

**Returns**

`-1` if the file was opened successfully, `0` otherwise.

**Related methods**

- `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231)
- `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `AVDoc.` [GetTitle](IAC_API_OLE_Objects.md#50532405_12179)
- `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575)
- `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014)
- `AVDoc.` [SetTitle](IAC_API_OLE_Objects.md#50532405_28000)
- `PDDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `PDDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_40575"></a>
### OpenInWindow

> **Note**
>
> As of Acrobat 3.0, this method simply returns `false`. Use the method `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014) instead.

**Syntax**

```
VARIANT_BOOL OpenInWindow(BSTR fileName, short hWnd);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fileName | The full path of the file to open. |
| hWnd | Handle for the window in which the file is displayed. |

**Returns**

`-1`

**Related methods**

- `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231)
- `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014)
- `PDDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `PDDoc.` [Open](IAC_API_OLE_Objects.md#50532405_41972)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_22014"></a>
### OpenInWindowEx

Opens a PDF file and displays it in a user-specified window. The default Windows file system is used to open the file.

> **Note**
>
> Acrobat uses only its built-in implementation of the file opening code—not any replacement file system version that a developer might have added with a plug-in.

An application must explicitly close any `AVDoc` that it opens by calling `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907) (the destructor for the `AcroExch.AVDoc` class does not call `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907) ).

Do not set the view mode to [Close](IAC_API_OLE_Objects.md#50532405_10907) with `AVDoc.` [SetViewMode](IAC_API_OLE_Objects.md#50532405_37022) when using `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014) ; this will cause the viewer and application to hang.

If you use a view mode of `AV_PAGE_VIEW`, the `pagemode` parameter will be ignored.

See `AVApp.` [Lock](IAC_API_OLE_Objects.md#50532405_19732) for a discussion of whether to lock the viewer before making this call.

**Syntax**

```
VARIANT_BOOL OpenInWindowEx(LPCTSTR szFullPath, long hWnd,

                 long openFlags, long useOpenParams

                 long pgNum, short pageMode,

                 short zoomType, long zoom, short top,

                 short left);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szFullPath | The full path of the file to open. |
| hWnd | Handle for the window in which the file is displayed. |
| openFlags | Type of window view. Must be one of the following:  `AV_EXTERNAL_VIEW`: Display the `AVPageView`, scrollbars, toolbar, and bookmark or thumbnails pane. Annotations are active.   `AV_DOC_VIEW`: Display the `AVPageView`, scrollbars, and bookmark or thumbnails pane. Annotations are active.   `AV_PAGE_VIEW`: Display only the `AVPageView` (the window that displays the PDF file). Do not display scrollbars, the toolbar, and bookmark or thumbnails pane. Annotations are active.  -  Use either `AV_DOC_VIEW` or `AV_PAGE_VIEW` whenever possible. Use `AV_EXTERNAL_VIEW` only if you do not want the application to display its own toolbar. Use `AV_PAGE_VIEW` to open the file with no scrollbars and no status window at the bottom of the page. |
| useOpenParams | `0` indicates that the open action of the file is used; a positive number indicates that the action is overridden with the parameters that follow. |
| pgNum | Page number at which the file is to be opened if `useOpenParams` is a positive number. The first page is zero. |
| pageMode | Specifies page view mode if `useOpenParams` is a positive number. Possible values:  `PDDontCare`: `0`: leave the view mode as it is  `PDUseNone`: `1`: display without bookmarks or thumbnails  `PDUseThumbs`: `2`: display using thumbnails  `PDUseBookmarks`: `3`: display using bookmarks  `PDFullScreen`: `4`: display in full screen mode |
| zoomType | Zoom type of the page view if `useOpenParams` is a positive number. Possible values are:  `AVZoomFitHeight`: Fits the page’s height in the window.  `AVZoomFitPage`: Fits the page in the window.  `AVZoomFitVisibleWidth`: Fits the page’s visible content into the window.  `AVZoomFitWidth`: Fits the page’s width into the window.  `AVZoomNoVary`: A fixed zoom, such as 100%. |
| zoom | Zoom factor, used only for `AVZoomNoVary` if `useOpenParams` is a positive number. |
| top | Used for certain zoom types (such as `AVZoomNoVary`) if `useOpenParams` is a positive number. See the [PDF Reference](https://www.adobe.com/go/pdfreference) for information on views. |
| left | Used for certain zoom types (such as `AVZoomNoVary`) if `useOpenParams` is a positive number. See the [PDF Reference](https://www.adobe.com/go/pdfreference) for information on views. |

**Returns**

`-1` if the document was opened successfully, `0` otherwise.

**Related methods**

- `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231)
- `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575)
- `PDDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `PDDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_30920"></a>
### PrintPages

Prints a specified range of pages displaying a print progress dialog box. `PrintPages` always uses the default printer setting. It is possible to create custom dialog boxes as shown in the ActiveViewVB sample. Such custom dialog boxes could be used in place of the print progress dialog box or any other dialog box.

**Syntax**

```
VARIANT_BOOL PrintPages(long nFirstPage,
                 long nLastPage,long nPSLevel,

                 long bBinaryOk, long bShrinkToFit);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFirstPage | The first page to be printed. The first page in a `PDDoc` object is page `0`. |
| nLastPage | The last page to be printed. |
| nPSLevel | Valid values are `2` and `3`. If `2`, PostScript  Level 2 operators are used. If `3`, PostScript Language Level 3 operators are also used. |
| bBinaryOk | If a positive number, binary data can be included in the PostScript program. If `0`, all data is encoded as 7-bit ASCII. |
| bShrinkToFit | If a positive number, the page is shrunk (if necessary) to fit within the imageable area of the printed page. If `0`, it is not. |

**Returns**

`0` if there were any exceptions while printing or if no document was open, `-1` otherwise.

**Related methods**

- `AVDoc.` [PrintPagesEx](IAC_API_OLE_Objects.md#50532405_37344)
- `AVDoc.` [PrintPagesSilent](IAC_API_OLE_Objects.md#50532405_16535)
- `AVDoc.` [PrintPagesSilentEx](IAC_API_OLE_Objects.md#50532405_38114)

<a id="50532405_37344"></a>
### PrintPagesEx

Prints a specified range of pages, displaying a print progress dialog box. `PrintPagesEx` has more parameters than `PrintPages`. `PrintPagesEx` always uses the default printer setting. It is possible to create custom dialog boxes as shown in the ActiveViewVB sample. Such custom dialog boxes could be used in place of the print progress dialog box or any other dialog box.

**Syntax**

```
VARIANT_BOOL printPagesEx(long nFirstPage,long nLastPage,
                 long nPSLevel, long bBinaryOk,

                 long bShrinkToFit, long bReverse,

                 long bFarEastFontOpt, long bEmitHalftones,

                 long iPageOption);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFirstPage | The first page to be printed. The first page in a `PDDoc` object is page `0`. |
| nLastPage | The last page to be printed. |
| nPSLevel | If `2`, PostScript Level 2 operators are used. If `3`, PostScript Language Level 3 operators are also used. |
| bBinaryOk | If a positive number, binary data may be included in the PostScript program. If `0`, all data is encoded as 7-bit ASCII. |
| bShrinkToFit | If a positive number, the page is shrunk (if necessary) to fit within the imageable area of the printed page. If `0`, it is not. |
| bReverse | (PostScript printing only) If a positive number, print the pages in reverse order. If false, print the pages in the regular order. |
| bFarEastFontOpt | (PostScript printing only) Set to a positive number if the destination printer has multibyte fonts; set to `0` otherwise. |
| bEmitHalftones | (PostScript printing only) If a positive number, emit the halftones specified in the document. If `0`, do not. |
| iPageOption | Pages in the range to print. Must be one of: `PDAllPages`, `PDEvenPagesOnly`, or `PDOddPagesOnly`. |

**Returns**

`0` if there were any exceptions while printing or if no document was open, `-1` otherwise.

**Related methods**

- `AVDoc.` [PrintPages](IAC_API_OLE_Objects.md#50532405_30920)
- `AVDoc.` [PrintPagesSilent](IAC_API_OLE_Objects.md#50532405_16535)
- `AVDoc.` [PrintPagesSilentEx](IAC_API_OLE_Objects.md#50532405_38114)

<a id="50532405_16535"></a>
### PrintPagesSilent

Prints a specified range of pages without displaying any dialog box. This method is identical to `AVDoc.` [PrintPages](IAC_API_OLE_Objects.md#50532405_30920) except for not displaying the dialog box. `PrintPagesSilent` always uses the default printer setting.

**Syntax**

```
VARIANT_BOOL PrintPagesSilent(long nFirstPage, long nLastPage,

                 long nPSLevel, long bBinaryOk,

                 long bShrinkToFit);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFirstPage | The first page to be printed. The first page in a `PDDoc` object is page `0`. |
| nLastPage | The last page to be printed. |
| nPSLevel | If `2`, PostScript Level 2 operators are used. If `3`, PostScript Language Level 3 operators are also used. |
| bBinaryOk | If a positive number, binary data may be included in the PostScript program. If `0`, all data is encoded as 7-bit ASCII. |
| bShrinkToFit | If a positive number, the page is shrunk (if necessary) to fit within the imageable area of the printed page. If `0`, it is not. |

**Returns**

`0` if there were any exceptions while printing or if no document was open, `-1` otherwise.

**Related methods**

- `AVDoc.` [PrintPages](IAC_API_OLE_Objects.md#50532405_30920)
- `AVDoc.` [PrintPagesEx](IAC_API_OLE_Objects.md#50532405_37344)
- `AVDoc.` [PrintPagesSilentEx](IAC_API_OLE_Objects.md#50532405_38114)

<a id="50532405_38114"></a>
### PrintPagesSilentEx

Prints a specified range of pages without displaying any dialog box. This method is identical to `AVDoc.` [PrintPagesEx](IAC_API_OLE_Objects.md#50532405_37344) except for not displaying the dialog box. `PrintPagesSilentEx` has more parameters than `PrintPagesSilent`. `PrintPagesSilentEx` always uses the default printer setting.

**Syntax**

```
VARIANT_BOOL PrintPagesSilentEx(long nFirstPage,
                 long nLastPage,

                 long nPSLevel, long bBinaryOk,

                 long bShrinkToFit, long bReverse,

                 long bFarEastFontOpt,

                 long bEmitHalftones,

                 long iPageOption);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFirstPage | The first page to be printed. |
| nLastPage | The last page to be printed. |
| nPSLevel | If `2`, PostScript Level 2 operators are used. If `3`, PostScript Language Level 3 operators are also used. |
| bBinaryOk | If a positive number, binary data may be included in the PostScript program. If `0`, all data is encoded as 7-bit ASCII. |
| bShrinkToFit | If a positive number, the page is shrunk (if necessary) to fit within the imageable area of the printed page. If `0`, it is not. |
| bReverse | (PostScript printing only) If a positive number, print the pages in reverse order. If false, print the pages in the regular order. |
| bFarEastFontOpt | (PostScript printing only) Set to a positive number if the destination printer has multibyte fonts; set to `0` otherwise. |
| bEmitHalftones | (PostScript printing only) If a positive number, emit the halftones specified in the document. If `0`, do not. |
| iPageOption | Pages in the range to print. Must be one of: `PDAllPages`, `PDEvenPagesOnly`, or `PDOddPagesOnly`. |

**Returns**

`0` if there were any exceptions while printing, `-1` otherwise.

**Related methods**

- `AVDoc.` [PrintPages](IAC_API_OLE_Objects.md#50532405_30920)
- `AVDoc.` [PrintPagesEx](IAC_API_OLE_Objects.md#50532405_37344)
- `AVDoc.` [PrintPagesSilentEx](IAC_API_OLE_Objects.md#50532405_38114)

<a id="50532405_14434"></a>
### SetFrame

Sets the window’s size and location.

**Syntax**

```
VARIANT_BOOL SetFrame(LPDISPATCH iAcroRect);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroRect | The `LPDISPATCH` for an `AcroExch.Rect` specifying the window frame. `iAcroRect's` instance variable `m_lpDispatch` contains this `LPDISPATCH`. |

**Returns**

Always returns `-1`.

**Related methods**

- `AVDoc.` [GetFrame](IAC_API_OLE_Objects.md#50532405_28538)

<a id="50532405_34749"></a>
### SetTextSelection

Sets the document’s selection to the specified text selection. Before calling this method, use one of the following to create the text selection:

- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819) : Creates from a rectangle.
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822) : Creates from a list of character offsets and counts.
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477) : Creates from a list of word offsets and counts.

After calling this method, use `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147) to show the selection.

**Syntax**

```
VARIANT_BOOL SetTextSelection(LPDISPATCH iAcroPDTextSelect);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroPDTextSelect | The `LPDISPATCH` for the text selection to use. `iAcroPDTextSelect` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

Returns `-1` if successful . Returns `0` if no document is open or the `LPDISPATCH` is not a `PDTextSelect` object.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_26583)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_28000"></a>
### SetTitle

Sets the window’s title.

**Syntax**

```
VARIANT_BOOL SetTitle(BSTR szTitle);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szTitle | The title to be set. This method cannot be used for document windows, but only for windows created by Plugins. |

**Returns**

Returns `0` if no document is open, `-1` otherwise.

**Related methods**

- `AVDoc.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)
- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_37022"></a>
### SetViewMode

Sets the mode in which the document will be viewed (pages only, pages and thumbnails, or pages and bookmarks).

**Syntax**

```
VARIANT_BOOL SetViewMode(long nType);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nType | The view mode to be set. Possible values:  `PDDontCare`: `0`: leave the view mode as it is  `PDUseNone`: `1`: display without bookmarks or thumbnails  `PDUseThumbs`: `2`: display using thumbnails  `PDUseBookmarks`: `3`: display using bookmarks  .. note::  Do not set the view mode to `Close` with `AVDoc.SetViewMode` when using `AVDoc.OpenInWindowEx` ; this will cause the viewer and application to hang. |

**Returns**

`0` if an error occurred while setting the view mode or if no document was open, `-1` otherwise.

**Related methods**

- `AVDoc.` [GetAVPageView](IAC_API_OLE_Objects.md#50532405_35375)
- `AVDoc.` [GetViewMode](IAC_API_OLE_Objects.md#50532405_29291)

<a id="50532405_27147"></a>
### ShowTextSelect

Changes the view so that the current text selection is visible.

**Syntax**

```
VARIANT_BOOL ShowTextSelect();
```

**Returns**

Returns `0` if no document is open, `-1` otherwise.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_15686)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_13484"></a>
## AcroExch.AVPageView

The area of the Acrobat application’s window that displays the contents of a document’s page. This is a non-creatable interface. Every `AVDoc` object has an `AVPageView` object and vice versa. The object provides access to the `PDDoc` and `PDPage` objects for the document being displayed.

### Methods

The `AVPageView` object has the following methods.

| Method | Description |
| --- | --- |
| [DevicePointToPage](IAC_API_OLE_Objects.md#50532405_34128) | Converts the coordinates of a point from device space to user space. |
| [DoGoBack](IAC_API_OLE_Objects.md#50532405_27205) | Goes to the previous view on the view history stack, if any. |
| [DoGoForward](IAC_API_OLE_Objects.md#50532405_15639) | Goes to the next view on the view history stack, if any. |
| [GetAperture](IAC_API_OLE_Objects.md#50532405_17623) | Gets the aperture of the specified page view. |
| [GetAVDoc](IAC_API_OLE_Objects.md#50532405_35267) | Gets the `AcroExch.AVDoc` associated with the current page. |
| [GetDoc](IAC_API_OLE_Objects.md#50532405_11484) | Gets the `AcroExch.PDDoc` corresponding to the current page. |
| [GetPage](IAC_API_OLE_Objects.md#50532405_11673) | Gets the `AcroExch.PDPage` corresponding to the current page. |
| [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046) | Gets the page number of the current page. |
| [GetZoom](IAC_API_OLE_Objects.md#50532405_27016) | Gets the current zoom factor, specified as a percent. |
| [GetZoomType](IAC_API_OLE_Objects.md#50532405_24520) | Gets the current zoom type. |
| [Goto](IAC_API_OLE_Objects.md#50532405_19981) | Goes to the specified page. |
| [PointToDevice](IAC_API_OLE_Objects.md#50532405_19347) | Deprecated. Converts the coordinates of a point from user space to device space. |
| [ReadPageDown](IAC_API_OLE_Objects.md#50532405_20099) | Scrolls forward through the document by one screen area. |
| [ReadPageUp](IAC_API_OLE_Objects.md#50532405_41587) | Scrolls backward through the document by one screen area. |
| [ScrollTo](IAC_API_OLE_Objects.md#50532405_28175) | Scrolls to the specified location on the current page. |
| [ZoomTo](IAC_API_OLE_Objects.md#50532405_19513) | Zooms to the specified magnification. |

<a id="50532405_34128"></a>
### DevicePointToPage

Converts the coordinates of a point from device space to user space.

**Syntax**

```
LPDISPATCH DevicePointToPage(LPDISPATCH iAcroPoint);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroPoint | The `LPDISPATCH` for the `AcroExch.Point` whose coordinates are converted. `iAcroPoint` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

The `LPDISPATCH` for an `AcroExch.Point` containing the converted coordinates.

**Related methods**

- `AVPageView.` [PointToDevice](IAC_API_OLE_Objects.md#50532405_19347)

<a id="50532405_27205"></a>
### DoGoBack

Goes to the previous view on the view history stack, if any.

**Syntax**

```
VARIANT_BOOL DoGoBack();
```

**Returns**

Always returns `-1`.

**Related methods**

- `AVPageView.` [DoGoForward](IAC_API_OLE_Objects.md#50532405_15639)

<a id="50532405_15639"></a>
### DoGoForward

Goes to the next view on the view history stack, if any.

**Syntax**

```
VARIANT_BOOL DoGoForward();
```

**Returns**

Always returns `-1`.

**Related methods**

- `AVPageView.` [DoGoBack](IAC_API_OLE_Objects.md#50532405_27205)

<a id="50532405_17623"></a>
### GetAperture

Gets the aperture of the specified page view. The aperture is the rectangular region of the window in which the document is drawn, measured in device space units.

**Syntax**

```
CAcroRect* GetAperture();
```

**Returns**

A pointer to the aperture rectangle. Its coordinates are specified in device space.

**Related methods**

- `AVDoc.` [GetAVPageView](IAC_API_OLE_Objects.md#50532405_35375)
- `AVPageView.` [GetAVDoc](IAC_API_OLE_Objects.md#50532405_26359)
- `AVPageView.` [GetDoc](IAC_API_OLE_Objects.md#50532405_11484)
- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_11673)
- `AVPageView.` [GetZoomType](IAC_API_OLE_Objects.md#50532405_24520)

<a id="50532405_35267"></a>
### GetAVDoc

Gets the `AcroExch.AVDoc` associated with the current page.

**Syntax**

```
LPDISPATCH GetAVDoc();
```

**Returns**

The `LPDISPATCH` for the `AcroExch.AVDoc`.

**Related methods**

- `AVDoc.` [GetAVPageView](IAC_API_OLE_Objects.md#50532405_35375)
- `AVDoc.` [GetPDDoc](IAC_API_OLE_Objects.md#50532405_25013)
- `AVPageView.` [GetDoc](IAC_API_OLE_Objects.md#50532405_11484)

<a id="50532405_11484"></a>
### GetDoc

Gets the `AcroExch.PDDoc` corresponding to the current page.

**Syntax**

```
LPDISPATCH GetDoc();
```

**Returns**

The `LPDISPATCH` for the `AcroExch.PDDoc`.

**Related methods**

- `AVDoc.` [GetAVPageView](IAC_API_OLE_Objects.md#50532405_35375)
- `AVDoc.` [GetPDDoc](IAC_API_OLE_Objects.md#50532405_25013)
- `AVPageView.` [GetAVDoc](IAC_API_OLE_Objects.md#50532405_26359)

<a id="50532405_11673"></a>
### GetPage

Gets the `AcroExch.PDPage` corresponding to the current page.

**Syntax**

```
LPDISPATCH GetPage();
```

**Returns**

The `LPDISPATCH` for the `AcroExch.PDPage`.

**Related methods**

- `AVPageView.` [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046)
- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDPage.` [GetDoc](IAC_API_OLE_Objects.md#50532405_11484)
- `PDPage.` [GetNumber](IAC_API_OLE_Objects.md#50532405_32146)
- `PDPage.` [GetRotate](IAC_API_OLE_Objects.md#50532405_14436)
- `PDPage.` [GetSize](IAC_API_OLE_Objects.md#50532405_37312)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_11673)

<a id="50532405_19046"></a>
### GetPageNum

Gets the page number of the current page. The first page in a document is page zero.

**Syntax**

```
long GetPageNum();
```

**Returns**

The current page’s page number.

**Related methods**

- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_11673)
- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDPage.` [GetDoc](IAC_API_OLE_Objects.md#50532405_40890)
- `PDPage.` [GetNumber](IAC_API_OLE_Objects.md#50532405_32146)
- `PDPage.` [GetRotate](IAC_API_OLE_Objects.md#50532405_14436)
- `PDPage.` [GetSize](IAC_API_OLE_Objects.md#50532405_37312)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_11673)

<a id="50532405_27016"></a>
### GetZoom

Gets the current zoom factor, specified as a percent. For example, 100 is returned if the magnification is 1.0.

**Syntax**

```
long GetZoom();
```

**Returns**

The current zoom factor.

**Related methods**

- `App.` [GetPreference](IAC_API_OLE_Objects.md#50532405_36273)
- `AVPageView.` [GetZoomType](IAC_API_OLE_Objects.md#50532405_24520)
- `AVPageView.` [ZoomTo](IAC_API_OLE_Objects.md#50532405_19513)

<a id="50532405_24520"></a>
### GetZoomType

Gets the current zoom type.

**Syntax**

```
short GetZoomType();
```

**Returns**

Zoom type. The value is one of the following:

- `AVZoomFitHeight`: Fits the page’s height in the window.
- `AVZoomFitPage`: Fits the page in the window.
- `AVZoomFitVisibleWidth`: Fits the page’s visible content into the window.
- `AVZoomFitWidth`: Fits the page’s width into the window.
- `AVZoomNoVary`: A fixed zoom, such as 100%.

**Related methods**

- `App.` [GetPreference](IAC_API_OLE_Objects.md#50532405_36273)
- `AVPageView.` [GetZoomType](IAC_API_OLE_Objects.md#50532405_24520)
- `AVPageView.` [ZoomTo](IAC_API_OLE_Objects.md#50532405_19513)

<a id="50532405_19981"></a>
### Goto

Goes to the specified page.

**Syntax**

```
VARIANT_BOOL GoTo(long nPage);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nPage | Page number of the destination page. The first page in a `PDDoc` object is page `0`. |

**Returns**

`-1` if the Acrobat application successfully went to the page, `0` otherwise.

**Related methods**

- `AVPageView.` [DoGoBack](IAC_API_OLE_Objects.md#50532405_27205)
- `AVPageView.` [DoGoForward](IAC_API_OLE_Objects.md#50532405_15639)
- `AVPageView.` [ReadPageDown](IAC_API_OLE_Objects.md#50532405_20099)
- `AVPageView.` [ReadPageUp](IAC_API_OLE_Objects.md#50532405_41587)
- `AVPageView.` [ScrollTo](IAC_API_OLE_Objects.md#50532405_28175)
- `AVPageView.` [ZoomTo](IAC_API_OLE_Objects.md#50532405_19513)

<a id="50532405_19347"></a>
### PointToDevice

Converts the coordinates of a point from user space to device space.

> **Note**
>
> Deprecated. Do not use this method.

**Syntax**

```
LPDISPATCH PointToDevice(LPDISPATCH iAcroPoint);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroPoint | The `LPDISPATCH` for the `AcroExch.Point` whose coordinates are converted. `iAcroPoint` contains the instance variable `m_lpDispatch`, which contains this `LPDISPATCH`. |

**Returns**

The `LPDISPATCH` for an `AcroExch.Point` containing the converted coordinates.

**Related methods**

- `AVPageView.` [DevicePointToPage](IAC_API_OLE_Objects.md#50532405_34128)

<a id="50532405_20099"></a>
### ReadPageDown

Scrolls forward through the document by one screen area.

**Syntax**

```
VARIANT_BOOL ReadPageDown();
```

**Returns**

Always returns `-1`.

**Related methods**

- `AVPageView.` [DoGoBack](IAC_API_OLE_Objects.md#50532405_27205)
- `AVPageView.` [DoGoForward](IAC_API_OLE_Objects.md#50532405_15639)
- `AVPageView.` [Goto](IAC_API_OLE_Objects.md#50532405_19981)
- `AVPageView.` [ReadPageUp](IAC_API_OLE_Objects.md#50532405_41587)
- `AVPageView.` [ScrollTo](IAC_API_OLE_Objects.md#50532405_28175)
- `AVPageView.` [ZoomTo](IAC_API_OLE_Objects.md#50532405_19513)

<a id="50532405_41587"></a>
### ReadPageUp

Scrolls backward through the document by one screen area.

**Syntax**

```
VARIANT_BOOL ReadPageUp();
```

**Returns**

Always returns `-1`.

**Related methods**

- `AVPageView.` [DoGoBack](IAC_API_OLE_Objects.md#50532405_27205)
- `AVPageView.` [DoGoForward](IAC_API_OLE_Objects.md#50532405_15639)
- `AVPageView.` [Goto](IAC_API_OLE_Objects.md#50532405_19981)
- `AVPageView.` [ReadPageDown](IAC_API_OLE_Objects.md#50532405_20099)
- `AVPageView.` [ScrollTo](IAC_API_OLE_Objects.md#50532405_28175)
- `AVPageView.` [ZoomTo](IAC_API_OLE_Objects.md#50532405_19513)

<a id="50532405_28175"></a>
### ScrollTo

Scrolls to the specified location on the current page.

**Syntax**

```
VARIANT_BOOL ScrollTo(short nX, short nY);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nX | The x–coordinate of the destination. |
| nY | The y–coordinate of the destination. |

**Returns**

`-1` if the Acrobat application successfully scrolled to the specified location, `0` otherwise.

**Related methods**

- `AVPageView.` [DoGoBack](IAC_API_OLE_Objects.md#50532405_27205)
- `AVPageView.` [DoGoForward](IAC_API_OLE_Objects.md#50532405_15639)
- `AVPageView.` [Goto](IAC_API_OLE_Objects.md#50532405_19981)
- `AVPageView.` [ReadPageDown](IAC_API_OLE_Objects.md#50532405_20099)
- `AVPageView.` [ReadPageUp](IAC_API_OLE_Objects.md#50532405_41587)
- `AVPageView.` [ZoomTo](IAC_API_OLE_Objects.md#50532405_19513)

<a id="50532405_19513"></a>
### ZoomTo

Zooms to the specified magnification.

**Syntax**

```
VARIANT_BOOL ZoomTo(short nType, short nScale);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nType | Zoom type. Possible values are:  `AVZoomFitHeight`: Fits the page’s height into the window.  `AVZoomFitPage`: Fits the page into the window.  `AVZoomFitVisibleWidth`: Fits the page’s visible content into the window.  `AVZoomFitWidth`: Fits the page’s width into the window.  `AVZoomNoVary`: A fixed zoom, such as 100%. |
| nScale | The desired zoom factor, expressed as a percentage. For example, 100 is a magnification of 1.0. |

**Returns**

`-1` if the magnification was set successfully, `0` otherwise.

**Related methods**

- `AVPageView.` [GetZoomType](IAC_API_OLE_Objects.md#50532405_24520)
- `AVPageView.` [Goto](IAC_API_OLE_Objects.md#50532405_19981)
- `AVPageView.` [ScrollTo](IAC_API_OLE_Objects.md#50532405_28175)

<a id="50532405_39171"></a>
## AcroExch.HiliteList

A highlighted region of text in a PDF document, which may include one or more contiguous groups of characters or words on a single page. This is a creatable interface. This object has a single method, `Add`, and is used by the `PDPage` object to create `PDTextSelect` objects.

<a id="50532405_30712"></a>
### Add

Adds the highlight specified by `nOffset` and `nLength` to the current highlight list. Highlight lists are used to highlight one or more contiguous groups of characters or words on a single page.

Highlight lists are used both for character-based and word-based highlighting, although a single highlight list cannot contain a mixture of character and word highlights. After creating a highlight list, use `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822) or `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477) (depending on whether the highlight list is used for characters or words) to create a text selection from the highlight list.

**Syntax**

```
VARIANT_BOOL Add(short nOffset, short nLength);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nOffset | Offset of the first word or character to be highlighted, the first of which has an offset of zero. |
| nLength | The number of consecutive words or characters to be highlighted. |

**Returns**

Always returns `-1`.

**Related methods**

- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)

<a id="50532405_42349"></a>
## AcroExch.PDAnnot

An annotation on a page in a PDF file. This is a non-creatable interface. Acrobat applications have two built-in annotation types: `PDTextAnnot` and `PDLinkAnnot`. The object provides access to the physical attributes of the annotation. Plugins may add movie and Widget (form field) annotations, and developers can define new annotation subtypes by creating new annotation handlers.

### Methods

The `PDAnnot` object has the following methods.

| Method | Description |
| --- | --- |
| [GetColor](IAC_API_OLE_Objects.md#50532405_37589) | Gets an annotation’s color. |
| [GetContents](IAC_API_OLE_Objects.md#50532405_16450) | Gets a text annotation’s contents. |
| [GetDate](IAC_API_OLE_Objects.md#50532405_41515) | Gets an annotation’s date. |
| [GetRect](IAC_API_OLE_Objects.md#50532405_19800) | Gets an annotation’s bounding rectangle. |
| [GetSubtype](IAC_API_OLE_Objects.md#50532405_17093) | Gets an annotation’s subtype. |
| [GetTitle](IAC_API_OLE_Objects.md#50532405_14780) | Gets a text annotation’s title. |
| [IsEqual](IAC_API_OLE_Objects.md#50532405_41878) | Determines whether an annotation is the same as the specified annotation. |
| [IsOpen](IAC_API_OLE_Objects.md#50532405_24800) | Tests whether a text annotation is open. |
| [IsValid](IAC_API_OLE_Objects.md#50532405_21326) | Tests whether an annotation is still valid. |
| [Perform](IAC_API_OLE_Objects.md#50532405_37155) | Performs a link annotation’s action. |
| [SetColor](IAC_API_OLE_Objects.md#50532405_39464) | Sets an annotation’s color. |
| [SetContents](IAC_API_OLE_Objects.md#50532405_22402) | Sets a text annotation’s contents. |
| [SetDate](IAC_API_OLE_Objects.md#50532405_40644) | Sets an annotation’s date. |
| [SetOpen](IAC_API_OLE_Objects.md#50532405_27381) | Opens or closes a text annotation. |
| [SetRect](IAC_API_OLE_Objects.md#50532405_16563) | Sets an annotation’s bounding rectangle. |
| [SetTitle](IAC_API_OLE_Objects.md#50532405_37671) | Sets a text annotation’s title. |

<a id="50532405_37589"></a>
### GetColor

Gets an annotation’s color.

**Syntax**

```
long GetColor();
```

**Returns**

The annotation’s color, a long value of the form 0x00BBGGRR where the first byte from the right (RR) is a relative value for red, the second byte (GG) is a relative value for green, and the third byte (BB) is a relative value for blue. The high-order byte must be `0`.

**Related methods**

- `PDAnnot.` [SetColor](IAC_API_OLE_Objects.md#50532405_39464)

<a id="50532405_16450"></a>
### GetContents

Gets a text annotation’s contents.

**Syntax**

```
BSTR GetContents();
```

**Returns**

The annotation’s contents.

**Related methods**

- `PDAnnot.` [SetContents](IAC_API_OLE_Objects.md#50532405_22402)
- `PDAnnot.` [GetDate](IAC_API_OLE_Objects.md#50532405_41515)
- `PDAnnot.` [GetRect](IAC_API_OLE_Objects.md#50532405_19800)
- `PDAnnot.` [GetSubtype](IAC_API_OLE_Objects.md#50532405_17093)
- `PDAnnot.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)

<a id="50532405_41515"></a>
### GetDate

Gets an annotation’s date.

**Syntax**

```
LPDISPATCH GetDate();
```

**Returns**

The `LPDISPATCH` for an `AcroExch.Time` object containing the date.

**Related methods**

- `PDAnnot.` [GetContents](IAC_API_OLE_Objects.md#50532405_16450)
- `PDAnnot.` [GetRect](IAC_API_OLE_Objects.md#50532405_19800)
- `PDAnnot.` [GetSubtype](IAC_API_OLE_Objects.md#50532405_17093)
- `PDAnnot.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)
- `PDAnnot.` [SetDate](IAC_API_OLE_Objects.md#50532405_40644)

<a id="50532405_19800"></a>
### GetRect

Gets an annotation’s bounding rectangle.

**Syntax**

```
LPDISPATCH GetRect();
```

**Returns**

The `LPDISPATCH` for an `AcroExch.Rect` containing the annotation’s bounding rectangle.

**Related methods**

- `PDAnnot.` [GetContents](IAC_API_OLE_Objects.md#50532405_16450)
- `PDAnnot.` [GetDate](IAC_API_OLE_Objects.md#50532405_41515)
- `PDAnnot.` [GetSubtype](IAC_API_OLE_Objects.md#50532405_17093)
- `PDAnnot.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)
- `PDAnnot.` [SetRect](IAC_API_OLE_Objects.md#50532405_16563)

<a id="50532405_17093"></a>
### GetSubtype

Gets an annotation’s subtype.

**Syntax**

```
BSTR GetSubtype();
```

**Returns**

The annotation’s subtype. The built-in subtypes are Text and Link.

**Related methods**

- `PDAnnot.` [GetContents](IAC_API_OLE_Objects.md#50532405_16450)
- `PDAnnot.` [GetDate](IAC_API_OLE_Objects.md#50532405_41515)
- `PDAnnot.` [GetRect](IAC_API_OLE_Objects.md#50532405_19800)
- `PDAnnot.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)

<a id="50532405_14780"></a>
### GetTitle

Gets a text annotation’s title.

**Syntax**

```
BSTR GetTitle();
```

**Returns**

The annotation’s title.

**Related methods**

- `PDAnnot.` [GetContents](IAC_API_OLE_Objects.md#50532405_16450)
- `PDAnnot.` [GetDate](IAC_API_OLE_Objects.md#50532405_41515)
- `PDAnnot.` [GetRect](IAC_API_OLE_Objects.md#50532405_19800)
- `PDAnnot.` [GetSubtype](IAC_API_OLE_Objects.md#50532405_17093)
- `PDAnnot.` [SetTitle](IAC_API_OLE_Objects.md#50532405_37671)

<a id="50532405_41878"></a>
### IsEqual

Determines whether an annotation is the same as the specified annotation.

**Syntax**

```
VARIANT_BOOL IsEqual(LPDISPATCH PDAnnot);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| PDAnnot | The `LPDISPATCH` for the `AcroExch.PDAnnot` to be tested. `PDAnnot` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

`-1` if the annotations are the same, `0` otherwise.

**Related methods**

- `PDAnnot.` [GetContents](IAC_API_OLE_Objects.md#50532405_16450)
- `PDAnnot.` [GetDate](IAC_API_OLE_Objects.md#50532405_41515)
- `PDAnnot.` [GetRect](IAC_API_OLE_Objects.md#50532405_19800)
- `PDAnnot.` [GetSubtype](IAC_API_OLE_Objects.md#50532405_17093)
- `PDAnnot.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)
- `PDAnnot.` [IsOpen](IAC_API_OLE_Objects.md#50532405_24800)
- `PDAnnot.` [IsValid](IAC_API_OLE_Objects.md#50532405_21326)

<a id="50532405_24800"></a>
### IsOpen

Tests whether a text annotation is open.

**Syntax**

```
VARIANT_BOOL IsOpen();
```

**Returns**

`-1` if open, `0` otherwise.

**Related methods**

- `PDAnnot.` [GetContents](IAC_API_OLE_Objects.md#50532405_16450)
- `PDAnnot.` [GetDate](IAC_API_OLE_Objects.md#50532405_41515)
- `PDAnnot.` [GetRect](IAC_API_OLE_Objects.md#50532405_19800)
- `PDAnnot.` [GetSubtype](IAC_API_OLE_Objects.md#50532405_17093)
- `PDAnnot.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)
- `PDAnnot.` [IsEqual](IAC_API_OLE_Objects.md#50532405_41878)
- `PDAnnot.` [IsValid](IAC_API_OLE_Objects.md#50532405_21326)
- `PDAnnot.` [SetOpen](IAC_API_OLE_Objects.md#50532405_27381)

<a id="50532405_21326"></a>
### IsValid

Tests whether an annotation is still valid. This method is intended only to test whether the annotation has been deleted, not whether it is a completely valid annotation object.

**Syntax**

```
VARIANT_BOOL IsValid();
```

**Returns**

`-1` if the annotation is valid, `0` otherwise.

**Related methods**

- `PDAnnot.` [GetContents](IAC_API_OLE_Objects.md#50532405_16450)
- `PDAnnot.` [GetDate](IAC_API_OLE_Objects.md#50532405_41515)
- `PDAnnot.` [GetRect](IAC_API_OLE_Objects.md#50532405_19800)
- `PDAnnot.` [GetSubtype](IAC_API_OLE_Objects.md#50532405_17093)
- `PDAnnot.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)
- `PDAnnot.` [IsEqual](IAC_API_OLE_Objects.md#50532405_41878)
- `PDAnnot.` [IsOpen](IAC_API_OLE_Objects.md#50532405_24800)

<a id="50532405_37155"></a>
### Perform

Performs a link annotation’s action.

**Syntax**

```
VARIANT_BOOL Perform(LPDISPATCH iAcroAVDoc);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroAVDoc | The `LPDISPATCH` for the `AcroExch.AVDoc` in which the annotation is located. `iAcroAVDoc` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

`-1` if the action was executed successfully, `0` otherwise.

**Related methods**

- `PDAnnot.` [IsValid](IAC_API_OLE_Objects.md#50532405_21326)

<a id="50532405_39464"></a>
### SetColor

Sets an annotation’s color.

**Syntax**

```
VARIANT_BOOL SetColor(long nRGBColor);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nRGBColor | The color to use for the annotation. |

**Returns**

`-1` if the annotation’s color was set, `0` if the Acrobat application does not support editing.

`nRGBColor` is a long value with the form 0x00BBGGRR where the first byte from the right (RR) is a relative value for red, the second byte (GG) is a relative value for green, and the third byte (BB) is a relative value for blue. The high-order byte must be `0`.

**Related methods**

- `PDAnnot.` [GetColor](IAC_API_OLE_Objects.md#50532405_37589)
- `PDAnnot.` [SetContents](IAC_API_OLE_Objects.md#50532405_22402)
- `PDAnnot.` [SetDate](IAC_API_OLE_Objects.md#50532405_40644)
- `PDAnnot.` [SetOpen](IAC_API_OLE_Objects.md#50532405_27381)
- `PDAnnot.` [SetRect](IAC_API_OLE_Objects.md#50532405_16563)
- `PDAnnot.` [SetTitle](IAC_API_OLE_Objects.md#50532405_37671)

<a id="50532405_22402"></a>
### SetContents

Sets a text annotation’s contents.

**Syntax**

```
VARIANT_BOOL SetContents(BSTR szContents);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szContents | The contents to use for the annotation. |

**Returns**

`0` if the Acrobat application does not support editing, `-1` otherwise.

**Related methods**

- `PDAnnot.` [GetContents](IAC_API_OLE_Objects.md#50532405_16450)
- `PDAnnot.` [SetColor](IAC_API_OLE_Objects.md#50532405_39464)
- `PDAnnot.` [SetDate](IAC_API_OLE_Objects.md#50532405_40644)
- `PDAnnot.` [SetOpen](IAC_API_OLE_Objects.md#50532405_27381)
- `PDAnnot.` [SetRect](IAC_API_OLE_Objects.md#50532405_16563)
- `PDAnnot.` [SetTitle](IAC_API_OLE_Objects.md#50532405_16583)

<a id="50532405_40644"></a>
### SetDate

Sets an annotation’s date.

**Syntax**

```
VARIANT_BOOL SetDate(LPDISPATCH iAcroTime);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroTime | The `LPDISPATCH` for the date and time to use for the annotation. `iAcroTime's` instance variable `m_lpDispatch` contains this `LPDISPATCH`. |

**Returns**

`-1` if the date was set, `0` if the Acrobat application does not support editing.

**Related methods**

- `PDAnnot.` [GetTitle](IAC_API_OLE_Objects.md#50532405_15243)
- `PDAnnot.` [SetColor](IAC_API_OLE_Objects.md#50532405_39464)
- `PDAnnot.` [SetContents](IAC_API_OLE_Objects.md#50532405_22402)
- `PDAnnot.` [SetOpen](IAC_API_OLE_Objects.md#50532405_27381)
- `PDAnnot.` [SetRect](IAC_API_OLE_Objects.md#50532405_16563)
- `PDAnnot.` [SetTitle](IAC_API_OLE_Objects.md#50532405_16583)

<a id="50532405_27381"></a>
### SetOpen

Opens or closes a text annotation.

**Syntax**

```
VARIANT_BOOL SetOpen(long bIsOpen);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bIsOpen | If a positive number, the annotation is open. If `0`, the annotation is closed. |

**Returns**

Always returns `-1`.

**Related methods**

- `PDAnnot.` [IsOpen](IAC_API_OLE_Objects.md#50532405_24800)
- `PDAnnot.` [SetColor](IAC_API_OLE_Objects.md#50532405_39464)
- `PDAnnot.` [SetContents](IAC_API_OLE_Objects.md#50532405_22402)
- `PDAnnot.` [SetDate](IAC_API_OLE_Objects.md#50532405_40644)
- `PDAnnot.` [SetRect](IAC_API_OLE_Objects.md#50532405_16563)
- `PDAnnot.` [SetTitle](IAC_API_OLE_Objects.md#50532405_16583)

<a id="50532405_16563"></a>
### SetRect

Sets an annotation’s bounding rectangle.

**Syntax**

```
VARIANT_BOOL SetRect(LPDISPATCH iAcroRect);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroRect | The `LPDISPATCH` for the bounding rectangle (`AcroExch.Rect`) to set. `iAcroRect` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

`-1` if a rectangle was supplied, `0` otherwise.

**Related methods**

- `PDAnnot.` [GetRect](IAC_API_OLE_Objects.md#50532405_19800)
- `PDAnnot.` [SetColor](IAC_API_OLE_Objects.md#50532405_39464)
- `PDAnnot.` [SetContents](IAC_API_OLE_Objects.md#50532405_22402)
- `PDAnnot.` [SetDate](IAC_API_OLE_Objects.md#50532405_40644)
- `PDAnnot.` [SetOpen](IAC_API_OLE_Objects.md#50532405_27381)
- `PDAnnot.` [SetTitle](IAC_API_OLE_Objects.md#50532405_37671)

<a id="50532405_37671"></a>
### SetTitle

Sets a text annotation’s title.

**Syntax**

```
VARIANT_BOOL SetTitle(BSTR szTitle);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szTitle | The title to use. |

**Returns**

`-1` if the title was set, `0` if the Acrobat application does not support editing.

**Related methods**

- `PDAnnot.` [GetByTitle](IAC_API_OLE_Objects.md#50532405_32270)
- `PDAnnot.` [SetColor](IAC_API_OLE_Objects.md#50532405_39464)
- `PDAnnot.` [SetContents](IAC_API_OLE_Objects.md#50532405_22402)
- `PDAnnot.` [SetDate](IAC_API_OLE_Objects.md#50532405_40644)
- `PDAnnot.` [SetOpen](IAC_API_OLE_Objects.md#50532405_27381)
- `PDAnnot.` [SetRect](IAC_API_OLE_Objects.md#50532405_16563)

<a id="50532405_29095"></a>
## AcroExch.PDBookmark

A bookmark for a page in a PDF file. This is a creatable interface. Each bookmark has a title that appears on screen, and an action that specifies what happens when a user clicks on the bookmark.

Bookmarks can either be created interactively by the user through the Acrobat application’s user interface or programmatically generated. The typical action for a user-created bookmark is to move to another location in the current document, although any action can be specified. It is not possible to create a bookmark with OLE—only to destroy one.

### Methods

The `PDBookmark` object has the following methods.

| Method | Description |
| --- | --- |
| [Destroy](IAC_API_OLE_Objects.md#50532405_26583) | Destroys a bookmark. |
| [GetByTitle](IAC_API_OLE_Objects.md#50532405_32270) | Gets the bookmark that has the specified title. |
| [GetTitle](IAC_API_OLE_Objects.md#50532405_15243) | Gets a bookmark’s title. |
| [IsValid](IAC_API_OLE_Objects.md#50532405_11084) | Determines whether the bookmark is valid. |
| [Perform](IAC_API_OLE_Objects.md#50532405_22695) | Performs a bookmark’s action. |
| [SetTitle](IAC_API_OLE_Objects.md#50532405_16583) | Sets a bookmark’s title. |

<a id="50532405_26583"></a>
### Destroy

Destroys a bookmark.

**Syntax**

```
VARIANT_BOOL Destroy();
```

**Returns**

`0` if the Acrobat application does not support editing (making it impossible to delete the bookmark), `-1` otherwise.

**Related methods**

- `PDBookmark.` [IsValid](IAC_API_OLE_Objects.md#50532405_11084)

<a id="50532405_32270"></a>
### GetByTitle

Gets the bookmark that has the specified title. The `AcroExch.PDBookmark` object is set to the specified bookmark as a side effect of the method; it is not the method’s return value. You cannot enumerate bookmark titles with this method.

**Syntax**

```
VARIANT_BOOL GetByTitle(LPDISPATCH iAcroPDDoc,
                 BSTR bookmarkTitle);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroPDDoc | The `LPDISPATCH` for the document (`AcroExch.PDDoc` object) containing the bookmark. `iAcroPDDoc` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |
| bookmarkTitle | The title of the bookmark to get. The capitalization of the title must match that in the bookmark. |

**Returns**

- `-1` if the specified bookmark exists (the method determines this using the `PDBookmark.` [IsValid](IAC_API_OLE_Objects.md#50532405_11084) method), `0` otherwise.

**Related methods**

- `PDBookmark.` [GetTitle](IAC_API_OLE_Objects.md#50532405_15243)
- `PDBookmark.` [SetTitle](IAC_API_OLE_Objects.md#50532405_16583)

**Example**

```
CAcroPDBookmark* bookmark = new CAcroPDBookmark;

bookmark->CreateDispatch("AcroExch.PDBookmark");

bookmark->GetByTitle(m_pAcroAVDoc->GetPDDoc(), "Name of Bookmark");

if (bookmark->IsValid())
    bookmark->Perform(m_pAcroAVDoc->m_lpDispatch);
else
    AfxMessageBox("Bookmark not valid");
```

<a id="50532405_15243"></a>
### GetTitle

Gets a bookmark’s title.

**Syntax**

```
BSTR GetTitle();
```

**Returns**

The title.

**Related methods**

- `PDBookmark.` [GetByTitle](IAC_API_OLE_Objects.md#50532405_32270)
- `PDBookmark.` [SetTitle](IAC_API_OLE_Objects.md#50532405_16583)

<a id="50532405_11084"></a>
### IsValid

Determines whether the bookmark is valid. This method only checks whether the bookmark has been deleted; it does not thoroughly check the bookmark’s data structures.

**Syntax**

```
VARIANT_BOOL IsValid();
```

**Returns**

`-1` if the bookmark is valid, `0` otherwise.

**Related methods**

- `PDBookmark.` [Destroy](IAC_API_OLE_Objects.md#50532405_26583)

**Syntax**

<a id="50532405_22695"></a>
### Perform

Performs a bookmark’s action.

**Syntax**

```
VARIANT_BOOL Perform(LPDISPATCH iAcroAVDoc);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroAVDoc | The `LPDISPATCH` for the `AcroExch.AVDoc` in which the bookmark is located. `iAcroAVDoc` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

`-1` if the action was executed successfully, `0` otherwise.

**Related methods**

- `PDBookmark.` [IsValid](IAC_API_OLE_Objects.md#50532405_42634)

<a id="50532405_16583"></a>
### SetTitle

Sets a bookmark’s title.

**Syntax**

```
VARIANT_BOOL SetTitle(BSTR szNewTitle);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szNewTitle | The title to set. |

**Returns**

`0` if the Acrobat application does not support editing, `-1` otherwise.

**Related methods**

- `PDBookmark.` [GetByTitle](IAC_API_OLE_Objects.md#50532405_32270)
- `PDBookmark.` [GetTitle](IAC_API_OLE_Objects.md#50532405_15243)

<a id="50532405_34812"></a>
## AcroExch.PDDoc

The underlying PDF representation of a document. This is a creatable interface. There is a correspondence between a `PDDoc` object and an `ASFile` object (an opaque representation of an open file made available through an interface encapsulating Acrobat’s access to file services), and the `PDDoc` object is the hidden object behind every `AVDoc` object. An `ASFile` object may have zero or more underlying files, so a PDF file does not always correspond to a single disk file. For example, an `ASFile` object may provide access to PDF data in a database.

Through `PDDoc` objects, your application can perform most of the Document menu items from Acrobat (delete pages, replace pages, and so on), create and delete thumbnails, and set and retrieve document information fields.

### Methods

The `PDDoc` object has the following methods.

| Method | Description |
| --- | --- |
| [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809) | Acquires the specified page. |
| [ClearFlags](IAC_API_OLE_Objects.md#50532405_39995) | Clears a document’s flags. |
| [Close](IAC_API_OLE_Objects.md#50532405_37346) | Closes a file. |
| [Create](IAC_API_OLE_Objects.md#50532405_58029) | Creates a new `AcroExch.PDDoc`. |
| [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819) | Creates a text selection from the specified rectangle on the specified page. |
| [CreateThumbs](IAC_API_OLE_Objects.md#50532405_27374) | Creates thumbnail images for the specified page range in a document. |
| [CropPages](IAC_API_OLE_Objects.md#50532405_22406) | Crops the pages in a specified range in a document. |
| [DeletePages](IAC_API_OLE_Objects.md#50532405_13365) | Deletes pages from a file. |
| [DeleteThumbs](IAC_API_OLE_Objects.md#50532405_37375) | Deletes thumbnail images from the specified pages in a document. |
| [GetFileName](IAC_API_OLE_Objects.md#50532405_30617) | Gets the name of the file associated with this `AcroExch.PDDoc`. |
| [GetFlags](IAC_API_OLE_Objects.md#50532405_24732) | Gets a document’s flags. |
| [GetInfo](IAC_API_OLE_Objects.md#50532405_19753) | Gets the value of a specified key in the document’s `Info` dictionary. |
| [GetInstanceID](IAC_API_OLE_Objects.md#50532405_27536) | Gets the instance ID (the second element) from the ID array in the document’s trailer. |
| [GetJSObject](IAC_API_OLE_Objects.md#50532405_28442) | Gets a dual interface to the JavaScript object associated with the PDDoc. |
| [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052) | Gets the number of pages in a file. |
| [GetPageMode](IAC_API_OLE_Objects.md#50532405_27507) | Gets a value indicating whether the Acrobat application is currently displaying only pages, pages and thumbnails, or pages and bookmarks. |
| [GetPermanentID](IAC_API_OLE_Objects.md#50532405_36645) | Gets the permanent ID (the first element) from the ID array in the document’s trailer. |
| [InsertPages](IAC_API_OLE_Objects.md#50532405_16929) | Inserts the specified pages from the source document after the indicated page within the current document. |
| [MovePage](IAC_API_OLE_Objects.md#50532405_35068) | Moves a page to another location within the same document. |
| [Open](IAC_API_OLE_Objects.md#50532405_41972) | Opens a file. |
| [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888) | Opens a window and displays the document in it. |
| [ReplacePages](IAC_API_OLE_Objects.md#50532405_40109) | Replaces the indicated pages in the current document with those specified from the source document. |
| [Save](IAC_API_OLE_Objects.md#50532405_28634) | Saves a document. |
| [SetFlags](IAC_API_OLE_Objects.md#50532405_31111) | Sets a document’s flags indicating whether the document has been modified, whether the document is a temporary document and should be deleted when closed, and the version of PDF used in the file. |
| [SetInfo](IAC_API_OLE_Objects.md#50532405_42162) | Sets the value of a key in a document’s `Info` dictionary. |
| [SetPageMode](IAC_API_OLE_Objects.md#50532405_34412) | Sets the page mode in which a document is to be opened: display only pages, pages and thumbnails, or pages and bookmarks. |

<a id="50532405_25809"></a>
### AcquirePage

Acquires the specified page.

**Syntax**

```
LPDISPATCH AcquirePage(long nPage);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nPage | The number of the page to acquire. The first page is page 0. |

**Returns**

The `LPDISPATCH` for the `AcroExch.PDPage` object for the acquired page . Returns `NULL` if the page could not be acquired.

**Related methods**

- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_11673)
- `AVPageView.` [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDPage.` [GetDoc](IAC_API_OLE_Objects.md#50532405_11484)
- `PDPage.` [GetNumber](IAC_API_OLE_Objects.md#50532405_32146)
- `PDPage.` [GetRotate](IAC_API_OLE_Objects.md#50532405_14436)
- `PDPage.` [GetSize](IAC_API_OLE_Objects.md#50532405_37312)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)

<a id="50532405_39995"></a>
### ClearFlags

Clears a document’s flags. The flags indicate whether the document has been modified, whether the document is a temporary document and should be deleted when closed, and the version of PDF used in the file. This method can be used only to clear, not to set, the flag bits.

**Syntax**

```
VARIANT_BOOL ClearFlags(long nFlags);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFlags | Flags to be cleared. See `PDDoc.` [GetFlags](IAC_API_OLE_Objects.md#50532405_24732) for a description of the flags. The flags [PDDocWasRepaired](IAC_API_OLE_Objects.md#50532405_17887) , [PDDocNewMajorVersion](IAC_API_OLE_Objects.md#50532405_41659) , [PDDocNewMinorVersion](IAC_API_OLE_Objects.md#50532405_16605) , and [PDDocOldVersion](IAC_API_OLE_Objects.md#50532405_19653) are read-only and cannot be cleared. |

**Returns**

Always returns `-1`.

**Related methods**

- `PDDoc.` [GetFlags](IAC_API_OLE_Objects.md#50532405_24732)
- `PDDoc.` [SetFlags](IAC_API_OLE_Objects.md#50532405_31111)

<a id="50532405_37346"></a>
### Close

Closes a file.

> **Note**
>
> If `PDDoc` and `AVDoc` are constructed with the same file, `PDDoc.Close` destroys both objects (which closes the document in the viewer).

**Syntax**

```
VARIANT_BOOL Close();
```

**Returns**

`-1` if the document was closed successfully, `0` otherwise.

**Related methods**

- `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231)
- `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575)
- `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014)
- `PDDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_58029"></a>
### Create

Creates a new `AcroExch.PDDoc`.

**Syntax**

```
VARIANT_BOOL Create();
```

**Returns**

`-1` if the document is created successfully, `0` if it is not or if the Acrobat application does not support editing.

<a id="50532405_34819"></a>
### CreateTextSelect

Creates a text selection from the specified rectangle on the specified page. After creating the text selection, use the `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749) method to use it as the document’s selection, and use `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147) to show the selection.

**Syntax**

```
LPDISPATCH CreateTextSelect(long nPage, LPDISPATCH iAcroRect);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nPage | The page on which the selection is created. The first page in a `PDDoc` object is page 0. |
| iAcroRect | The `LPDISPATCH` for the `AcroExch.Rect` enclosing the region to select. `iAcroRect` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

The `LPDISPATCH` for an `AcroExch.PDTextSelect` containing the text selection . Returns `NULL` if the text selection was not created successfully.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_15686)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_27374"></a>
### CreateThumbs

Creates thumbnail images for the specified page range in a document.

**Syntax**

```
VARIANT_BOOL CreateThumbs(long nFirstPage, long nLastPage);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFirstPage | First page for which thumbnail images are created. The first page in a `PDDoc` object is page `0`. |
| nLastPage | Last page for which thumbnail images are created. |

**Returns**

`-1` if thumbnail images were created successfully, `0` if they were not or if the Acrobat application does not support editing.

**Related methods**

- `PDDoc.` [DeleteThumbs](IAC_API_OLE_Objects.md#50532405_37375)

<a id="50532405_22406"></a>
### CropPages

Crops the pages in a specified range in a document. This method ignores the request if either the width or height of the crop box is less than 72 points (one inch).

**Syntax**

```
VARIANT_BOOL CropPages(long nStartPage, long nEndPage,

                 short nEvenOrOddPagesOnly,

                 LPDISPATCH iAcroRect);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nStartPage | First page that is cropped. The first page in a `PDDoc` object is page 0. |
| nEndPage | Last page that is cropped. |
| nEvenOrOddPagesOnly | Value indicating which pages in the range are cropped. Must be one of the following:  `0`: crop all pages in the range  `1`: crop only odd pages in the range  `2`: crop only even pages in the range |
| iAcroRect | An `LPDISPATCH` for a `CAcroRect` specifying the cropping rectangle, which is specified in user space. |

**Returns**

`-1` if the pages were cropped successfully, `0` otherwise.

**Related methods**

- `PDPage.` [CropPages](IAC_API_OLE_Objects.md#50532405_22406)

<a id="50532405_13365"></a>
### DeletePages

Deletes pages from a file.

**Syntax**

```
VARIANT_BOOL DeletePages(long nStartPage, long nEndPage);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nStartPage | The first page to be deleted. The first page in a `PDDoc` object is page `0`. |
| nEndPage | The last page to be deleted. |

**Returns**

`-1` if the pages were successfully deleted . Returns `0` if they were not or if the Acrobat application does not support editing.

**Related methods**

- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDDoc.` [DeletePages](IAC_API_OLE_Objects.md#50532405_13365)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDDoc.` [InsertPages](IAC_API_OLE_Objects.md#50532405_16929)
- `PDDoc.` [MovePage](IAC_API_OLE_Objects.md#50532405_35068)
- `PDDoc.` [ReplacePages](IAC_API_OLE_Objects.md#50532405_40109)

<a id="50532405_37375"></a>
### DeleteThumbs

Deletes thumbnail images from the specified pages in a document.

**Syntax**

```
VARIANT_BOOL DeleteThumbs(long nStartPage, long nEndPage);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nStartPage | First page whose thumbnail image is deleted. The first page in a `PDDoc` object is page `0`. |
| nEndPage | Last page whose thumbnail image is deleted. |

**Returns**

`-1` if the thumbnails were deleted, `0` if they were not deleted or if the Acrobat application does not support editing.

**Related methods**

- `PDDoc.` [CreateThumbs](IAC_API_OLE_Objects.md#50532405_27374)

<a id="50532405_30617"></a>
### GetFileName

Gets the name of the file associated with this `AcroExch.PDDoc`.

**Syntax**

```
BSTR GetFileName();
```

**Returns**

The file name, which can currently contain up to 256 characters.

**Related methods**

- `PDDoc.` [Save](IAC_API_OLE_Objects.md#50532405_28634)

<a id="50532405_24732"></a>
### GetFlags

Gets a document’s flags. The flags indicate whether the document has been modified, whether the document is a temporary document and should be deleted when closed, and the version of PDF used in the file.

**Syntax**

```
long GetFlags();
```

**Returns**

The document’s flags, containing an OR of the following:

| Flag | Description |
| --- | --- |
| PDDocNeedsSave | Document has been modified and needs to be saved. |
| PDDocRequiresFullSave | Document cannot be saved incrementally; it must be written using `PDSaveFull`. |
| PDDocIsModified | Document has been modified slightly (such as bookmarks or text annotations have been opened or closed), but not in a way that warrants saving. |
| PDDocDeleteOnClose | Document is based on a temporary file that must be deleted when the document is closed or saved. |
| PDDocWasRepaired | Document was repaired when it was opened. |
| PDDocNewMajorVersion | Document’s major version is newer than current. |
| PDDocNewMinorVersion | Document’s minor version is newer than current. |
| PDDocOldVersion | Document’s version is older than current. |
| PDDocSuppressErrors | Don’t display errors. |

**Related methods**

- `PDDoc.` [ClearFlags](IAC_API_OLE_Objects.md#50532405_39995)
- `PDDoc.` [SetFlags](IAC_API_OLE_Objects.md#50532405_31111)

<a id="50532405_19753"></a>
### GetInfo

Gets the value of a specified key in the document’s `Info` dictionary. A maximum of 512 bytes are returned.

**Syntax**

```
BSTR GetInfo(BSTR szInfoKey);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szInfoKey | The key whose value is obtained. |

**Returns**

The string if the value was read successfully . Returns an empty string if the key does not exist or its value cannot be read.

**Related methods**

- `PDDoc.` [SetInfo](IAC_API_OLE_Objects.md#50532405_42162)

<a id="50532405_27536"></a>
### GetInstanceID

Gets the instance ID (the second element) from the ID array in the document’s trailer.

**Syntax**

```
BSTR GetInstanceID();
```

**Returns**

A string whose maximum length is 32 characters, containing the document’s instance ID.

**Related methods**

- `PDDoc.` [GetPermanentID](IAC_API_OLE_Objects.md#50532405_36645)

<a id="50532405_28442"></a>
### GetJSObject

Gets a dual interface to the JavaScript object associated with the `PDDoc`. This allows automation clients full access to both built-in and user-defined JavaScript methods available in the document.

**Syntax**

```
LDispatch* GetJSObject();
```

**Returns**

The interface to the JavaScript object if the call succeeded, `NULL` otherwise.

<a id="50532405_30052"></a>
### GetNumPages

Gets the number of pages in a file.

**Syntax**

```
long GetNumPages();
```

**Returns**

The number of pages, or `-1` if the number of pages cannot be determined.

**Related methods**

- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `AVPageView.` [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046)
- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDPage.` [GetNumber](IAC_API_OLE_Objects.md#50532405_32146)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)

<a id="50532405_27507"></a>
### GetPageMode

Gets a value indicating whether the Acrobat application is currently displaying only pages, pages and thumbnails, or pages and bookmarks.

**Syntax**

```
long GetPageMode();
```

**Returns**

The current page mode. Will be one of the following values:

- `PDDontCare`: `0`: leave the view mode as it is
- `PDUseNone`: `1`: display without bookmarks or thumbnails
- `PDUseThumbs`: `2`: display using thumbnails
- `PDUseBookmarks`: `3`: display using bookmarks
- `PDFullScreen`: `4`: display in full screen mode

**Related methods**

- `PDDoc.` [SetPageMode](IAC_API_OLE_Objects.md#50532405_34412)

<a id="50532405_36645"></a>
### GetPermanentID

Gets the permanent ID (the first element) from the ID array in the document’s trailer.

**Syntax**

```
BSTR GetPermanentID();
```

**Returns**

A string whose maximum length is 32 characters, containing the document’s permanent ID.

**Related methods**

- `PDDoc.` [GetInstanceID](IAC_API_OLE_Objects.md#50532405_27536)

<a id="50532405_16929"></a>
### InsertPages

Inserts the specified pages from the source document after the indicated page within the current document.

**Syntax**

```
VARIANT_BOOL InsertPages(long nInsertPageAfter,
                 LPDISPATCH iPDDocSource,long nStartPage,
                 long nNumPages, long bBookmarks);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nInsertPageAfter | The page in the current document after which pages from the source document are inserted. The first page in a `PDDoc` object is page 0. |
| iPDDocSource | The `LPDISPATCH` for the `AcroExch.PDDoc` containing the pages to insert. `iPDDocSource` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |
| nStartPage | The first page in `iPDDocSource` to be inserted into the current document. |
| nNumPages | The number of pages to be inserted. |
| bBookmarks | If a positive number, bookmarks are copied from the source document. If `0`, they are not. |

**Returns**

`-1` if the pages were successfully inserted . Returns `0` if they were not or if the Acrobat application does not support editing.

**Related methods**

- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDDoc.` [DeletePages](IAC_API_OLE_Objects.md#50532405_13365)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDDoc.` [MovePage](IAC_API_OLE_Objects.md#50532405_35068)
- `PDDoc.` [ReplacePages](IAC_API_OLE_Objects.md#50532405_40109)

<a id="50532405_35068"></a>
### MovePage

Moves a page to another location within the same document.

**Syntax**

```
VARIANT_BOOL MovePage(long nMoveAfterThisPage,
                 long nPageToMove);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nMoveAfterThisPage | The page being moved is placed after this page number. The first page in a `PDDoc` object is page `0`. |
| nPageToMove | Page number of the page to be moved. |

**Returns**

`0` if the Acrobat application does not support editing, `-1` otherwise.

**Related methods**

- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDDoc.` [DeletePages](IAC_API_OLE_Objects.md#50532405_13365)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDDoc.` [InsertPages](IAC_API_OLE_Objects.md#50532405_16929)
- `PDDoc.` [ReplacePages](IAC_API_OLE_Objects.md#50532405_40109)

<a id="50532405_41972"></a>
### Open

Opens a file. A new instance of `AcroExch.PDDoc` must be created for each open PDF file.

**Syntax**

```
VARIANT_BOOL Open(BSTR szFullPath);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szFullPath | Full path of the file to be opened. |

**Returns**

`-1` if the document was opened successfully, `0` otherwise.

**Related methods**

- `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231)
- `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575)
- `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014)
- `PDDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `PDDoc.` [OpenAVDoc](IAC_API_OLE_Objects.md#50532405_14888)

<a id="50532405_14888"></a>
### OpenAVDoc

Opens a window and displays the document in it.

**Syntax**

```
LPDISPATCH OpenAVDoc(BSTR szTitle);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szTitle | The title to be used for the window. A default title is used if `szTitle` is `NULL` or an empty string. |

**Returns**

The `LPDISPATCH` for the `AcroExch.AVDoc` that was opened, or `NULL` if the open fails.

**Related methods**

- `App.` [CloseAllDocs](IAC_API_OLE_Objects.md#50532405_33231)
- `AVDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `AVDoc.` [GetTitle](IAC_API_OLE_Objects.md#50532405_14780)
- `AVDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)
- `AVDoc.` [OpenInWindow](IAC_API_OLE_Objects.md#50532405_40575)
- `AVDoc.` [OpenInWindowEx](IAC_API_OLE_Objects.md#50532405_22014)
- `AVDoc.` [SetTitle](IAC_API_OLE_Objects.md#50532405_37671)
- `PDDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907)
- `PDDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963)

<a id="50532405_40109"></a>
### ReplacePages

Replaces the indicated pages in the current document with those specified from the source document. No links or bookmarks are copied from `iPDDocSource`, but text annotations may optionally be copied.

**Syntax**

```
VARIANT_BOOL ReplacePages(long nStartPage,
                 LPDISPATCH iPDDocSource,

                 long nStartSourcePage, long nNumPages,

                 long bMergeTextAnnotations);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nStartPage | The first page within the source file to be replaced. The first page in a `PDDoc` object is page `0`. |
| iPDDocSource | The `LPDISPATCH` for the `AcroExch.PDDoc` containing the new copies of pages that are replaced. `iPDDocSource` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |
| nStartSourcePage | The first page in `iPDDocSource` to use as a replacement page. |
| nNumPages | The number of pages to be replaced. |
| bMergeTextAnnotations | If a positive number, text annotations from `iPDDocSource` are copied. If `0`, they are not. |

**Returns**

`-1` if the pages were successfully replaced . Returns `0` if they were not or if the Acrobat application does not support editing.

**Related methods**

- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDDoc.` [DeletePages](IAC_API_OLE_Objects.md#50532405_13365)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDDoc.` [InsertPages](IAC_API_OLE_Objects.md#50532405_16929)
- `PDDoc.` [MovePage](IAC_API_OLE_Objects.md#50532405_35068)

<a id="50532405_28634"></a>
### Save

Saves a document.

**Syntax**

```
VARIANT_BOOL Save(short nType, BSTR szFullPath);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nType | Specifies the way in which the file should be saved.  `nType` is a logical OR of one or more of the following flags:  `PDSaveIncremental`: Write changes only, not the complete file. This will always result in a larger file, even if objects have been deleted.  `PDSaveFull`: Write the entire file to the filename specified by `szFullPath`.   `PDSaveCopy`: Write a copy of the file into the file specified by `szFullPath`, but keep using the old file. This flag can only be specified if `PDSaveFull` is also used.   `PDSaveCollectGarbage`: Remove unreferenced objects; this often reduces the file size, and its usage is encouraged. This flag can only be specified if `PDSaveFull` is also used.  `PDSaveLinearized`: Save the file optimized for the web, providing hint tables. This allows the PDF file to be byte-served. This flag can only be specified if `PDSaveFull` is also used.  -  If you save a file optimized for the web using the `PDSaveLinearized` flag, you must follow this sequence:  1. Open the PDF file with `PDDoc.` [Open](IAC_API_OLE_Objects.md#50532405_23963).  2. Call `PDDoc.` [Save](IAC_API_OLE_Objects.md#50532405_28634) using the `PDSaveLinearized` flag.  3. Call `PDDoc.` [Close](IAC_API_OLE_Objects.md#50532405_10907).  This allows batch optimization of files. |
| szFullPath | The new path to the file, if any. |

**Returns**

`-1` if the document was successfully saved . Returns `0` if it was not or if the Acrobat application does not support editing.

**Related methods**

- `PDDoc.` [GetFileName](IAC_API_OLE_Objects.md#50532405_30617)

<a id="50532405_31111"></a>
### SetFlags

Sets a document’s flags indicating whether the document has been modified, whether the document is a temporary document and should be deleted when closed, and the version of PDF used in the file. This method can be used only to set, not to clear, the flag bits.

**Syntax**

```
VARIANT_BOOL SetFlags(long nFlags);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFlags | Flags to be set. See `PDDoc.` [GetFlags](IAC_API_OLE_Objects.md#50532405_24732) for a description of the flags. The flags [PDDocWasRepaired](IAC_API_OLE_Objects.md#50532405_17887) , [PDDocNewMajorVersion](IAC_API_OLE_Objects.md#50532405_41659) , [PDDocNewMinorVersion](IAC_API_OLE_Objects.md#50532405_16605) , and [PDDocOldVersion](IAC_API_OLE_Objects.md#50532405_19653) are read-only and cannot be set. |

**Returns**

Always returns `-1`.

**Related methods**

- `PDDoc.` [ClearFlags](IAC_API_OLE_Objects.md#50532405_39995)
- `PDDoc.` [GetFlags](IAC_API_OLE_Objects.md#50532405_24732)

<a id="50532405_42162"></a>
### SetInfo

Sets the value of a key in a document’s Info dictionary.

**Syntax**

```
VARIANT_BOOL SetInfo(BSTR szInfoKey, BSTR szBuffer);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szInfoKey | The key whose value is set. |
| szBuffer | The value to be assigned to the key. |

**Returns**

`-1` if the value was added successfully, `0` if it was not or if the Acrobat application does not support editing.

**Related methods**

- `PDDoc.` [GetInfo](IAC_API_OLE_Objects.md#50532405_19753)

<a id="50532405_34412"></a>
SetPageMode

Sets the page mode in which a document is to be opened: display only pages, pages and thumbnails, or pages and bookmarks.

**Syntax**

```
VARIANT_BOOL SetPageMode(long nPageMode);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nPageMode | The page mode to be set. Possible values:  `PDDontCare`: `0`: leave the view mode as it is  `PDUseNone`: `1`: display without bookmarks or thumbnails  `PDUseThumbs`: `2`: display using thumbnails  `PDUseBookmarks`: `3`: display using bookmarks |

**Returns**

Always returns `-1`.

**Related methods**

- `PDDoc.` [GetPageMode](IAC_API_OLE_Objects.md#50532405_27507)
- `PDDoc.` [SetPageMode](IAC_API_OLE_Objects.md#50532405_34412)

<a id="50532405_28781"></a>
## AcroExch.PDPage

A single page in the PDF representation of a document. This is a non-creatable interface. Just as PDF files are partially composed of their pages, `PDDoc` objects are composed of `PDPage` objects. A page contains a series of objects representing the objects drawn on the page (`PDGraphic` objects), a list of resources used in drawing the page, annotations (`PDAnnot` objects), an optional thumbnail image of the page, and the threads used in any articles that occur on the page. The first page in a `PDDoc` object is page 0.

### Methods

The `PDPage` object has the following methods.

| Method | Description |
| --- | --- |
| [AddAnnot](IAC_API_OLE_Objects.md#50532405_29239) | Adds a specified annotation at a specified location in the page’s annotation array |
| [AddNewAnnot](IAC_API_OLE_Objects.md#50532405_27501) | Creates a new text annotation and adds it to the page. |
| [CopyToClipboard](IAC_API_OLE_Objects.md#50532405_24289) | Copies a PDF image to the clipboard without requiring an `hWnd` or `hDC` from the client. |
| [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822) | Creates a text selection from a list of character offsets and character counts on a single page. |
| [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477) | Creates a text selection from a list of word offsets and word counts on a single page. |
| [CropPage](IAC_API_OLE_Objects.md#50532405_26025) | Crops the page. |
| [Draw](IAC_API_OLE_Objects.md#50532405_24561) | Deprecated. Draws page contents into a specified window. |
| [DrawEx](IAC_API_OLE_Objects.md#50532405_35894) | Draws page contents into a specified window. |
| [GetAnnot](IAC_API_OLE_Objects.md#50532405_15604) | Gets the specified annotation from the page’s array of annotations. |
| [GetAnnotIndex](IAC_API_OLE_Objects.md#50532405_12469) | Gets the index (within the page’s annotation array) of the specified annotation. |
| [GetDoc](IAC_API_OLE_Objects.md#50532405_40890) | Gets the `AcroExch.PDDoc` associated with the page. |
| [GetNumAnnots](IAC_API_OLE_Objects.md#50532405_24017) | Gets the number of annotations on the page. |
| [GetNumber](IAC_API_OLE_Objects.md#50532405_32146) | Gets the page number of the current page. The first page in a document is page zero. |
| [GetRotate](IAC_API_OLE_Objects.md#50532405_14436) | Gets the rotation value, in degrees, for the current page. |
| [GetSize](IAC_API_OLE_Objects.md#50532405_37312) | Gets a page’s width and height in points. |
| [RemoveAnnot](IAC_API_OLE_Objects.md#50532405_26919) | Removes the specified annotation from the page’s annotation array. |
| [SetRotate](IAC_API_OLE_Objects.md#50532405_33224) | Sets the rotation, in degrees, for the current page. |

<a id="50532405_29239"></a>
### AddAnnot

Adds a specified annotation at a specified location in the page’s annotation array.

**Syntax**

```
VARIANT_BOOL AddAnnot(long nIndexAddAfter,
                 LPDISPATCH iPDAnnot);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nIndexAddAfter | Location in the page’s annotation array to add the annotation. The first annotation on a page has an index of zero. |
| iPDAnnot | The `LPDISPATCH` for the `AcroExch.PDAnnot` to add. `iPDAnnot` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

`0` if the Acrobat application does not support editing, `-1` otherwise.

**Related methods**

- `PDPage.` [AddNewAnnot](IAC_API_OLE_Objects.md#50532405_27501)
- `PDPage.` [RemoveAnnot](IAC_API_OLE_Objects.md#50532405_26919)

<a id="50532405_27501"></a>
### AddNewAnnot

Creates a new text annotation and adds it to the page.

The newly-created text annotation is not complete until `PDAnnot.` [SetContents](IAC_API_OLE_Objects.md#50532405_22402) has been called to fill in the `/Contents` key.

**Syntax**

```
LPDISPATCH AddNewAnnot(long nIndexAddAfter, BSTR szSubType,

                 LPDISPATCH iAcroRect);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nIndexAddAfter | Location in the page’s annotation array after which to add the annotation. The first annotation on a page has an index of zero. |
| szSubType | Subtype of the annotation to be created. Must be text. |
| iAcroRect | The `LPDISPATCH` for the `AcroExch.Rect` bounding the annotation’s location on the page. `iAcroRect` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

The `LPDISPATCH` for an `AcroExch.PDAnnot` object, or `NULL` if the annotation could not be added.

**Related methods**

- `PDAnnot.` [SetContents](IAC_API_OLE_Objects.md#50532405_22402)
- `PDPage.` [AddAnnot](IAC_API_OLE_Objects.md#50532405_29239)
- `PDPage.` [RemoveAnnot](IAC_API_OLE_Objects.md#50532405_26919)

<a id="50532405_24289"></a>
### CopyToClipboard

Copies a PDF image to the clipboard without requiring an `hWnd` or `hDC` from the client. This method is only available on 32-bit systems.

**Syntax**

```
VARIANT_BOOL CopyToClipboard(LPDISPATCH boundRect,
                 short nXOrigin,short nYOrigin,
                 short nZoom);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| boundRect | The `LPDISPATCH` for the `AcroExch.Rect` bounding rectangle in device space coordinates. `boundRect` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |
| nXOrigin | The x–coordinate of the portion of the page to be copied. |
| nYOrigin | The y–coordinate of the portion of the page to be copied. |
| nZoom | Zoom factor at which the page is copied, specified as a percent. For example, 100 corresponds to a magnification of 1.0. |

**Returns**

`-1` if the page is successfully copied, `0` otherwise.

**Related methods**

- `PDPage.` [DrawEx](IAC_API_OLE_Objects.md#50532405_35894)

<a id="50532405_37822"></a>
### CreatePageHilite

Creates a text selection from a list of character offsets and character counts on a single page. The text selection can then be set as the current selection using `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749) , and the view can be set to show the selection using `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147).

**Syntax**

```
LPDISPATCH CreatePageHilite(LPDISPATCH iAcroHiliteList);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroHiliteList | The `LPDISPATCH` for the highlight list for which a text selection is created. `iAcroHiliteList` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`.   Use `HiliteList.` [Add](IAC_API_OLE_Objects.md#50532405_30712) to create a highlight list. |

**Returns**

The `LPDISPATCH` for the `AcroExch.PDTextSelect` containing the text selection, or `NULL` if the selection could not be created.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `HiliteList.` [Add](IAC_API_OLE_Objects.md#50532405_30712)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_15686)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_14477"></a>
### CreateWordHilite

Creates a text selection from a list of word offsets and word counts on a single page. The text selection can then be set as the current selection using `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749) , and the view can be set to show the selection using `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147).

**Syntax**

```
LPDISPATCH CreateWordHilite(LPDISPATCH iAcroHiliteList);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroHiliteList | The `LPDISPATCH` for the highlight list for which a text selection is created. `iAcroHiliteList` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`.   Use `HiliteList.` [Add](IAC_API_OLE_Objects.md#50532405_30712) to create a highlight list. |

**Returns**

The `LPDISPATCH` for the `AcroExch.PDTextSelect`, or `NULL` if the selection could not be created.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `HiliteList.` [Add](IAC_API_OLE_Objects.md#50532405_30712)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_15686)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_26025"></a>
### CropPage

Crops the page. This method ignores the request if either the width or height of the crop box is less than 72 points (one inch).

**Syntax**

```
VARIANT_BOOL CropPage(LPDISPATCH iAcroRect);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iAcroRect | An `LPDISPATCH` for a `CAcroRect` specifying the cropping rectangle, which is specified in user space. |

**Returns**

`-1` if the page was cropped successfully, `0` otherwise.

**Related methods**

- `PDDoc.` [CropPages](IAC_API_OLE_Objects.md#50532405_22406)

<a id="50532405_24561"></a>
### Draw

> **Note**
>
> Deprecated. As of Acrobat 3.0, this method simply returns `false`. Use the method `AVDoc.` [DrawEx](IAC_API_OLE_Objects.md#50532405_35894) instead.

**Syntax**

```
VARIANT_BOOL Draw(short window, short displayContext,
                 short XOrigin,short YOrigin, short zoom);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| window | `HWND` into which the page is to be drawn. |
| displayContext | `hDC` to use for drawing. If `NULL`, the `HDC` for `window` is used.   `displayContext` cannot be reliably used as the `hDC` for a printer device. In particular, Visual Basic applications cannot use [Draw](IAC_API_OLE_Objects.md#50532405_24561) to print. |
| XOrigin | The x–coordinate of the portion of the page to be drawn. |
| YOrigin | The y–coordinate of the portion of the page to be drawn. |
| zoom | Zoom factor at which the page is to be drawn, specified as a percent. For example, 100 corresponds to a magnification of 1.0. |

**Returns**

`-1` if the page is successfully drawn, `0` otherwise.

**Related methods**

- `PDPage.` [CopyToClipboard](IAC_API_OLE_Objects.md#50532405_24289)
- `PDPage.` [DrawEx](IAC_API_OLE_Objects.md#50532405_35894)

<a id="50532405_35894"></a>
### DrawEx

Draws page contents into a specified window.

You can use `PDPage.` [CopyToClipboard](IAC_API_OLE_Objects.md#50532405_24289) to copy page contents to the clipboard without an `hWnd` or `hDC` from the client.

**Syntax**

```
VARIANT_BOOL DrawEx(long window, long displayContext,

                 LPDISPATCH updateRect, short xOrigin,

                 short yOrigin, short zoom);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| window | Handle for the window (`HWND`) into which the page is drawn. |
| displayContext | This parameter is invalid; do not use it. Assign it a `NULL` value. If it is not assigned `NULL`, an exception is thrown.   -  `displayContext` cannot be reliably used as the `hDC` for a printer device. In particular, Visual Basic applications cannot use [DrawEx](IAC_API_OLE_Objects.md#50532405_35894) to print. |
| updateRect | `LPDISPATCH` for an `AcroExch.Rect` to be drawn with user space coordinates. `updateRect` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`.   Any objects outside of `updateRect` are not drawn. All objects are drawn if `updateRect` is `NULL`.   Use methods in the `CAcroRect` class to set the size of the rectangle. For example:<br><br>```<br>CAcroRect* rect = new CAcroRect;<br>rect->CreateDispatch("AcroExch.Rect", &e);<br>   if (rect) { /* Set values for rect - increases from right to left and bottom to top */<br>   rect->SetLeft(100);<br>   rect->SetTop(400);<br>   rect->SetRight(400);<br>   rect->SetBottom(100); }<br>``` |
| xOrigin | The x–coordinate of the portion of the page to be drawn. |
| yOrigin | The y–coordinate of the portion of the page to be drawn. |
| zoom | Zoom factor at which the page is drawn, specified as a percent. For example, 100 corresponds to a magnification of 1.0. |

**Returns**

A positive number if the page is successfully drawn, `0` otherwise.

**Related methods**

- `PDPage.` [CopyToClipboard](IAC_API_OLE_Objects.md#50532405_24289)

<a id="50532405_15604"></a>
### GetAnnot

Gets the specified annotation from the page’s array of annotations.

**Syntax**

```
LPDISPATCH GetAnnot(long nIndex);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nIndex | Index (in the page’s annotation array) of the annotation to be retrieved. The first annotation in the array has an index of zero. |

**Returns**

The `LPDISPATCH` for the `AcroExch.PDAnnot` object.

**Related methods**

- `PDPage.` [GetAnnotIndex](IAC_API_OLE_Objects.md#50532405_12469)
- `PDPage.` [GetNumAnnots](IAC_API_OLE_Objects.md#50532405_24017)

<a id="50532405_12469"></a>
### GetAnnotIndex

Gets the index (within the page’s annotation array) of the specified annotation.

**Syntax**

```
long GetAnnotIndex(LPDISPATCH iPDAnnot);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| iPDAnnot | `LPDISPATCH` for the `AcroExch.PDAnnot` whose index is obtained. `iPDAnnot` contains the instance variable `m_lpDispatch`, which contains the `LPDISPATCH`. |

**Returns**

The annotation’s index.

**Related methods**

- `PDPage.` [GetAnnot](IAC_API_OLE_Objects.md#50532405_15604)
- `PDPage.` [GetNumAnnots](IAC_API_OLE_Objects.md#50532405_24017)

<a id="50532405_40890"></a>
### GetDoc

Gets the `AcroExch.PDDoc` associated with the page.

**Syntax**

```
LPDISPATCH GetDoc();
```

**Returns**

The `LPDISPATCH` for the page’s `AcroExch.PDDoc`.

**Related methods**

- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_11673)
- `AVPageView.` [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046)
- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDPage.` [GetNumber](IAC_API_OLE_Objects.md#50532405_32146)
- `PDPage.` [GetRotate](IAC_API_OLE_Objects.md#50532405_14436)
- `PDPage.` [GetSize](IAC_API_OLE_Objects.md#50532405_37312)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)

<a id="50532405_24017"></a>
### GetNumAnnots

Gets the number of annotations on the page.

Annotations that have associated pop-up windows, such as a strikeout, count as two annotations. Also note that widget annotations (Acrobat form fields) are included.

**Syntax**

```
long GetNumAnnots();
```

**Returns**

The number of annotations on the page.

**Related methods**

- `PDPage.` [GetAnnot](IAC_API_OLE_Objects.md#50532405_15604)
- `PDPage.` [GetAnnotIndex](IAC_API_OLE_Objects.md#50532405_12469)

<a id="50532405_32146"></a>
### GetNumber

Gets the page number of the current page. The first page in a document is page zero.

**Syntax**

```
long GetNumber();
```

**Returns**

The page number of the current page. The first page in a `PDDoc` object is page `0`.

**Related methods**

- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `AVPageView.` [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046)
- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDPage.` [GetDoc](IAC_API_OLE_Objects.md#50532405_40890)
- `PDPage.` [GetRotate](IAC_API_OLE_Objects.md#50532405_14436)
- `PDPage.` [GetSize](IAC_API_OLE_Objects.md#50532405_37312)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)

<a id="50532405_14436"></a>
### GetRotate

Gets the rotation value, in degrees, for the current page.

**Syntax**

```
short GetRotate();
```

**Returns**

Rotation value.

**Related methods**

- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_11673)
- `AVPageView.` [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046)
- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDPage.` [GetNumber](IAC_API_OLE_Objects.md#50532405_32146)
- `PDPage.` [GetSize](IAC_API_OLE_Objects.md#50532405_37312)
- `PDPage.` [SetRotate](IAC_API_OLE_Objects.md#50532405_33224)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)

<a id="50532405_37312"></a>
### GetSize

Gets a page’s width and height in points.

**Syntax**

```
LPDISPATCH GetSize();
```

**Returns**

The `LPDISPATCH` for an `AcroExch.Point` containing the width and height, measured in points. Point x contains the width, point y the height.

**Related methods**

- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `AVPageView.` [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046)
- `PDDoc.` [AcquirePage](IAC_API_OLE_Objects.md#50532405_25809)
- `PDPage.` [GetNumber](IAC_API_OLE_Objects.md#50532405_32146)
- `PDPage.` [GetRotate](IAC_API_OLE_Objects.md#50532405_14436)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)

<a id="50532405_26919"></a>
### RemoveAnnot

Removes the specified annotation from the page’s annotation array.

**Syntax**

```
VARIANT_BOOL RemoveAnnot(long nIndex);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nIndex | Index within the page’s annotation array of the annotation to be deleted. The first annotation on a page has an index of zero. |

**Returns**

`0` if the Acrobat application does not support editing, a positive number otherwise.

**Related methods**

- `PDPage.` [AddAnnot](IAC_API_OLE_Objects.md#50532405_29239)
- `PDPage.` [AddNewAnnot](IAC_API_OLE_Objects.md#50532405_27501)
- `PDPage.` [GetAnnotIndex](IAC_API_OLE_Objects.md#50532405_12469)

<a id="50532405_33224"></a>
### SetRotate

Sets the rotation, in degrees, for the current page.

**Syntax**

```
VARIANT_BOOL SetRotate(short nRotate);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nRotate | Rotation value of 0, 90, 180, or 270. |

**Returns**

`0` if the Acrobat application does not support editing, `-1` otherwise.

**Related methods**

- `PDPage.` [GetRotate](IAC_API_OLE_Objects.md#50532405_14436)

<a id="50532405_33981"></a>
## AcroExch.PDTextSelect

A selection of text on a single page that may contain more than one disjointed group of words. This is a non-creatable interface. A text selection is specified by one or more ranges of text, with each range containing the word numbers of the selected words. Each range specifies a start and end word, where “start” is the number of the first word of a series of selected words and “end” is the number of the next word after the last word in the selection.

### Methods

The `PDTextSelect` object has the following methods.

| Method | Description |
| --- | --- |
| [Destroy](IAC_API_OLE_Objects.md#50532405_15686) | Destroys a text selection object. |
| [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335) | Gets a text selection’s bounding rectangle. |
| [GetNumText](IAC_API_OLE_Objects.md#50532405_40099) | Gets the number of text elements in a text selection. |
| [GetPage](IAC_API_OLE_Objects.md#50532405_34289) | Gets the page number on which the text selection is located. |
| [GetText](IAC_API_OLE_Objects.md#50532405_24003) | Gets the text from the specified element of a text selection. |

<a id="50532405_15686"></a>
### Destroy

Destroys a text selection object.

**Syntax**

```
VARIANT_BOOL Destroy();
```

**Returns**

Always returns `-1`.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_15335"></a>
### GetBoundingRect

Gets a text selection’s bounding rectangle.

**Syntax**

```
LPDISPATCH GetBoundingRect();
```

**Returns**

The `LPDISPATCH` for an `AcroExch.Rect` corresponding to the text selection’s bounding rectangle.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_15686)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_40099"></a>
### GetNumText

Gets the number of text elements in a text selection. Use this method to determine how many times to call the `PDTextSelect`. [GetText](IAC_API_OLE_Objects.md#50532405_24003) method to obtain all of a text selection’s text.

> **Note**
>
> A text element is not necessarily a word. A text element consists of characters of the same font, size and style; therefore, there may be more than one text element in a word.

**Syntax**

```
long GetNumText();
```

**Returns**

The number of elements in the text selection.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_15686)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_34289"></a>
### GetPage

Gets the page number on which the text selection is located.

**Syntax**

```
long GetPage();
```

**Returns**

The text selection’s page number. The first page in a `PDDoc` object is page 0.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `AVPageView.` [GetPage](IAC_API_OLE_Objects.md#50532405_11673)
- `AVPageView.` [GetPageNum](IAC_API_OLE_Objects.md#50532405_19046)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDDoc.` [GetNumPages](IAC_API_OLE_Objects.md#50532405_30052)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDPage.` [GetNumber](IAC_API_OLE_Objects.md#50532405_32146)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_15686)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetText](IAC_API_OLE_Objects.md#50532405_24003)

<a id="50532405_24003"></a>
### GetText

Gets the text from the specified element of a text selection. To obtain all the text within the text selection, use `PDTextSelect`. [GetNumText](IAC_API_OLE_Objects.md#50532405_40099) to determine the number of elements in the text selection, then call this method in a loop to obtain each of the elements.

**Syntax**

```
BSTR GetText(long nTextIndex);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nTextIndex | The element of the text selection to get. |

**Returns**

The text, or an empty string if `nTextIndex` is greater than the number of elements in the text selection.

**Related methods**

- `AVDoc.` [ClearSelection](IAC_API_OLE_Objects.md#50532405_16710)
- `AVDoc.` [SetTextSelection](IAC_API_OLE_Objects.md#50532405_34749)
- `AVDoc.` [ShowTextSelect](IAC_API_OLE_Objects.md#50532405_27147)
- `PDPage.` [CreatePageHilite](IAC_API_OLE_Objects.md#50532405_37822)
- `PDDoc.` [CreateTextSelect](IAC_API_OLE_Objects.md#50532405_34819)
- `PDPage.` [CreateWordHilite](IAC_API_OLE_Objects.md#50532405_14477)
- `PDTextSelect.` [Destroy](IAC_API_OLE_Objects.md#50532405_15686)
- `PDTextSelect.` [GetBoundingRect](IAC_API_OLE_Objects.md#50532405_15335)
- `PDTextSelect.` [GetNumText](IAC_API_OLE_Objects.md#50532405_40099)
- `PDTextSelect.` [GetPage](IAC_API_OLE_Objects.md#50532405_34289)

<a id="50532405_76536"></a>
## AcroExch.Point

Defines the location of an `AcroPoint.`

**Properties**

The `Point` object has the following properties.

| Property | Description |
| --- | --- |
| [X](IAC_API_OLE_Objects.md#50532405_14799) | Gets or sets the x-coordinate of an `AcroPoint`. |
| [Y](IAC_API_OLE_Objects.md#50532405_33201) | Gets or sets the y-coordinate of an `AcroPoint`. |

<a id="50532405_14799"></a>
### X

Gets or sets the x-coordinate of an `AcroPoint`.

**Syntax**

```
[get/set] Short
```

**Returns**

The x-coordinate of the `AcroPoint`.

<a id="50532405_33201"></a>
### Y

Gets or sets the y-coordinate of an `AcroPoint`.

**Syntax**

```
[get/set] Short
```

**Returns**

The y-coordinate of the `AcroPoint`.

<a id="50532405_39836"></a>
## AcroExch.Rect

Defines the location of an `AcroRect`.

The `Rect` object has the following properties.

**Properties**

| Property | Description |
| --- | --- |
| [Bottom](IAC_API_OLE_Objects.md#50532405_51838) | Gets or sets the bottom y-coordinate of an `AcroRect`. |
| [Left](IAC_API_OLE_Objects.md#50532405_44078) | Gets or sets the left x-coordinate of an `AcroRect`. |
| [Right](IAC_API_OLE_Objects.md#50532405_59707) | Gets or sets the right x-coordinate of an `AcroRect`. |
| [Top](IAC_API_OLE_Objects.md#50532405_28094) | Gets or sets the top y-coordinate of an `AcroRect`. |

<a id="50532405_51838"></a>
### Bottom

Gets or sets the bottom y-coordinate of an `AcroRect`.

**Syntax**

```
[get/set] Short
```

**Returns**

The y-coordinate of the bottom of the `AcroRect`.

<a id="50532405_44078"></a>
### Left

Gets or sets left x-coordinate of an `AcroRect`.

**Syntax**

```
[get/set] Short
```

**Returns**

The x-coordinate of the left side of the `AcroRect`.

<a id="50532405_59707"></a>
### Right

Gets or sets the right x-coordinate of an `AcroRect`.

**Syntax**

```
[get/set] Short
```

**Returns**

The x-coordinate of the right side of the `AcroRect`.

<a id="50532405_28094"></a>
### Top

Gets or sets the top y-coordinate of an `AcroRect`.

**Syntax**

```
[get/set] Short
```

**Returns**

The y-coordinate of the top of the `AcroRect`.

<a id="50532405_86731"></a>
## AcroExch.Time

Defines a specified time, accurate to the millisecond.

**Properties**

The `Time` object has the following properties.

| Property | Description |
| --- | --- |
| [Date](IAC_API_OLE_Objects.md#50532405_19244) | Gets or sets the date from an `AcroTime`. |
| [Hour](IAC_API_OLE_Objects.md#50532405_34062) | Gets or sets the hour from an `AcroTime`. |
| [Millisecond](IAC_API_OLE_Objects.md#50532405_89313) | Gets or sets the milliseconds from an `AcroTime`. |
| [Minute](IAC_API_OLE_Objects.md#50532405_71117) | Gets or sets the minutes from an `AcroTime`. |
| [Month](IAC_API_OLE_Objects.md#50532405_57342) | Gets or sets the month from an `AcroTime`. |
| [Second](IAC_API_OLE_Objects.md#50532405_73027) | Gets or sets the seconds from an `AcroTime`. |
| [Year](IAC_API_OLE_Objects.md#50532405_58044) | Gets or sets the year from an `AcroTime`. |

<a id="50532405_19244"></a>
### Date

Gets or sets the date from an `AcroTime`.

**Syntax**

```
[get/set] Short
```

**Returns**

The date from the `AcroTime`. The date runs from `1` to `31`.

<a id="50532405_34062"></a>
### Hour

Gets or sets the hour from an `AcroTime`.

**Syntax**

```
[get/set] Short
```

**Returns**

The hour from the `AcroTime`. The hour runs from `0` to `23`.

<a id="50532405_89313"></a>
### Millisecond

Gets or sets the milliseconds from an `AcroTime`.

**Syntax**

```
[get/set] Short
```

**Returns**

The milliseconds from the `AcroTime`. Milliseconds run from `0` to `999`.

<a id="50532405_71117"></a>
### Minute

Gets or sets the minutes from an `AcroTime`.

**Syntax**

```
[get/set] Short
```

**Returns**

The minutes from the `AcroTime`. Minutes run from `0` to `59`.

<a id="50532405_57342"></a>
### Month

Gets or sets the month from an `AcroTime`.

**Syntax**

```
[get/set] Short
```

**Returns**

The month from the `AcroTime`. The month runs from `1` to `12`, where `1` is January and `12` is December.

<a id="50532405_73027"></a>
### Second

Gets or sets the seconds from an `AcroTime`.

**Syntax**

```
[get/set] Short
```

**Returns**

The seconds from the `AcroTime`. Seconds run from `0` to `59`.

<a id="50532405_58044"></a>
### Year

Gets or sets the year from an `AcroTime`.

**Syntax**

```
[get/set] Short
```

**Returns**

The year from the `AcroTime`. The Year runs from `1` to `32767`.

<a id="50532405_76583"></a>
## AxAcroPDFLib.AxAcroPDF

An object containing a set of methods that provide access to PDF browser controls. This is a creatable interface. This object makes it possible to load a file, move to various pages within the file, and specify various display and print options.

### Methods

The `AxAcroPDF` object has the following methods.

| Method | Description |
| --- | --- |
| [GetVersions](IAC_API_OLE_Objects.md#50532405_36441) | Deprecated |
| [GoBackwardStack](IAC_API_OLE_Objects.md#50532405_27582) | Goes to the previous view on the view stack, if the previous view exists. |
| [GoForwardStack](IAC_API_OLE_Objects.md#50532405_83885) | Goes to the next view on the view stack, if the next view exists. |
| [GotoFirstPage](IAC_API_OLE_Objects.md#50532405_37358) | Goes to the first page in the document, maintaining the current location within the page and zoom level. |
| [GotoLastPage](IAC_API_OLE_Objects.md#50532405_56061) | Goes to the last page in the document, maintaining the current location within the page and zoom level. |
| [GotoNextPage](IAC_API_OLE_Objects.md#50532405_61327) | Goes to the next page in the document, if it exists. Maintains the current location within the page and zoom level. |
| [GotoPreviousPage](IAC_API_OLE_Objects.md#50532405_38257) | Goes to the previous page in the document, if it exists. Maintains the current location within the page and zoom level. |
| [LoadFile](IAC_API_OLE_Objects.md#50532405_77539) | Opens and displays the specified document within the browser. |
| [Print](IAC_API_OLE_Objects.md#50532405_80023) | Prints the document according to the options selected in a user dialog box. |
| [PrintAll](IAC_API_OLE_Objects.md#50532405_67867) | Prints the entire document without displaying a user dialog box. |
| [PrintAllFit](IAC_API_OLE_Objects.md#50532405_87648) | Prints the entire document without displaying a user dialog box, and the pages are shrunk, if necessary, to fit into the imageable area of a page in the printer. |
| [PrintPages](IAC_API_OLE_Objects.md#50532405_35579) | Prints the specified pages without displaying a user dialog box. |
| [PrintPagesFit](IAC_API_OLE_Objects.md#50532405_72769) | Prints the specified pages without displaying a user dialog box. |
| [PrintWithDialog](IAC_API_OLE_Objects.md#50532405_48290) | Prints the document according to the options selected in a user dialog box. |
| [SetCurrentHighlight](IAC_API_OLE_Objects.md#50532405_42701) | Highlights the text selection within the specified bounding rectangle on the current page. |
| [SetCurrentPage](IAC_API_OLE_Objects.md#50532405_60750) | Goes to the specified page in the document. |
| [SetLayoutMode](IAC_API_OLE_Objects.md#50532405_65913) | Sets the layout mode for a page view according to the specified string. |
| [SetNamedDest](IAC_API_OLE_Objects.md#50532405_95088) | Changes the page view to the named destination in the specified string. |
| [SetPageMode](IAC_API_OLE_Objects.md#50532405_17156) | Sets the page mode according to the specified string. |
| [SetShowScrollbars](IAC_API_OLE_Objects.md#50532405_92910) | Determines whether scrollbars will appear in the document view. |
| [SetShowToolbar](IAC_API_OLE_Objects.md#50532405_48320) | Determines whether a toolbar will appear in the viewer. |
| [SetView](IAC_API_OLE_Objects.md#50532405_82737) | Sets the view of a page according to the specified string. |
| [SetViewRect](IAC_API_OLE_Objects.md#50532405_50198) | Sets the view rectangle according to the specified coordinates. |
| [SetViewScroll](IAC_API_OLE_Objects.md#50532405_41219) | Sets the view of a page according to the specified string. |
| [SetZoom](IAC_API_OLE_Objects.md#50532405_17296) | Sets the magnification according to the specified value. |
| [SetZoomScroll](IAC_API_OLE_Objects.md#50532405_23108) | Sets the magnification according to the specified value, and scrolls the page view both horizontally and vertically according to the specified amounts. |

**Properties**

The `AxAcroPDF` object has the following property.

| Property | Description |
| --- | --- |
| [Src](IAC_API_OLE_Objects.md#50532405_53488) | Gets or sets the URL for the document. |

<a id="50532405_36441"></a>
### GetVersions

> **Note**
>
> Deprecated. This method is no longer available.

**Syntax**

```
VARIANT GetVersions();
```

<a id="50532405_27582"></a>
### GoBackwardStack

Goes to the previous view on the view stack, if the previous view exists. The previous view may be in a different document.

**Syntax**

```
void GoBackwardStack();
```

**Related methods**

- `AcroPDF.` [GoForwardStack](IAC_API_OLE_Objects.md#50532405_83885)

<a id="50532405_83885"></a>
### GoForwardStack

Goes to the next view on the view stack, if the next view exists. The next view may be in a different document.

**Syntax**

```
void GoForwardStack();
```

**Related methods**

- `AcroPDF.` [GoBackwardStack](IAC_API_OLE_Objects.md#50532405_27582)

<a id="50532405_37358"></a>
### GotoFirstPage

Goes to the first page in the document, maintaining the current location within the page and the current zoom level.

**Syntax**

```
void gotoFirstPage();
```

**Related methods**

- `AcroPDF.` [GotoLastPage](IAC_API_OLE_Objects.md#50532405_56061)
- `AcroPDF.` [GotoNextPage](IAC_API_OLE_Objects.md#50532405_61327)
- `AcroPDF.` [GotoPreviousPage](IAC_API_OLE_Objects.md#50532405_38257)
- `AcroPDF.` [SetCurrentPage](IAC_API_OLE_Objects.md#50532405_60750)

<a id="50532405_56061"></a>
### GotoLastPage

Goes to the last page in the document, maintaining the current location within the page and the current zoom level.

**Syntax**

```
void gotoLastPage();
```

**Related methods**

- `AcroPDF.` [GotoFirstPage](IAC_API_OLE_Objects.md#50532405_37358)
- `AcroPDF.` [GotoNextPage](IAC_API_OLE_Objects.md#50532405_61327)
- `AcroPDF.` [GotoPreviousPage](IAC_API_OLE_Objects.md#50532405_38257)
- `AcroPDF.` [SetCurrentPage](IAC_API_OLE_Objects.md#50532405_60750)

<a id="50532405_61327"></a>
### GotoNextPage

Goes to the next page in the document, if it exists. Maintains the current location within the page and the current zoom level.

**Syntax**

```
void gotoNextPage();
```

**Related methods**

- `AcroPDF.` [GotoFirstPage](IAC_API_OLE_Objects.md#50532405_37358)
- `AcroPDF.` [GotoLastPage](IAC_API_OLE_Objects.md#50532405_56061)
- `AcroPDF.` [GotoPreviousPage](IAC_API_OLE_Objects.md#50532405_38257)
- `AcroPDF.` [SetCurrentPage](IAC_API_OLE_Objects.md#50532405_60750)

<a id="50532405_38257"></a>
### GotoPreviousPage

Goes to the previous page in the document, if it exists. Maintains the current location within the page and the current zoom level.

**Syntax**

```
void gotoPreviousPage();
```

**Related methods**

- `AcroPDF.` [GotoFirstPage](IAC_API_OLE_Objects.md#50532405_37358)
- `AcroPDF.` [GotoLastPage](IAC_API_OLE_Objects.md#50532405_56061)
- `AcroPDF.` [GotoNextPage](IAC_API_OLE_Objects.md#50532405_61327)
- `AcroPDF.` [SetCurrentPage](IAC_API_OLE_Objects.md#50532405_60750)

<a id="50532405_77539"></a>
### LoadFile

Opens and displays the specified document within the browser.

**Syntax**

```
VARIANT_BOOL LoadFile(BSTR fileName);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| fileName | The path of the file to be opened. |

**Returns**

`0` if the file could not be opened, `-1` otherwise.

<a id="50532405_80023"></a>
### Print

Prints the document according to the options selected in a user dialog box. The options include embedded printing (printing within a bounding rectangle on a given page), as well as interactive printing to a specified printer. This method returns immediately, even if the printing has not completed.

> **Note**
>
> If security settings do not allow printing, this method is ignored.

**Syntax**

```
void Print();
```

**Related methods**

- `AcroPDF.` [PrintAll](IAC_API_OLE_Objects.md#50532405_67867)
- `AcroPDF.` [PrintAllFit](IAC_API_OLE_Objects.md#50532405_87648)
- `AcroPDF.` [PrintPages](IAC_API_OLE_Objects.md#50532405_35579)
- `AcroPDF.` [PrintPagesFit](IAC_API_OLE_Objects.md#50532405_72769)
- `AcroPDF.` [PrintWithDialog](IAC_API_OLE_Objects.md#50532405_48290)

<a id="50532405_67867"></a>
### PrintAll

Prints the entire document without displaying a user dialog box. The current printer, page settings, and job settings are used. This method returns immediately, even if the printing has not completed.

> **Note**
>
> If security settings do not allow printing, this method is ignored.

**Syntax**

```
void printAll();
```

**Related methods**

- `AcroPDF.` [Print](IAC_API_OLE_Objects.md#50532405_80023)
- `AcroPDF.` [PrintAllFit](IAC_API_OLE_Objects.md#50532405_87648)
- `AcroPDF.` [PrintPages](IAC_API_OLE_Objects.md#50532405_35579)
- `AcroPDF.` [PrintPagesFit](IAC_API_OLE_Objects.md#50532405_72769)
- `AcroPDF.` [PrintWithDialog](IAC_API_OLE_Objects.md#50532405_48290)

<a id="50532405_87648"></a>
### PrintAllFit

Prints the entire document without displaying a user dialog box, and the pages are shrunk, if necessary, to fit into the imageable area of a page in the printer. The current printer, page settings, and job settings are used. This method returns immediately, even if the printing has not completed.

> **Note**
>
> If security settings do not allow printing, this method is ignored.

**Syntax**

```
void printAllFit(VARIANT_BOOL bOn);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bOn | Determines whether to scale the imageable area when printing the document. A value of `0` indicates that no scaling should be used, and a positive value indicates that the pages are shrunk, if necessary, to fit into the imageable area of a page in the printer. |

**Related methods**

- `AcroPDF.` [Print](IAC_API_OLE_Objects.md#50532405_80023)
- `AcroPDF.` [PrintAll](IAC_API_OLE_Objects.md#50532405_67867)
- `AcroPDF.` [PrintPages](IAC_API_OLE_Objects.md#50532405_35579)
- `AcroPDF.` [PrintPagesFit](IAC_API_OLE_Objects.md#50532405_72769)
- `AcroPDF.` [PrintWithDialog](IAC_API_OLE_Objects.md#50532405_48290)

<a id="50532405_35579"></a>
### PrintPages

Prints the specified pages without displaying a user dialog box. The current printer, page settings, and job settings are used.This method returns immediately, even if the printing has not completed.

> **Note**
>
> If security settings do not allow printing, this method is ignored.

**Syntax**

```
void printPages( Long nFrom, Long nTo);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFrom | The page number of the first page to be printed. The first page in a document is page `0`. |
| nTo | The page number of the last page to be printed. |

**Related methods**

- `AcroPDF.` [Print](IAC_API_OLE_Objects.md#50532405_80023)
- `AcroPDF.` [PrintAll](IAC_API_OLE_Objects.md#50532405_67867)
- `AcroPDF.` [PrintAllFit](IAC_API_OLE_Objects.md#50532405_87648)
- `AcroPDF.` [PrintPagesFit](IAC_API_OLE_Objects.md#50532405_72769)
- `AcroPDF.` [PrintWithDialog](IAC_API_OLE_Objects.md#50532405_48290)

<a id="50532405_72769"></a>
### PrintPagesFit

Prints the specified pages without displaying a user dialog box. The current printer, page settings, and job settings are used. A parameter specifies whether to shrink pages, if necessary. This method returns immediately, even if the printing has not completed.

> **Note**
>
> If security settings do not allow printing, this method is ignored.

**Syntax**

```
void printPagesFit( Long nFrom, Long nTo,
                 VARIANT_BOOL bShrinkToFit);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nFrom | The page number of the first page to be printed. The first page in a document is page `0`. |
| nTo | The page number of the last page to be printed. |
| bShrinkToFit | Specifies whether the pages will be shrunk, if necessary, to fit into the imageable area of a page in the printer. |

**Related methods**

- `AcroPDF.` [Print](IAC_API_OLE_Objects.md#50532405_80023)
- `AcroPDF.` [PrintAll](IAC_API_OLE_Objects.md#50532405_67867)
- `AcroPDF.` [PrintAllFit](IAC_API_OLE_Objects.md#50532405_87648)
- `AcroPDF.` [PrintPages](IAC_API_OLE_Objects.md#50532405_35579)
- `AcroPDF.` [PrintWithDialog](IAC_API_OLE_Objects.md#50532405_48290)

<a id="50532405_48290"></a>
### PrintWithDialog

Prints the document according to the options selected in a user dialog box. The options include embedded printing (printing within a bounding rectangle on a given page), as well as interactive printing to a specified printer. This method returns immediately, even if the printing has not completed.

> **Note**
>
> If security settings do not allow printing, this method is ignored.

**Syntax**

```
void printWithDialog();
```

**Related methods**

- `AcroPDF.` [Print](IAC_API_OLE_Objects.md#50532405_80023)
- `AcroPDF.` [PrintAll](IAC_API_OLE_Objects.md#50532405_67867)
- `AcroPDF.` [PrintAllFit](IAC_API_OLE_Objects.md#50532405_87648)
- `AcroPDF.` [PrintPages](IAC_API_OLE_Objects.md#50532405_35579)
- `AcroPDF.` [PrintPagesFit](IAC_API_OLE_Objects.md#50532405_72769)

<a id="50532405_42701"></a>
### SetCurrentHighlight

Highlights the text selection within the specified bounding rectangle on the current page.

**Syntax**

```
void setCurrentHighlight(LONG nLeft, LONG nTop,
                 LONG nRight, LONG nBottom);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nLeft | The distance in points from the left side of the page. |
| nTop | The distance in points from the top of the page. |
| nRight | The width of the bounding rectangle. |
| nBottom | The height of the bounding rectangle. |

<a id="50532405_60750"></a>
### SetCurrentPage

Goes to the specified page in the document. Maintains the current location within the page and the current zoom level.

**Syntax**

```
void setCurrentPage(LONG nPage);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| nPage | The page number of the destination page. The first page in a document is page `0`. |

**Related methods**

- `AcroPDF.` [GotoFirstPage](IAC_API_OLE_Objects.md#50532405_37358)
- `AcroPDF.` [GotoLastPage](IAC_API_OLE_Objects.md#50532405_56061)
- `AcroPDF.` [GotoNextPage](IAC_API_OLE_Objects.md#50532405_61327)
- `AcroPDF.` [GotoPreviousPage](IAC_API_OLE_Objects.md#50532405_38257)

<a id="50532405_65913"></a>
### SetLayoutMode

Sets the layout mode for a page view according to the specified string.

**Syntax**

```
void setLayoutMode(BSTR szLayoutMode);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szLayoutMode | Possible values:  `DontCare`: use the current user preference  `SinglePage`: use single page mode (as it would have appeared in pre-Acrobat 3.0 viewers)   `OneColumn`: use one-column continuous mode  `TwoColumnLeft`: use two-column continuous mode with the first page on the left  `TwoColumnRight`: use two-column continuous mode with the first page on the right |

**Related methods**

- `AcroPDF.` [SetNamedDest](IAC_API_OLE_Objects.md#50532405_95088)
- `AcroPDF.` [SetView](IAC_API_OLE_Objects.md#50532405_82737)
- `AcroPDF.` [SetViewRect](IAC_API_OLE_Objects.md#50532405_50198)
- `AcroPDF.` [SetViewScroll](IAC_API_OLE_Objects.md#50532405_41219)

<a id="50532405_95088"></a>
### SetNamedDest

Changes the page view to the named destination in the specified string.

**Syntax**

```
void setNamedDest(BSTR szNamedDest);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szNamedDest | The named destination to which the viewer will go. |

**Related methods**

- `AcroPDF.` [SetLayoutMode](IAC_API_OLE_Objects.md#50532405_65913)
- `AcroPDF.` [SetView](IAC_API_OLE_Objects.md#50532405_82737)
- `AcroPDF.` [SetViewRect](IAC_API_OLE_Objects.md#50532405_50198)
- `AcroPDF.` [SetViewScroll](IAC_API_OLE_Objects.md#50532405_41219)

<a id="50532405_17156"></a>
### SetPageMode

Sets the page mode according to the specified string.

**Syntax**

```
void setPageMode(BSTR szPageMode);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szPageMode | Possible values:  `none`: displays the document, but does not display bookmarks or thumbnails (default)  `bookmarks`: displays the document and bookmarks  `thumbs`: displays the document and thumbnails |

**Related methods**

- `AcroPDF.` [SetShowScrollbars](IAC_API_OLE_Objects.md#50532405_92910)
- `AcroPDF.` [SetShowToolbar](IAC_API_OLE_Objects.md#50532405_48320)

<a id="50532405_92910"></a>
### SetShowScrollbars

Determines whether scrollbars will appear in the document view.

**Syntax**

```
void setShowScrollbars(VARIANT_BOOL bOn);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bOn | A positive value indicates that scrollbars will appear, `0` indicates that they will not. |

**Related methods**

- `AcroPDF.` [SetPageMode](IAC_API_OLE_Objects.md#50532405_17156)
- `AcroPDF.` [SetShowToolbar](IAC_API_OLE_Objects.md#50532405_48320)

<a id="50532405_48320"></a>
### SetShowToolbar

Determines whether a toolbar will appear in the viewer.

**Syntax**

```
void setShowToolbar(VARIANT_BOOL bOn);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| bOn | A positive value indicates that the toolbar will appear, `0` indicates that it will not. |

**Related methods**

- `AcroPDF.` [SetPageMode](IAC_API_OLE_Objects.md#50532405_17156)
- `AcroPDF.` [SetShowScrollbars](IAC_API_OLE_Objects.md#50532405_92910)

<a id="50532405_82737"></a>
### SetView

Sets the view of a page according to the specified string.

**Syntax**

```
void setView(BSTR szViewMode);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szViewMode | Possible values:  `Fit`: Fits the entire page within the window both vertically and horizontally.  `FitH`: Fits the entire width of the page within the window.  `FitV`: Fits the entire height of the page within the window.  `FitB`: Fits the bounding box within the window both vertically and horizontally.  `FitBH`: Fits the entire width of the bounding box within the window.  `FitB`: Fits the entire height of the bounding box within the window. |

**Related methods**

- `AcroPDF.` [SetLayoutMode](IAC_API_OLE_Objects.md#50532405_65913)
- `AcroPDF.` [SetNamedDest](IAC_API_OLE_Objects.md#50532405_95088)
- `AcroPDF.` [SetViewRect](IAC_API_OLE_Objects.md#50532405_50198)
- `AcroPDF.` [SetViewScroll](IAC_API_OLE_Objects.md#50532405_41219)

<a id="50532405_50198"></a>
### SetViewRect

Sets the view rectangle according to the specified coordinates.

**Syntax**

```
void setViewRect(FLOAT left, FLOAT top,
                 FLOAT width, FLOAT height);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| left | The upper left horizontal coordinate. |
| top | The vertical coordinate in the upper left corner. |
| width | The horizontal width of the rectangle. |
| height | The vertical height of the rectangle. |

**Related methods**

- `AcroPDF.` [SetLayoutMode](IAC_API_OLE_Objects.md#50532405_65913)
- `AcroPDF.` [SetNamedDest](IAC_API_OLE_Objects.md#50532405_95088)
- `AcroPDF.` [SetView](IAC_API_OLE_Objects.md#50532405_82737)
- `AcroPDF.` [SetViewScroll](IAC_API_OLE_Objects.md#50532405_41219)

<a id="50532405_41219"></a>
### SetViewScroll

Sets the view of a page according to the specified string. Depending on the view mode, the page is either scrolled to the right or scrolled down by the amount specified in `offset`.

**Syntax**

```
void setViewRect(BSTR szViewMode, FLOAT offset);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| szViewMode | Possible values:  `Fit`: Fits the entire page within the window both vertically and horizontally.  `FitH`: Fits the entire width of the page within the window.  `FitV`: Fits the entire height of the page within the window.  `FitB`: Fits the bounding box within the window both vertically and horizontally.  `FitBH`: Fits the entire width of the bounding box within the window.  `FitBV`: Fits the entire height of the bounding box within the window. |
| offset | The horizontal or vertical coordinate positioned either at the left or top edge. |

**Related methods**

- `AcroPDF.` [SetLayoutMode](IAC_API_OLE_Objects.md#50532405_65913)
- `AcroPDF.` [SetNamedDest](IAC_API_OLE_Objects.md#50532405_95088)
- `AcroPDF.` [SetView](IAC_API_OLE_Objects.md#50532405_82737)
- `AcroPDF.` [SetViewRect](IAC_API_OLE_Objects.md#50532405_50198)

<a id="50532405_17296"></a>
### SetZoom

Sets the magnification according to the specified value.

**Syntax**

```
void setZoom(FLOAT percent);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| percent | The desired zoom factor, expressed as a percentage. For example, 1.0 represents a magnification of 100%. |

**Related methods**

- `AcroPDF.` [SetZoomScroll](IAC_API_OLE_Objects.md#50532405_23108)

<a id="50532405_23108"></a>
### SetZoomScroll

Sets the magnification according to the specified value, and scrolls the page view both horizontally and vertically according to the specified amounts.

**Syntax**

```
void setZoomScroll(FLOAT percent, FLOAT left, FLOAT top);
```

**Parameters**

| Parameter | Description |
| --- | --- |
| percent | The desired zoom factor, expressed as a percentage. For example, 1.0 represents a magnification of 100%. |
| left | The horizontal coordinate positioned at the left edge. |
| top | The vertical coordinate positioned at the top edge. |

**Related methods**

- `AcroPDF.` [SetZoom](IAC_API_OLE_Objects.md#50532405_17296)

<a id="50532405_53488"></a>
### Src

Gets or sets the URL for the document.

**Syntax**

```
[get/set] src
```

**Returns**

The URL for the document, formatted as a string.
