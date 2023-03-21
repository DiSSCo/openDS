# TypeStatus

## openDS
Will be harmonised to `dwc:typeStatus`
This MIDS element seems to have an exact match to `dwc:typeStatus`

## Mapping
Before searching for typeStatus in the below terms we will first check if a default value or explicit mapping has been set.
In the case of typeStatus this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order::
- `dwc:typeStatus`
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG we need to combine several fields.
An important assumption is that we only use the first `nomenclaturalTypeDesignation` we encounter.
We will combine the three terms using a vertical slash `|` as the delimiter.
The three fields we check are:
- `abcd:specimenUnit/nomenclaturalTypeDesignations/nomenclaturalTypeDesignation/0/typeStatus`
- `abcd:specimenUnit/nomenclaturalTypeDesignations/nomenclaturalTypeDesignation/0/typifiedName/fullScientificNameString`
- `abcd:specimenUnit/nomenclaturalTypeDesignations/nomenclaturalTypeDesignation/0/nomenclaturalReference/titleCitation`

If in all three fields a value was found we will publish `value1 | value2 | value3`
If only in the second and third field values were found we will publish `value1 | value2`
If in none of the fields a value was encountered we will leave the field empty (`null`)

