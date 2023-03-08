# DateCollected

## openDS
Will be harmonised to `ods:dateCollected`
There is no exact match for dateCollected in either DWC nor ABCD(EFG)

## Mapping
Before searching for dateCollected in the below terms we will first check if a default value or explicit mapping has been set.
In the case of dateCollected this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order:
- `dwc:eventDate`
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:gathering/dateTime/isodateTimeStart`
- `abcd:gathering/dateTime/isodateTimeEnd`
- `abcd:gathering/dateTime/dateText`
If these term(s) are not available or are null we will leave this field empty (`null`).
