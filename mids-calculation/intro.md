# MIDS Calculation

Within DiSSCo the Digital Specimen Processing Service calculates MIDS values for the Digital Specimen.
The translator harmonises all fields into the openDS data specification see [harmonisation](../harmonisation/intro.md)
Based on the harmonised data model the MIDS level will be calculated.
This is often based on checking if certain fields (or a list of fields) do not have a `null` value or an `""` or the field value of `"null"`
If this is not the case we accept the value for this field, and it complies to MIDS.
The MIDS level are built on top of each other so level 1 requires everything from level 0 and MIDS level 2 requires all requirements from level 0 and 1.

## MIDS level 0
All specimen need to be at least of MIDS level 0 otherwise they will not be accepted into the system.
This means that all specimen in DiSSCo comply to MIDS level 0 because the following fields are available:
- `ods:physicalSpecimenId`
- `ods:organizationId`

## MIDS level 1
For MIDS level 1 all specimen should have some value for the following fields:
- `dcterms:license`
- `ods:modified`
- `ods:objectType`
- `ods:type`
- `ods:specimenName`

## MIDS level 2
From MIDS level 2 onwards MIDS makes a distinction in three different types:
- Biological 
- Palaeontological
- Geological


### Biological
For Biological specimen to comply to MIDS level 2 the following fields need to have a valid value:
- `ods:collectingNumber`
- `ods:collector`
- `ods:dateCollected`
- `dwc:typeStatus`
- `ods:hasMedia` This term needs to be filled as well as has the value `"true"`
- It needs to have *one** of the following Qualitative Location fields filled:
  - `dwc:continent` 
  - `dwc:country`
  - `dwc:countryCode`
  - `dwc:county`
  - `dwc:island`
  - `dwc:islandGroup`
  - `dwc:locality`
  - `dwc:municipality`
  - `dwc:stateProvince`
  - `dwc:waterBody`
- It needs to have **all** the following Quantitative Location fields filled:
  - `dwc:decimalLatitude`
  - `dwc:decimalLongitude`

### Palaeontological and Geological
For Biological specimen to comply to MIDS level 2 the following fields need to have a valid value:
- `dwc:typeStatus`
- It needs to have **one** of the following Stratigraphy fields filled:
  - `dwc:earliestAgeOrLowestStage`
  - `dwc:earliestEonOrLowestEonothem`
  - `dwc:earliestEpochOrLowestSeries`
  - `dwc:earliestEraOrLowestErathem`
  - `dwc:earliestPeriodOrLowestSystem`
  - `dwc:latestAgeOrHighestStage`
  - `dwc:latestEonOrHighestEonothem`
  - `dwc:latestEpochOrHighestSeries`
  - `dwc:latestEraOrHighestErathem`
  - `dwc:latestPeriodOrHighestSystem`
  - `dwc:bed`
  - `dwc:formation`
  - `dwc:group`
  - `dwc:member`
  - `dwc:highestBiostratigraphicZone`
  - `dwc:lowestBiostratigraphicZone`
- It needs to have **one** of the following Qualitative Location fields filled:
  - `dwc:continent`
  - `dwc:country`
  - `dwc:countryCode`
  - `dwc:county`
  - `dwc:island`
  - `dwc:islandGroup`
  - `dwc:locality`
  - `dwc:municipality`
  - `dwc:stateProvince`
  - `dwc:waterBody`
- It needs to have **all** the following Quantitative Location fields filled:
  - `dwc:decimalLatitude`
  - `dwc:decimalLongitude`