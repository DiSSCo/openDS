# Lithostratigraphic terms

This is a set of terms which are combined in this single file.
This is mainly te reduce the amount of files.

## openDS
Will be harmonised to the DWC terms for lithostratigraphy.
- `dwc:bed`
- `dwc:formation`
- `dwc:group`
- `dwc:member`

## Mapping
Before searching for the lithostratigraphy term in the below terms we will first check if a default value or explicit mapping has been set.
In the case of lithostratigraphy terms this is improbable however, the functionality is there.

### DWC
As we use the DWC fields we will look for an exact match for the lithostratigraphic field.
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For the ABCDEFG we will look in the specific lithographic field to get a value.
We do make the assumption that we can use the first match we can find, so index 0.
#### Bed
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/lithostratigraphicAttributions/lithostratigraphicAttribution/0/bed`
If these term(s) are not available or are null we will leave this field empty (`null`).
#### Formation
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/lithostratigraphicAttributions/lithostratigraphicAttribution/0/formation`
If these term(s) are not available or are null we will leave this field empty (`null`).
#### Group
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/lithostratigraphicAttributions/lithostratigraphicAttribution/0/group`
If these term(s) are not available or are null we will leave this field empty (`null`).
#### Member
#### Formation
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/lithostratigraphicAttributions/lithostratigraphicAttribution/0/member`
If these term(s) are not available or are null we will leave this field empty (`null`).
