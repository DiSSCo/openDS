# ObjectType

## openDS
Will be harmonised to `ods:objectType`
There is no exact match for objectType in either DWC nor ABCD(EFG)

## Mapping
Before searching for objectType in the below terms we will first check if a default value or explicit mapping has been set.
In the case of objectType this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order:
- `dwc:preparations`
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:kindOfUnit/0/value`
Here we make the assumption that the first value is the correct one.