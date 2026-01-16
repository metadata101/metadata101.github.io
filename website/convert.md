---
layout: page
title: Metadata Conversion (XSLT)
permalink: /convert/
---


The **convert** directory contains XSLT (Extensible Stylesheet Language Transformation) files that enable conversion of metadata records from one schema to another or to different formats. This component is essential for metadata interoperability and data exchange.

## Overview

### Purpose
- Convert metadata records between different schemas
- Support multiple output formats (ISO19115/19139, Dublin Core, ANDS RIFCS, etc.)
- Support schema version migrations
- Facilitate data exchange with external systems
- Provide fallback conversions to base standards

### XSLT Technology
XSLT is a W3C standard language for transforming XML documents. It provides powerful mechanisms for:
- Mapping element structures between schemas
- Reformatting and restructuring metadata
- Filtering and selecting relevant content
- Creating derived schemas from base schemas

## Directory Structure

### File Organization
```
schema-name/
├── schema-conversions.xml (configuration file - at root level)
├── convert/ (mandatory directory for XSLT files)
│   ├── iso19139.mcp.xsl (profile-specific conversion)
│   ├── iso19139.mcp-1.4.xsl (version-specific conversion)
│   ├── oai_dc.xsl (Dublin Core output)
│   ├── rif.xsl (ANDS RIFCS format)
│   ├── to19139.xsl (base ISO19115/19139)
│   └── other-format.xsl (additional conversions)
└── [other schema components]
```

### Important Notes on Modern GeoNetwork

In modern GeoNetwork versions (4.x):
- The configuration file is named **`schema-conversions.xml`** (not `convert.xml`)
- It is located at the **root level** of the schema plugin directory (not inside convert/)
- The **`convert/` directory is mandatory** in all schema plugins
- All XSLT files are stored within the `convert/` subdirectory

### Naming Conventions
- `<target>-<format>.xsl` or similar descriptive naming for XSLT files
- Examples: `oai_dc.xsl`, `iso19139.xsl`, `dcat.xsl`, `fromISO19139.xsl`

## Schema-Conversions.xml Configuration File

The `schema-conversions.xml` file defines all available conversions and their metadata. It is located at the schema plugin root level.

### Structure
```xml
<?xml version="1.0" encoding="UTF-8"?>
<conversions>
  <converter 
    name="xml_iso19139.mcp"
    nsUri="http://bluenet3.antcrc.utas.edu.au/mcp" 
    schemaLocation="http://bluenet3.antcrc.utas.edu.au/mcp-1.5-experimental/schema.xsd" 
    xslt="iso19139.mcp.xsl" 
  />
  <converter 
    name="xml_iso19139.mcpTooai_dc"
    nsUri="http://www.openarchives.org/OAI/2.0/" 
    schemaLocation="http://www.openarchives.org/OAI/2.0/oai_dc.xsd" 
    xslt="oai_dc.xsl" 
  />
</conversions>
```

### Modern GeoNetwork Implementation

**Important**: In modern GeoNetwork versions (4.x):
- The configuration file is **`schema-conversions.xml`** located at the schema root level
- Previous versions used `convert.xml` inside the `convert/` directory, but this is no longer the standard approach
- The file is **automatically discovered** by GeoNetwork's SchemaManager
- All XSLT files must be in the `convert/` subdirectory
- The `convert/` directory is **mandatory** even if conversions are minimal

### Converter Attributes

#### `name` Attribute
- Unique identifier for this conversion
- Used internally by GeoNetwork to reference the conversion
- **Convention**: Use `xml_<source>To<target>` format (e.g., `xml_iso19139mcpTooai_dc`)
- The `xml_` prefix identifies this as an XML-to-XML transformation service
- Example: `xml_iso19139.mcp`, `xml_iso19139.mcpTooai_dc`, `xml_iso19139.mcpToRIFCS`

#### `nsUri` Attribute
- **Namespace URI**: The primary XML namespace of the output format
- Identifies the schema/format produced by this conversion
- Used for schema detection and validation
- Examples:
  - `http://www.isotc211.org/2005/gmd` (ISO19115/19139)
  - `http://www.openarchives.org/OAI/2.0/` (Dublin Core via OAI-PMH)
  - `http://ands.org.au/standards/rif-cs/registryObjects` (ANDS RIFCS)

#### `schemaLocation` Attribute
- **URL** of the XML Schema Definition (XSD) for the output format
- Tells validating parsers where to find the schema
- Should point to the authoritative schema location
- Added to output XML documents for validation purposes
- Examples:
  - Official standards URLs: `http://www.isotc211.org/2005/gmd/gmd.xsd`
  - External service URLs: `http://www.openarchives.org/OAI/2.0/oai_dc.xsd`

#### `xslt` Attribute
- **Filename** of the XSLT stylesheet that performs the conversion
- Located in the `convert/` directory
- Path is relative to the convert.xml file
- Examples: `iso19139.mcp.xsl`, `oai_dc.xsl`, `rif.xsl`

