# CollectingNumber

## openDS
Will be harmonised to `ods:collectingNumber`
There is no exact match for collectingNumber in either DWC nor ABCD(EFG)

## Mapping
Before searching for collectingNumber in the below terms we will first check if a default value or explicit mapping has been set.
In the case of collectingNumber this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order:
- `dwc:recordNumber`

If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:collectorsFieldNumber`
- `abcd:gathering/code`

If these term(s) are not available or are null we will leave this field empty (`null`).
