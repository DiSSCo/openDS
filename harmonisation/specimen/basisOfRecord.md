# Basis of Record

## openDS
Will be harmonised to `dwc:basisOfRecord`

In principle this field cannot be empty, as we use it to determine whether we should process the specimen or not.
Specimen with Basis of Record that are accepted are:
- Preserved Specimen
- Fossil Specimen
- Material Sample
- Living Specimen
- Rock Specimen
- Mineral Specimen
- Meteorite specimen

All specimen with a Basis of Record not in this list will be ignored on ingestion.

## Mapping
Before searching for the basisOfRecord in the below terms, we will first check if a default value or explicit mapping has been set.
In the case of collector this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order:
- `dwc:basisOfRecord`


### ABCDEFG
For ABCD(EFG) we will look at matches on the term(s) in this order:
- `abcd:recordBasis`
