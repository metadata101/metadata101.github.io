---
layout: page
title: Codelists and Thesauri
permalink: /codelists-and-thesauri/
---

Codelists and thesauri are essential components of metadata schemas that provide controlled vocabularies for describing resources. They help ensure consistency and enable better discovery and interoperability of metadata.

## Codelists

### Definition
A codelist is a list of predefined values that can be assigned to a metadata element. Codelists are typically derived from enumerated types in XML schema definitions (XSDs). They provide a controlled vocabulary for specific metadata elements, ensuring data consistency and quality.

### Purpose
- Standardize values for specific metadata fields
- Enable consistent metadata tagging across records
- Facilitate metadata validation
- Support metadata search and filtering

### Implementation in Metadata Schemas
Codelists are typically defined in the `codelists.xml` file, organized by language in the `/loc/<language-code>/` directory (e.g., `loc/eng/codelists.xml`).

#### Structure
Each codelist entry includes:
- **Code**: The enumerated value from the XSD
- **Label**: A human-readable label for the code
- **Description**: An explanation of what the code represents

#### Example
ISO19115/19139 defines a codelist for topic categories:

```xml
<codelist name="gmd:MD_TopicCategoryCode">
  <entry>
    <code>farming</code>
    <label>Farming</label>
    <description>Rearing of animals and/or cultivation of plants. Examples: agriculture, irrigation, aquaculture, plantations, herding</description>
  </entry>
  <entry>
    <code>biota</code>
    <label>Biota</label>
    <description>Flora and/or fauna in natural environment. Examples: wildlife, vegetation, biological sciences, ecology</description>
  </entry>
  <!-- Additional entries... -->
</codelist>
```

### External Codelists
External codelists can be sourced from standards organizations (e.g., ISO codelists in `gmxCodelists.xml`). These can be:
- Extracted from external catalog/vocabulary files
- Included in schema plugins for localization
- Used as fallback when profile-specific codelists don't define a required value

## Thesauri

### Definition
A thesaurus is a controlled vocabulary representing concepts from a specialized field of knowledge. In metadata catalogs, thesauri enable the assignment of keywords to metadata records, associating them with standardized concepts.

### Purpose
- Provide standardized terminology for a domain
- Enable precise metadata tagging with controlled keywords
- Support semantic search capabilities
- Ensure consistency in metadata across organizations

### Types of Thesauri
GeoNetwork recognizes three types of thesauri:

1. **External Thesauri**: Managed by external organizations and imported as SKOS files. These are read-only and flagged as `external`.
2. **Local Thesauri**: Created within GeoNetwork and stored as SKOS files. These can be edited by authorized users and are flagged as `local`.
3. **Register Thesauri**: Created from ISO19135 register records. These are generated from existing register metadata and can be updated by editing the ISO19135 record.

### Thesaurus Categories
All thesauri in GeoNetwork are categorized using ISO19115/19139 keyword type codes:

| Category | Description |
|----------|-------------|
| **place** | Concepts identifying geographic locations |
| **stratum** | Concepts identifying layers of deposited substances |
| **temporal** | Concepts identifying time periods |
| **theme** | Concepts identifying a subject or topic |
| **discipline** | Concepts identifying a branch of specialized learning |

### SKOS Format
GeoNetwork uses the Simple Knowledge Organisation Systems (SKOS) format to store thesaurus information. SKOS provides a standard way to represent concepts and relationships between them.

#### SKOS Concept Structure
Each concept in SKOS includes:
- **Identifier**: A unique URI for the concept
- **Preferred Label**: The primary term (with optional language tags)
- **Definition**: Description of the concept
- **Relationships**: Links to related, broader, and narrower concepts

#### Example SKOS Concept
```xml
<skos:Concept rdf:about="http://example.org/concept#fish">
    <skos:prefLabel xml:lang="en">Fish</skos:prefLabel>
    <skos:prefLabel xml:lang="fr">Poisson</skos:prefLabel>
    <skos:broader rdf:resource="http://example.org/concept#aquaticLife"/>
    <skos:narrower rdf:resource="http://example.org/concept#trout"/>
    <skos:definition>Aquatic vertebrate animals with gills</skos:definition>
</skos:Concept>
```

### Concept Relationships
SKOS supports three types of relationships:
- **Broader Terms**: More general concepts
- **Narrower Terms**: More specific concepts
- **Related Terms**: Concepts at similar levels with logical connections

### Multilingual Thesauri
SKOS supports multilingual thesauri, allowing concepts to have labels and definitions in multiple languages using the `xml:lang` attribute. Search and editing in GeoNetwork adapts to the current user interface language.

### ISO19135 Register Format
ISO19135 is an ISO standard for describing registers of items. It captures:
- Register metadata (name, version, contacts)
- Item descriptions (name, status, lineage, relationships)
- Evolution tracking of concepts

ISO19135 records in GeoNetwork can be converted to SKOS thesauri, enabling the creation of thesauri from ISO standard register records.

## Managing Codelists and Thesauri

### File Organization
In a metadata schema plugin:
- **Codelists**: Located in `/loc/<language-code>/codelists.xml`
- **Labels**: Located in `/loc/<language-code>/labels.xml`
- **Thesauri Files**: Stored in the GeoNetwork data directory under `config/codelist/`

### Localization
Both codelists and thesauri support localization:
- Codelist labels and descriptions can be provided in multiple languages
- Thesauri in SKOS format support language-specific labels and definitions
- Fallback mechanisms exist for profile codelists (using base schema codelists when needed)

### Integration with Metadata Records
- **In ISO19115/19139**: Keywords are assigned using the codelist picker in the metadata editor
- **Keyword Grouping**: Keywords from the same thesaurus are grouped together in metadata records
- **Thesaurus Citation**: A URL pointing to the source thesaurus is included in the Thesaurus Name citation

### Search and Discovery
- Keywords are indexed in a `tag` field for general keyword search
- Thesaurus-specific fields are created (e.g., `th_theme` for INSPIRE themes)
- Facet panels allow users to browse and filter by keywords

## Best Practices

1. **Use Existing Standards**: Before creating custom codelists or thesauri, review existing standards and vocabularies from your field.
2. **Document Thoroughly**: Include clear descriptions for codelist entries and concept definitions in thesauri.
3. **Support Multiple Languages**: When possible, provide labels and definitions in relevant languages.
4. **Maintain Version Control**: Track changes to codelists and thesauri over time.
5. **Regular Reviews**: Periodically review and update codelists and thesauri to ensure they remain relevant.
6. **Consistency**: Ensure consistency between codelist values used in different parts of the schema.

## References

- [GeoNetwork Managing Thesaurus Documentation](https://docs.geonetwork-opensource.org/4.2/administrator-guide/managing-classification-systems/managing-thesaurus/)
- [GeoNetwork Implementing Schema Plugins - Codelists](https://docs.geonetwork-opensource.org/4.2/customizing-application/implementing-a-schema-plugin/#more-on-codelistsxml)
- [SKOS Reference](http://www.w3.org/TR/skos-reference/)
- [ISO19115 Metadata Standard](http://www.isotc211.org/)
