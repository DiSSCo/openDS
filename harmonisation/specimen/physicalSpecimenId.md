# PhysicalSpecimenId

## openDS
Will be harmonised to `dwc:physicalSpecimenId`
There is no exact match for physicalSpecimenId in either DWC nor ABCD(EFG)

## Mapping
Before searching for typeStatus in the below terms we will first check if a default value or explicit mapping has been set.
In the case of physicalSpecimenId this is highly improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order::
- `dwc:occurrenceID`
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG we will look at matches on the term(s) in this order::
- `abcd:unitID`

## Additional Transformation
In the rest of the system we need to a globally unique physicalSpecimenId.
Based on the physicalSpecimenIdType we determine if we need additional transformation to make it globally unique.
If the identifier is globally unique (`cetaf`) we can copy it as-is.
If it is not globally unique (`combined`) we need to combine it with the ror.
For the ror we only use the unique id part of the ror.
This will be following the format of `id:ror`