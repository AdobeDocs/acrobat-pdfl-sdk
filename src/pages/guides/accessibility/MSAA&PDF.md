# Reading PDF Files Through MSAA

Microsoft Active Accessibility defines the `IAccessible` interface to applications. This interface consists of a set of methods and properties that are defined in the MSAA documentation.

Acrobat implements and exports a set of `IAccessible` objects of different types to represent a document, its pages, and other elements of the document hierarchy.

An MSAA client can retrieve an `IAccessible` object for a user interface element in the following four ways:

- Set a `WinEvent` hook, receive a notification, and call `AccessibleObjectFromEvent` to retrieve an `IAccessible` interface pointer for the user interface element that generated the event. See [Handling event notifications](index.md#21082) for details.
- Call `AccessibleObjectFromWindow` and pass the user interface element’s window handle. Each open document in Acrobat is associated with its own window handle.
- Call `AccessibleObjectFromPoint` and pass a screen location that lies within the user interface element’s bounding rectangle.
- Call an `IAccessible` method such as `accNavigate` or `get_accParent` to move to a different `IAccessible` object.

## Acrobat implementation of IAccessible objects

Each type of `IAccessible` object has a different implementation of the standard methods:

- Links, tables, and form fields are explicitly identified through MSAA.
- Headers, paragraphs, and other elements of document structure are only represented implicitly.

> **Note**
>
> These elements are explicit in the DOM interface; see [Reading PDF Files Through the DOM Interface](Access_DOM.md#30124).

For each document, Acrobat builds a tree of `IAccessible` objects representing the document and its internal structure. Because there is just one window handle associated with the document, Acrobat posts all event notifications to that window. In each notification, a `childID` identifies an `IAccessible` object for an element in the document. For example, when the user tabs to the next link, the `EVENT_OBJECT_FOCUS` notification includes a `childID` that is the UID of the link object. See [Handling event notifications](index.md#21082).

The following interfaces are exported from the `IAccessible` object by Acrobat:

<a id="10950"></a>
## IGetPDDomNode interface

This interface exports one function, `get_PDDomNode` , which returns a DOM object. The methods described in [Reading PDF Files Through the DOM Interface](Access_DOM.md#30124)” can then be used on this object.

### get\_PDDomNode

Returns a DOM object. For more information, see [Reading PDF Files Through the DOM Interface](Access_DOM.md#30124).

`varID` is the same as for the other MSAA methods (see [Descriptive properties and methods](MSAA&PDF.md#89440))

```
HRESULT get_PDDomNode(
VARIANT varID,
IPDDomNode **ppDispDoc);
```

## ISelectText interface

In Acrobat 7.0, the `ISelectText` interface is an interface exported by the `IAccessible` objects. It exports one function, `selectText` , that sets the text selection, but specifies the end location via `IAccessible` objects instead of DOM nodes. The `ISelectText` interface is available from the root `IAccessible` object.

### selectText

Sets the text selection. `startAccID` and `endAccID` are the `accID` identifiers for the starting and ending `IAccessible` elements, and `startIndex` and `endIndex` are zero-based indexes into the text of those `IAccessible` objects.

```
LRESULT selectText(
long startAccID,
long startIndex,
long endAccID,
long endIndex);
```

<a id="99842"></a>
## Identifying IAccessible objects in a document

You can identify the type of an `IAccessible` object by using the `get_accRole` method to get its Role attribute. However, you must also distinguish individual objects from others of the same type. You can do this by means of a unique identifier (UID) defined by Acrobat.

The `IAccessible` objects defined by Acrobat export a private interface, `IAccID` , defined in the file `IAccID.h`.  It contains one function, `get_accID`.  Use this UID to determine when two `IAccessible` objects refer to the same element in the document.

When a value-change notification or a focus notification has a non-zero `childID` , the value of `childID` is the UID of one of the objects on the page or document. Use the UID to uniquely identify the object that is the target of the notification.

### get\_accID

Returns an identifier that is unique within the open document or page.

```
HRESULT get_accID(long *id);
```

**Parameters**

**Returns**

Always returns `s_ok`.

**Example**

```
IAccID *pID;
 long uid;
 /* query for the IAccID interface */
 RESULT hr = pObj->QueryInterface (IID_IAccID,
                                         reinterpret_cast<void **>(&pID));
 if (!FAILED(hr))
 {
         pID->get_accID(&uid);
         pID->Release();
 }
```

> **Note**
>
> If you obtained the `IAccessible` object via a call to `AccessibleObjectFrom` XXX, it is not possible to query directly for this private interface. In that case, you must use this alternate code:

```
IServiceProvider *sp = NULL;
 hr = n->QueryInterface(IID_IServiceProvider, (LPVOID*)&sp);
 if (SUCCEEDED(hr) && sp) {
         hr = sp->QueryService(SID_AccID, IID_IAccID, (LPVOID*)&pID);
         sp->Release();
 }
```

<a id="29922"></a>
## IAccessible method summary

This section provides a brief syntax summary of the `IAccessible` interface methods as defined by MSAA. All methods return `HRESULT`.  The methods and properties are organized into the following groups:

- [Navigation and hierarchy](MSAA&PDF.md#73526)
- [Descriptive properties and methods](MSAA&PDF.md#89440)
- [Selection and focus](MSAA&PDF.md#22290)
- [Spatial mapping](MSAA&PDF.md#57514)

<a id="73526"></a>
## Navigation and hierarchy

This section provides information on the APIs used in navigation and to traverse the hierarchy.

### accNavigate

Traverses to another user interface element within a container and retrieves the object. All visual objects support this method.

```
accNavigate (long navDir, VARIANT varStart, VARIANT* pvarEnd);
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accChild

Retrieves an `IDispatch` interface pointer for the specified child, if one exists. All objects support this property.

```
get_accChild (VARIANT varChildID, IDispatch** ppdispChild);
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accChildCount

Retrieves the number of children that belong to this object. All objects support this property.

```
get_accChildCount (long* pcountChildren);
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accParent

Retrieves an `IDispatch` interface pointer for the parent of this object. All objects support this property.

```
get_accParent (IDispatch** ppdispParent);
```

**Properties**

**Returns**

```
HRESULT
```

<a id="89440"></a>
## Descriptive properties and methods

This section provides information on the descriptive APIs.

### accDoDefaultAction

Performs the object’s default action. Not all objects have a default action.

```
accDoDefaultAction (VARIANT varID);
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accDefaultAction

Retrieves a string that describes the object’s default action. Not all objects have a default action.

```
get_accDefaultAction(VARIANT varID, BSTR* pszDefaultAction);
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accDescription

Retrieves a string that describes the visual appearance of the object. Not all objects have a description.

```
get_accDescription (VARIANT varID, BSTR* pszDescription);
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accName

Retrieves the name of the object. All objects have a name.

```
get_accName (VARIANT varID, BSTR* pszName );
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accRole

Retrieves the role of the object. All objects have a role.

```
get_accRole (VARIANT varID, VARIANT* pvarRole );
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accState

Retrieves the state of the object. All objects have a state.

```
get_accState (VARIANT varID, VARIANT* pvarState );
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accValue

Retrieves the value of the object. Not all objects have a value.

```
get_accValue (VARIANT varID, BSTR* pszValue );
```

**Properties**

**Returns**

```
HRESULT
```

<a id="22290"></a>
## Selection and focus

This section provides information on the selection and focus APIs.

### accSelect

Modifies the selection or moves the keyboard focus of the object. All objects that support selection or receive the keyboard focus support this method.

```
accSelect (long flagsSelect, VARIANT varID);
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accFocus

Retrieves the object that has the keyboard focus. All objects that receive the keyboard focus support this property.

```
get_accFocus (VARIANT* pvarID);
```

**Properties**

**Returns**

```
HRESULT
```

### get\_accSelection

Retrieves the selected children of the object. All objects that support selection support this property.

```
get_accSelection (VARIANT* pvarChildren);
```

**Properties**

**Returns**

```
HRESULT
```

<a id="57514"></a>
## Spatial mapping

### accLocation

Retrieves the object’s current screen location. All visual objects support this method.

```
accLocation (long* pxLeft, long* pyTop, long* pcxWidth, long* pcyHeight, VARIANT varID );
```

**Properties**

**Returns**

```
HRESULT
```

### accHitTest

Retrieves the object at a specific screen location. All visual objects support this method.

```
accHitTest (long, long, VARIANT* pvarID);
```

**Properties**

**Returns**

```
HRESULT
```

<a id="88342"></a>
## IAccessible object types for PDF

This section describes the MSAA `IAccessible` object types that are defined to represent PDF documents and their elements. For each object, its methods are listed along with notes on how the implementation is specific to the object type.

> **Note**
>
> Methods that are not listed are not implemented for a given object type.

The objects are:

- [PDF Document](MSAA&PDF.md#39396)
- [PDF Page](MSAA&PDF.md#89992)
- [PDF Protected Document](MSAA&PDF.md#72837)
- [Empty PDF Document](MSAA&PDF.md#10863)
- [PDF Structure Element](MSAA&PDF.md#77828)
- [PDF Content Element](MSAA&PDF.md#23328)
- [PDF Comment](MSAA&PDF.md#22500)
- [PDF Link](MSAA&PDF.md#55866)
- [PDF Text Form Field](MSAA&PDF.md#40546)
- [PDF Button Form Field](MSAA&PDF.md#91493)
- [PDF CheckBox Form Field](MSAA&PDF.md#13511)
- [PDF RadioButton Form Field](MSAA&PDF.md#19394)
- [PDF ComboBox Form Field](MSAA&PDF.md#25792)
- [PDF List Box Form Field](MSAA&PDF.md#20747)
- [PDF Digital Signature Form Field](MSAA&PDF.md#91488)
- [PDF Caret](MSAA&PDF.md#49405)

The following are some general notes:

- PDF form fields generally correspond closely to standard user interface elements described in the MSAA SDK document. The `IAccessible` objects of form fields attempt to match the behavior described in Appendix A, “Supported User Interface Elements,” of the MSAA document. An exception is the PDF combo box, which has a much simpler structure.
- Form fields, links, and comments, as well as the document as a whole, can take keyboard focus. Subparts of the document (sections, paragraphs, and so on) cannot take focus.
- A document’s contents may be only partially visible on the screen. The `get_accLocation` method for a given object returns the screen location of the visible part of the object only. You can use this method to determine which portions of the content are visible.

<a id="39396"></a>
### PDF Document

Represents the contents of an entire PDF document. The subtree of `IAccessible` objects beneath the PDF Document object reflects the logical structure of the document.

> **Note**
>
> Content that is not part of the logical structure, such as page headers and footers, is not presented through the MSAA interface.

| Method | Implementation notes |
| --- | --- |
| accHitTest | Returns the object at a given location if the location is within the document’s bounding box. |
| accLocation | Returns the screen coordinates of the visible part of the document. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | For `SELFLAG_TAKEFOCUS` , the focus is set to the window containing the document and the document is positioned at the beginning. The other `SELFLAG` values are not supported. |
| get\_accChild | Returns a child object. |
| get\_accChildCount | Returns the number of child objects beneath this one. |
| get\_accDescription | The description contains the full path name of the document and the number of pages it contains: “fileName, XXX pages”. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accParent | The parent is `NULL`. |
| get\_accRole | The role is `ROLE_SYSTEM_DOCUMENT`. |
| get\_accSelection | Returns `NULL`. |
| get\_accState | The state is `STATE_SYSTEM_READONLY`. |
| get\_accValue | If the root of the structure tree has an `Alt` attribute, the value is the contents of the `Alt` attribute. |

<a id="89992"></a>
### PDF Page

Represents the contents of one page of a PDF document. The subtree of `IAccessible` objects beneath the PDF Page node reflects the logical structure of the page.

> **Note**
>
> Content that is not part of the logical structure, such as page headers and footers, is not presented through the MSAA interface.

| Method | Implementation notes |
| --- | --- |
| accHitTest | Returns the object at the given location if the location is within the page’s bounding box. |
| accLocation | Returns the screen coordinates of the visible part of the page. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | For `SELFLAG_TAKEFOCUS` , the focus is set to the window containing the page and the page is positioned at the top. The other `SELFLAG` values are not supported. |
| get\_accChild | Returns a child object. |
| get\_accChildCount | Returns the number of child objects beneath this one. |
| get\_accDescription | The description contains the full path name of the document and the page number of the page: “fileName, page XXX”. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accParent | The parent is `NULL`. |
| get\_accRole | A custom role, `Page` , is defined for this object. |
| get\_accSelection | Returns `NULL`. |
| get\_accState | The state is `STATE_SYSTEM_READONLY`. |
| get\_accValue | If the root of the structure tree has an `Alt` attribute, the value is the contents of the `Alt` attribute |

<a id="72837"></a>
### PDF Protected Document

Represents a protected document. When the permissions associated with a document disable accessibility, the contents are not exported through the MSAA interface. The `IAccessible` object for such a document informs the client that the document is protected.

| Method | Implementation notes |
| --- | --- |
| accHitTest | Returns `NULL`. |
| accLocation | The screen coordinates of the visible part of the document. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Returns `NULL`. |
| get\_accChildCount | The child count is 0. |
| get\_accFocus | Returns `NULL`. |
| get\_accName | The name is “Alert: Protection Failure”. |
| get\_accParent | The parent is `NULL`. |
| get\_accRole | The role is `ROLE_SYSTEM_TEXT`. |
| get\_accSelection | Returns `NULL`. |
| get\_accState | The state is `STATE_SYSTEM_ALERT_MEDIUM + STATE_SYSTEM_UNAVAILABLE + STATE_SYSTEM_READONLY`. |
| get\_accValue | The value is “This document’s security settings prevent access.” |

<a id="10863"></a>
### Empty PDF Document

Represents an empty or apparently empty document. A PDF file may have no contents to export through MSAA if, for instance, the file is a scanned image that has not been run through an optical character recognition (OCR) tool. The `IAccessible` object for empty documents and pages informs the client that there may be a problem, even if the document or page is genuinely empty.

| Method | Implementation notes |
| --- | --- |
| accHitTest | Returns `NULL`. |
| accLocation | Returns the screen coordinates of the visible part of the document. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Returns `NULL`. |
| get\_accChildCount | The child count is 0. |
| get\_accFocus | Returns `NULL`. |
| get\_accName | The name is “Alert: Empty document”. |
| get\_accParent | The parent is `NULL`. |
| get\_accRole | The role is `ROLE_SYSTEM_TEXT`. |
| get\_accSelection | Returns `NULL`. |
| get\_accState | The state is `STATE_SYSTEM_READONLY`. |
| get\_accValue | The value is “This document appears to be empty. It may be a scanned image that needs OCR or it may have malformed structure.” |

<a id="77828"></a>
### PDF Structure Element

Represents a subtree of the logical structure tree for the document. It might correspond to a paragraph, a heading, a chapter, a span of text within a word, or a figure.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | If the element has state `STATE_SYSTEM_LINKED` , performs the action associated with the link. |
| accHitTest | Returns this object or any child at the given location if the location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the subtree. |
| accNavigate | Only spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ) is supported for table elements (`ROLE_SYSTEM_CELL` , `ROLE_SYSTEM_ROW` , `ROLE_SYSTEM_ROWHEADER` , `ROW_SYSTEM_COLUMNHEADER` ). |
| accSelect | For `SELFLAG_TAKEFOCUS` , sets focus to the document window and positions the document to the beginning of the structure element content. The other `SELFLAG` values are not supported. |
| get\_accChild | Returns a child object. |
| get\_accChildCount | Returns the number of child objects beneath this one.<br><br>If the node has an `Alt` or `ActualText` attribute, the child count is always zero. |
| get\_accDefaultAction | If the element has state `STATE_SYSTEM_LINKED` , returns a text description of the action associated with the link (such as “go to page 5” or “play movie”). |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accParent | The parent is either another structure element or the document structure root. |
| get\_accRole | The role is one of:<br><br>ROLE\_SYSTEM\_GROUPINGROLE\_SYSTEM\_TABLE<br>ROLE\_SYSTEM\_CELL<br>ROLE\_SYSTEM\_ROW<br>ROLE\_SYSTEM\_ROWHEADER<br><br>ROW\_SYSTEM\_COLUMNHEADER |
| get\_accSelection | Returns `NULL`. |
| get\_accState | The state is a logical OR of one or more of the following:<br><br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_LINKED<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_FOCUSED<br><br>- `STATE_SYSTEM_READONLY` is always set.<br>- If the element is part of a link (that is, if it has an ancestor of role `ROLE_SYSTEM_LINK` ) then both `STATE_SYSTEM_LINKED` and `STATE_SYSTEM_FOCUSABLE` are set, and `STATE_SYSTEM_FOCUSED` can also be set. |
| get\_accValue | If this node has an `Alt` or `ActualText` attribute, the value is the contents of the attribute. |

<a id="23328"></a>
### PDF Content Element

Corresponds to a leaf node of the logical structure tree for the document. It corresponds to marking commands in the page content stream.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | If the element has state `STATE_SYSTEM_LINKED` , performs the action associated with the link. |
| accHitTest | Returns this object if the given location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the element. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | For `SELFLAG_TAKEFOCUS` , sets focus to the document window and positions the document to the beginning of the content. The other `SELFLAG` values are not supported. |
| get\_accChildCount | The child count is 0. |
| get\_accDefaultAction | If the element has state `STATE_SYSTEM_LINKED` , describes the action associated with the link. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accParent | The parent is either a structure element or the document structure root. |
| get\_accRole | The role is one of:<br><br>ROLE\_SYSTEM\_TEXT<br><br>ROLE\_SYSTEM\_GRAPHIC<br><br>ROLE\_SYSTEM\_CLIENT |
| get\_accSelection | Returns `NULL`. |
| get\_accState | The state is a logical OR of one or more of the following:<br><br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_LINKED<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_FOCUSED<br><br>- `STATE_SYSTEM_READONLY` is always set.<br>- If the element is part of a link (that is, if it has an ancestor of role `ROLE_SYSTEM_LINK` ) then both `STATE_SYSTEM_LINKED` and `STATE_SYSTEM_FOCUSABLE` are set, and `STATE_SYSTEM_FOCUSED` can also be set. |
| get\_accValue | If this node has an `Alt` or `ActualText` attribute, the value is the content of that attribute. Otherwise, the value is all of the text contained in the marking commands for this node. |

<a id="22500"></a>
### PDF Comment

Corresponds to a comment, such as a text note or highlight comment, attached to the document.

> **Note**
>
> PDF comments cover a range of objects, many of which do not map into the standard MSAA roles. The `IAccessible` object captures the most important properties of comments.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | The default action depends on the type of comment. It can, for example, open or close a popup. |
| accHitTest | Returns this object if the given location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the object. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Supports `SELFLAG_TAKEFOCUS` (that is, selecting the comment gives it the keyboard focus). |
| get\_accChildCount | The child count is 0. |
| get\_accDefaultAction | Describes the default action, which depends on the type of comment. |
| get\_accDescription | For file attachment and sound comments, a description of the icon for the comment. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | - The name indicates the type of comment; for example, Text Comment or Underline Comment.<br>- If the comment is open and has a title, the name also contains the title of the comment.<br>- If the comment is a Free Text comment or modifies a span of text (such as an Underline or Strikeout Comment), the name also contains the text. |
| get\_accParent | The parent is either a structure element or the document structure root. |
| get\_accRole | The role is one of:<br><br>ROLE\_SYSTEM\_TEXT<br><br>ROLE\_SYSTEM\_WHITESPACE<br><br>ROLE\_SYSTEM\_PUSHBUTTON |
| get\_accSelection | Returns `NULL`. |
| get\_accState | The state is a logical OR of one or more of the following:<br><br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_INVISIBLE<br>- STATE\_SYSTEM\_LINKED<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_EXPANDED<br>- STATE\_SYSTEM\_COLLAPSED<br>- STATE\_SYSTEM\_FOCUSED<br><br>- If a comment can be opened, `STATE_SYSTEM_LINKED` is set.<br>- `STATE_SYSTEM_EXPANDED` and `STATE_SYSTEM_COLLAPSED` indicate whether the comment is open. |
| get\_accValue | - If the comment is open, the value is the contents of the comment pop-up window.<br>- If the comment is a type that does not open, the value is the contents of the comment itself. |

<a id="55866"></a>
### PDF Link

Corresponds to a link in the document.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | Performs the link’s action. |
| accHitTest | Returns this object or any child at the given location if the location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the object. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Supports `SELFLAG_TAKEFOCUS` |
| get\_accChild | Returns a child object. |
| get\_accChildCount | Returns the number of children. If the node has an `Alt` or `ActualText` attribute, the child count is always zero. |
| get\_accDefaultAction | Describes the action defined for this link. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | If there is an `Alt` or `ActualText` attribute associated with this link, the name is the associated `Alt` text or `ActualText`.  Otherwise, the name is the value of the first content child. |
| get\_accParent | The parent is either a structure element or the document structure root. |
| get\_accRole | The role is `ROLE_SYSTEM_LINK`. |
| get\_accSelection | Returns `NULL`. |
| get\_accState | The state is a logical OR of the following:<br><br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_INVISIBLE<br>- STATE\_SYSTEM\_LINKED<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_FOCUSED |
| get\_accValue | The value is a unique identifier for each link. |

<a id="40546"></a>
### PDF Text Form Field

Corresponds to a text form field in the document.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | Sets focus to the text field for editing. |
| accHitTest | Returns this object if the given location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the object. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Supports `SELFLAG_TAKEFOCUS` (that is, selecting the field gives it the keyboard focus). |
| get\_accChildCount | The child count is 0. |
| get\_accDefaultAction | The default action is “DoubleClick”, which sets the keyboard focus to this field. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | The user name (short description) of the form field. |
| get\_accParent | Returns the parent object. |
| get\_accRole | The role is `ROLE_SYSTEM_TEXT`. |
| get\_accState | The state of the text field is a logical OR of one of more of:<br><br>- STATE\_SYSTEM\_INVISIBLE<br>- STATE\_SYSTEM\_UNAVAILABLE<br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_SELECTABLE<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_FOCUSED<br>- STATE\_SYSTEM\_PROTECTED |
| get\_accValue | The value is the text in the text field. |

<a id="91493"></a>
### PDF Button Form Field

Corresponds to a button form field in the document.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | Presses the button. |
| accHitTest | Returns this object if the given location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the object. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Supports `SELFLAG_TAKEFOCUS` (that is, selecting the field gives it the keyboard focus). |
| get\_accChildCount | The child count is 0. |
| get\_accDefaultAction | The default action is “Press”. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | The user name of the form field (short description). |
| get\_accParent | Returns the parent object. |
| get\_accRole | The role is `ROLE_SYSTEM_PUSHBUTTON`. |
| get\_accState | The state of the button is a logical OR of one or more of:<br><br>- STATE\_SYSTEM\_INVISIBLE<br>- STATE\_SYSTEM\_UNAVAILABLE<br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_FOCUSED |

<a id="13511"></a>
### PDF CheckBox Form Field

Corresponds to a checkbox form field in the document.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | Checks or unchecks the box. |
| accHitTest | Returns this object if the given location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the object. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Supports `SELFLAG_TAKEFOCUS` (that is, selecting the field gives it the keyboard focus). |
| get\_accChildCount | The child count is 0. |
| get\_accDefaultAction | - If the check box has been selected, the default action is “UnCheck”.<br>- If the check box has not been selected, the default action is “Check”. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | The user name (short description) of the form field. |
| get\_accParent | Returns the parent object. |
| get\_accRole | The role is `ROLE_SYSTEM_CHECKBUTTON`. |
| get\_accState | The state of the check box is a logical OR of one or more of:<br><br>- STATE\_SYSTEM\_INVISIBLE<br>- STATE\_SYSTEM\_UNAVAILABLE<br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_FOCUSED<br>- STATE\_SYSTEM\_CHECKED |

<a id="19394"></a>
### PDF RadioButton Form Field

Corresponds to a radio button form field in the document.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | Clicks the radio button. |
| accHitTest | Returns this object if the given location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the object. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Supports `SELFLAG_TAKEFOCUS` (that is, selecting the field gives it the keyboard focus). |
| get\_accChildCount | The child count is 0. |
| get\_accDefaultAction | The default action is “Check”. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | The user name (short description) of the form field. |
| get\_accParent | Returns the parent object. |
| get\_accRole | The role is `ROLE_SYSTEM_RADIOBUTTON`. |
| get\_accState | The state of the radio button is a logical OR of one or more of:<br><br>- STATE\_SYSTEM\_INVISIBLE<br>- STATE\_SYSTEM\_UNAVAILABLE<br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_FOCUSED<br>- STATE\_SYSTEM\_CHECKED |

<a id="25792"></a>
### PDF ComboBox Form Field

Corresponds to a combo box form field in the document. It can represent either the combo box itself, or a list item in a combo box.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | - The combo box does not have a default action.<br>- For a list item, the default action is “DoubleClick”, which selects the list item. |
| accHitTest | - For a combo box, returns this object or any child at the given location if the location is within the bounding box of this object.<br>- For a list item, returns this object if the given location is within the bounding box of this object. |
| accLocation | - For a combo box, returns the screen coordinates of the visible part of the object.<br>- For a list item, the location is always reported as 0,0,0,0. |
| accNavigate | - Spatial directions `NAVDIR_UP` and `NAVDIR_DOWN` are available for list items. |
| accSelect | - The combo box supports `SELFLAG_TAKEFOCUS` (that is, selecting the field gives it the keyboard focus).<br>- For a list item, sets the combo box to the list item value. |
| get\_accChild | - For a combo box, gets the child items.<br>- A list item has no children. |
| get\_accChildCount | - For a combo box, the child count is the number of items in the list.<br>- For a list item, the child count is 0. |
| get\_accDefaultAction | - The combobox does not have a default action.<br>- For a list item, the default action is “DoubleClick”, which selects the list item. |
| get\_accFocus | - Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | - For a combo box, the name is the user name (short description) of the form field if it has been defined.<br>- For a list item, the name is the text of the list item. |
| get\_accParent | - Returns the parent object. |
| get\_accSelection | - Returns `NULL`. |
| get\_accRole | - For a combo box, the role is `ROLE_SYSTEM_COMBOBOX`.<br>- For a list item, the role is `ROLE_SYSTEM_LISTITEM`. |
| get\_accState | - For a combo box, the state is a logical OR of one or more these values:<br>  - STATE\_SYSTEM\_INVISIBLE<br>  - STATE\_SYSTEM\_UNAVAILABLE<br>  - STATE\_SYSTEM\_READONLY<br>  - STATE\_SYSTEM\_FOCUSABLE<br>  - STATE\_SYSTEM\_FOCUSED<br>  - STATE\_SYSTEM\_SELECTABLE<br>  - STATE\_SYSTEM\_SELECTED<br>- For a list box item, the state is a logical OR of one or more these values:- STATE\_SYSTEM\_READONLY<br>  - STATE\_SYSTEM\_SELECTABLE<br>  - STATE\_SYSTEM\_SELECTED<br>  - STATE\_SYSTEM\_INVISIBLE<br>  - STATE\_SYSTEM\_UNAVAILABLE |
| get\_accValue | - For a combo box, the value is the text value of the currently selected list item.<br>- For a list item, the value is the text of the list item. |

<a id="20747"></a>
### PDF List Box Form Field

Corresponds to a list box form field in the document. It can represent either the list box itself or a list item in a list box.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | - The list box does not have a default action.<br>- For a list item, the default action is “Double Click,” which selects the item. |
| accHitTest | - For a list box, returns this object or any child at the given location if the location is within the bounding box of this object.<br>- For a list item, returns this object if the given location is within the bounding box of this object. |
| accLocation | - For a list box, returns the screen coordinates of the visible part of the object.<br>- For a list item, the location is always reported as 0,0,0,0. |
| accNavigate | - Spatial directions `NAVDIR_UP` and `NAVDIR_DOWN` are available for list items. |
| accSelect | - The list box supports `SELFLAG_TAKEFOCUS` (that is, selecting the field gives it the keyboard focus).<br>- For a list item, sets the list box selection to the list item value. |
| get\_accChild | - For a list box, gets the child items.<br>- A list item has no children. |
| get\_accChildCount | - For a list box, the child count is the number of items in the list box.<br>- For a list item, the child count is 0. |
| get\_accDefaultAction | - The list box does not have a default action.<br>- For a list item, the default action is “Double Click,” which selects the item. |
| get\_accFocus | - Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | - For a list box, the name is the user name (short description) for the form field.<br>- For a list item, the name is the text of the list item. |
| get\_accParent | - Returns the parent object. |
| get\_accRole | - For a list box, the role is `ROLE_SYSTEM_LIST`.<br>- For a list item, the role is `ROLE_SYSTEM_LISTITEM`. |
| get\_accState | - For a list box, the state is a logical OR of one or more these values:<br>  - STATE\_SYSTEM\_INVISIBLEc<br>  - STATE\_SYSTEM\_UNAVAILABLE<br>  - STATE\_SYSTEM\_READONLY<br>  - STATE\_SYSTEM\_FOCUSABLE<br>- For a list item, the state is a logical OR of one or more these values:<br>  - STATE\_SYSTEM\_READONLY<br>  - STATE\_SYSTEM\_SELECTABLE<br>  - STATE\_SYSTEM\_SELECTED<br>  - STATE\_SYSTEM\_INVISIBLE<br>  - STATE\_SYSTEM\_UNAVAILABLE |
| get\_accSelection | - Returns `NULL`. |
| get\_accValue | - For a list box, the value is the text value of the currently selected list item.<br>- For a list item, the `Value` attribute is the text of the list item. |

<a id="91488"></a>
### PDF Digital Signature Form Field

Corresponds to a digital signature form field in the document.

| Method | Implementation notes |
| --- | --- |
| accDoDefaultAction | Signs the document if the signature field is unsigned and has either been opened with Acrobat or the document has permissions that allow signing. If the document is signed, the default action brings up a dialog box containing the signature information. |
| accHitTest | Returns this object if the given location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the visible part of the object. |
| accNavigate | Does not support spatial navigation (`NAVDIR_UP` , `NAVDIR_DOWN` , `NAVDIR_RIGHT` , `NAVDIR_LEFT` ). |
| accSelect | Supports `SELFLAG_TAKEFOCUS`. |
| get\_accChildCount | The child count is 0. |
| get\_accDefaultAction | Returns `NULL`. |
| get\_accFocus | Returns the object that has the keyboard focus if it is this object or its child. |
| get\_accName | The user name (short description) of the form field. |
| get\_accParent | Returns the parent object. |
| get\_accRole | The Digital Signature form field does not map to any of the existing roles, and a custom role, `Signature` , has been defined for it. |
| get\_accState | The `State` attribute of the digital signature is a logical OR of one of more of these values:<br><br>- STATE\_SYSTEM\_INVISIBLE<br>- STATE\_SYSTEM\_UNAVAILABLE<br>- STATE\_SYSTEM\_READONLY<br>- STATE\_SYSTEM\_FOCUSABLE<br>- STATE\_SYSTEM\_FOCUSED<br>- STATE\_SYSTEM\_CHECKED<br>- STATE\_SYSTEM\_TRAVERSED<br><br>- If `STATE_SYSTEM_CHECKED` is set, but not `STATE_SYSTEM_TRAVERSED` , the signature is unverified.<br>- If `STATE_SYSTEM_TRAVERSED` is set, but not `STATE_SYSTEM_CHECKED` , the signature is invalid.<br>- If both `STATE_SYSTEM_CHECKED` and `STATE_SYSTEM_TRAVERSED` are set, the signature is valid. |
| get\_accValue | The `Value` attribute is the name and date of the signature, if that information is present. |

<a id="49405"></a>
### PDF Caret

Represents a caret (text cursor). If a document contains the system caret because focus is within an editable text field or an editable ComboBox field, clients can obtain an `IAccessible` object for the caret to determine where it is located.

| Method | Implementation notes |
| --- | --- |
| accHitTest | Returns this object if the given location is within the bounding box of this object. |
| accLocation | Returns the screen coordinates of the caret, both when the caret is in a form field and when it is in the document. |
| get\_accChildCount | The child count is 0. |
| get\_accDescription | The description is a string containing the index of the character in the field that follows the caret.<br><br>If the caret is at the beginning of the field, the description string is “0”. If the caret follows the first character, the description string is “1”. |
| get\_accParent | The parent is the field containing the caret. However, the caret `IAccessible` object is not listed among the children of that field’s `IAccessible` object. |
| get\_accRole | The role is `ROLE_SYSTEM_CARET`. |
| get\_accState | The state is 0. |
| get\_accValue | The value is the current value of the Text field or ComboBox form field containing the caret. |
