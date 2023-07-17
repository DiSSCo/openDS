# DiSSCo adaption of GBIF UM

DiSSCo investigates how the [GBIF Unified Model](https://github.com/gbif/model-material/tree/master) can be implemented for DiSSCo.
For this adaption we propose several changes want to make several changes to the GBIF UM.
These changes are proposed [here](https://docs.google.com/document/d/1NIIGwh-FUmoONGrUGY4ARbsi8dBQDHXdfLiGb9B0oUQ/edit?usp=sharing)
In this document we will provide a quick introduction of the structure.
The DiSSCo's adaption is written in [JSON Schema](https://json-schema.org/).
Two type of object are covered with the adaption:
- Digital Specimen
- Digital Media Object

## Digital Specimen
For the Digital Specimen we take `Organism` from the GBIF UM as basis.
Instead of creating three records we flatten the Organism table, the Material Entity table and the Entity table into a single object.
The fields from these three tables are top-level fields of the object.
In addition to the fields from the GBIF UM we also include several fields coming from DiSSCo's openDS ontology.
Next to a set of fields on the top-level we have several connected objects.

### Occurrence (zero to many)
A digital specimen could have one-to-many occurrences.
Again we flatten this in comparison to the GBIF UM.
Within the Occurences we included the Location fields as well as the Georeference fields.

### Identifiers (zero to many)
Contains all identifiers connected to the digital specimen

### Assertions (zero to many)
Contains all assertions connected to the digital specimen

### Material entities (zero to many) 
The material entities connect to the digital specimen are specimen parts.
This means that they are part of the digital specimen but do not have their own registration/catalogue number.
If they do have their own number, they will be registered as a digital specimen of their own.
Each material entity will also have their own events, assertions, citations, entity_relationships and identifiers

### Citations (zero to many)
The Citations of the digital specimen.
We flattened the Citations table and the Reference table into a single object.

### Entity Relationships (zero to many)
The specimen can have multiple relationships with other resources.
This relationship could be a relationship to another specimen.
It could also be a relationship to an external resources, where we will match on the identifier.

### Chronometric Age (zero to many)
The specimen can have multiple chronometric age objects attached to it.

## Digital Media Object 
For the Digital Media Object we use Digital Entity from GBIF UM as basis.
We combine the toplevel fields from Entity and Digital Entity and add the DiSSCo fields as top level fields.
Besides the top level fields we have the connected objects:

### Assertions (zero to many)
Contains all assertions connected to the digital media objects

### Identifiers (zero to many)
Contains all identifiers connected to the digital media object

### Citations (zero to many)
The Citations of the digital media object.
We flattened the Citations table and the Reference table into a single object.

### Entity Relationships (zero to many)
The digital media can have multiple relationships with other resources.
The main entity relationship will be to the digital specimen.
Without the relationship to the digital specimen the object should not exist.
Besides the digital specimen the digital media object could have a relationship to external sources.
