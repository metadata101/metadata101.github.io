---
layout: page
title: Sample Data
permalink: /sample-data/
---

# Sample Data

The **sample-data** directory contains sample metadata records that demonstrate how the metadata schema should be used. These examples serve as templates, references, and validation test cases for metadata creators and developers working with the schema.

## Overview

### Purpose
- Demonstrate proper usage of schema elements
- Provide realistic examples for metadata creators
- Enable schema validation and testing
- Serve as templates for creating new metadata records
- Document best practices and common patterns
- Facilitate schema comprehension for new users
- Support automated testing and quality assurance

### Benefits
- **Learning Resource**: Users can study examples to understand how elements should be populated
- **Reference Implementation**: Shows the correct structure and content for metadata records
- **Testing Material**: Sample records can be used to validate schema implementations
- **Documentation**: Illustrates patterns and best practices in metadata creation
- **Quality Baseline**: Provides examples of well-formed, complete metadata

## File Format and Organization

### File Naming
```
sample-data/
├── sample-agriculture
├── sample-marine-biodiversity
├── sample-urban-planning
├── sample-geospatial-framework
└── sample-minimum-elements
```

**Naming Convention**: `sample-<descriptive-name>`
- Use descriptive names reflecting the metadata subject
- Use lowercase with hyphens as separators
- Examples: `sample-forest-inventory`, `sample-coastal-zones`

### MEF Format (GeoNetwork Standard)
The `sample-data` directory contains MEF (Metadata Exchange Format) files but unzipped. MEF is a ZIP archive containing:
- **metadata.xml**: The actual metadata record
- **info.xml**: Metadata about the metadata (creation date, language, etc.)
- **thumbnails/**: Optional directory with thumbnail images
- **public/**: Optional online resources and supporting files


## Creating Effective Sample Metadata Records

### Types of Sample Records

#### 1. **Minimal Valid Record**
Contains only mandatory elements, demonstrating the minimum viable metadata:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<gmd:MD_Metadata xmlns:gmd="http://www.isotc211.org/2005/gmd"
                 xmlns:gco="http://www.isotc211.org/2005/gco">
  <gmd:fileIdentifier>
    <gco:CharacterString>minimum-metadata-example</gco:CharacterString>
  </gmd:fileIdentifier>
  <gmd:hierarchyLevel>
    <gmd:MD_ScopeCode>dataset</gmd:MD_ScopeCode>
  </gmd:hierarchyLevel>
  <gmd:dateStamp>
    <gco:Date>2024-01-15</gco:Date>
  </gmd:dateStamp>
  <!-- Other mandatory elements -->
</gmd:MD_Metadata>
```

#### 2. **Comprehensive Record**
Includes extended elements demonstrating complete metadata usage:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<gmd:MD_Metadata xmlns:gmd="http://www.isotc211.org/2005/gmd"
                 xmlns:gco="http://www.isotc211.org/2005/gco"
                 xmlns:srv="http://www.isotc211.org/2005/srv">
  <gmd:fileIdentifier>
    <gco:CharacterString>comprehensive-dataset-2024</gco:CharacterString>
  </gmd:fileIdentifier>
  
  <gmd:hierarchyLevel>
    <gmd:MD_ScopeCode>dataset</gmd:MD_ScopeCode>
  </gmd:hierarchyLevel>
  
  <gmd:dateStamp>
    <gco:Date>2024-01-15</gco:Date>
  </gmd:dateStamp>
  
  <gmd:identificationInfo>
    <gmd:MD_DataIdentification>
      <gmd:title>
        <gco:CharacterString>Comprehensive Agricultural Land Use Dataset</gco:CharacterString>
      </gmd:title>
      <gmd:abstract>
        <gco:CharacterString>Detailed land use classification covering agricultural areas...</gco:CharacterString>
      </gmd:abstract>
      <!-- Additional elements -->
    </gmd:MD_DataIdentification>
  </gmd:identificationInfo>
  
  <!-- Additional metadata sections -->
</gmd:MD_Metadata>
```

#### 3. **Domain-Specific Examples**
Specialized samples for specific use cases:
- Geographic data samples
- Scientific research metadata
- Environmental monitoring records
- Administrative/statistical data
- Service metadata

#### 4. **Profile-Specific Examples**
For profile schemas, samples should demonstrate profile-specific extensions:

```xml
<!-- Profile-specific extension example -->
<mcp:revisionDate xmlns:mcp="http://bluenet3.antcrc.utas.edu.au/mcp">
  <gco:Date>2024-01-20</gco:Date>
</mcp:revisionDate>
```

### Best Practices for Sample Records

1. **Validity**: Ensure all samples validate against the schema (XSD and Schematron)
2. **Completeness**: Include at least one comprehensive example with most/all elements
3. **Simplicity**: Provide a minimal example showing only required elements
4. **Diversity**: Cover different metadata types and use cases
5. **Realistic Data**: Use realistic values that accurately represent the domain
6. **Documentation**: Include comments explaining key elements and patterns
7. **Localization**: Provide samples in multiple languages if supported
8. **Maintainability**: Keep samples up-to-date as the schema evolves

## Quantity and Selection

### Recommended Number of Samples
- **Minimum**: 1-2 samples (minimal and basic examples)
- **Standard**: 3-5 samples (covering different scenarios)
- **Comprehensive**: 8-10+ samples (extensive coverage of use cases)

### Selection Criteria
Include samples that:
- Demonstrate mandatory elements
- Show optional elements in context
- Illustrate common patterns
- Cover primary use cases for the schema
- Include edge cases or complex structures
- Represent different organizational sectors (if applicable)


## References

- [GeoNetwork Sample Data Documentation](https://docs.geonetwork-opensource.org/4.2/customizing-application/implementing-a-schema-plugin/#creating-the-sample-data-directory)
- [GeoNetwork MEF Format](https://docs.geonetwork-opensource.org/4.2/api/)
- [ISO19115 Metadata Standard](http://www.isotc211.org/)
- [Sample Data Best Practices](https://en.wikipedia.org/wiki/Test_data)