# Modified

## openDS
Will be harmonised to `dcterms:modified`
This field is an exact match with the dublin core field `modified`

## Mapping
Before searching for modified in the below terms we will first check if a default value or explicit mapping has been set.
In the case of modified this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order:
- `dcterms:modified`
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
Within ABCDEFG the modified can be part of both the unit level and the dataset level.
We will first look at the unit level as it is the more precise level.
Here we will look at two place for modified information:
- `abcd:hasDateModified`
- `abcd:dateLastEdited`

If we cannot find a modified at the unit level, we will look at the dataset level:
- `abcd:metadata/revisionData/dateModified`