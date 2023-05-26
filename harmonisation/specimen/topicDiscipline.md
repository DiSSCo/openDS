# Topic Discipline

## openDS
Will be harmonised to `ods:topicDiscipline`
This is a new field, described by this [RFC](https://docs.google.com/document/d/19OPyOm9VF2qfI3M6RmJPvRfo8JlZ3tt0II05aGCyBHQ/edit).

## Mapping
Before calculating topicDiscipline with the below logic we will first check if a default value or explicit mapping has been set.

## Mapping
This field is created based on several other fields.
First we determine the [`dwc:basisOfRecord`](./basisOfRecord.md) and the [`dwc:kingdom`](./taxonomicTerms.md).
Based on the `dwc:basisOfRecord` we use the following logic to make a determination:
- Fossil Specimen -> Palaeontology
- Meteorite Specimen -> Astrogeology
- Rock Specimen OR Mineral Specimen -> Earth System
- For all other types of basis of Record we check the kingdom:
  - Animalia -> Zoology
  - Plantae -> Bontany
  - Bacteria -> Microbiology
- If none of these match then we put the specimen in Unclassified.

The taxonomy details such as kingdom are currently only taken over from the orginal data.
If `dwc:kingdom` is empty we cannot determine the topicDiscipline.