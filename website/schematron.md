---
layout: page
title: Schematron
permalink: /schematron/
---

Schematron is a powerful language for validating XML documents. It provides a set of rules to enforce complex constraints and conditions on metadata records that go beyond what XML Schema Definition (XSD) validation alone can achieve.

## Overview

The **schematron** directory contains validation rules that are applied to metadata records to ensure they meet specific requirements and constraints. Schematrons complement XML schema definitions by enabling complex, context-dependent validation rules.

### Purpose
- Validate complex constraints on metadata content
- Enforce business rules and domain-specific requirements
- Provide detailed error messages for validation failures
- Support conditional validation based on metadata context
- Enable localized error messages and warnings

## Schematron Format

Schematrons use ISO/IEC 19757-3 (Schematron) language, which is XML-based and allows for pattern-based rule definition.

### Basic Structure
A schematron document consists of:
- **Patterns**: Groups of related rules
- **Rules**: Constraints applied to specific elements
- **Assertions**: Conditions that must be true
- **Reports**: Messages when conditions are met

#### Example Structure
```xml
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://purl.oclc.org/dsdl/schematron">
  <pattern>
    <title>Metadata Validation Rules</title>
    <rule context="//gmd:MD_Metadata">
      <assert test="gmd:fileIdentifier">
        Metadata must have a file identifier
      </assert>
    </rule>
  </pattern>
</schema>
```

### Key Elements

#### Pattern
Groups related validation rules together. Patterns can have:
- `title`: A descriptive title for the pattern
- `id`: A unique identifier (optional)

#### Rule
Defines the context where validation applies and contains assertions and reports.
- `context`: XPath expression indicating where the rule applies

#### Assert
Specifies a condition that must be true:
- `test`: XPath expression that should evaluate to true
- Content: Error message if the assertion fails

#### Report
Specifies information to report when a condition is true:
- `test`: XPath expression that triggers the report
- Content: Message to display

## Implementation in Metadata Schemas

### Directory Structure
Schematron files are organized in the schema plugin:
- **Directory**: `/schematron/`
- **Naming Convention**: `schematron-rules-<schema-identifier>.sch`
- **Example**: `schematron-rules-iso-mcp.sch`

## References

- [ISO/IEC 19757-3 Schematron Specification](http://purl.oclc.org/dsdl/schematron/)
- [GeoNetwork Schematron Implementation](https://docs.geonetwork-opensource.org/4.2/customizing-application/implementing-a-schema-plugin/#creating-schematrons-to-describe-mcp-conditions)
- [ISO19115 Metadata Validation Rules](http://www.isotc211.org/)


