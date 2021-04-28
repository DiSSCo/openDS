---
# Basic json - example 2
---

## Introduction
Continuing from the [JSON for example 1 and its corresponding schema](basic-json-schema.md), let's add some images.

## Example 2: MIDS level 1, authoritative information and available images

If we look at the [source of the data](https://science.mnhn.fr/institution/mnhn/collection/im/item/2013-8488) we can find there are two images available:
- a low resolution image: http://imager.mnhn.fr/imager3/w400/media/1427463506459UAeHPJw9jXoET1sF 
- a higher resolution image: http://mediaphoto.mnhn.fr/media/1427463506459UAeHPJw9jXoET1sF 

Inspecting the image files with a suitable [Exif metadata viewer](https://exifinfo.org/), we discover the format is [JFIF](https://fileinfo.com/extension/jfif), a JPEG variation intended to allow easy exchange of images across platforms and to provide additional useful metadata not provided for by the base JPEG standard. The low res image has very little information given about it - just an indication of size (400 x 280) pixels with no resolution information. It's a 'thumbnail' image that displays on a standard computer screen with a resolution of 72dpi. For the high res image, considerably more information is [available](https://exifinfo.org/detail/UAO-L0dx_KQM5DDMXxKv8w). The image is 3780 x 2646 pixels at a resolution of 300dpi in each of the X and Y directions. It uses standard RGB colour representation with a specified standard International Colour Consortium (ICC) colour profile for rendering/printing on specialist display/printer devices. The image was created on March 27th, 2015.

A machine could deduce the above details by examining the files directly, for example using the [EXifTool Perl library](https://exiftool.org/). Even so, there is little information provided that would allow a user to deduce where the image had come from, who made it or why. A human can read from the [webpage](https://science.mnhn.fr/institution/mnhn/collection/im/item/2013-8488) that the image was created in 2015 by Manuel Caballer as part of the French e-ReColNat project, and that it is licensed as [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). This is information about the image but it is part of the webpage for the specimen and not part of the image metadata itself. Nevertheless, from the openDS perspective this is useful information to include with the image. 

For the present example, we'll assume we want to include the following as the specimen image information:

- the thumbnail image itself, with its pixel dimensions so people can immediately see a picture of the specimen;
- the location of the high resolution image, such that it can be retrieved for further use by someone interested in the specimen;
- the metadata about the high res image i.e., pixel dimensions, resolution, colour profile, creation date, name of the person creating the image, the project producing it and licensing details.

From the JSON perspective, this indicates we need to provide for an array of one or more image objects. We can extend our earlier [example 1](basic-json-schema.md) as follows below with an images (i_) section that contains an array of image objects. Since, in the general case we don't know how many images can be associated with a specimen we do not name the objects within the JSON `availableImages` array.

>>Update this uri once we've put the example into nsidr.org
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
  },
  "images": {
    "availableImages": [
      {
        "imageName": "thumbnail",
        "source": "#/payloads",
        "mediaType": "image/jpeg", 
        "imageWidth": "400",
        "imageHeight": "280",
        "xResolution": "",
        "yResolution": "", 
        "colorSpace": "",
        "iccProfileName": "", 
        "creator": "",
        "created": "",
        "project": "",
        "license": "CC BY 4.0" 
      },
      {
        "imageName": "hi-res",
        "source": "http://mediaphoto.mnhn.fr/media/1427463506459UAeHPJw9jXoET1sF",
        "mediaType": "image/jpeg",
        "imageWidth": "3780",
        "imageHeight": "2646",
        "xResolution": "300",
        "yResolution": "300",
        "colorSpace": "sRGB",
        "iccProfileName": "sRGB IEC61966-2.1", 
        "creator": "Manuel Caballer",
        "created": "2015:03:27T14:33:02Z",
        "project": "e-ReColNat",
        "license": "CC BY 4.0" 
      }
    ]
  },
  "payloads": [
    {
      "name": "thumbnail",
      "filename": "1427463506459UAeHPJw9jXoET1sF.jfif",
      "mediaType": "image/jpeg",
      "size": 15063
    }
  ]
}
```

# Validation
There are several JSON validators available online we can use to work with this JSON fragment. 

## Simple validators and formatters
Simple validators and/or formatters can tell us the fragment is syntactically correct and reveal the structure of complex fragments. Some offer transformation between JSON and other representations such as XML and CSV. Here are a few to try:
- [JSONLint validator](https://jsonlint.com/)
- [jsonformatter.org](https://jsonformatter.org/)
- [curiousconcept.com](https://jsonformatter.curiousconcept.com/#)

## Validating against a schema
More interesting and useful is these tools that validate a JSON fragment against a JSON schema supplied by the user:
- [jsonschemavalidator.net](https://www.jsonschemavalidator.net/)
- [with common java json tools](https://json-schema-validator.herokuapp.com/)
- [jsonschemalint](https://jsonschemalint.com/)

## Generating schemas
Generating JSON schemas is a time-consuming and error-prone process when done by hand. The best approach is to automatically generate a schema from an example JSON fragment and then to optimise by hand.

Several automatic JSON schema generators are available online, with varying capabilities. Some generate just a bare minimum schema whilst others generate more comprehensive, more descriptive schemas that include example codings as well. These tend to be more verbose but easier to comprehend and optimise by hand.
- [jsonschema.net](https://www.jsonschema.net/home) - looks a good one because it allows editing of the JSON and the schema side by side. It has a graph visualization of the schema as well too. However, it doesn't appear to support the draft/2019-09/schema, only supporing upto draft-07. Having said that, there is an [open GitHub issue](https://github.com/jackwootton/json-schema/issues/86) for that.
- [extendsclass](https://extendsclass.com/json-schema-validator.html) makes use of the widely used [Ajv validator](https://ajv.js.org/) and allows to generate schemas from fragments and vice versa. Ajv has the added benefit of being capable of generating code to turn Schemas into JavaScript validation functions that can be bundled as part of applications.

The main differences between these two generators are that the first places a complete exampe at the beginning of the schema whereas the latter breaks the example up into multiple short examples, each at its own place in the schema. The first includes a $description for each property (thus more documenting), whereas the latter doesn't include this (although it can be added by hand).

- [liquid-technologies](https://www.liquid-technologies.com/online-json-to-schema-converter) - has tools for both directions i.e., JSON -> JSON schema, and vive-versa.
- [quicktype](https://quicktype.io/)

## Schema(s) - What do we need?

- a schema that can be used to generate (by a producer) and validate (by a consumer) an open Digital Specimen as it is communicated from one system to another.
- a CORDRA schema that can be used internally within CORDRA for storing open Digital Specimens. This schema will be similar to the above one, but contains more details specific to the CORDRA implementation, such as what to preview in search results, etc.
  
- type definitions into a type registry that ODS can be produced/validated/stored against in an object repository/server such as CORDRA.


So, what should be the workflow for preparing these schemas?
1. Prepare an exemplar JSON fragment, similar to above containing required structures, K/V pairs, etc.
2. Use an appropriate generator tool to auto-generate a JSON schema for the fragment.
3. From the auto-generated schema, optimise an 'ODStype schema' by hand in an iterative process until it works with (validates) a variety of JSON fragment examples, including boundary conditions. This should include producing JSON fragments against the schema in one system and consuming those fragments against the schema in another system. Note that optimisations must be kept to a minimum and a record of them must also be kept so that they can subsequently be re-applied to a newly generated schema as necessary. Note that at present for development purposes, it is the schema `title` (corresponding to `typeName` in the JSON fragment instance) that distinguishes one version/variant of the schema from another. We are using four digits beginning at '1802', thus `"title": "ODStype1802"`, `"title": "ODStype1803"`, etc.
4. Further optimise the schema to become a CORDRA (or other object server) internal schema. Ditto, a record of optimisations must be kept.
5. Derive and register type definitions into type registry

The above implies several related artefacts to be kept under version control:
- the exemplar JSON fragment
- the auto-generated schema
- the hand-optimised ODStype schema and list of optimisations
- the CORDRA variant of the ODStype schema and list of variations from the ODStype schema
- the type definitions

How to make this error-proof as possible?


The schema example in [example2-schema.json](example2-schema.json) has been generated with the [quicktype](https://quicktype.io/) tool.

Got to here>>The next step might to take this schema and insert some examples and defaults into it and see if we can use extendclass tool to recreate the JSON example from it, paying attention to how it deals with the two alternative sources for images - a file in the payload or a uri.
Also, apply some of the schema customisations from below.


# More real example from MeiseBG
Have a look at this prov exampe, which illustrates how massive it can grow when many people perform activities on an entity! https://api.gbif-uat.org/v1/occurrence/2840596485/fragment 
https://cite.research-software.org/ 

See Claus's email of 14th April on validation in python.
Spare below here>>>


To explain this JSON fragment, 
- The `id` is the persistent identifier of the DS. We use 20.5000.1025/*\_suffix\_* for the examples here, where the *\_suffix\_* is randomly generated by the repository server where this DS object is first created.
- The `typeName` is the formal name given to the definition of this specific structure for a DS. The `typeName` "ODStype1802" means this JSON fragment is of '*open digital specimen type*' with a version identity '*1802*'. This `typeName` corresponds to the name of the JSON Schema against which this JSON fragment was constructed, and against which it can be parsed/verified. The schema is given below.
- The next part `authoritative: { ... }` is the authoritative a_section with content corresponding to what we expect to see at [MIDS level 1](https://github.com/tdwg/mids/issues?q=is%3Aissue+is%3Aopen+sort%3Acreated-asc+label%3A%22MIDS+Element%22+label%3AMIDS-1) i.e., the following six information elements, each with one or more values.

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

```json
  "availableImages": {
      "$id": "#/properties/availableImages",
      "items": {
        "$id": "#/properties/availableImages/image",
        "items": [
          {
            "type": "string",
            "title": "Creator"
          },
          {
            "type": "string",
            "title": "Format"
          },
          {
            "type": "string",
            "title": "Resolution"
          },
          {
            "type": "string",
            "title": "Rights holder"
          },
          {
            "type": "string",
            "title": "Rights"
          },
          {
            "format": "uri",
            "type": "string",
            "title": "Image"
          }
        ],
        "type": "array",
        "title": "Image"
      },
      "title": "Available images",
      "type": "array",
      "$ref": "#/definitions/previewInResultsFalse"
    },
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

To do:
- SDR requires a data object for describing labelled regions (ROIs) on an image. IIIF now supports polygon region descriptions, and will be used internally for image data. 
- Image section must contain description of regions of interest for each image. https://www.loc.gov/standards/alto/ instead of iiif.

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