## Complete Example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<conversions>
  <!-- Convert to this schema itself (with updated schemaLocation) -->
  <converter 
    name="xml_iso19139.mcp"
    nsUri="http://bluenet3.antcrc.utas.edu.au/mcp" 
    schemaLocation="http://bluenet3.antcrc.utas.edu.au/mcp-1.5-experimental/schema.xsd" 
    xslt="iso19139.mcp.xsl" 
  />

  <!-- Convert to MCP version 1.4 (removes experimental 1.5 elements) -->
  <converter 
    name="xml_iso19139.mcp-1.4"
    nsUri="http://bluenet3.antcrc.utas.edu.au/mcp" 
    schemaLocation="http://bluenet3.antcrc.utas.edu.au/mcp/schema.xsd" 
    xslt="iso19139.mcp-1.4.xsl" 
  />

  <!-- Convert to OAI Dublin Core format for harvesting -->
  <converter 
    name="xml_iso19139.mcpTooai_dc"
    nsUri="http://www.openarchives.org/OAI/2.0/" 
    schemaLocation="http://www.openarchives.org/OAI/2.0/oai_dc.xsd" 
    xslt="oai_dc.xsl" 
  />

  <!-- Convert to ANDS RIFCS format (Australian National Data Service) -->
  <converter 
    name="xml_iso19139.mcpToRIFCS"
    nsUri="http://ands.org.au/standards/rif-cs/registryObjects" 
    schemaLocation="http://services.ands.org.au/home/orca/schemata/registryObjects.xsd" 
    xslt="rif.xsl" 
  />

  <!-- Convert to base ISO19115/19139 (remove profile-specific elements) -->
  <converter 
    name="xml_iso19139"
    nsUri="http://www.isotc211.org/2005/gmd" 
    schemaLocation="http://www.isotc211.org/2005/gmd/gmd.xsd" 
    xslt="to19139.xsl" 
  />
</conversions>
```

## XSLT Stylesheet Basics

### Purpose of Conversion XSLTs
- Map source metadata elements to target schema elements
- Transform XML structure and namespace
- Handle incompatible data models
- Filter unwanted or incompatible content
- Apply business logic for format-specific requirements

### Basic XSLT Structure
```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" 
  xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
  xmlns:gmd="http://www.isotc211.org/2005/gmd"
  xmlns:dc="http://purl.org/dc/elements/1.1/"
  exclude-result-prefixes="gmd">

  <!-- Match the root element -->
  <xsl:template match="/gmd:MD_Metadata">
    <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
             xmlns:dc="http://purl.org/dc/elements/1.1/">
      <!-- Transform metadata to target format -->
      <rdf:Description rdf:about="...">
        <dc:title>
          <xsl:value-of select="gmd:hierarchyLevel/..."/>
        </dc:title>
      </rdf:Description>
    </rdf:RDF>
  </xsl:template>

</xsl:stylesheet>
```

### Common XSLT Elements
- **`<xsl:template>`**: Defines transformation rules for matched elements
- **`<xsl:value-of>`**: Extracts and outputs text values
- **`<xsl:for-each>`**: Iterates over element collections
- **`<xsl:if>` / `<xsl:choose>`**: Conditional logic
- **`<xsl:apply-templates>`**: Applies templates recursively

## Common Conversion Scenarios

### 1. Profile to Base Schema Conversion
Remove profile-specific elements and convert to base ISO19115/19139:

```xml
<!-- Remove profile elements, keep only base ISO elements -->
<xsl:template match="mcp:revisionDate"/>
```

### 2. Version Migration
Convert between different versions of the same schema:
- Remove deprecated elements
- Map old element names to new names
- Add default values for new mandatory elements

### 3. Format Conversion (OAI-PMH)
Convert to Dublin Core for metadata harvesting:
```xml
<dc:title><xsl:value-of select="gmd:title"/></dc:title>
<dc:description><xsl:value-of select="gmd:abstract"/></dc:description>
<dc:creator><xsl:value-of select="gmd:pointOfContact/*/gmd:individualName"/></dc:creator>
```

### 4. System-Specific Format
Convert to formats required by other systems (ANDS RIFCS, CSW, etc.)

## Best Practices

1. **Define Core Conversions**: Include conversions to base schema and common formats (Dublin Core)
2. **Namespace Accuracy**: Ensure correct namespace URIs in `convert.xml`
3. **Schema Validation**: Test output against target schema definitions
4. **Lossless Design**: When possible, preserve metadata during conversion
5. **Documentation**: Document mapping logic and assumptions in XSLT comments
6. **Error Handling**: Include templates for unexpected elements (identity templates)
7. **Performance**: Optimize XSLT for large metadata records
8. **Testing**: Validate conversions with real-world metadata samples

## Example Conversion Use Cases

### Interoperability
- Share metadata with external catalogs
- Support multiple discovery protocols
- Enable metadata aggregation

### Migration
- Upgrade metadata to new schema versions
- Convert proprietary formats to standards
- Harmonize metadata from multiple sources

### Harvesting
- Support OAI-PMH for automated discovery
- Enable metadata federation
- Support CSW (Catalog Service for Web)

## References

- [W3C XSLT Specification](https://www.w3.org/TR/xslt/)
- [GeoNetwork Conversion Configuration](https://docs.geonetwork-opensource.org/4.2/customizing-application/implementing-a-schema-plugin/#schema_conversions)
- [OAI-PMH Protocol](https://www.openarchives.org/pmh/)
- [Dublin Core Metadata Initiative](https://dublincore.org/)
- [ANDS RIFCS Format](https://documentation.ardc.edu.au/display/DOC/RIFCS)