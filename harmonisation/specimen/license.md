# License on Specimen level

## openDS
Will be harmonised to `dcterms:license`

## Mapping
Before searching for license in the below terms we will first check if a default value or explicit mapping has been set.

### DWC
For DWCA we will look at matches on two terms:
- `dcterms:license`
- `dc:license`

If these terms are not available or are null we will leave this field empty.

### ABCDEFG
Within ABCDEFG the license is not part of the unit level but is part of the dataset level.
Within ABCDEFG data we will also look at two possible places:
- datasets/dataset/metadata/IPRStatements/Licenses/0/URI
- datasets/dataset/metadata/IPRStatements/Licenses/0/Text 

Here we make the assumption that the first license is the correct one.