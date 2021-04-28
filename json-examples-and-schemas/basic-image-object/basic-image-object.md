# Basic image object
## Introduction
The [Specimen Data Refinery (SDR)](https://github.com/DiSSCo/sdr) has a specific requirement for [a JSON Schema for image objects](https://github.com/DiSSCo/SDR/issues/17) as inputs and outputs of refinement workflows.

Within this object, the image will be a payload file in jpeg format. This is accompanied by some basic information about the image, such as technical details of the image, the owning institution, the license for use of the image, etc. A controlled vocabulary is used to describe what the image contains. A PID is assigned automatically when the image object is first created. 

Further fields are required later on. These will either provide additional information to accompany the image as it serves as an input to a workflow; and/or they can be enriched by specific workflow steps and filled as output of the workflow. These fields will be defined later. It is an open issue as to whether they are part of the image object type or a separate object type.

## Design
The initial design of openDS posits an 'i_section' of a Digital Specimen containing metadata about and references to images or the images themselves as payload files within the DS object. The i_section is represented by a self-contained `images` JSON object structure.

The storage location and manner of storage of images is highly variable. Usually (today) images are to be found at the endpoint of a URI in a simple filestore or in a more sophisticated media management system. Increasingly, images can and will be served through, for example the Image and Presentation APIs of the [International Image Interoperability Framework (IIIF)](https://iiif.io/). The Presentation API in particular is oriented towards standardized descriptions of the structure, layout and presentation mode of compound digital objects. Further work is needed in DiSSCo to properly understand how to integrate IIIF and object server technologies and how to dynamically serve and manipulate specimen images. For now, we assume a straightforward delivery of static image files one-by-one.

At hand also is a continuing thought process around the granularity of openDS objects. From one extreme of including all data in a single object to the opposite extreme of splitting up data into a large number of related tiny objects, it is still an open issue as to where an open Digital Specimen and its constituent parts sit on this spectrum.

A first representation in [example 2](basic-json-example2.md) is based on the idea of an open-ended array of image objects within an i_section object. But such an approach, when adopted for a specimen with many images (as in 3D stacked images, for example) or when applied in a similar manner to other data types of the open DS leads to rapid JSON expansion with significant repetition of common data elements. Nevertheless, each image and its pertinent metadata should be self-standing for the cases where that image alone is used. Again, for now we assume this is the case and treat images objects with a granularity of one i.e., one image per basic image object with the image file as the payload of the object.

The i_section of an open Digital Specimen then will point to one or more basic image objects associated with the specimen rather than including those directly into the DS itself. Only the thumbnail image will be included directly to reduce the number of fetches from an object before deciding whether a specimen and its image are of any potential interest.

## Artefacts
The following artefacts are associated with this basic-image-object description:
1. Example of an [basic image object](bio-example.json) (JSON file).
2. JSON [schema file auto-generated](auto-schema.json) from (1).
3. [openDS JSON Schema file](openDS-bio-schema.json) derived from hand-optimisation of (2) and [list of optimisations](bio-optimisations.md) applied.
4. [CORDRA schema file](bio-cordra-schema.json) (in JSON) derived from adaptation of (3) and [list of adaptations](bio-cordra-schema-adaptions.md) made.

## Workflow steps
The following steps were taken to produce the artefacts listed above.
1. Create by hand the example of an [basic image object](bio-example.json) (JSON file).
2. Validate (1) using [JSONLint](https://jsonlint.com/). = valid JSON.
3. Autogenerate a schema ...Got to here>>


END.