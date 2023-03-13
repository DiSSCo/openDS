# Biostratigraphic terms

This is a set of terms which are combined in this single file.
This is mainly te reduce the amount of files.

## openDS
Will be harmonised to the DWC terms for biostratigraphy.
- `dwc:highestBiostratigraphicZone`
- `dwc:lowestBiostratigraphicZone`

## Mapping
Before searching for the Biostratigraphy term in the below terms we will first check if a default value or explicit mapping has been set.
In the case of Biostratigraphy terms this is improbable however, the functionality is there.

### DWC
As we use the DWC fields we will look for an exact match for the biostratigraphic field.
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG there is no distinction between highest and lowest so we put all information in both fields.
The biostratigraphic information is separated in ABCD in several field.
We will combine three fields for the harmonisation and separate the values with a vertical slash `|`
The three fields we check are:
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/biostratigraphicAttributionsType/biostratigraphicAttribution/0/zonalFossilType`
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/biostratigraphicAttributionsType/biostratigraphicAttribution/0/fossilZoneName`
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/biostratigraphicAttributionsType/biostratigraphicAttribution/0/fossilSubzoneName`
  
If these term(s) are not available or are null we will leave this field empty (`null`).