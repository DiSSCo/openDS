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

The main differences between these two generators are that the first places a complete example at the beginning of the schema whereas the latter breaks the example up into multiple short examples, each at its own place in the schema. The first includes a description for each property (thus more documenting), whereas the latter doesn't include this (although it can be added by hand).

- [liquid-technologies](https://www.liquid-technologies.com/online-json-to-schema-converter) - has tools for both directions i.e., JSON -> JSON schema, and vive-versa.
- [quicktype](https://quicktype.io/)

## Schema(s) - What do we need?

- a schema that can be used to generate (by a producer) and validate (by a consumer) an open Digital Specimen as it is communicated from one system to another.
- a CORDRA schema that can be used internally within CORDRA for storing open Digital Specimens. This schema will be similar to the above one, but contains more details specific to the CORDRA implementation, such as what to preview in search results, etc.
  
- type definitions into a type registry that ODS can be produced/validated/stored against in an object repository/server such as CORDRA.


So, what should be the workflow for preparing these schemas?
1. Prepare an exemplar JSON fragment, similar to above containing required structures, K/V pairs, etc.
2. Use an appropriate generator tool to auto-generate a JSON schema for the fragment.
3. From the auto-generated schema, optimise an 'ODStype schema' by hand in an iterative process until it works with (validates) a variety of JSON fragment examples, including boundary conditions. This should include producing JSON fragments against the schema in one system and consuming those fragments against the schema in another system. Note that optimisations must be kept to a minimum and a record of them must also be kept so that they can subsequently be re-applied to a newly generated schema as necessary. Note that at present for development purposes, it is the schema `title` (corresponding to `typeName` in the JSON fragment instance) that distinguishes one version/variant of the schema from another. We are using four digits beginning at '1802', thus `"title": "ODStype1802"`, `"title": "ODStype1802"`, etc.
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
Have a look at this prov example, which illustrates how massive it can grow when many people perform activities on an entity! https://api.gbif-uat.org/v1/occurrence/2840596485/fragment 
https://cite.research-software.org/ 

See Claus's email of 14th April on validation in python.

To do:
- SDR requires a data object for describing labelled regions (ROIs) on an image. IIIF now supports polygon region descriptions, and will be used internally for image data. 
- Image section must contain description of regions of interest for each image. https://www.loc.gov/standards/alto/ instead of iiif.




## Complete JSON schema for validation testing
To be completed.


END.



