---
layout: page
title: Metadata Schemas and Profiles
permalink: /metadata-schemas-and-profiles/
---

An XML metadata schema in metadata101 consists of:

1. The XML schema documents describing the structure of a metadata record — see [Schema]({% link schema.md %}).
2. Human-readable names and descriptions of the elements in a metadata record — see [Help]({% link help.md %}).
3. Codelists and thesauri for those elements of a metadata record that have a controlled vocabulary - see [Codelists And Thesauri]({% link codelists-and-thesauri.md %}).
4. Schematron rules for validating metadata records — see [Schematron]({% link schematron.md %}).
5. XML Stylesheet Language (XSL) transformers that can be used to convert records to other metadata schemas — see [Convert]({% link convert.md %}).
6. Sample metadata records (optional) — see [Sample Data]({% link sample-data.md %}).

This information, along with an identifier, name, and description for the metadata schema, is described in an XML file called `ident.xml`.

An example metadata101 schema is the Marine Community Profile of ISO19115/19139, which can be found [here](http://github.com/metadata101/Marine-Community-Profile-1.5).

---

## What is the difference between a metadata schema and a metadata profile?

A **metadata schema** is an implementation of a metadata standard. It describes the elements of the standard, how they can be used in a metadata record, and how the metadata record can be validated to ensure that both the structure and the content are correct.

A **metadata profile** is a community version of a metadata standard — it may subset or extend a metadata standard and should describe how to use a metadata standard in a particular community.  
For example, MCP is the Marine Community version of the ISO19115 metadata standard; it is a superset (adds elements to the base standard) and describes how the ISO19115 (and extension) elements should be used by the members of the community.

