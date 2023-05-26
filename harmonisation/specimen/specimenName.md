# SpecimenName

## openDS
Will be harmonised to `ods:specimenName`
This MIDS term doesn't seem to have an exact match 

## Mapping
Before searching for specimenName in the below terms we will first check if a default value or explicit mapping has been set.
In the case of specimenName this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order:
- `dwc:scientificName`
If no scientificName is available in the core file, we check the Identifications extension.
We follow the logic described for the [taxonomicTerms](./taxonomicTerms.md) to determine which identification to use.  
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG there is a difference between ABCD and ABCDEFG on where to find the specimenName.
As there can be multiple identification we use the logic described for the [taxonomicTerms](./taxonomicTerms.md) to determine which identification to use.
If we encounter the `preferredFlag` we will then search first for the ABCD term and then for the ABCDEFG term.
- `abcd:identifications/identification/{index}/result/taxonIdentified/scientificName/fullScientificNameString`
- `abcd-efg:identifications/identification/{index}/result/mineralRockIdentified/classifiedName/fullScientificNameString`

Important assumption is that we will take the first `prefferedFlag: true` we encounter.
If there are multiple `prefferedFlag: true` are set we will take the one with the lowest index.

When no preferred flag has been set, we assume that the name with the lowest index is the correct one.
We will again first check the ABCD field and then the ABDEFG field:
- `abcd:identifications/identification/0/result/taxonIdentified/scientificName/fullScientificNameString`
- `abcd-efg:identifications/identification/0/result/mineralRockIdentified/classifiedName/fullScientificNameString`

If in none of these were found or if none of the fields contained a value we leave this field empty (`null`)