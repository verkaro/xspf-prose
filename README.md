# XSPF Prose Extension Specification v1

**Namespace URI:** `https://github.com/verkaro/xspf-prose/tree/v1`

## 1. Introduction

This document specifies a method for embedding multi-paragraph, Markdown-formatted prose within an XSPF (XML Shareable Playlist Format) file. It uses the standard XSPF `<extension>` element to ensure that documents using this specification remain fully compliant with the base XSPF v1 standard.

## 2. Specification

The Prose Extension is defined by the following structure within an XSPF `<track>` element.

### 2.1. The Extension Element

  * **Element:** `<extension>`
  * **`application` Attribute:** MUST be `https://github.com/verkaro/xspf-prose/tree/v1`.

### 2.2. The Content Element

  * The `<extension>` element MUST contain one child element in the same namespace.
  * **Element Name:** `<prose:content>` (where `prose` is the prefix mapped to the Namespace URI).
  * **Content:** The content of this element MUST be wrapped in a `<![CDATA[...]]>` section. The character data within this section should be interpreted as Markdown.

## 3. Complete Example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<playlist 
  version="1" 
  xmlns="http://xspf.org/ns/0/"
  xmlns:prose="https://github.com/verkaro/xspf-prose/tree/v1">
  
  <title>Playlist with Embedded Prose</title>
  
  <trackList>
    <track>
      <location>https://archive.org/download/some-track/track.mp3</location>
      <title>A Track with a Story</title>
      <extension application="https://github.com/verkaro/xspf-prose/tree/v1">
        <prose:content>
          <![CDATA[
### The Story of This Track
This prose tells a story about the track and is formatted using Markdown.
          ]]>
        </prose:content>
      </extension>
    </track>
  </trackList>
</playlist>
