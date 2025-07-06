# XSPF Prose Extension Specification v1.1

**Namespace URI:** `https://github.com/verkaro/xspf-prose/tree/v1.1`

## 1. Introduction

This document specifies a method for embedding multi-paragraph, Markdown-formatted prose within an XSPF (XML Shareable Playlist Format) file. It uses the standard XSPF `<extension>` element to ensure that documents using this specification remain fully compliant with the base XSPF v1 standard. Playlists using this extension will be functional in any standard XSPF player, which will safely ignore the extension.

## 2. Conformance

A conforming document MUST use the `<extension>` element with its `application` attribute set to the exact Namespace URI specified above.

## 3. Specification

The Prose Extension is defined by the following structure within an XSPF `<track>` element.

### 3.1. The Extension Element

  * **Element:** `<extension>`
  * **`application` Attribute:** MUST be `https://github.com/verkaro/xspf-prose/tree/v1.1`.

### 3.2. The Content Element

  * The `<extension>` element MUST contain one child element in the same namespace.
  * **Element Name:** `<prose:content>` (where `prose` is the prefix mapped to the Namespace URI).
  * **Content:** The content of this element MUST be wrapped in a `<![CDATA[...]]>` section to prevent parsing errors. The character data within this section should be interpreted as Markdown, preferably compliant with the [CommonMark](https://commonmark.org/) specification.

## 4. Complete Example

Here is a complete, valid XSPF playlist demonstrating the use of the Prose Extension.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<playlist 
  version="1" 
  xmlns="http://xspf.org/ns/0/"
  xmlns:prose="https://github.com/verkaro/xspf-prose/tree/v1.1">
  
  <title>Playlist with Embedded Prose</title>
  
  <trackList>
    <track>
      <location>https://archive.org/download/some-track/track.mp3</location>
      <title>A Track with a Story</title>
      <extension application="https://github.com/verkaro/xspf-prose/tree/v1.1">
        <prose:content>
          <![CDATA[
### The Story of This Track

This is the first paragraph of prose that tells a story about the track. It can contain multiple lines and paragraphs.

* Use lists for key points.
* Use *emphasis* or **bolding** for effect.
* Even include [links](https://example.com) for more information.
          ]]>
        </prose:content>
      </extension>
    </track>
  </trackList>
</playlist>
```

## 5. Implementation Guidance for Parsers

1.  When parsing an XSPF `<track>`, check for an `<extension>` element where the `application` attribute matches the Namespace URI (`https://github.com/verkaro/xspf-prose/tree/v1.1`).
2.  If found, retrieve the string data from the `CDATA` section of its `<prose:content>` child.
3.  Process this string through a standard Markdown renderer before displaying it in the application's user interface.
4.  If the extension is not present, no prose is associated with the track. The UI view for prose should not be displayed.
