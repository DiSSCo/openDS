---
# Structure of openDS json schemas
---

## Introduction
Using examples, this page explains the structure of an [open Digital Specimen](https://github.com/DiSSCo/openDS) and declares the [JSON schema](https://json-schema.org/) to support those.

In this form it serves as a basis for discussion and understanding.

Important starting points for understanding are the following:

- The structure of an openDS corresponds to the Minimum Information about a Digital Specimen (MIDS), level by level.
- The definition of an openDS here corresponds to the Digital Specimen class in the [object model](https://github.com/DiSSCo/openDS/blob/master/data-model/data-model-intro.md).

## Example 1: MIDS level 1, authoritative information only
An example DS for a physical specimen in the collection of the Muséum National d'Histoire Naturelle, Paris (MNHN) with the identifier "MNHN-IM-2013-8488"; compliant with MIDS level 1 and having no images or supplementary information.

Source of data: https://science.mnhn.fr/institution/mnhn/collection/im/item/2013-8488

Location of DS: https://nsidr.org/objects/20.5000.1025/64ae0cf0dacb7bd20ba5?pretty

```json
{
  "id": "20.5000.1025/64ae0cf0dacb7bd20ba5",
  "typeName": "ODStype1802",
  "authoritative": {
    "modified": "2021-02-22T14:10:20.824Z",
    "midsLevel": 1,
    "physicalSpecimenId": "MNHN-IM-2013-8488",
    "institution": [
      "MNHN",
      "https://ror.org/03wkt5x30"
    ],
    "materialType": "Alcohol, 95%",
    "name": "Pygmaepterys pointieri Garrigues & Merle, 2014"
  }
}
```

## Structure of the schema for the above example
The JSON schema for the above example begins with the definition of the schema itself - the first five lines of the JSON fragment below. It states the version of the [JSON schema specification](https://json-schema.org/) that applies and gives an identifier, description, type and title to the schema definition.

```json
{
  "$schema": "http://json-schema.org/draft/2019-09/schema#",
  "$id": "https://nsidr.org/schemas/opendsschema.json",
  "description": "v0.4, 22 February 2021. JSON schema for an open Digital Specimen.",
  "type": "object",
  "title": "ODStype1802",
  "properties": {
    "id": { "type": "string" },
    "typeName": { "type": "string", "const": [ "ODStype1802" ] },
    "authoritative": {
      "$id": "#/properties/a_section",
      "type": "object",
      "properties": {
        "$comment": "authoritative properties here; list mandatory ones as required (below)"
      },
      "required": [ ]  
    },
    "$comment": " ... several more optional sections of the schema appear here, see below ... "
  },
  "required": [ "id", "typeName", "authoritative" ]
}
```

The schema then specifies as its properties what is being defined i.e., an object of type "ODStype1802" with its included subsets of specimen related properties. The first subset of specimen related properties - the authoritative properties - appears next. At the end of the authoritative (a_section) a list of those property keys that are mandatory in that section appears as the `required` validation array. This `required` array is empty in the fragment above and will be filled in later on below. The ODS object's  `id`, `typeName` and `authoritative` section are all required for an open Digital Specimen to be a valid construct. So, this is the minimum viable construct for an open Digital Specimen. The ODS object's `id` must be a valid Handle. This constraint still needs to be added to the schema fragment.

*Notes to self about the fragment above:*

- *We need to constrain the `id` to be a valid Handle. How to do that?*
- *do we need to pull in the $context here? Unresolved issue as to how we exploit links to semantics*
- *the ODSType1802 schema is deployed at http://nsidr.org/#objects/20.5000.1025/af08540a7a96066fdf23.*
- *the json description of the DTR ***type definition*** of an openDS is different from this schema definition. Logically they will be the same but how they are used is different.*
- *how do we process type definitions? What general purspose software exists for dealing with them? Out of date now, but gives some hints: https://dlib.org/dlib/may07/saidis/05saidis.html.*
- *The schema references the current draft 2019-09 of the JSON-schema specification. However, some schema validator tools work only with earlier versions. e.g., the https://extendsclass.com/json-schema-validator.html works with /draft-07/schema#.*
- *Consider that we might want to enforce a convention (pattern) for any specific propertyNames that are not already in the schema but which might be added to a JSON instance.*
- *Consider that we might want to use the additionalProperties keyword to control how the extensions (E) section works.*

## Overall structure (sections of the schema)
At the highest level of structure, the properties of an open Digital Specimen are divided into several sections, each represented in the schema as a nested JSON object. We've already been introduced to the first of these, the authoritative or a_section. It together with the other section types are explained as follows:

- **authoritative a_section**, contains essential data about a specimen. The a_section is represented by an a_section object containing all the key/value pair properties that are deemed to be authoritative information about a physical specimen. The complete schema definition of the a_section corresponds to the information elements expected to be present at MIDS level 2. The a_section is mandatory.

- **images i_section**, containing references to images or images themselves of the specimen and/or its labels. The images section is represented by an i_section object containing metadata about the available images.

- **supplementary s_section**, containing links to supplementary data derived from a specimen. The supplementary section is represented by an s_section object, which itself may contain multiple objects grouping specific kinds of supplementary information (such as external links) together. The definition of the s_section corresponds to the additional information elements expected to be present at MIDS level 3 and more.

- **tertiary t_section**, containing links to related data associated with a specimen but not directly derived from the physical specimen.
  
Expanding on the basic schema construct above, the JSON schema fragment describing this overall structure is the following:

```json
{
  "$schema": "http://json-schema.org/draft/2019-09/schema#",
  "$id": "https://nsidr.org/schemas/opendsschema.json",
  "description": "v0.4, 22 February 2021. JSON schema for an open Digital Specimen.",
  "type": "object",
  "title": "ODStype1802",
  "properties": {
    "id": { "type": "string" },
    "typeName": { "type": "string", "const": [ "ODStype1802" ] },
    "authoritative": {
      "$id": "#/properties/a_section",
      "type": "object",
      "properties": {
        "$comment": "authoritative properties here; list mandatory ones as required (below)"
      },
      "required": [ ]  
    },
    "images": {
      "$id": "#/properties/i_section",
      "type": "object",
      "properties": {
        "$comment": "image properties here; list mandatory ones as required (below)"
      },  
      "required": [  ]
    },
    "supplementary": {
      "$id": "#/properties/s_section",
      "type": "object",
      "properties": {
        "$comment": "supplementary properties here; list mandatory ones as required (below)"
      },  
      "required": [  ]
    },
    "tertiary": {
      "$id": "#/properties/t_section",
      "type": "object",
      "properties": {
        "$comment": "tertiary properties here; list mandatory ones as required (below)"
      },  
      "required": [  ]
    },
    "$comment": " ... further optional sections of the schema can appear here ... "
  },
  "required": [ "id", "typeName", "authoritative" ]
}
```

### Other section types
*For further study.*

There are several additional section types for further study, including:

- **extension e_section**, *for further study. This is likely to be proprietary to specific organisations/systems.*

- **operations/methods o_section**, *for further study.*
  
- **payloads (contents) p_section**, *for further study.* *thumbnail images perhaps?*
  
- ***Others ...***

## Authoritative (a_section) information elements
The information element content of the authoritative section aligns with the [Minimum Information about a Digital Specimen (MIDS)](https://github.com/tdwg/mids/blob/main/MIDS-definition.md) that we expect to see i.e., information at one of the MIDS levels 0 - 3. The simplest example, [example 1 above](#example-1-mids-level-1-authoritative-information-only) helps us to understand the structure of the a_section schema. It contains six information elements. Definitions of each of these are given in the table below. Each is basically a key/value pair definition. That for the `institution` element is a little more complex, as it consists of two parts.

| **Info element** | **Definition** |
| --- | --- |
| modified | Date-time. Refer to [MIDS Information - Modified](https://github.com/tdwg/mids/issues/8) |
| midsLevel| Integer value, range 0-3. |
| physicalSpecimenId | Physical specimen identifier. Refer to [MIDS Information - PhysicalSpecimenId](https://github.com/tdwg/mids/issues/10) |
| institution | Refer to [MIDS Information - Institution](https://github.com/tdwg/mids/issues/11) |
| materialType | Refer to [MIDS Information - MaterialType](https://github.com/tdwg/mids/issues/14) |
| name | Refer to [MIDS Information - Name](https://github.com/tdwg/mids/issues/12) |

### JSON fragment for a_section
Here is the JSON fragment for the a_section property definitions above.

```json
    "authoritative": {
      "$id": "#/properties/a_section",
      "type": "object",
      "properties": {
        "modified": { "type": "string", "title": "Modified (date:time)", "format": "date-time" },
        "midsLevel": { "type": "integer", "minimum": 0, "maximum": 3 },
        "physicalSpecimenId": { "type": "string", "title": "Physical specimen identifier" },
        "institution": {
          "type": "array", "items": [ {"type": "string", "title": "Code (GRSciColl)" },
                                      {"type": "string", "format": "uri", "title": "Referent" } ] 
        },
        "materialType": { "type": "string", "title": "Material type" },
        "name": { "type": "string", "maxLength": 128, "title": "Name" }
      },  
      "required": [ "modified", "midsLevel", "physicalSpecimenId", "institution", "materialType", "name" ]
    }
```
### Minimum required
Together with `id` and `title` (above) only a very small number of information elements are mandatory for an open digital specimen to come into existence (i.e., to be created). The first of these is `midsLevel`, which is a declared or calculated value of the present MIDS Level reached by the available  specimen data. Also required are the information elements `modified`, `physicalSpecimenId` and `institution`. These correspond to the information elements required at [MIDS level 0](https://github.com/tdwg/mids/issues?q=is%3Aopen+is%3Aissue+label%3AMIDS-0+label%3A%22MIDS+Element%22) according to the [TDWG MIDS definition](https://github.com/tdwg/mids/blob/main/MIDS-definition.md). Thus, these are specified as needed in the `required` array for the a_section. Because this schema corresponds to the [example 1 above](#example-1-mids-level-1-authoritative-information-only), we also include `materialType` and `name` as being required.

### Other a_section properties: conditional subschemas for different values of midsLevel
At the present time (25Feb2021) and based on the example, only the MIDS-0 and MIDS-1 properties have been defined. Others, for MIDS levels 2 and 3 will be added later. This leads to the need for conditional subschemas for different values of midsLevel.

Depending on the declared MIDS level, we'd expect to see a certain set of properties present in the ODS. We can apply subschemas conditionally, using If-Then-Else constructs. 

*Note to self: Need to look at subschemas and how to structure these as separate schema fragments / type definitions i.e., the type definition of an ODS a_section will be different depending on the declared/calculated MIDSLevel.*

To implement this, something along the following lines is likely. This example distinguishes between what is required at MIDS-0 and MIDS-1. It would be more complext when we add additional constructions for MIDS-2 and MIDS-3. It still needs to checked, tested and optimised. Of course, it would be better that key definitions only appear once to reduce the possibility of introducing errors when changes are made.

```json
    "authoritative": {
      "$id": "#/properties/a_section",
      "type": "object",
      "properties": {
        "modified": { "type": "string", "title": "Modified (date:time)", "format": "date-time" },
        "midsLevel": { "type": "integer", "minimum": 0, "maximum": 3 },
      },
      "if": { "properties": { "midsLevel": { "const": 0 } },
      "then": { "properties": {
                  "$comment": "MIDS-0 elements",
                  "physicalSpecimenId": { "type": "string", "title": "Physical specimen identifier" },
                  "institution": { "type": "array", "items": [ {"type": "string", "title": "Code  (GRSciColl)" }, {"type": "string", "title": "Referent" } ] 
                   },
                "required": [ "physicalSpecimenId", "institution" ] },
      },
      "else": { "properties": {
                  "$comment": "MIDS-1 elements",
                  "physicalSpecimenId": { "type": "string", "title": "Physical specimen identifier" },
                  "institution": { "type": "array", "items": [ {"type": "string", "title": "Code (GRSciColl)" }, {"type": "string", "title": "Referent" } ] 
                   },
                  "materialType": {},
                  "name": { "type": "string", "maxLength": 128, "title": "Name" }
                },
                "required": [ "physicalSpecimenId", "institution", "materialType", "name" ]
                },
      "required": [ "modified", "midsLevel" ] },
      }
    }
```

## Image i_section information elements
*To be completed.*

## Supplementary s_section information elements
Definitions of individual information elements belonging to the supplementary s_section follow. Each definition is a key/value pair.

*To be completed. The schema fragment below is just an illustration/placeholder.*

```json
    "supplementary": {
      "$id": "#/properties/s_section",
      "type": "object",
      "properties": {
        "externalLinks": {
          "type": "array",
          "items": {
            "type": "string",
            <other elements of the external link quad. Sort out repetitions.>
            },
          }
        }
      }
    }
```
## Complete JSON schema for validation testing
Putting the schema fragments together for [example 1 above](#example-1-mids-level-1-authoritative-information-only) we obtain the following schema for validation.

```json
{
  "$schema": "http://json-schema.org/draft/2019-09/schema#",
  "$id": "https://nsidr.org/schemas/opendsschema.json",
  "description": "v0.4, 22 February 2021. JSON schema for an open Digital Specimen.",
  "type": "object",
  "title": "ODStype1802",
  "properties": {
    "id": { "type": "string" },
    "typeName": { "type": "string", "const": [ "ODStype1802" ] },
    "authoritative": {
      "$id": "#/properties/a_section",
      "type": "object",
      "properties": {
        "modified": { "type": "string", "title": "Modified (date:time)", "format": "date-time" },
        "midsLevel": { "type": "integer", "minimum": 0, "maximum": 3 },
        "physicalSpecimenId": { "type": "string", "title": "Physical specimen identifier" },
        "institution": {
          "type": "array", "items": [ {"type": "string", "title": "Code (GRSciColl)" },
                                      {"type": "string", "format": "uri", "title": "Referent" } ] 
        },
        "materialType": { "type": "string", "title": "Material type" },
        "name": { "type": "string", "maxLength": 128, "title": "Name" }
      },  
      "required": [ "modified", "midsLevel", "physicalSpecimenId", "institution", "materialType", "name" ]
    },
  "required": [ "id", "typeName", "authoritative" ]
}
```

*Notes to self, 25/02/2021:*
- *Note, deployed (adapted) into nsidr.org as schema ODStype1802 on 18th February 2021.*
- *Institution array is open-ended, allowing as many items as you like to be added. In CORDRA How do I allow additional referents to be added as format=uri rather than just as uncontrolled strings? Within an array, is it possible in the schema to constrain the number of elements and their order?*
- *Material Type is not fully specified yet. Needs a controlled vocabulary At the moment in CORDRA, just a string type.*


END.



