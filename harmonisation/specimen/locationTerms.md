# Location Terms

This is a set of terms which are combined in this single file.
This is mainly te reduce the amount of files.
For the below terms we can only fill most of them for DWC data as ABCD does make a similar fine-grained distinction.
This means that most often for ABCD data we can at maximum provide countryCode, country and locality.

## openDS
Will be harmonised to the DWC terms for location.
- `dwc:country`
- `dwc:countryCode`
- `dwc:continent`
- `dwc:county`
- `dwc:island`
- `dwc:islandGroup`
- `dwc:locality`
- `dwc:municipality`
- `dwc:stateProvince`
- `dwc:waterBody`

## Mapping
Before searching for the Location term in the below terms we will first check if a default value or explicit mapping has been set.
In the case of Location terms this is improbable however, the functionality is there.

### DWC
As we use the DWC fields we will look for an exact match for the location field.
If these term(s) are not available or are null we will leave this field empty (`null`).

#### Locality
For DWC we will look at matches on the term(s) in this order:
- `dwc:locality`
- `dwc:verbatimLocality`

If these term(s) are not available or are null we will leave this field empty (`null`).
 
### ABCDEFG

#### Country
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:gathering/country/name/value`
- `abcd:gathering/country/nameDerived/value`

If these term(s) are not available or are null we will leave this field empty (`null`).

#### CountryCode
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:gathering/country/iso3166Code`

If these term(s) are not available or are null we will leave this field empty (`null`).

#### GeodeticDatum
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:gathering/localityText/value`

If these term(s) are not available or are null we will leave this field empty (`null`).