# Searching and Indexing

With Acrobat and the Acrobat SDK, you can use the Search plug-in to locate an occurrence of a word in document content, metadata, attachments or other objects. You can use the Catalog plug-in to create a full-text index of a PDF document or document collection. This chapter summarizes these plug-ins.

<a id="72992"></a>
## Search plug-in

With Acrobat, Adobe provides a full-text search system. Using the Acrobat search system, you can perform the following tasks:

- Initiate a search with options. You can pass query expressions and search settings (for example, whole words only, word stemming, case sensitive, and so forth) to the Acrobat search plug-in and initiate the search. Search results will be presented to the user.
- Control the list of indexes to search. The search interface allows searches to be performed on one or more of the available indexes. You can control the list of active indexes.

The Acrobat Search plug-in allows users to perform text searches in PDF documents. It adds menus, menu items, toolbar buttons, and a Search panel to Acrobat or Acrobat Reader.

You can communicate with the Search plug-in through its plug-in API, IAC (DDE or Apple events) or JavaScript. You can perform all search options from each of these development environments.

The Acrobat Search plug-in provided with Acrobat is a true Acrobat plug-in. You can remove it from the system by simply removing it from the Plug-ins directory and restarting Acrobat.

<a id="61573"></a>
## Indexes and the Catalog plug-in

You can use the Acrobat SDK to create a full-text index of a set of PDF documents. A full-text index is a searchable database of all the text in the documents. After building an index, you can use search the entire library quickly. You can build and manipulate indexes from a plug-in, through JavaScript, or from an external application using IAC (DDE or Apple events) calls.

For indexing PDF files, Acrobat provides text extraction APIs. Text extraction also supplies position information that can be used to highlight search hits in the original PDF file. The text extraction tools are provided as calls in the plug-in API on Windows and Mac OS. You can extract ASCII text from a PDF file using a plug-in or using JavaScript. You can also save the PDF document as text or rich text.

Acrobat Catalog is a plug-in that allows you to create a full-text index of a set of PDF documents. The Catalog plug-in has an HFT consisting of several methods that plug-in developers can import and use. In addition, Catalog supports DDE, and broadcasts several Windows messages.

For more information, see [Acrobat Plugin Developer Guide](http://www.adobe.com/go/acrobatsdk_pluginguide) , [Acrobat and PDF Library API Reference](https://www.adobe.com/go/pdflibrary) , and the [Acrobat JavaScript Developer Guide](http://www.adobe.com/go/acrobatsdk_jsdevguide).
