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
Within ABCDEFG the license can be part of both the unit level and the dataset level.
We will for look at the unit level as it is the more precise level.
Here we will look at two place for license information:
- unit/iprstatements/licenses/license/0/uri
- unit/iprstatements/licenses/license/0/text

If we cannot find a license at the unit level we will look at the dataset level:
- datasets/dataset/metadata/IPRStatements/Licenses/0/URI
- datasets/dataset/metadata/IPRStatements/Licenses/0/Text 

If there are multiple licenses defined in the file we will take the first one we encounter.