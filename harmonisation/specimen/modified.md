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
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:hasDateModified`
- `abcd:dateLastEdited`
