---
layout: page
title: Localized Descriptions (Labels)
permalink: /help-directory/
---

The localized descriptions for metadata schema elements are stored in the **loc** directory under **labels.xml** files. These files provide human-readable names and descriptions for XML elements, enabling metadata applications to display user-friendly interfaces to metadata editors.

## Overview

### Purpose
- Provide human-readable labels for XML elements
- Supply descriptions and help text for metadata editors
- Offer suggestions for element content
- Support multiple languages
- Replace technical XML names with domain-specific terminology

### Organization
In modern GeoNetwork schema plugins, localized information is organized as follows:
- **Base Directory**: `/loc/`
- **Language Subdirectories**: `/loc/<language-code>/` (e.g., `/loc/eng/`, `/loc/fra/`, `/loc/spa/`)
- **Files**:
  - `labels.xml` - Element names, descriptions, and helper suggestions
  - `codelists.xml` - Controlled vocabulary definitions and localized values
  - `strings.xml` - Other localized strings and messages

## Directory Structure

```
loc/
├── eng/
│   ├── labels.xml
│   ├── codelists.xml
│   └── strings.xml
├── fra/
│   ├── labels.xml
│   ├── codelists.xml
│   └── strings.xml
└── spa/
    ├── labels.xml
    ├── codelists.xml
    └── strings.xml
```

## Labels.xml Format

The `labels.xml` file contains structured information about metadata elements. Each element description includes multiple components:

### Element Structure
```xml
<element name="gmd:elementName" id="1.0">
  <label>Human Readable Label</label>
  <description>Detailed description of the element's purpose and content</description>
  <helper>
    <option value="actual_value">Display Label</option>
    <option value="another_value">Another Display Label</option>
  </helper>
  <condition>Optional XPath condition for when element applies</condition>
</element>
```

### Components

#### `name` Attribute
- The XML element name including namespace prefix (e.g., `gmd:credit`)
- Uniquely identifies the element within the schema
- Must match the actual element name in the XSD

#### `id` Attribute
- Optional unique identifier for the element
- Useful for tracking and organizing descriptions
- Convention: Use numeric IDs like `1.0`, `1.1`, etc.

#### `label` Element
- A human-readable name for the element
- Replaces the technical XML tag name in user interfaces
- Example: `"Credit"` instead of `"gmd:credit"`
- Should be concise and understandable to domain users

#### `description` Element
- Detailed explanation of the element's purpose
- Provides context for metadata editors
- May include examples and best practices
- Can contain multiple lines for comprehensive documentation

#### `helper` Element (Optional)
- Suggests predefined values for the element
- Displays as dropdown/select lists in editors
- Contains `<option>` sub-elements with:
  - `value`: The actual value to insert into the metadata
  - Element content: Display label shown to user

#### `condition` Element (Optional)
- XPath expression defining when the element applies
- Enables conditional visibility in editors
- Example: Element only appears if parent element has certain value

## Complete Example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<labels>
  <element name="gmd:credit" id="27.0">
    <label>Credit</label>
    <description>Recognition of those who contributed to the resource(s). 
      Include names and affiliations of organizations or individuals who 
      played significant roles in developing or providing the resource.</description>
    <helper>
      <option value="University of Tasmania">UTAS</option>
      <option value="University of Queensland">UQ</option>
      <option value="CSIRO">CSIRO</option>
    </helper>
  </element>

  <element name="gmd:abstract" id="28.0">
    <label>Abstract</label>
    <description>Brief narrative summary of the content of the resource. 
      The abstract should be informative, describing the key aspects, 
      spatial and temporal coverage, and main findings of the resource.</description>
  </element>

  <element name="gmd:keyword" id="29.0">
    <label>Keywords</label>
    <description>Commonly used abbreviations or words that define the subject matter 
      of the resource. Keywords are used for indexing and searching metadata records.</description>
    <condition>gmd:descriptiveKeywords/gmd:MD_Keywords</condition>
  </element>

  <element name="gmd:MD_TopicCategoryCode" id="30.0">
    <label>Topic Category</label>
    <description>Main theme or subject of the dataset. Topic categories help 
      organize and classify metadata records by their primary subject area.</description>
    <helper>
      <option value="farming">Farming</option>
      <option value="biota">Biota</option>
      <option value="boundaries">Boundaries</option>
      <option value="climatologyMeteorologyAtmosphere">Climate and Meteorology</option>
      <option value="elevation">Elevation</option>
      <option value="environment">Environment</option>
      <option value="geoscientificInformation">Geoscience</option>
      <option value="health">Health</option>
      <option value="imageryBaseMapsEarthCover">Imagery and Base Maps</option>
      <option value="inlandWaters">Inland Waters</option>
      <option value="location">Location</option>
      <option value="oceans">Oceans</option>
      <option value="planningCadastre">Planning and Cadastre</option>
      <option value="society">Society</option>
      <option value="structure">Structure</option>
      <option value="transportation">Transportation</option>
      <option value="utilitiesCommunication">Utilities and Communication</option>
    </helper>
  </element>
</labels>
```

## Profile-Specific Labels

For profiles of base schemas:
- **Include only profile-specific elements** in the profile's `labels.xml`
- Labels for base schema elements are inherited from the base schema
- Override base schema labels by defining them in the profile's `labels.xml`
- Use the same element names and structure as the base schema

### Profile Example
If your schema is a profile of ISO19115/19139, include only new or modified elements:

```xml
<labels>
  <!-- Profile-specific extension -->
  <element name="mcp:revisionDate" id="100.0">
    <label>Revision Date</label>
    <description>Date on which the metadata record was last revised or updated</description>
  </element>

  <!-- Override base schema element -->
  <element name="gmd:title" id="101.0">
    <label>Title (Profile Version)</label>
    <description>Profile-specific guidance on creating descriptive titles...</description>
  </element>
</labels>
```

### Best Practices for Labels

1. **Clarity**: Use clear, domain-specific terminology that users understand
2. **Consistency**: Use consistent labeling across related elements
3. **Brevity**: Keep labels short (typically 2-4 words)
4. **Completeness**: Provide descriptions that explain the element's purpose and usage
5. **Examples**: Include examples in descriptions when helpful
6. **Localization**: Provide translations for all languages you support
7. **Validation**: Ensure all elements in your schema have corresponding labels
8. **Maintenance**: Keep labels up-to-date as your schema evolves

## Codelists and Strings Files

While this page focuses on `labels.xml`, the same directory structure contains related files:

- **codelists.xml**: Defines controlled vocabulary values with localized labels and descriptions
- **strings.xml**: Contains other localized strings used in error messages, help text, and UI elements

All three files follow similar localization patterns and are organized by language subdirectory.

## References

- [GeoNetwork Localization Guide](https://docs.geonetwork-opensource.org/4.2/customizing-application/implementing-a-schema-plugin/#creating-the-localized-strings-in-the-loc-directory)
- [GeoNetwork Schema Plugin Structure](https://docs.geonetwork-opensource.org/4.2/customizing-application/implementing-a-schema-plugin/#contents-of-a-geonetwork-schema)
- [ISO19115 Metadata Elements](http://www.isotc211.org/)